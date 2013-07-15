---
title: Questions about Virgil project
layout: default
---

# Questions about Virgil project

This page is a bunch of questions I've asked myself.

## Why use Gallium3D as the transport?
The other options for a transport were OpenGL or Direct3D based. Something like GLES2 subset of GL might have been possible to transport simply, but the OpenGL API is quite vast and having to deal with every corner case and fallback for it would have been a lot of work. Direct3D based would also have been possible, but the API is externally controlled and wasn't seen a good basis for this work. Gallium3D API is a concise API reflecting both the needs of OpenGL and Direct3D users for drivers in the Mesa project, and it was seen as the most practical place to start.

## SPICE
### Is this project related to SPICE?

The spice project also created by Red Hat is a remote virtualisation solution for the VDI space. It concentrates on remoting 2D rendering commands. This project is developed independently of SPICE and is not intended to replace it. Remoting 3D rendering using the techniques spice uses is not considered practical by the author, also the spice architecture relies on rendering capabilities in the server side that mean the same 3D gpu would be required on client and host side in order to guarantee the same results. This project is starting from a simpler place in order to build up knowledge of how 3D virtualisation can be done.

