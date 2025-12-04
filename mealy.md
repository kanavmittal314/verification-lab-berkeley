---
title: Mealy FSM (Partner B)
layout: page
nav_order: 3
---

# Mealy FSM

## FIFO Design (Mealy)

The FIFO buffer is modeled as a Mealy Finite State Machine (FSM) with the following characteristics:

### Simplifying Assumptions

1. The depth of the FIFO is **2** (it can store at most 2 pieces of data at any point in time).
2. Data written on a given cycle **cannot** also be read on that same cycle.
3. Only **one** piece of data can be read from the FIFO on a given cycle.

### FSM Specification

* **States:**
    * `S0 = 2'b01`
    * `S1 = 2'b11`
    * `S2 = 2'b10`

* **Inputs:** `{Write, Read}`
    * `{0,0}`: `!write & !read`
    * `{0,1}`: `!write & read`
    * `{1,0}`: `write & !read`
    * `{1,1}`: `write & read`

* **Outputs:** `{Valid, Ready}`
    * `{0,1}`: `!valid & ready`
    * `{1,1}`: `valid & ready`
    * `{1,0}`: `valid & !ready`

---

## State Transition Diagram

![Mealy FSM]({{ site.baseurl }}/mealy-fsm.png)

## Encoded State Transition Table


| Current State | Input | Next State | Output |
| :--- | :--- | :--- | :--- |
| {0,1} (S0) | {0,0} (!write & !read) | {0,1} (S0) | {0,1} (!valid & ready) |
| {0,1} (S0) | {0,1} (!write & read) |  |  |
| {0,1} (S0) | {1,0} (write & !read) |  |  |
| {0,1} (S0) | {1,1} (write & read) |  |  |
| {1,1} (S1) | {0,0} (!write & !read) | {1,1} (S1) | {1,1} (valid & ready) |
| {1,1} (S1) | {0,1} (!write & read) |  |  |
| {1,1} (S1) | {1,0} (write & !read) |  |  |
| {1,1} (S1) | {1,1} (write & read) |  |  |
| {1,0} (S2) | {0,0} (!write & !read) | {1,0} (S2) | {1,0} (valid & !ready) |
| {1,0} (S2) | {0,1} (!write & read) |  |  |
| {1,0} (S2) | {1,0} (write & !read) |  |  |
| {1,0} (S2) | {1,1} (write & read) |  |  |

---

# Time to write assertions!

## Sample assertions

A couple of sample assertions are filled in below to get you started.

TODO

## Check your understanding

What properties do the sample assertions check for?

## Instructions

Given a Verilog implementation of the Mealy FIFO FSM, write a comprehensive set of assertions that verify the state transitions, output, and interface protocol as outlined in the pre-lab document.

<!-- Add Mealy-specific assertion examples here if available -->
