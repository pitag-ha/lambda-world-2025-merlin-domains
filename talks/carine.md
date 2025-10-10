{pause up #perf}
### 🐉 A Beast to Slay: Large Buffers with Cold Caches

{pause}
###  🪄 Some New Magic 

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
> > {.block}
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
### OCaml 5: 🫕 New Magical Components

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
> > - *another one for cancellation mechanism (IMAGE)*
> > 
> > 
> > 
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


<!-- {pause exec}
```slip-script
  let overlay = document.getElementById("emoticon-overlay");

  if (!overlay) {
    overlay = document.createElement("div");
    overlay.id = "emoticon-overlay";
    overlay.textContent = "😎"; // <-- you can change the emoticon here
    document.body.appendChild(overlay);
  }

  let style =
  "position: fixed;\
  top: 0;\
  left: 0;\
  width: 500%;\
  height: 500%;\
  background: rgba(0, 0, 0, 0.4); /* semi-transparent backdrop */\
  display: flex;\
  justify-content: center;\
  align-items: center;\
  font-size: 10rem;\
  color: white;\
  z-index: 9999;\
  visibility: hidden; /* start hidden */ ";

  overlay.setAttribute("style", style);

  overlay.style.visibility = "visible";

  return {undo : () => { overlay.style.visibility = "hidden"; }}
```

{pause exec}
```slip-script
  let overlay = document.getElementById("emoticon-overlay");
  overlay.style.visibility = "hidden";
    return {undo : () => { overlay.style.visibility = "visible"; }}
``` -->

{pause up=merlin-multicore}
## 🧙‍♀️ Merlin +  🐫 OCaml 5 = ❤️?{#merlin-multicore}



<!-- 🐉 ➕ ❄️ (cold cache) ➡️ 😱 -->
```
🧙‍♀️✨ Merlin ➕ 🌱 Parallelism ➕ 🍄 Effect Handlers

  🟰 ✨ Cancellation ➕ ⚡️ Partial Typing
    
```
{pause}

```

✨ ➕ ⚡️ 🟰 🐉❌  (Beast slain!)
```

Seems like a great plan, right ?



But ... {pause} 
- Merlin a lot of mutable states
- We can't change it too much (at least at start)

{.block}
With parallelism, isn't it the recipe for a **disaster** (i.e. data races) ?

So why even bother ?

{pause}
- OCaml 5 memory model is great! {pause}
- Merlin is a non-critical system. {pause}

{.block}
And also, it seemed very fun to try (and it was)!

{pause up}
## Let see the magic ✨

Include the graph of the flow of the code ()
