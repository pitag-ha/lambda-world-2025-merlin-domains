---
dimension: 16:9
---

<!-- slipshow serve -o presentation/presentation.html presentation/presentation.md -->

{#beginning}

<h1 style="text-align: center;">When magic meets multicore</h1>
<h3 style="margin-top: -15px; text-align: center">OCaml and its elegant era of parallelism</h3>

{pause}

<br>

#### Content

blabla

{pause up-at-unpause=questions}

#### A few questions {#questions}

blabla

{pause up-at-unpause=ocaml}

#### OCaml 🐪 {#ocaml}

blabla

{pause up-at-unpause=merlin}

#### OCaml's language server Merlin 🧙‍♀️ {#merlin}

Live demo!

{pause}

You've just seen OCamlLSP live. OCamlLSP is one of the two frontends of OCaml's language server backend Merlin 💫💫 . Let's talk about Merlin:

{pause unreveal=AST}

![](arbol_magico_cadiz.png){ style="width:400px; vertical-align:middle; margin-right:2em;" }
<span id="AST" style="vertical-align:middle;"> ----> Let's talk about ASTs. </span>

{reveal=AST}

{pause}

{#question_frontend}
**Question**: Who here remembers, e.g. from uni, roughly what an AST is and what the compiler frontend does? (lexing, parsing, typing)

{pause up-at-unpause=question_frontend}

An AST is a representation of the program in the form of a tree.

In OCaml, a statically typed language, there are two ASTs:

- **Parsetree**: the raw syntax tree from parsing source code.
- **Typedtree**: a version of the syntax tree where the compiler has annotated every expression with its inferred type.

{pause}

The compiler frontend builds up these different representations of your program step by step. Merlin does the same.

{pause}

![](pipeline_with_typer.svg)

{pause up-at-unpause=cfd}

{#cfd}
{.svg-container include src=merlin_cfd_with_typer.svg}

<style>
.svg-container {
  height: 55vh; /* 80% of viewport height */
  padding-bottom: 0.5em; /* adds visual space inside the container */
  box-sizing: border-box; /* include padding in container height */
}

.svg-container svg {
  width: 100%;
  height: 100%;
  display: block;     /* remove extra whitespace below SVG */
}
</style>

{pause up-at-unpause=perf_table}

{#perf_table}
TODO: Add perf table

{pause}

#### Cache mechanisms in Merlin

There are two cache mechanisms:

1. File caches

   - `cmi` cache
     - .cmi files store the compiled interface of an OCaml module (remember the demo). They let the typer see the types of values, functions, and modules defined elsewhere.
     - Merlin keeps the contents of read .cmi files in memory.
     - Thanks to this cache, the 2nd, 3rd… query in a file is much faster than the first.
   - Other similar file caches

{pause up-at-unpause=typer_cache}

{#typer_cache} 2. Typer cache

{pause}

Remember:

![](typer.svg)

{pause}

{#simplification}
That was overly simplified.

Actually, there's a cache mechanism in between: The next item only gets typed if it hasn't changed since the last time Merlin ran. If not, it gets drawn from cache

{pause}

So: When you modify code near the top of a file, Merlin needs to retype most of the file, so queries are slower.
Changes near the end have little impact as almost all previous typing results can be reused.

{pause}

{#take-away}
**Take-away from the typer cache** 🍕: When you modify a long file at the beginning of the file, Merlin is slow. (If you remember the demo, you saw this in action!)

{pause up-at-unpause=take-away}

**Take-away from performance analysis** 🍣: The typer is the main performance bottlenecks. The query analysis can also be quite slow. Partly parallelising the two things would help.

{pause}

**Also** ✨➕✨: Currently, Merlin finishes the whole process for one query before starting the next. If there were a way to cancel in-progress work when new queries arrive, queries could respond even faster. LSP does skip queued queries. If Merlin could also cancel ongoing query processing, that’d be magic!
