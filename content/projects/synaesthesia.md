---
title: Synaesthesia
description: Randomly generated music in the browser
date: 2018-09-08T00:00:00Z
categories:
  - project
tags:
  - javascript
  - tone.js
  - random
repo_url: https://github.com/wheelibin/synaesthesia
demo_url: https://wheelibin.github.io/synaesthesia/
main_image: images/synaesthesia.png
list_image: images/synaesthesia.png
---

# About

This is a little experiment with creating randomly generated music in the browser.

It uses the amazing [Tone.js](https://tonejs.github.io/) (a wrapper around the Web Audio API).

All the sounds are generated using various Synth instruments from Tone.js, there are no samples.

## How it works

The "song" is generated like so:

- A key is chosen (root note and scale, e.g. A Minor)
- A chord progression is generated for the key
- A bassline is generated for the chord progression
- A simple higher octave part is generated for the chord progression
- Drums patterns for kick, snare, hihat, shaker, openhat are chosen to create percussion
- A random BPM is chosen within a certain range
- A random swing amount is chosen

All the elements are randomly chosen from various arrays, collections of instruments, and patterns.

The random number generator is seeded to allow recreation of the same randomly selected song.
