---
title: Assertion-Based Verification Lab Specification
layout: home
---

##  Overview

This lab will help you grow your assertion-based verification knowledge and develop skills like FSM comprehension and assertion writing. Assertion-based verification is an increasingly important step in hardware design, and industry is paying attention. We hope that this assignment will equip you with skills needed to pursue a successful career in hardware verification. In this lab, you will write SystemVerilog Assertions to functionally verify the FIFO buffer shown in Figure 8 of the pre-lab document (copied below for your convenience).

**placeholder**

##  Pre-lab

Prior to coming into your assigned lab section, you must read through and understand this [pre-lab document](https://inst.eecs.berkeley.edu/~eecs151/fa23/static/resources/ready_valid_interface.pdf), which details a handshake-based, ready-valid interface protocol for transmitting data from one component of a design (source) to another (sink).

## Background

The standard approach to verification is to write assertions on the signals being driven by the module of interest (in this case, the outgoing signals of the FIFO: `Ready -> Module A (Source)`, `Valid + Data -> Module B (Sink)`). The behavior of these signals with respect to design expectations lies under the jurisdiction of the FIFO itself.

Conversely, from the FIFO's perspective, it will need to make assumptions about its incoming signals, in particular that they are also adhering to the same handshake-based, ready-valid interface protocol.

## FIFO Design

We will model the FIFO buffer as a Finite State Machine (FSM), similar to what you have seen in previous lectures, discussions, and labs. This will help us write assertions. Below we provide the description of the FSM. 

### Simplifying Assumptions

The FSM implementation of the FIFO buffer is based on the following two simplifying assumptions:
1.  The depth of the FIFO is **2** (i.e., it can store at most 2 pieces of data at any point in time).
2.  Data written on a given cycle **cannot** also be read on that same cycle.
3.  Only **one** piece of data can be read from the FIFO on a given cycle.

### FSM Specification

* **States:**
    * `Empty = 2'b01`
    * `Partial = 2'b11`
    * `Full = 2'b10`

* **Inputs:** Take the form of `{Write, Read}`
    * `{0,0}`: `!write & !read`
    * `{0,1}`: `!write & read`
    * `{1,0}`: `write & !read`
    * `{1,1}`: `write & read`

* **Outputs:** Take the form of `{Valid, Ready}`
    * `{0,1}`: `!valid & ready`
    * `{1,1}`: `valid & ready`
    * `{1,0}`: `valid & !ready`

---

## FIFO FSM State Transition Diagram

*(This section is a placeholder for your FSM diagram image.)*

---

## FIFO FSM Encoded State Transition Table

### State Transitions

| Current State | Input `{Write, Read}` | Next State |
| :--- | :--- | :--- |
| **{0,1} (Empty)** | {0,0} (!write & !read) | {0,1} (Empty) |
| **{0,1} (Empty)** | {0,1} (!write & read) | |
| **{0,1} (Empty)** | {1,0} (write & !read) | |
| **{0,1} (Empty)** | {1,1} (write & read) | |
| **{1,1} (Partial)**| {0,0} (!write & !read) | {1,1} (Partial) |
| **{1,1} (Partial)**| {0,1} (!write & read) | |
| **{1,1} (Partial)**| {1,0} (write & !read) | |
| **{1,1} (Partial)**| {1,1} (write & read) | |
| **{1,0} (Full)** | {0,0} (!write & !read) | {1,0} (Full) |
| **{1,0} (Full)** | {0,1} (!write & read) | |
| **{1,0} (Full)** | {1,0} (write & !read) | |
| **{1,0} (Full)** | {1,1} (write & read) | |

### Outputs

| Current State | Output `{Valid, Ready}` |
| :--- | :--- |
| **{0,1} (Empty)** | {0,1} (!valid & ready) |
| **{1,1} (Partial)**| |
| **{1,0} (Full)** | |

> ## Note
> The current state of the design is itself the output, given this convenient 1:1 mapping of the bit-level representations of the current state and output.

---

## Instructions

Given a Verilog implementation of the above FIFO FSM, write a comprehensive set of assertions that verify the state transitions, output, and interface protocol as outlined in the pre-lab document. 

A couple of sample assertions are filled in below to get you started.

**FIFO State Transition Assertion (non-overlapping implication):**
```systemverilog
Empty state transitions
assert property((@posedge clk) disable iff (rst) (state==2'b01 && write && !read)
  |=> (next_state==2'b11));
```

**Output Assertion (overlapping implication)**:
```systemverilog
assert property((@posedge clk) disable iff (rst) (state==2'b01) |-> (!valid && ready));
```
