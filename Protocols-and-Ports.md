---
title: Protocols and Ports
layout: topic
categories: intro
---

## Protocols and Ports

There's this thing called the internet layer, which allows `hosts`, (all `servers` are considered to be hosts, but not the other way around) to communicate with each other using `ports`. In computer networking, a port is a communication endpoint. It is where data is sent and recieved in the form of `packets`.

With basic websites you'll be dealing with ports `80` and `443`. Port `80` serves packets over `http`. HTTP stands for
HyperText Transfer Protocol - the standard protocol for internet layer communication.

Port 443 serves `https`, HTTPS stands for HyperText Transfer Protocol Secure. It almost the same as `http` except that it uses Transport Layer Security (`TLS`), or its predecessor, Secure Sockets Layer (`SSL`) to encrypt packets.