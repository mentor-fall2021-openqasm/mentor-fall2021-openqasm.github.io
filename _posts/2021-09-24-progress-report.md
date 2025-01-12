---
title: "Progress as of September 24, 2021"
date: 2021-09-24 16:41:55 +0530
categories: [Progress, "September 24, 2021"]
tags: [progress,progress_report]     # TAG names should always be lowercase
---

Progress report and discussion summary for OpenQASM 3.0 Reference Implementaion #23 as discussed on September 24, 2021

# Plan as of 2021-09-24
* Continue to integrate AST work with code generation.
* Before 0ct 7 QAMP mentorship checkpoint:
  * Blog
  * Slides
* October 17 Vishal to present progress at IEEE Quantum Week 2021

# Progress so far
* Abeer's QOSF QuantumCircuit Generator: [https://github.com/mentor-fall2021-openqasm/QASM_to_QuantumCircuit_Gen](https://github.com/mentor-fall2021-openqasm/QASM_to_QuantumCircuit_Gen)
* Adrien's update build_ast.py to make life easier
* Website initial build

# Jack's Meeting Notes
* Classic feedback undoable with normal Qiskit access and also with Qiskit Runtime.
* Measurement needs special types that we need to subclass from Python types.
* Parsing is essentially complete, but Adrien will want to verify the AWS team’s implementation of recommended changes.
* In AST we don’t have an information on included files. Thus, error lines from includes don’t match.
* Adrien & Abeer are converging their work. Both are working on translator.
* Vishal working on blogging for Organization. Team will provide content when blog fully available.
* Vishal presenting IEEE Quantum Week. Slides for that may be used for Oct. 7 QAMP checkpoint.
* Any shortfalls in the reference AST from the AWS team should continue to be noted or PR’ed, whatever appropriate.
* Implementation of gate definitions with names.

# Notes from Conversation with Dr. Bello
We had a problem with implementing unfolding loops of the form:
```
OPENQASM 3;
include "stdgates.inc";

const n = 10;
qubit q;
angle[n] c = 0;

for i in [0: n - 1] { 
  phase(c) q[0];
  measure q -> c[i];
  c <<= 1;
}
```
Abeer Vaishnav met with Dr. Bello by WebEx. The summary:
* Qiskit does not support shift instructions. They are trivial to add, kind like an opaque inst. But those things that consume qiskit objects do not know about it.
* Getting a random QASM file and trying to express that in Qiskit is hard. Probably better to get an algorithm in Qiskit, write the QASM for it, and use that last QASM as the example.
* Unfolding loops is not always possible.
