---
title: "How I set up my Go development environment"
date: 2022-05-26
# weight: 1
# aliases: ["/first"]
tags: ["Go", "environment"]
author: "Soroush Mirzaei"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "How I set up my Go development environment for maximum productivity, and correctness."
# canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: false
ShowPostNavLinks: false
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
editPost:
    URL: "https://github.com/smirzaei/soroush.codes/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

In this post, I'm going to explain how I set up my development environment mainly for developing Golang applications. I'll be using VS Code but I'm sure you can use the same tooling if you are developing in GoLand.

Also I'll be skipping the obvious parts such as how to install VS Code or the Go compiler itself.

## First things first, we need a good linter

I highly recommend using [`golangci-lint`](https://golangci-lint.run). It's very vast, and combines multiple lint tools including [`staticcheck`](https://staticcheck.io) which is one of my favorite tools and [is enabled by default](https://golangci-lint.run/usage/linters).

Enabling it on VS Code is just as easy as going to the settings and selecting `golangci-lint` for your Go lint tool. Or you can edit the `settings.json` file (type "open settings (JSON)" in the command palette) and adding the following line:

```JSON
{
    "go.lintTool": "golangci-lint"
}
```

 After selecting it, the editor will ask you to install a few dependencies (if you don't have them already).

## Second, let's break the long lines

I work in different environments. At home I do have a wide monitor but while coding on the go (No pun intended 😆), I'm left with my laptop's monitor which is not ideal for reading long lines. To fix this problem, I've found this handy formatter called [`golines`](https://github.com/segmentio/golines) which shortens the long lines.

Basically it changes this:

```GO
myMap := map[string]string{"first key": "first value", "second key": "second value", "third key": "third value", "fourth key": "fourth value", "fifth key": "fifth value"}
```

To this:

```GO
myMap := map[string]string{
	"first key": "first value",
	"second key": "second value",
	"third key": "third value",
	"fourth key": "fourth value",
	"fifth key": "fifth value",
}
```

In my opinion, it looks much more readable no matter how wide your display is.

In order to install it, you need to first install the executable by running:

```BASH
go install github.com/segmentio/golines@latest
```

Then install [`Run On Save`](https://marketplace.visualstudio.com/items?itemName=emeraldwalk.RunOnSave) extension for VS code, which allows you to run a command when a file is saved.

Now open `settings.json` file (type "Open settings (JSON)" in the command palette) and add the following config:

```JSON
{
    "emeraldwalk.runonsave": {
        "commands": [
            {
                "match": "\\.go$",
                "cmd": "golines ${file} -w"
            }
        ]
    }
}
```

The default behavior, shortens the lines that are longer than 100 columns. If you want to change this number you can use the `-m` flag, for example: `"cmd": "golines ${file} -w -m 80"`. I'm pretty happy with the default configuration.

## Finally, a list of extensions that I find useful (in no particular order)

* [Better Comments](https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments)
* [Error Lens](https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens)
* [Lowlight Go Errors](https://marketplace.visualstudio.com/items?itemName=ohanedan.lowlight-go-errors) (It reduces a lot of clutter)
* [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)
* [Output Colorizer](https://marketplace.visualstudio.com/items?itemName=IBM.output-colorizer)
* [Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)
* [Change Case](https://marketplace.visualstudio.com/items?itemName=wmaurer.change-case)
* [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)
* [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)
* [File Utils](https://marketplace.visualstudio.com/items?itemName=sleistner.vscode-fileutils)
* [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
* [Go](https://marketplace.visualstudio.com/items?itemName=golang.Go) (Duh!)
* [indent-rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow) (Very useful, specially if you need to work with Python scripts)
* [Jumpy](https://marketplace.visualstudio.com/items?itemName=wmaurer.vscode-jumpy)
* [Run On Save](https://marketplace.visualstudio.com/items?itemName=emeraldwalk.RunOnSave)
* [Trailing Spaces](https://marketplace.visualstudio.com/items?itemName=shardulm94.trailing-spaces)
* [vscode-position](https://marketplace.visualstudio.com/items?itemName=jtr.vscode-position) (Excellent tool if you need to debug errors that give you the position of the offending characters)

