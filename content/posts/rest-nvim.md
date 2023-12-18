---
title: rest.nvim - a neovim plugin for rest calls
description: Goodbye Postman!
date: 2023-12-01T00:00:00Z
categories:
  - blog
tags:
  - neovim
  - plugin
list_image: images/rest-nvim.png
main_image: images/rest-nvim.png
---

# why?

In the continual quest to never leave neovim, I stumbled across a plugin to make REST calls.

Like the vast majority of developers I have used Postman over the years for this task, but obviously that requires me to switch applications, and possibly (shock horror) use the mouse.

# how?

## plugin

The plugin repo is here: https://github.com/rest-nvim/rest.nvim

## setup

This is my plugin definition for Lazy:

```lua
{
    "rest-nvim/rest.nvim",
    dependencies = { { "nvim-lua/plenary.nvim" } },
    lazy = true,
    keys = {
      { "<leader>x", "<Plug>RestNvim",
        desc = "Execute request"
      }
    },
    config = function()
      require("rest-nvim").setup({
        result_split_in_place = true
      })
    end
}
```

> The option **result_split_in_place** is there to override the (somewhat odd) default of having the result replace the call window.
> With **result_split_in_place = true** the result is opened in a split to the right of the current buffer, which to me is the most obvious choice.

## usage

Simply define the calls in a buffer, and, with the cursor in one of the call blocks, trigger the configured key map

```nginx
# a simple GET example
GET https://reqres.in/api/users?page=5
a-header: something

# POST example
# define the body after the headers
POST https://something.com/
content-type: application/json

{
  "name": "wheelibin"
}
```

The call is then executed and the result is opened in a split, resulting in something like the below.

{{< figure class="post-image" src="/images/rest-nvim.png" >}}
