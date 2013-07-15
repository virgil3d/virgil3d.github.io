---
title: Questions about Virgil project
---

# Questions about Virgil project

This page is a bunch of questions I've asked myself.

## How do I get this running?
Currently you'd be willing to spend a lot of time learning the code base and wanting to develop on this before you'd get it running. I'm not providing instructions at the moment, as I don't have time to support people who won't contribute back much. The project doesn't need "testing" at the moment, since I've got an endless list of things to fix, it needs "developing".

## Major pitfalls?
It leaks like a sieve.

It fails a lot of renderering.

It crashes some drivers.

## What drivers does this run on, what GL requirements
Plans are to target GL2.1 + GLSL 1.20 as the possible lowest GL interface to support. The guest would then expose the same level of GL. Currently the renderer is GLSL 1.30 based, and requires some extensions from later GL levels. I've only really tested on the open source nouveau driver exposing GL3.0/GL3.1 core profile, and the binary nvidia driver exposing GL 4.3. Future plans to add a capabilities system will be required to work make things work across more systems.
The current guest driver exposes GL2.1 and GLSL 1.20.

## What is obviously missing.
The main missing feature missing at this time for proper GL2.1 support are queries (occlusion, timers). Beyond that GLSL1.30 and GL3.0 features will need investigating. Transform feedback is also currently missing.

## Can I run wayland/weston in the guest?
There is currently no vblank support in the guest. Plans to emulate vblank support using a timer in the future, no idea when though, this would enable running wayland/weston.

## Why use Gallium3D as the transport?
The other options for a transport were OpenGL or Direct3D based. Something like GLES2 subset of GL might have been possible to transport simply, but the OpenGL API is quite vast and having to deal with every corner case and fallback for it would have been a lot of work. Direct3D based would also have been possible, but the API is externally controlled and wasn't seen a good basis for this work. Gallium3D API is a concise API reflecting both the needs of OpenGL and Direct3D users for drivers in the Mesa project, and it was seen as the most practical place to start.

## SPICE
### Is this project related to SPICE?

The spice project also created by Red Hat is a remote virtualisation solution for the VDI space. It concentrates on remoting 2D rendering commands. This project is developed independently of SPICE and is not intended to replace it. Remoting 3D rendering using the techniques spice uses is not considered practical by the author, also the spice architecture relies on rendering capabilities in the server side that mean the same 3D gpu would be required on client and host side in order to guarantee the same results. This project is starting from a simpler place in order to build up knowledge of how 3D virtualisation can be done.

