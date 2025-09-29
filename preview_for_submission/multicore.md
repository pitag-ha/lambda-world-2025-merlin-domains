# 2. Multicore OCaml

{pause}

We'll explain two concepts:

{pause}

{.block title="Domains"}
> A domain in OCaml is a **parallel execution unit** that has its own minor heap, and execution stack.
> Domains allow OCaml programs to run **code in parallel on multiple CPU** cores without a global runtime lock.
>
> (imagine a visualization)

{pause}

{.block title="Effects and effect handlers" color="blue"}
> An **effect** is an operation in a program that can **suspend the linear flow of execution** and delegate control
> to an external handler to decide how to proceed.
>
> An **effect handler** captures and defines the behavior of effects when they are performed. It has
> access to the continuation (the rest of the computation).
>
> (imagine code snippet building up)