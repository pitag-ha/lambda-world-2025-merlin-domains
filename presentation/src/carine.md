{include src=summary.md}

{unfocus pause up #ocaml5}
## Brewing New Magic Tricks with OCaml 5

<!-- {pause style="text-align:center" up-at-unpause=ocaml5} -->
<style>
.svg-container-carine svg {
  width: 55%;
  height: auto;
}
</style>

<style>
.svg-container-3 svg {
  width: 180%;
  height: auto;
}
</style>

<style>
.svg-container-cfg svg {
  width: 60%;
  height: auto;
}
</style>

{style="display: flex; gap: 1rem; position:relative"}
> {slip}
> > # 🌱 Shared Memory Parallelism
> >
> > {pause}
> > {unreveal=domain-example}
> >
> > {include src="cancellation_extra.md"}
> >
> > {.block title="Domains" pause}
> > ---
> >
> > A domain in OCaml is a **parallel execution unit** that has its own minor heap, and execution stack.
> > Domains allow OCaml programs to run **code in parallel on multiple CPU** cores without a global runtime lock.
> >
> > {pause}
> >
> > **Rule of thumb:** Spawn the domains at the start of the world and keep them waiting until they are needed.
> >
> > ---
> >
> > {reveal="domain-example"}
> >
> > {style="display: flex; gap: 1rem; position:relative"}
> > > {slip}
> > > >
> > > > {carousel change-page='~n:"all"' }
> > > > ----
> > > >
> > > > ---
> > > >
> > > > # Control Flow Graph
> > > > {style="display: flex; gap: 1rem; position:relative"}
> > > > > > {.svg-container-cfg include src=merlin_cfd_with_typer.svg}
> > > > >
> > > > > > 
> > > > > > {.svg-container-3 include src=images/detail_graph_to_temporal_small.svg}  
> > > > 
> > > > ---
> > > > # Sequence Diagram
> > > > {.svg-container-carine pause include src=images/cancellation2.svg style="text-align:center"} 
> > > > {unreveal="step2-1 step3-1 step4-1"}
> > > >
> > > > {reveal="step2-1"}
> > > >
> > > > {reveal="step3-1"}
> > > >
> > > > {reveal="step4-1"}
> > > > 
> > > > ----
> > >
> > > <!-- {slip}
> > > > {pause}
> > > > {.svg-container-carine include src=images/cancellation.svg}  
> > > > {unreveal="step2-2 step3-2 step4-2 step5-2 step6-2"}
> > > >
> > > > {reveal="step2-2"}
> > > >
> > > > {reveal="step3-2"}
> > > >
> > > > {reveal="step4-2"}
> > > >
> > > > {reveal="step5-2"}
> > > >
> > > > {reveal="step6-2"}-->
> > > >
> > > > 
> > >
> > ---
>
>
> {#part2 slip enter}
> > # 🍄 Effect Handlers
> >
> > {pause}
> >
> > {.block title="Effects and effect handlers" color="blue" #eff}
> > ---
> >
> > An **effect** is an operation in a program that can **suspend the linear flow of execution** and delegate control to an external handler to decide how to proceed.
> > 
> > An **effect handler** captures and defines the behavior of effects when they are performed. It has access to the continuation (the rest of the computation).
> >
> > ---
> >
> > {pause}
> >
> > {carousel #my-carousel}
> > ----
> >
> > {include src=effect_example.md}
> >
> > ---
> >
> > {pause up-at-unpause=my-carousel}
> > {.svg-container-carine include src=images/partial_typing.svg style="text-align:center"} 
> > {unreveal="step2-3 step3-3 step4-3 step4a-3 step4b-3 step5-3 step6-3"}
> > 
> > {change-page=my-carousel}
> >
> > {reveal="step2-3"}
> >
> > {focus="focus-rect"}
> >
> > {reveal="step3-3"}
> >
> > {reveal="step4-3"}
> >
> > {reveal="step4a-3"}
> > 
> > {reveal="step4b-3"}
> > 
> > {unfocus}
> >
> > {reveal="step5-3"}
> >
> > {pause reveal="step6-3"}
> >
> > {change-page=my-carousel}
> >
> > ---
> >
> > {include src=partial_typing.md}
> >
> > ----
> > 
>
> 
> {up-at-unpause=ocaml5}

{pause up}
## Everything together

{pause }
{.svg-container-carine include src=images/complete_graph.svg} 
{unreveal="step2-4 step3-4 step4-4 step5-4"}

{reveal="step2-4"}

{reveal="step3-4"}

{reveal="step4-4"}

{reveal="step5-4"}


{pause up}
## 🧙‍♀️ Merlin +  🐫 OCaml 5 = ❤️?{#merlin-multicore}

{pause}
And they lived happily ever after. 
[**The End 👑**]{focus}

{unfocus}

{pause}
**Plot twist:**
- Merlin has a lot of mutable states 
  - 77 top-level definition of mutable references,
  - 4 hashtables defined at top-level.
- The internal typer comes from OCaml: 
  - we don't want to change
  - also highly mutable

{.block pause}
With parallelism, isn't this the recipe for a **disaster** (i.e. data races 💥) ?

{pause}
So why even bother ?

{pause}
- OCaml 5 memory model is great! {pause}
- Merlin is a non-critical system. {pause} 

{.block}
And also, it seemed very fun to try (and it was)!

{pause up}
{carousel change-page='~n:"all"' }
-----

----
## Sequence Diagram with Data Races
{.svg-container-carine include src=images/complete_graph.svg} 

----
## With mutex
{.svg-container-carine include src=images/complete_graph_with_mutex2.svg} 

----
## Another Bumps: Cancellation Mechanism
{.svg-container-carine include src=images/complete_graph_last.svg} 


-----



