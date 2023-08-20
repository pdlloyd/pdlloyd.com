+++
# Best practices from https://www.opengraph.xyz/: Keep title under 60 characters.
#        |----------------------------------------------------------|
title = "Mirroring GitLab to GitHub Using SSH"

# Best practices from https://www.opengraph.xyz/: Keep description between 155 - 160 characters.
#              |---------------------------------------------------------------------------------------------------------------------------------------------------------|----|
description = "GitLab is currently the canonical \"source of truth\" for my personal Git repositories. This post shows how to automatically push them to GitHub using SSH deploy keys (and why you'd want to do it in the first place)."

# YYYY-MM-DD (2012-10-02) or RFC3339 (2002-10-02T15:00:00Z)
date = 2022-08-13
updated = 2023-08-18

draft = false

in_search_index = true

#[taxonomies]
#tags = ["ssh", "git", "github", "gitlab"]

# template = 
# weight = 
# slug = 
# path = 
# aliases = 
[extra]
+++

Git**Lab** is currently the canonical "source of truth" for my [personal Git repositories](https://gitlab.com/pdlloyd). This post shows how to automatically push them to Git**Hub** using SSH deploy keys (and why you'd even want to do this in the first place). There are a few quirks to navigate but this process can help give your projects extra reach while simultaneously helping your projects combat a little bit of vendor lock-in.

<!-- more -->

## Motivation

Companies love platform lock-in. It makes it so that the burden of moving to another platform is so great that customers are forced to keep using a product they would otherwise have dropped for someting better. A common strategy for locking-in users is to adopt a popular open source tool (like [Git](https://git-scm.com/)), wrap proprietary features around it (like issue tracking and project management), and make it so that those features disadvantage the competition (the code repository is easily portable but the add-on features are not). Microsoft famously embodied this with their ["embrace, extend, extinguish"](https://en.wikipedia.org/wiki/Embrace,_extend,_and_extinguish) strategy and many are (reasonably) worried about this happening with Microsoft's purchase of GitHub (or maybe they'll just [yoink your code without asking](https://githubcopilotlitigation.com/) and train their [products](https://github.com/features/copilot) with it). 

However, since GitHub turned software version control into a gamified social experience with stars, achievement badges, followers, etc., a lot of people use it as their primary way of discovering and participating in software projects. There is something to be said about the network effect of popular repositories linking to others (e.g. [Awesome](https://github.com/topics/awesome) lists). I would like to leverage the social (and potentially the free CI/CD) aspects of multiple Social Version Control (SVC) platforms like GitLab, GitHub, Codeberg, etc., but not be locked into any particular one. The first step in this process is being able to mirror canonical repositories to "downstream" ones unidirectionally. It may be interesting/useful to figure out some way of stiching together APIs so that you can get unified bidirectional repositories with synchronized issues, pull requests, wikis, etc., but let's crawl before we run here. 
 
## Manual Setup in GitLab and GitHub

First order of business is to create the Git repositories on both sides of the push. I'm using [this website's repo](https://github.com/pdlloyd/pdlloyd.com) as the demonstrator of this process so that detail is already taken care of on the '**Lab** side. Now on the '**Hub** side, I created an empty repository opting to _not_ include anything like a README or LICENSE file. Just to not confuse GitHub users who come across the repo, I turned off issues, wikis, and other features on the repo in GitHub for the time being, and included a link in the README and description to point back to GitLab.

## Settings, Schemes, & SSH Fingerprints

Now, go into the settings of the Git**Lab** repository and find this:

{{ image(src="gl-mirror-repo.png",
         style="border-radius: 8px;",
         position="center",
         alt="The section on mirroring repositories") }}

Click `Expand` and you'll be greeted with a form to add your '**Hub** repo's URL. I prefer the convenience and security of public key authentication for this, and so I copied from Git**Hub** the SSH URL (that _is_ what this article is about, after all):

{{ image(src="gh-copy-repo-url.png",
         style="border-radius: 8px;",
         position="center",
         alt="Copy the SSH URL") }}

_However_... it is here I discovered an annoying quirk. GitHub presents us `git@github.com:pdlloyd/pdlloyd.com.git` (note the colon after `com`). Putting this URL as is into the GitLab form and clicking `Detect host keys`, you will be presented with an `Invalid URL` error and not much else. According to this [fairly obscure issue](https://gitlab.com/gitlab-org/gitlab-foss/-/issues/59032), Gitlab requires formatting the URL like this: `ssh://git@github.com/pdlloyd/pdlloyd.com.git` (notice the explicit `ssh://` URI scheme, and replacing the original colon with a slash). Now when you click `Detect Host Keys`, the form should produce [GitHub's public SSH key fingerprints](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints):

{{ image(src="gl-mirror-repo-settings.png",
         style="border-radius: 8px;",
         position="center",
         alt="GitHub SSH public key fingerprints") }}

Making sure the fingerprints in GL match the ones in GH gurantees that GitHub is who they claim to be and you aren't pushing to a man-in-the-middle. I just did a Ctrl+F to manually verify across browser windows. Once you're satisfied, click `Mirror repository`.

## Deploy Keys and the First Sync

Now, while still in GitLab, copy the public deploy key by clicking the little clipboard:

{{ image(src="gl-mirror-copy-pubk.png",
         style="border-radius: 8px;",
         position="center",
         alt="Copy GitLab SSH public deploy key") }}

Go to the GitHub repo and find the _repository_ settings (not the user settings.) & find `Deploy keys` under `Security`. Paste the GitLab public key into the main textbox and name it something fun. Be sure allow write access since we're pushing, not pulling.

{{ image(src="gh-add-key.png",
         style="border-radius: 8px;",
         position="center",
         alt="Copy GitLab SSH public deploy key") }}

Finally, test out the system by performing a test sync in GitLab by pressing the swirl next to the clipboard. Now you should be able to `git push` your cake to GitLab and eat it on GitHub too.

## Future Trippin'

There's a lot of room for future improvement with this:

- Add GitHub actions to the repo in addition to GitLab CI/CD. [GitHub has an importer](https://github.com/github/gh-actions-importer) that could be leveraged.
- Set up push mirror for other Git hosts like CodeBerg
- Self-host a Git server using something like Gitea or Forgejo to use as the canonical SOT and push to the SaaS ones as backups
- Dig into the API's of the SaaS Git hosts and connect together similar features for bidirectional synchronization (issues, PRs, wikis, container repos, etc.)

We'll see what this turns into over time. I definitely want to host my own Forgejo instance (even if just on my LAN) but I think the interop project would be the most generally useful (higher impact). There may even be products out there that do this already. 

Resources: 
- https://docs.gitlab.com/ee/user/project/repository/mirror/index.html#authentication-methods-for-mirrors
- https://docs.gitlab.com/ee/user/project/repository/mirror/push.html
- https://docs.github.com/en/developers/overview/managing-deploy-keys
- https://gitlab.com/gitlab-org/gitlab-foss/-/issues/59032
