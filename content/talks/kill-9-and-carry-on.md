+++
title = "Kill -9 and Carry On"
date = 2026-10-28
slides = "durable-execution"
thumbnail = "/presentations/durable-execution/img/thumbnail.jpg"
description = "How four JVM durable execution engines keep a workflow running after its process is killed."
+++

{{< slides durable-execution >}}

Kill a process in the middle of a function and the function carries on. Local variables stay intact, timers stay pending, and execution resumes on another node. This talk looks under the hood of four durable execution engines on the JVM: Temporal, Restate, Axoniq Workflows and Akka. It compares how each one handles clocks, randomness and side effects, deploys with workflows in flight, and why none of them gives exactly-once side effects. As a co-author of Akka's workflow component, I show the trade-offs from the inside, with real Java code and a process killed live on stage.

Presented at Axoniq Conference 2026.
