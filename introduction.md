---
title: Pre-Lab + Introduction (Partners A + B)
layout: page
---



## Pre-lab

Prior to coming into your assigned lab section, you must read through and understand this [pre-lab document](https://inst.eecs.berkeley.edu/~eecs151/fa23/static/resources/ready_valid_interface.pdf), which details a handshake-based, ready-valid interface protocol for transmitting data from one component of a design (source) to another (sink).

## Concept Check

Concept check question goes here 

## Background

The standard approach to verification is to write assertions on the signals being driven by the module of interest (in this case, the outgoing signals of the FIFO: `Ready -> Module A (Source)`, `Valid + Data -> Module B (Sink)`). The behavior of these signals with respect to design expectations lies under the jurisdiction of the FIFO itself.

Conversely, from the FIFO's perspective, it will need to make assumptions about its incoming signals, in particular that they are also adhering to the same handshake-based, ready-valid interface protocol.

---

Now, you and your partner will split up. Choose one of you to be Partner A and the other to be Partner B.

Partner A will write assertions for the Moore FSM, and Partner B will write assertions for the Mealy FSM.

[Go to Moore FSM →]({{ site.baseurl }}/moore)
[Go to Mealy FSM →]({{ site.baseurl }}/mealy)
