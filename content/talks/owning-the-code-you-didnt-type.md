+++
title = "Owning the Code You Didn't Type"
date = 2026-10-08
slides = "owning-the-code"
thumbnail = "/presentations/owning-the-code/img/cordas.jpg"
description = "Practical recipes to stay in control of code that an assistant writes faster than you can read it."
+++

{{< slides owning-the-code >}}

For most of our careers, the scarce thing was producing code. That world is ending. An assistant now produces competent code faster than any of us can read it, and the bottleneck has moved from writing to understanding.

Nothing moved on the responsibility side, though. We are still accountable for every line we merge, no matter who or what typed it. Staying in the loop, knowing the system, owning the design, that is the job description now.

This talk is not a manifesto, it is a set of recipes. The practices I use daily to stay in control of code that arrives faster than I could write it:

- **Made for humans** - Correct is not the bar, understandable is. Design and readability are acceptance criteria, and I send back what does not meet them.
- **Files and comments** - Sessions produce files and in-code comments instead of long chat threads. Easy to navigate, easy to annotate for the assistant.
- **Walk-throughs** - The assistant guides me through a change step by step, in reading order, instead of leaving me alone with a raw diff.
- **Phased delivery** - Large tasks are split into small phases with a review gate after each one. No big-bang diffs.
- **Engineering depth** - Know your stuff. The deeper you understand your system, the harder it is to be fooled by a confident, plausible answer.

Together these form a flow that keeps me in control and grows my knowledge instead of eroding it. You will leave with techniques you can apply the next day, whatever assistant you use.

Presented at Devoxx Belgium 2026.
