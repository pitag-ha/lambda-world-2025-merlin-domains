{include src=summary.md}

{unfocus pause up #ocaml5}
## Brewing New Magics with OCaml 5

<!-- 🫕 New Magical Components -->

<!-- ✨ 🪄 🧙‍♂️ 🧙‍♀️ 🧹 🧪 🦄

🌊 🔥 🌪️ 🌱 ⚡️ 🪨 ❄️ 💥 -->

<!-- {pause style="text-align:center" up-at-unpause=ocaml5} -->
<style>
.svg-container svg {
  width: 80%;
  height: auto;
}
</style>


{style="display: flex; gap: 1rem; position:relative"}
> {slip}
> > # 🌱 Shared Memory Parallelism
> >
> > {pause}
> > {include src="cancellation_extra.md"}
> >
> > {.block title="Domains" pause}
> > ---
> >
> > A domain in OCaml is a **parallel execution unit** that has its own minor heap, and execution stack.
> > Domains allow OCaml programs to run **code in parallel on multiple CPU** cores without a global runtime lock.
> >
> > ---
> >
> > {pause}
> > ### Cancellation mechanism
> >
> > {style="display: flex; gap: 1rem; position:relative"}
> > > {slip}
> > > >
> > > > {carousel change-page='~n:"all"' }
> > > > ----
> > > >
> > > > ---
> > > > {.svg-container include src=images/detail_graph_to_temporal_small.svg}  
> > > > 
> > > > ---
> > > > {.svg-container pause include src=images/cancellation2.svg} 
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
> > > {slip}
> > > > {pause}
> > > > {.svg-container include src=images/cancellation.svg} 
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
> > > > {reveal="step6-2"}
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
> > {pause up}
> >
> > {carousel #my-carousel}
> > ----
> >
> >
> > {pause}
> > {.svg-container include src=images/partial_typing.svg } 
> > {unreveal="step2-3 step3-3 step4-3 step4b-3 step5-3 step6-3"}
> > 
> > {reveal="step2-3"}
> >
> > {focus="focus-rect"}
> >
> > {reveal="step3-3"}
> >
> > {reveal="step4-3"}
> >
> > {reveal="step4b-3"}
> > 
> > {unfocus}
> >
> > {reveal="step5-3"}
> >
> > {reveal="step6-3"}
> >
> > {change-page=my-carousel}
> >
> > ---
> >
> > {include src=partial_typing.md}
> >
> > ----
> > 
> {pause up-at-unpause=ocaml5}

<!-- rect26279-7-2-7-1-0-6 -->
{pause up}
## Everything together

{pause }
{.svg-container include src=images/complete_graph.svg} 
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
{carousel change-page='~n:"1-2 -1 +2"' }
-----

----
## Previous Sequence Diagram
{.svg-container include src=images/complete_graph.svg} 

----
## With some multicore safety one
{.svg-container include src=images/complete_graph_with_mutex.svg} 

----
## Another issue
{.svg-container include src=images/complete_graph_last.svg} 


-----

{pause up}
## Some metrics 

{pause up}
## Conclusion

{pause .block}
Is it working ?

{pause} 
Yes!

{pause .block}
Do we still have data races ?

{pause}
Yes!

{pause .block}
Is it an issue ?

{Pause}
 Maybe. 

{#q3 pause up .block}
Could we avoid data races at all? 

Yes, but:
- would limit parallelism

OR

- would require changing the internal typer

We are also exploring using a static way to enforce data-race freedom with modes thanks to a branch of OCaml called OxCaml.

{pause up="q3" .block}
Would some design be better ?

{pause}
Most likely. We are currently exploring!

- (short term) single-core design
- (short term) guarantee data race freedom
- (long term) other way of sharing the work between multiple domains

{pause up .block}
What we've learned ?

- Merlin can be made parallel! 🥳 
- Making it more efficient, more parallel, will require way more refactoring.
- More insight on performance bottlenecks 

{pause .block}
What next ?

Keep improving and trying to understand what we currently have:
- better cancellation mechanism
- a single-core design to study the improvement brought by parallelism alone

Explore other designs:
- data-race free design with OXcaml
- other way of sharing the work between multiple domains


