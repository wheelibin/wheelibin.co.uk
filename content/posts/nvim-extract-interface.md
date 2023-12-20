---
title: "vim tip: select all lines matching pattern"
description: "extract interface?"
date: 2023-12-10T21:30:50Z
categories:
  - blog
tags:
  - neovim
list_image: images/neovim.png
---

## Background

Various IDEs/tools I have used over the years have provided a code action `Extract Interface`, which would take the function signatures of a class and produce an interface from them.

I found myself needing to do this in `Neovim` and went looking for a solution.

## A vim way?

Essentially `Extract Interface` boils down to "Copy all function signatures to a new code block".

To get us most of the way there then we can further simplify this to `Copy all lines matching a pattern`.

It turns out this is very simple in vim/neovim:

### Copy

```vim
" clear register a
qaq
" yank all lines matching patten into register a
:g/pattern/y A
```

### Paste:

```vim
"ap
```

## An example using go

```go
func (h *HueAPIService) GetRooms() ([]models.HughGroup, error) {
    ...
}

func (h *HueAPIService) GetZones() ([]models.HughGroup, error) {
    ...
}

func (h *HueAPIService) GetAllGroups() ([]models.HughGroup, error) {
    ...
}
```

First we clear the register we are using

```vim
qaq
```

Then we copy the function signature lines

```vim
:g/func (h \*Hue/y A
```

#### Then we can paste these lines into an empty interface declaration

```go
type SomeInterface interface {
  // cursor here
}
```

Paste from register a

```vim
"ap
```

We then have something like this.

```go
type SomeInterface interface {
    func (h *HueAPIService) GetRooms() ([]models.HughGroup, error) {
    func (h *HueAPIService) GetZones() ([]models.HughGroup, error) {
    func (h *HueAPIService) GetAllGroups() ([]models.HughGroup, error) {
}
```

All that's left to do is remove some extra things from the lines, but simple find/replace can easily take care of that.

> yes, just blindly creating an interface from something is usually not the way to work in go, this is purely an example
