---
title: "The Ultimate Guide to JTAG"
date: "2020-8-9"
image: assets/images/jtag.png
author: name
layout: post
tags: [ guide, JTAG ]
categories: [ guides ]
---

If you are interested in the hacking industry, chances are that you have come across JTAG.

Chances are you have used it in the past to reflash some piece of hardware.

But how exactly does JTAG work?

## Hardware Debugging for Reverse Engineers

We are going to take a look at JTAG from a reverse-engineering point of view.

JTAG is a hardware interface that was developed with the intent to assist developers and testers with lower-level debugging.

JTAG was developed with the original intent for testing integrated circuits and sampling IO pins on a target which is being tested.

This kind of debugging interface allows any engineer to test connections on PCBs without needing to probe the physical pin.

JTAG utilizes two registers.

<![if !supportLists]>· <![endif]>The first one is the instruction register.

<![if !supportLists]>· <![endif]>The second one is the data register.

To take advantage of these registers, the proper states in the state machine must be entered using certain interface signals.  
  
These are:

<![if !supportLists]>· <![endif]>TMS – the pin used to navigate and control the JTAG state machine.

<![if !supportLists]>· <![endif]>TDI – the input pin which is used to write data to the target.

<![if !supportLists]>· <![endif]>TDO – the output pin which is used to read data back out from the target.

<![if !supportLists]>· <![endif]>TCK – which is used to determine when the data is sampled for all of the inputs and all of the outputs.

<![if !supportLists]>· <![endif]>TRST- a pin which can be used to reset the state machine to the starting state, although this one is fully optional.

The state machine can be navigated using the TMS and TCK lines, specifically, when the data is written to or read by TDI or TDO.

TMS is sampled on TCK, which means that the TMS line must be asserted before TCK can be toggled to navigate through the state machine.

The Data is then finally shifted into the instruction register known as IR or data register known as DR, which is dependent on the state of the JTAG state machine.

Once an operation is successfully completed, the resulting data can be shifted out of DR by entering the “Shift-DR” state.

When all of this takes place, all manufacturers can implement whichever features they want to over JTAG.

The JTAG standard can treat IR and DR as shift registers and as such allow multiple targets to be daisy-chained.

Simply put, JTAG can define a state machine that is navigated through at least 4 signals, and with it, the end-users can write and read from two shift registers known as IR and DR.

## The Registers

Now we will go back to the two registers which JTAG utilizes, the instruction register and the data register.

When it comes to the instruction register, it is used to determine what function the JTAG controller is about to carry out as a memory write or memory read.

When it comes to the data register, it is used as an additional input to the instruction register, which allows the user to provide an address to read from or write to.

Here are the steps that need to be taken in order to successfully write a register:

<![if !supportLists]>· <![endif]>Enter the test logic reset state or LTR – done by asserting the TMS line and cycling CLK a total of 5 times.

<![if !supportLists]>· <![endif]>Enter Select IR State.

<![if !supportLists]>· <![endif]>Enter Capture IR State.

<![if !supportLists]>· <![endif]>Enter Shift IR, where the data can be loaded into the IR from TDI.

<![if !supportLists]>· <![endif]>Enter Exit IR State.

<![if !supportLists]>· <![endif]>Enter Update IR State – the stage which latches the value into IR.

After the following steps, the operation will be performed and the result would be loaded onto the data register to be shifted out.

Keep in mind that many instructions require a data register to be filled out before operating properly.

Once the data register is written and updated, the operation can be performed and the result can be shifted out of the data register as a whole.

There are also certain registers which do not require the DR to be loaded.

When it comes to the JTAG standard, it defines the following instruction registers.

BYPASS – an instruction that connects TDI and TDO, and when in the Shift DR State, data can be transferred from TDI to TDO with a delay of one TCK cycle, and 0 is loaded into the data register during the Capture DR state.

This is used to determine how many devices are in a scan chain together.

INCODE – an instruction that when loaded, the Device Code ID Register is selected as the serial path between TDI and TDO, and in the Capture-DR state, the 32-bit Device ID code is loaded into this shift section.

In the Shift-DR state, however, this data is shifted out.

## Reverse Engineering with JTAG

The JTAG signal lines can often be found grouped together, and you are bound to see one of these headers.

When you want to reverse engineer something similar, you need to start with what is known.

Many manufacturers implement IDCODE and BYPASS, so we can take advantage of these two instructions.

If you manage to identify a potential JTAG header or pinout, you can use the behavior of the two registers to determine the pinout.

IDCODE as a register is loaded as the default IR, and as such we can test an assumed pinout by following these steps:

<![if !supportLists]>· <![endif]>Assigning roles to potential output pins such as TMS, TCK and so on.

<![if !supportLists]>· <![endif]>Entering the Test Logic Reset State.

<![if !supportLists]>· <![endif]>Entering the Select DR Scan, Capture DR and Shift DR.

<![if !supportLists]>· <![endif]>Click 32 values on TDI and monitor TDO for a valid IDCODE value.

<![if !supportLists]>· <![endif]>Checking the IDCODE value that was shifted out to determined if it looks valid.

<![if !supportLists]>· <![endif]>If it ends up being valid, the attempt is successful, if not, reassign pints and repeat.

You can also take advantage of the IDCODE register, which is often loaded into the IR by default.

Due to this, you can utilize the fact that both the IR and DR behave as shift registers.

Assuming the common register length is 32 bits, you can attempt to brute force the pinout by following these steps:

<![if !supportLists]>· <![endif]>Assigning roles to potential output pins such as TMS, TCK and so on.

<![if !supportLists]>· <![endif]>Using the assumed values and entering the Test Logic Reset state.

<![if !supportLists]>· <![endif]>Entering the Shift IR State.

<![if !supportLists]>· <![endif]>Shift in a unique 32-bit value on TDI.

<![if !supportLists]>· <![endif]>Continue to shift 1’s on TDI while monitoring for a unique pattern on TDO.

<![if !supportLists]>· <![endif]>If the pattern is discovered, the attempt is successful, if not, choose new assignments for the pins and repeat the process.

Once the pinout of the target is determined, the next step is to determine the length of the IR / DR.

This can be done by starting with IR, entering the Shift IR state and flood the chain with 1’s on TDI.

You can do this by using a large number such as 1024 or 4096 and then clock in a 0.

Once this has been done, you can continue to clock in 1’s on TDI, while counting the number of clock cycles that it takes before a 0 appears on TDO.

This will indicate the length of the IR, and once you have that, you can enter the Shift DR state and repeat the process until you figure out the state of the DR.


## References 

- xjtag(https://www.xjtag.com/about-jtag/jtag-a-technical-overview/){:target="_blank"}
- hackaday(https://hackaday.com/2020/04/08/a-hackers-guide-to-jtag/){:target="_blank"}