{pause up #perf}
## 🐉 A Beast to Slay: Large Buffers with Cold Caches

{pause}
##  🪄 Some New Magic 

{style="display: flex; gap: 1em; position:relative"}
> {#part1.a slip}
> > # ✨ Cancellation Mechanism 
> >
> > {pause}
> >
> > Ability to cancel the current queries if a new one comes up.
> >
> > *(Add something like a picture ?)*
> {up=perf}
>
> {#part1.2 slip enter}
> > # ⚡️ Partial Typing 
> > {.block pause}
> > > **Idea**: if you need the type of a top-level item line 10, Merlin does not need to type what comes after
> > 
> > {pause}
> > True most of the time!
> > {pause}
> > ```ocaml
> >  let l = ref [] 
> >  (* '_weak1 list ref *)
> >  
> >  l := 1 :: !l
> >  (* int list ref *)
> > ```
> {pause up-at-unpause=perf}


<!-- > > {.unrevealed . .flex #cancellation_text}  -->
<!-- > > {.unrevealed #partial_text} -->
<!-- {pause reveal=cancellation_text}
{pause reveal=partial_text}
 -->

{pause #ocaml5}
## OCaml 5: 🫕 New Magical Components

<!-- ✨ 🪄 🧙‍♂️ 🧙‍♀️ 🧹 🧪 🦄

🌊 🔥 🌪️ 🌱 ⚡️ 🪨 ❄️ 💥 -->


{pause style="text-align:center" up-at-unpause=ocaml5}

{style="display: flex; gap: 1rem; position:relative"}
> {#part1 slip}
> > # 🌱 Shared Memory Parallelism
> >
> > Having multiple cores running in parallel (like `pthread`) {pause}
> >
> > *(Include a picture of several core running in //)*
> >
> > {.block title="Domains"}
> > A domain in OCaml is a **parallel execution unit** that has its own minor heap, and execution stack.
> > Domains allow OCaml programs to run **code in parallel on multiple CPU** cores without a global runtime lock.
> > 
> > *Possible images to include:*
> > - *one for pthreads = spawn in for loop (CODE or IM)*
> > - *one for domains = spawn should happen at the star of the world (CODE or IM)*
> >
> > ![Cancellation Mechanism](images/cancellation_mechanism2.jpg){width=300px focus} 
> >
>
> {up=ocaml5}
>
> {#part2 slip enter}
> > # 🍄 Effect Handlers
> >
> > {pause}
> >
> > {.block title="Effects and effect handlers" color="blue" #eff}
> > > An **effect** is an operation in a program that can **suspend the linear flow of execution** and delegate control
> > > to an external handler to decide how to proceed.
> > >
> > > An **effect handler** captures and defines the behavior of effects when they are performed. It has
> > > access to the continuation (the rest of the computation).
> >
> > {pause up=eff}
> > ```ocaml
> > type style = Emo | Text
> > type _ Effect.t += Love : style -> unit t | World : unit t
> > 
> > let foo () =
> >   Format.printf "I ";
> >   perform (Love Emo);
> >   Format.printf " Lambda World!@."
> > 
> > (* Prints "I ♥ Lambda World!"*)
> > let main () =
> >   match foo () with
> >   | () -> ()
> >   | effect World, k -> Format.printf "World"; continue k ()
> >   | effect Love style, k ->
> >     let str = match style with | Emo -> "♥" | Text -> "love"
> >     in
> >     Format.printf "%s" str;
> >     continue k ()
> > ```
> >
> {pause up-at-unpause=perf}


<!--
 {pause up=merlin-multicore}
## 🧙‍♀️ Merlin +  🐫 OCaml 5 = ❤️?{#merlin-multicore}

```
🌱 Parallelism ➕ 🍄 Effect Handlers 
  🟰 ✨ Cancellation ➕ ⚡️ Partial Typing
    
```
{pause }

```
🧙‍♀️✨ Merlin ➕ ✨ ➕ ⚡️ 🟰 🐉❌  (Beast slain!)
```

{pause}
Seems like a great plan, right ?


But ... {pause} 
- Merlin has a lot of mutable states
- We can't change it too much

{.block pause}
With parallelism, isn't it the recipe for a **disaster** (i.e. data races 💥) ?

{pause}
So why even bother ?

{pause}
- OCaml 5 memory model is great! {pause}
- Merlin is a non-critical system. {pause}

{.block}
And also, it seemed very fun to try (and it was)!
 -->

{pause up}
## Brewing new spells 

*Explain the new design with the diagram and some carousel*

{pause up}
## 🧙‍♀️ Merlin +  🐫 OCaml 5 = ❤️?{#merlin-multicore}

{pause}
And They lived happily ever after. 
[**The End 🎬**]{focus}

{unfocus}

{pause}
Except:
- Merlin has a lot of mutable states
- We can't change it too much

{.block pause}
With parallelism, isn't it the recipe for a **disaster** (i.e. data races 💥) ?



blabla..

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

{#q3 pause .block}
Could have we done thing differently ? 

{pause}
Yes, with ou without parallelism, there are many other ways to do it.

{pause up="q3" .block}
Would some designs be better ?

{pause}
Most likely. We are currently exploring!

- No-parallelism design
- guarantee data race free  

{pause .block}
What next ?


{pause up}
## What we've learned


