---
title: Moore FSM (Partner A)
layout: page
nav_order: 2
---

# Moore FSM

## FIFO Design (Moore)

The FIFO buffer is modeled as a Moore Finite State Machine (FSM) with the following characteristics:

### Simplifying Assumptions

1. The depth of the FIFO is **2** (it can store at most 2 pieces of data at any point in time).
2. Data written on a given cycle **cannot** also be read on that same cycle.
3. Only **one** piece of data can be read from the FIFO on a given cycle.

### FSM Specification

* **States:**
    * `Empty = 2'b01`
    * `Partial = 2'b11`
    * `Full = 2'b10`

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

## Moore FSM State Transition Diagram

![Moore FSM]({{ site.baseurl }}/moore-fsm.png)

## Moore FSM Encoded State Transition Table

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

# Time to write assertions!

## Sample assertions

A couple of sample assertions are filled in below to get you started.

**FIFO State Transition Assertion (non-overlapping implication):**
```systemverilog
// Empty state transitions
assert property((@posedge clk) disable iff (rst) (state==2'b01 && write && !read)
  |=> (next_state==2'b11));
```

**Output Assertion (overlapping implication)**:
```systemverilog
// Empty state output
assert property((@posedge clk) disable iff (rst) (state==2'b01) |-> (!valid && ready));
```

## Check your understanding

What properties do the sample assertions check for?

## Instructions

Given a Verilog implementation of the above FIFO FSM, write a comprehensive set of assertions that verify the state transitions, output, and interface protocol as outlined in the pre-lab document. 


