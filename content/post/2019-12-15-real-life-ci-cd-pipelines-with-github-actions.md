---
title: "Real-life CI/CD pipelines with Github Actions"
author: Tobias (DH1TW)
date: 2019-12-12T12:00:38+01:00
layout: post
categories:
  - Software
  - Golang
tags:
  - continuous-integration
  - docker
  - github
thumbnailImage: "img/2019/12/octocat-actions.jpg"
thumbnailImagePosition: "left"
---

Earlier this year, [Github](https://github.com) released their *workflow automation tool* [Actions](https://github.com/features/actions). Github claims to provide nothing less than *world class* CI/CD with [Actions](https://github.com/features/actions). After it's release in Autumn 2019, I took the chance and migrated the multi-stage CI Pipeline of [remoteAudio](https://github.com/dh1tw/remoteAudio) to Github Actions.

Now it's time to share [the **good**, the **bad** and the **ugly**](https://en.wikipedia.org/wiki/The_Good,_the_Bad_and_the_Ugly) parts of [Github Actions](https://github.com/features/actions).

<!--more-->

## How Actions work

I have to admit that Github Actions are much more than just a Continuous Integration / Continuous Delivery tool. I fully share their official slogan of being a **workflow automation tool**. That sad, generalization unfortunately comes often with a cost. But before we go into the details, let me briefly explain how Github Actions work. The following section is not meant to replace the [official documentation](https://help.github.com/en/actions/automating-your-workflow-with-github-actions), but rather to give you an idea about the concepts behind Github Actions.

{{< figure src="/img/2019/12/github-actions-workflow.jpg" height=500px caption="Figure 1: Github Actions Workflows in a nutshell" >}}

### Workflows

Everything is organized in **Workflows**. Workflows are written in [YAML](https://yaml.org) and live in the `/.github/workflows` directory of your repository. Workflows are independent of each other. Workflows are triggered by either an Event (e.g. Push or Pull Request) or scheduled ([cron style](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/configuring-a-workflow#triggering-a-workflow-with-events)).

### Jobs

A workflow contains one or more jobs. A job basically consists of two parts. First you do the job setup (specifying build platform, matrix parameters, run strategy, ...) then you run the real tasks or *steps*, how they are called in Actions. A job can depend on previous jobs, however only on jobs within the same workflow. Jobs can run in parallel.

### Steps

Steps are a set of tasks performed as part of a job. This is where the work gets done. Steps can either run commands or Actions. There is an evolving [Marketplace](https://github.com/marketplace?type=actions) with predefined actions which can be easily used. Steps run sequentially, but are executed in isolation (actually as containers). They only share the same filesystem.

## My CI workflow

The application [remoteAudio](https://github.com/dh1tw/remoteAudio) is an audio streaming application written in [golang](https://golang.org). It has a small footprint and runs well on embedded or desktop devices. I try [to provide binaries](https://github.com/dh1tw/remoteAudio/releases) for as many platforms as possible.

For native [golang](https://golang.org) code, the compiler handles cross compilation fine. However when `cgo` and platform specific C libraries are involved, things get a bit more complicated. I have dedicated an entire blog post on [how I cross compile cgo based projects](/content/post/2019-12-08-crosscompiling-golang-cgo-projects.md), in case you are curious.

So basically the CI pipeline consists of the following steps:

1. Execute the build process for all platforms on `push` and `pull_request`. Stash the build artifacts temporarily
2. Create a [release](https://help.github.com/en/github/administering-a-repository/creating-releases) if our commit is tagged
3. Upload and attach the build artifacts to the corresponding [release](https://github.com/dh1tw/remoteAudio/releases)

{{< figure src="/img/2019/12/remoteaudio-ci-workflow.jpg"
           link="/img/2019/12/remoteaudio-ci-workflow.jpg"
           caption="Figure 2: CI Workflow for remoteAudio (click to enlarge)" >}}

You can find the [complete workflow](https://github.com/dh1tw/remoteAudio/blob/master/.github/workflows) in the [remoteAudio](https://github.com/dh1tw/remoteAudio) repository. Since it is over 200 lines long, I prefer not to paste it into this article.

{{< figure src="/img/2019/12/remoteaudio-ci-workflow-screenshot.jpg"
           link="https://github.com/dh1tw/remoteAudio/blob/master/.github/workflows" >}}

I consider this CI pipeline nothing overly complicated, but somewhat more advanced than the average example pipeline.

In the following chapters we will dive into the details and discuss the **good**, the **bad** and the **ugly** parts of Github Actions.

## The Good

### Beefy VMs & generous quotas

Github Actions run on the [Microsoft's Azure cloud](https://azure.microsoft.com). Jobs can run on Linux, Windows and MacOS. The machines are really fast and spin up almost immediately, once the workflow has been triggered. By the time of writing, the VMs come with 2 CPU cores, 7GByte of RAM and 14Gbyte of SSD disk space. The [VM images](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/software-installed-on-github-hosted-runners) are well maintained and come with a [ton of pre-installed software](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/software-installed-on-github-hosted-runners). Workflows and jobs within workflows can be executed in parallel. Since I'm compiling remoteAudio for 6 platforms at once, this is a huge time saver. For now, Github Actions allow *unlimited* build time for public repositories. But also for private repositories, you'll get 2000 minutes / month for free.

Overall, I have to say that this is **very generous**. I couldn't be happier with the performance of the runners.

If all of that isn't enough, you can set up and incorporate your own [self hosted Runners](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/using-self-hosted-runners-in-a-workflow) within Actions.

### Flexibility

Github Actions can either be a [Docker](https://docker.com) container or a [Node.js](https://nodejs.org) application.
**That's pretty powerful!** You can write custom Actions in the programming language of your choice, doing (almost) everything you ever wanted to do in a CI Pipeline. Literally your imagination is the limit. This site explains everything to get you started [with your own custom Actions](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/about-actions).

### Github Integration

Well, Actions wouldn't be a Github service if it wasn't well integrated with other Github services. Getting started with Actions is really easy. While in other CI systems you first have to generate and manually encrypt an API access token, with Actions, this is done automatically for us.

By having a look at the [events that can trigger workflows](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/events-that-trigger-workflows) we clearly see that Actions is much more than just a CI system. You can automate almost any aspect of your Github repo, including fine grain event triggers on Issues and Wikis.

### Secret Management

Secret Management has been implemented straight forward and is really easy to use. Instead of storing sensitive information, like passwords within your workflow document, you store them in your Project's `Settings > Secrets` engine and query them directly from within your workflow. Github related keys, like the `GITHUB_TOKEN` are automatically available.

{{< figure src="/img/2019/12/github-secrets.jpg"
           caption="Figure 3: Secret Management in Github">}}

Retrieving a secret is as easy as:

```html {hl_lines=[6]}
  steps:
    - name: Create Release
      id: create_release
      uses: actions/create-release@v1.0.0
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      with:
[...further details omitted]
```

### Status badge

Who doesn't love Status badges? Actions provides automatically a status badge for your workflow. They can be easily embedded in your `readme.md` and if desired, filtered by `branch`.

![Build Status](https://github.com/dh1tw/remoteAudio/workflows/Cross%20Platform%20build/badge.svg?branch=master)

```markdown
![Build Status](https://github.com/dh1tw/remoteAudio/workflows/Cross%20Platform%20build/badge.svg?branch=master)
```

## The bad

### Limited git/repo information

Within Actions, a couple of [Context objects](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/contexts-and-expression-syntax-for-github-actions) are available. One of them is the [Github context](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/contexts-and-expression-syntax-for-github-actions#github-context). You can use the values of these context objects in your workflow to some extend.

Examples:

- `github.sha` provides for example the SHA1 fingerprint of the current commit
- `github.ref` provides the branch or tag name that triggered the workflow

Sound good, yes? Well, actually there are a lot of fundamental values missing. Imagine you need the `branch` *and* `tag` of a commit. Well, that's not possible. Want the `short SHA` of the commit? Again, not available. **A lot of basic git information is missing**. Just have a look at the information available in [Gitlab CI workflows](https://docs.gitlab.com/ee/ci/variables/README.html#syntax-of-environment-variables-in-job-scripts) or in [TravisCI workflows](https://docs.travis-ci.com/user/environment-variables/#default-environment-variables).

So if we want to use a slugged version of our `tag`, we have to first extract it in one step. Afterwards we have to copy the output variable `VERSION` of that step into a environment variable of all consecutive steps where it is needed. Since jobs are completely independent of each other, we have to include this code in all the jobs where we need the slugged version of our tag.

```yaml {hl_lines=[5,9]}
# [non relevant details omitted...]
  steps:
    - name: Get the version (git tag)
      id: get_version
      run: echo ::set-output name=VERSION::${GITHUB_REF/refs\/tags\//}

    - name: Print semver tag
      env:
        VERSION: ${{ steps.get_version.outputs.VERSION }}
      run: echo $VERSION
```

### Immature Actions

By the time of writing, the [Github Marketplace for Actions](https://github.com/marketplace?type=actions) showed close to 2000 available Actions. After poking around with a few actions I found the maturity and quality of most Actions sobering. This applies to 3rd-party Actions and Actions maintained directly by Github. Granted, Github Actions are publicly available for just about 3 month. I fully expect that the maturity will improve over time.

One example is the [actions/upload-release-asset](https://github.com/actions/upload-release-asset). It is quite common practice to include the semantic version tag (e.g. `v0.5.3`) in the asset's / archive's name. In other CI systems, we can include environment variables in the parameters. Here we can't. So setting `asset_path` and `asset_name` as shown below is unfortunately not possible.

```yaml {hl_lines=[9,10]}
# [non relevant details omitted...]
    - name: Upload Release Artifact ${{ matrix.version }}
      uses: actions/upload-release-asset@v1.0.1
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        VERSION: ${{ steps.get_version.outputs.VERSION }}
      with:
        upload_url: ${{ steps.get_release_url.outputs.URL }}
        asset_path: ./remoteAudio-$VERSION-${{ matrix.OS }}-${{ matrix.ARCH }}.zip
        asset_name: remoteAudio-$VERSION-${{ matrix.OS }}-${{ matrix.ARCH }}.zip
        asset_content_type: application/gzip
```

As a workaround, we have to add the intermediary step `prepare_artifact_metadata` in which we create the strings for `asset_path` and `asset_name`.

```yaml {hl_lines=[7,8,15,16]}
[non relevant details omitted...]
    - name: Prepare artifact metadata
      id: prepare_artifact_metadata
      env:
        VERSION: ${{ steps.get_version.outputs.VERSION }}
      run: |
        echo ::set-output name=ARTIFACT_PATH::./remoteAudio-$VERSION-${{ matrix.OS }}-${{ matrix.ARCH }}.zip
        echo ::set-output name=ARTIFACT_NAME::remoteAudio-$VERSION-${{ matrix.OS }}-${{ matrix.ARCH }}.zip
    - name: Upload Release Artifact ${{ matrix.version }}
      uses: actions/upload-release-asset@v1.0.1
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      with:
        upload_url: ${{ steps.get_release_url.outputs.URL }}
        asset_path: ${{ steps.prepare_artifact_metadata.outputs.ARTIFACT_PATH }}
        asset_name: ${{ steps.prepare_artifact_metadata.outputs.ARTIFACT_NAME }}
        asset_content_type: application/gzip
```

### Insufficient filtering

Actions only allow to do some filtering on the triggered events on a *per-workflow* basis. In Continuous Integration pipelines we often want to execute jobs only when certain conditions are met. For example, we only want to create a deployment when a commit is on the `master` branch **AND** has a `tag`.

The `on` keyword provides some filtering:

```yaml
on:
  push:
    # Sequence of patterns matched against refs/heads
    branches:
      - master         # Push events on master branch
      - 'mona/octocat' # Push events to branches matching refs/heads/mona/octocat
      - 'releases/**'  # Push events to branches matching refs/heads/releases/10
    # Sequence of patterns matched against refs/tags
    tags:
      - v1             # Push events to v1 tag
      - v1.*           # Push events to v1.0, v1.1, and v1.9 tags

```

**BUT**, all those filters are logically **OR**ed. By today there is no way to trigger a workflow which meet a condition on branches **AND** tags.

### Limited helper functions

Actions provide [operators](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/contexts-and-expression-syntax-for-github-actions#operators) and [functions](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/contexts-and-expression-syntax-for-github-actions#functions) which allow us to evaluate certain conditions or do basic string transformation. Some examples are `format( string, replaceValue0, replaceValue1, ..., replaceValueN)` or `join( element, optionalElem )`. Unfortunately, that's too basic. The missing support of RegEx hurts. In my case, the missing functions have lead to additional intermediary steps in which I had to do the string transformations in the shell.

## The ugly

### No shared Variables

There is no way to define common variables between jobs. This sucks big time. For example, after creating a release, the release URL has to be provided to the job that actually uploads the artifact to the release. If you have implemented a *fan-in/fan-out* matrix jobs as I have with remoteAudio, you will find yourself in a situation that you can not pass the string, containing the upload URL, to the upload jobs in the matrix.

My workaround is to store the release URL in a *textfile*, upload it as a build artifact and then download it again in the respective upload job. This workaround looks like this:

```yaml {hl_lines=[12,14,29,35]}
  create_release:
    runs-on: ubuntu-18.04
    needs: [build_linux, build_macos, build_windows]
    if: startsWith(github.ref, 'refs/tags/v')
    steps:
    # [non relevant details omitted...]
    # since jobs can not share any variables we have to copy the URL of the created Github release
    # into a file and stash it as an artifact
    - name: Copy release URL into file
      run: |
        mkdir release
        printf "%s" "${{ steps.create_release.outputs.upload_url }}" > release/url.txt
    - name: Stash file containing the release URL as an artifact
      uses: actions/upload-artifact@v1
      with:
        name: release-url
        path: ./release

  upload:
    runs-on: ubuntu-18.04
    needs: create_release # release must be created before this job can start
    strategy:
      matrix:
        version: ['linux-armhf', 'linux-arm64', 'linux-i386', 'linux-amd64', 'darwin-amd64', 'windows-amd64', 'windows-i386']
    steps:
    # [non relevant details omitted...]
    # Download the previously uploaded artifact which contains the release URL
    - name: Retrieve stashed release URL
      uses: actions/download-artifact@v1
      with:
        name: release-url
    # Write content of downloaded file (a string which contains the release URL) into a step.outputs variable
    - name: Read release URL
      id: get_release_url
      run: echo ::set-output name=URL::$(cat release-url/url.txt)
    # [non relevant details omitted...]
```

By contrast, below you find all you need to create a release and upload the artifacts with [TravisCI](https://travis-ci.com). Quite a difference, eh?

```yaml
# [non relevant details omitted...]
deploy:
  provider: releases
  api_key:
    secure: "encrypted token"
  file: remoteAudio-$TRAVIS_TAG-$GIMME_OS-$GIMME_ARCH.tar.gz
  skip_cleanup: true
  on:
    repo: dh1tw/remoteAudio
    tags:
      true
    draft: true
    go: "1.13"
```

### Don't repeat yourself

When I learnt programming, one of the mantras I heared over and over was: **DRY - Don't repeat yourself**. As you have seen in the examples above, we are forced to copy & paste the same code over and over. This obviously makes increasingly complex workflows less and less maintainable. By today, Github Actions doesn't provide a way for reusing code blocks, other than implementing them into Actions. I think Github should provide a way to reuse jobs or partial workflows.

## Summary

As you can see, it took me quite some time to wrap my head around Github Actions. After a few quick wins, I unfortunately hit several times a wall. If your CI pipeline is a bit more sophisticated then the rudimentary examples, you will find yourself implementing more than one *dirty* workaround due to missing functionality or current limitations of Github Actions.

IMHO, Github Actions is still far away from providing *worldclass CI/CD*. That said, I recognize that they are providing this service actually for free for all Open Source repositories. The underlying hardware is *kickass* and the runners are blazing fast. Let's hope, that Github listens to the users and fixes the shortcomings over time.
