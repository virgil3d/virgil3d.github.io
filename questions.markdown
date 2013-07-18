---
title: Questions about Virgil project
---

# Questions about Virgil project

## What are Red Hat's intentions for this project?
Well its mostly a personally driven project by me that I've wanted to attempt for a long time. Red Hat have kindly managed to find some time to let me go for it and do as much research on what is needed to create a solution to 3D inside a virtual machine. However at the moment there is no commitment to maintain or support this going forward, if this changes I'll let people know. For now I'm just developing it in between my other work commitments.

## How do I get this running?
Currently you'd be willing to spend a lot of time learning the code base and wanting to develop on this before you'd get it running. I'm not providing instructions at the moment, as I don't have time to support people who won't contribute back much. The project doesn't need "testing" at the moment, since I've got an endless list of things to fix, it needs "developing". The trees are not guaranteed at the moment to build and run at any specific moment as I'm still in heavy development mode.

## Major pitfalls?
It leaks like a sieve.

It fails a lot of renderering.

It crashes some drivers.

## What drivers does this run on, what GL requirements?
Plans are to target GL2.1 + GLSL 1.20 as the possible lowest GL interface to support. The guest would then expose the same level of GL. Currently the renderer is GLSL 1.30 based, and requires some extensions from later GL levels. I've only really tested on the open source nouveau driver exposing GL3.0/GL3.1 core profile, and the binary nvidia driver exposing GL 4.3. Future plans to add a capabilities system will be required to work make things work across more systems. The
capabilities system will expose different guest GL levels dependant on the
host GL level, this could allow for a GLES2 specific interface etc.
The current guest driver exposes GL2.1 and GLSL 1.20.

## What is obviously missing?
The main missing feature missing at this time for proper GL2.1 support are queries (occlusion, timers). Beyond that GLSL1.30 and GL3.0 features will need investigating. Transform feedback is also currently missing.

## Can I run wayland/weston in the guest?
There is currently no vblank support in the guest. Plans to emulate vblank support using a timer in the future, no idea when though, this would enable running wayland/weston.

## Why use Gallium3D as the transport?
The other options for a transport were OpenGL or Direct3D based. Something like GLES2 subset of GL might have been possible to transport simply, but the OpenGL API is quite vast and having to deal with every corner case and fallback for it would have been a lot of work. Direct3D based would also have been possible, but the API is externally controlled and wasn't seen a good basis for this work. Gallium3D API is a concise API reflecting both the needs of OpenGL and Direct3D users for drivers in the Mesa project, and it was seen as the most practical place to start.

## What are the performance expectations?
So far I've been just running openarena and gnome-shell inside my guest, the
speed is in the range or 40-50% of native, but can be improved a lot. There
is a lot of work to see how other apps work once the basics are covered.

## Is there any security considerations?
Since in order to go fast, qemu will have to link with the mesa or closed libGL,
there maybe be possibilites for security issues in these drivers like buffer
overflows, similiar to what WebGL has. However these should be containable in
some ways and otherwise Mesa will require fixes like it does for WebGL vulnerabilities.

## Can we avoid GL on the host and go straight to gallium?
This is probably possible, I've avoided this as we have non-gallium drivers
like Intel and the closed source drivers, however if there was shown to be
an advantage to doing a virgil state tracker to accept data direct from qemu
then it might be a nice side project.

## SPICE
### Is this project related to SPICE?

The spice project also created by Red Hat is a remote virtualisation solution for the VDI space. It concentrates on remoting 2D rendering commands. This project is developed independently of SPICE and is not intended to replace it. Remoting 3D rendering using the techniques spice uses is not considered practical by the author, also the spice architecture relies on rendering capabilities in the server side that mean the same 3D gpu would be required on client and host side in order to guarantee the same results. This project is starting from a simpler place in order to build up knowledge of how 3D virtualisation can be done.

