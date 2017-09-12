---
layout: post
published: false
mathjax: true
featured: false
comments: false
title: Build a Small Robot
description: Small Robot Controlled Remotely by JavaScript App
headline: Build a Small Robot
categories:
  - personal
  - interesting
  - JavaScript
  - Robotic
tags: chOpen JavaScript Robotic
---
## Tools
### Digital design for the Hardware Production
- "Inkscape" for svg data for laser cutter
- "TinkerCAD" for 3D printer
- "Cura" is the 3D software coming with the printer itself
- "OnShape" a good CAD alternative

## Programming the Remote Control
- johnny-five API
- different hardware plugs and there configuration
- Communication with Firmata Protocol

### Node.js
- Only one thread and this one is handled
- Asynchronous event listeners

## The Robot
The central unit is a NodeMCU with an underlying RTOS and a Firmata Receiver unit.
The file wifiConfig.h configures the wireless connection to upload data and connect the remote.

### Hardware
- SumoBot (nodebots.ch)
- NodeMCU ESP8266
- LIS3DH (Accelerometer)
- LED Matrix HT16K33 8x8
