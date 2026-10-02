+++
title = "Reification and Type-Safety in a CQRS World"
date = 2017-06-23
youtube = "qwYs0J7xp78"
duration = 2996
description = "Modeling a CQRS domain, its commands, and its events as one cohesive, well-typed set of algebraic data types."
+++

{{< youtube qwYs0J7xp78 >}}

In CQRS applications, commands and events are modeled as separate types with no direct link to the domain model. That is a challenge for fans of statically typed languages. This talk shows how to model a domain as an algebraic data type whose operations are commands and events. It compares three approaches: type parameters, type projections, and path-dependent types, with the pros and cons of each.

Recorded at Scala Days Copenhagen 2017.
