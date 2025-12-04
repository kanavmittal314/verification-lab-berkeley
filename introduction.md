---
title: Introduction (Partners A + B)
layout: page
nav_order: 2
---

# Introduction to Assertion-Based Verification

The standard approach to verification is to write assertions on the signals being driven by the module of interest (in this case, the outgoing signals of the FIFO: `Ready -> Module A (Source)`, `Valid + Data -> Module B (Sink)`). The behavior of these signals with respect to design expectations lies under the jurisdiction of the FIFO itself.

Conversely, from the FIFO's perspective, it will need to make assumptions about its incoming signals, in particular that they are also adhering to the same handshake-based, ready-valid interface protocol.

## Writing assertions
Assertions are written in SystemVerilog. We encourage you to look over [this guide to writing SVA assertions](https://www.systemverilog.io/verification/sva-basics/) and refer back to it when you are writing assertions.

---

Now, you and your partner will split up. Choose one of you to be Partner A and the other to be Partner B.

Partner A will write assertions for the Moore FSM, and Partner B will write assertions for the Mealy FSM.

[Go to Moore FSM →]({{ site.baseurl }}/moore)
[Go to Mealy FSM →]({{ site.baseurl }}/mealy)
