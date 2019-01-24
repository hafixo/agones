---
title: "Documentation Editing and Contribution"
linkTitle: "Contribute"
weight: 1000
description: >
  How to contribute to the docs
---

## Writing Documentation

We welcome contributions to documentation! 

## Running the site

If you clone the repository and run `make site-server` from the `build` directory, this will run the live hugo server, 
running as a showing the next version's content and upcoming `publishedDate`'d content as well. This is likely to be
the next releases' version of the website.

To show the current website's view, run it as `make site-server ENV=RELEASE_VERSION={{< release-version >}} ARGS=`

## Platform

This site and documentation is built with a combination of Hugo, static site generator,
with the Docsy theme for open source documentation.

- [Hugo Documentation](https://gohugo.io/documentation/)
- [Docsy Guide](https://github.com/google/docsy)

## Documentation for upcoming features

Since we may want to update the existing documentation for a given release, when writing documentation,
you will likely want to make sure it doesn't get published until the next release.

There are two approaches for hiding documentation for upcoming features, such that it only gets published when the
version is incremented on the release:

### At the Page Level

Use `publishDate` and `expiryDate` in [Hugo Front Matter](https://gohugo.io/content-management/front-matter/) to control
when the page is displayed (or hidden). You can look at the [Release Calendar](https://github.com/GoogleCloudPlatform/agones/blob/master/docs/governance/release_process.md#release-calendar)
to align it with the next release
candidate release date - or whichever release is most relevant.  

### Within a Page

We have a `feature` shortcode that can be used to show, or hide sections of pages based on the current semantic version
(set in config.toml, and overwritable by env variable).

For example, to show a section only from 0.8.0 forwards: 

> remove the initial "\" in front of the % - needed to escape the shortcode

```markdown
{{\% feature publishVersion="0.8.0" %}}
  This is my special content that should only display >= 0.8.0
{{\% /feature %}}
```

or to hide a section from 0.8.0 onward:

```markdown
{{\% feature expiryVersion="0.8.0" %}}
  This is my special content that she be hidden <= 0.8.0
{{\% /feature %}}
```

> Due to [this hugo bug](https://github.com/gohugoio/hugo/issues/4695) headers wrapped in this shortcode will
  not be displayed in the Table of Contents. So we will need to actively remove the `feature` shortcode once
  the release versions have been passed for new content, for content that is affected.