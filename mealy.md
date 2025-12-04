title: Mealy FSM (Partner B)
layout: page
nav_order: 3
---

## Mealy FSM State Transition Diagram

![Mealy FSM]({{ site.baseurl }}/mealy-fsm.png)

## Mealy FSM Encoded State Transition Table


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

## Instructions

Given a Verilog implementation of the Mealy FIFO FSM, write a comprehensive set of assertions that verify the state transitions, output, and interface protocol as outlined in the pre-lab document.

<!-- Add Mealy-specific assertion examples here if available -->
