---
title: Introduction (Partners A + B)
layout: page
nav_order: 2
---

# Introduction to Assertion-Based Verification

The standard approach to verification is to write assertions on the signals being driven by the module of interest (in this case, the outgoing signals of the FIFO: `Ready -> Module A (Source)`, `Valid + Data -> Module B (Sink)`). The behavior of these signals with respect to design expectations lies under the jurisdiction of the FIFO itself.

Conversely, from the FIFO's perspective, it will need to make assumptions about its incoming signals, in particular that they are also adhering to the same handshake-based, ready-valid interface protocol.

## Writing assertions
Assertions are written in SystemVerilog. We encourage you to look over [the EECS151 FA25 guest lecture from Apple on SystemVerilog assertions (SVA)](https://inst.eecs.berkeley.edu/~eecs151/fa25/static/lectures/lec18.pdf) and [this guide to writing SVA](https://www.systemverilog.io/verification/sva-basics/) and refer back to it when you are writing assertions.

## Running assertions
The way in which we run SystemVerilog Assertions on the design is by placing them in the SystemVerilog file for the FSM design itself, writing a testbench file that specifies the clock and is capable of feeding test stimulus to the design, and finally running the testbench file against the design file to simulate the design running under a predefined clock and check whether the SVA written pass on the design. For this lab, you will add your SVA to a SystemVerilog file containing the FSM design in [https://www.edaplayground.com/](EDA Playground).

Before continuing the lab, you will need to make an account on EDA Playground. Register with your berkeley.edu email (do not log in with Google) to gain access to commercial simulators. You will need to go to your inbox to verify your email. 

Then, paste the following SystemVerilog code in `testbench.sv`.

```
// Test module with assertions
module tb_fifo_fsm;
    logic clk, rst;
    logic write, read;
    logic valid, ready;
    logic [7:0] data;

    fifo_fsm dut (
        .clk(clk),
        .rst(rst),
        .write(write),
        .read(read),
        .valid(valid),
        .ready(ready),
        .data(data)
    );

    // Clock generation
    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    // Test stimulus
    initial begin
        // Reset
        rst = 1;
        write = 0;
        read = 0;
        repeat (2) @(posedge clk);
        rst = 0;

        // Test sequence: write to partial, attempt write when full, read
        repeat (1) @(posedge clk);
        write = 1;
        repeat (2) @(posedge clk);
        write = 0;
        repeat (1) @(posedge clk);
        read = 1;
        repeat (2) @(posedge clk);
        read = 0;
        repeat (2) @(posedge clk);

        $finish;
    end
   
endmodule
```

On the left sidebar, make sure the following settings are chosen:

- Languages & Libraries
    - Testbench + Design: SystemVerilog/Verilog
    - UVM/OVM: None
    - Other Libraries: None
    - Enable TL-Verilog: Not checked
    - Enable Easier UVM: Not checked
    - Enable VUnit: Not checked
- Tools & Simulators
    - Select Synopsys VCS 2023.03
    - Open EPWave after run: Not checked
    - Show output file after run: Not checked
    - Download files after run: Not checked

---

Now, you and your partner will split up. Choose one of you to be Partner A and the other to be Partner B.

Partner A will write assertions for the Moore FSM, and Partner B will write assertions for the Mealy FSM.

[Partner A: Go to Moore FSM →]({{ site.baseurl }}/moore)

[Partner B: Go to Mealy FSM →]({{ site.baseurl }}/mealy)
