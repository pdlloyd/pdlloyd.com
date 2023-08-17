+++
# Best practices from https://www.opengraph.xyz/: Keep title under 60 characters.
#        |----------------------------------------------------------|
title = "Mirroring GitLab to GitHub Using SSH"

# Best practices from https://www.opengraph.xyz/: Keep description between 155 - 160 characters.
#              |---------------------------------------------------------------------------------------------------------------------------------------------------------|----|
description = "GitLab is currently the canonical \"source of truth\" for my personal Git repositories. This post shows how to automatically push them to GitHub using SSH deploy keys (and why you'd want to do it in the first place)."

# YYYY-MM-DD (2012-10-02) or RFC3339 (2002-10-02T15:00:00Z)
date = 2022-08-13
updated = 2023-08-16

draft = true
in_search_index = true

#[taxonomies]
#tags = ["ssh", "git", "github", "gitlab", "lock-in"]

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

Companies love platform lock-in. It makes it so that the burden of moving to another platform is so great that customers are forced to keep using a product they would otherwise have dropped for someting better. A common strategy for locking-in users is to adopt a popular open source tool (like Git), wrap proprietary features around it (like issue tracking and project management), and make it so that those features disadvantage the competition (the code repository is easily portable but the add-on features are not). Microsoft famously embodied this with their ["embrace, extend, extinguish"](https://en.wikipedia.org/wiki/Embrace,_extend,_and_extinguish) strategy and many are (reasonably) worried about this happening with Microsoft's purchase of GitHub. 

However, since GitHub turned software version control into a gamified social experience with stars, achievement badges, followers, etc., a lot of people use it as their primary way of discovering and participating in software projects. There is something to be said about the network effect of popular repositories linking to others (e.g. [Awesome](https://github.com/topics/awesome) lists). I would like to leverage the social (and potentially the free CI/CD) aspects of multiple Social Version Control platforms like GitLab, GitHub, Codeberg, etc., but not be locked into any particular one. The first step in this process is being able to mirror canonical repositories to "downstream" ones unidirectionally.
 

## Manual Setup in GitLab and GitHub

First order of business is to create the Git repositories. I'm using [this website's repo](https://github.com/pdlloyd/pdlloyd.com) as the demonstrator of this process so that detail is already taken care of on the '**Lab** side. Now on the '**Hub** side, I created an empty repository opting to _not_ include anything like a README or LICENSE file.

Now, go into the settings of the Git**Lab** repository and find 

{{ image(src="gl-mirror-repo.png",
         style="border-radius: 8px;",
         position="center",
         alt="The section on mirroring repositories") }}

GitHub gives us: git@github.com:pdlloyd/pdlloyd.com.git
but 
Gitlab requires: ssh://git@github.com/pdlloyd/pdlloyd.com.git (otherwise `Invalid URL`)
see https://gitlab.com/gitlab-org/gitlab-foss/-/issues/59032 

Click "Detect Host Keys"

It should produce these:
https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints

Check with Ctrl+F manually

Copy the GL pubkey

Create GH repo, to GH repo settings

Add GL pubkey as a deploy key, allow write access 

Do the test sync

Bonus: turn off issues and stuff

## `git push` your Cake and Eat it Too


Resources: 
- https://docs.gitlab.com/ee/user/project/repository/mirror/index.html#authentication-methods-for-mirrors
- https://docs.gitlab.com/ee/user/project/repository/mirror/push.html
- https://docs.github.com/en/developers/overview/managing-deploy-keys
- https://gitlab.com/gitlab-org/gitlab-foss/-/issues/59032
