---
title: Hugh
description: Automated Hue light control
date: 2023-11-25T00:00:00Z
categories:
  - project
tags:
  - go
  - hue_lights
repo_url: https://github.com/wheelibin/hugh
code_language: typescript
main_image: images/hugh.png
list_image: images/hugh.png
---

# About

Hugh is a service that runs on your computer and automates your [Philips Hue](https://www.philips-hue.com/en-gb) lights.

The main purpose is to automate the colour temperature of your lights throughout the day, taking the local sunset/sunrise into account.
Think of it like [f.lux](https://justgetflux.com/), [redshift](https://github.com/jonls/redshift), or Apple's Night Shift for your home's lights.

## Schedules

An example Hugh schedule might look like this:

| time       | colour temp | brightness |
| :--------- | ----------: | ---------: |
| sunrise    |        2000 |         40 |
| sunrise+1h |        2890 |         80 |
| sunrise+2h |        4291 |        100 |
| sunset-2h  |        3500 |        100 |
| sunset-1h  |        2890 |        100 |
| sunset     |        2890 |         80 |
| sunset-1h  |        2300 |         70 |
| 23:00      |         off |        off |

Hugh will then smoothly transition between the different points as the day goes on.

Local sunrise/sunset is calculated every day.

## Tech

Hugh is written in go and uses the Philips Hue API to control the lights.

It takes advantage of the V2 API which provides server-sent events for changes to lights which means the hue bridge doesn't have to be constantly polled for their latest status.
