# 3. Multicore Merlin

{pause}

By now, we've explained two things:

- OCaml multicore
- Merlin [🧙‍♀️]{step focus-at-unpause #wizard} {pause unfocus-at-unpause}
    - friendly wizard: everybody _loves_ Merlin
    - old wizard: 10+ years **legacy** code base with highly **sequential** logic and lots of global **mutable state**

{pause}

It sounded like a horrible idea to use the new multicore paradigm on Merlin. {pause}

So, {pause} we did it anyways! :) {#anyways}

{.block title="The gist of the work" pause up-at-unpause=anyways class="blurred"}
> - The type-checking logic is run on a separate domain from the computations.
> - Effect handlers allow to have an easy-to-handle control flow
> - Lock spells are used to manage shared state
> - We used a tool called TSan to dynamically detect data races

{.block title="Main performance achievements" class="blurred"}
> - Queries are now cancellable
> - Computations can be started on top of partial typing results
> - The new model opens the door to more performance improvements


<style>
    .blurred {
      filter: blur(4px); /* Adjust the value for more or less blur */
      pointer-events: none; /* Optional: prevents interaction */
      user-select: none;    /* Optional: prevents text selection */
    }
</style>

{pause}

**Spoiler**: It has worked surprisingly well!

{pause}

