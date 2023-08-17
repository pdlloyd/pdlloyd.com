+++
# Best practices from https://www.opengraph.xyz/: Keep title under 60 characters.
#        |----------------------------------------------------------|
title = "Hello World!"

# Best practices from https://www.opengraph.xyz/: Keep description between 155 - 160 characters.
#              |---------------------------------------------------------------------------------------------------------------------------------------------------------|----|
description = "The first blog post on PDLloyd.com. It covers some of the reasoning behind choosing Zola as a SSG framework and compares a few different methods of deployment."

# Two formats are allowed: YYYY-MM-DD (2012-10-02) and RFC3339 (2002-10-02T15:00:00Z).
date = 2022-08-08
updated = 2023-08-16

draft = false
in_search_index = true

#[taxonomies]
#tags = ["notes", "meta", "blogs"]

# template = 
# weight = 
# slug = 
# path = 
# aliases = 
# [extra]
+++

## Why Build This Blog? 

In recent years, big internet companies have siloed huge swaths of the internet into their platforms, all in the name of capturing every bit of data from our interactions and selling it for a huge profit.

I'm a firm believer in taking ownership of one's information presence online and being in control of the data that is created and shared. This blog is my attempt to not only express myself, share my personal projects, and let others know about who I am, but also to learn the various technologies of the modern web to enable my own digital soverignty.

<!-- more -->

## Finding a Framework

My [background](/about) is in electronic hardware and embedded systems, and so the code that I tend to write is either low level systems programming (C/C++) or scripting (Python). Even though Javascript is the language of the Web, I don't know how to write it. I also take issue with its many known [quirks](https://wtfjs.com) and [security vulnerabilities in many JS packages and frameworks](https://thesecurityvault.com/security-of-the-npm-packages/).

```javascript
// JavaScript being... itself
>>> [1, 2, 3, 15, 30, 7, 5, 45, 60].sort()
[1, 15, 2, 3, 30, 45, 5, 60, 7]
```

These were a few of my design goals:
- minimal tooling (compiled single binary a plus)
- small attack surface (memory safe language a plus)
- statically rendered
- easily customizable, but opinionated
- responsive / works well on mobile
- existing themes that look good

This is a good job for a static site generator and I had [a lot to choose from](https://jamstack.org/generators/). I started with Next.js and worked through some tutorials. While I like the power of React components and its ability to use Typescript instead of Javascript, I eventually ran into security issues in dependencies that I didn't know how to resolve. I decided to try my hand at [Hugo](https://gohugo.io/) instead.

The [Hugo framework](https://github.com/gohugoio/hugo) and [it's templates](https://pkg.go.dev/text/template) are written in [Go](https://go.dev/), and there are many great [themes](https://themes.gohugo.io/) to support it. The project has an active community and lots of examples. I used Hugo to build my other website [Jacana.io](https://jacana.io). 

I didn't want to limit myself to just a single framework, however, and was interested in finding one built in Rust to make this site. [Rust](https://www.rust-lang.org/) is another systems language I'm interested in learning, and I wanted to use projects that would eventually allow me to contribute to its ecosystem. Once again I browsed [Jamstack](https://jamstack.org/generators/), and found [MdBook](https://rust-lang.github.io/mdBook/) and [Zola](https://www.getzola.org/). MdBook looks really nice, but it's meant for documentation and books more than blogs and personal sites. That left Zola.

## Zola (né Gutenberg)
Zola does everything I need, in Rust, with an [active community](https://github.com/getzola/zola), and [lots of themes](https://www.getzola.org/themes/) to choose from and modify. The content is written in a strongly defined version of [Markdown](https://www.markdownguide.org/) called [CommonMark](https://commonmark.org/), and it uses a template engine called [Tera](https://tera.netlify.com/). So far I'm really happy with it and found it quite easy to get started.

## Hosting (and VCS)
I'm not at the point in my skillset where I feel comfortable hosting a website on my own self-run infrastructure, and so I decided to go with a hosting service, but one that promotes open-source software and respects my privacy. Free hosting would also be a nice perk.

One of the cool features of both GitHub and GitLab is that they can host the Git repository, build static assets, and host them on their own servers and CDNs, all automatically and triggered by a push from my laptop. They both also support custom domain names and automatic provisioning of SSL certificates with [Let's Encrypt](https://letsencrypt.org/), all for free.

I went with GitLab since they allow their service to be self-hosted much easier than GitHub, and they also aren't a Microsoft subsidiary. You can check out the source for this site [here](https://gitlab.com/pdlloyd/pdlloyd.com). Unfortunately, due to a [pretty lame bug](https://gitlab.com/gitlab-org/gitlab/-/issues/15921), I had to wait a week to set up the build pipeline but eventually got it working. C'est la vie.

## Conclusion
The technology stack involved in getting my ideas onto your screen is immense -- from the tools that build and format the content, to the servers that host it, to the protocols that serve it, it makes sense why paid services exist to make this stuff easier. I'm clearly not so much of a purist as to avoid using other peoples' computers, but I would if I could and hope to eventually. 
