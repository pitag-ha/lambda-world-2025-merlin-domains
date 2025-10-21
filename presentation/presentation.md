---
dimension: 16:9
---

<!-- slipshow serve -o presentation/presentation.html presentation/presentation.md -->

{#beginning}

<h1 style="text-align: center;">✨When magic meets multicore</h1>
<h3 style="margin-top: -15px; text-align: center">🐪 OCaml and its elegant era of parallelism</h3>

{pause}

<br>

#### Content

blabla

{pause up-at-unpause=questions}

#### A few questions {#questions}

{pause}

{pause}

- Who of you has used OCaml? 🐪
  {pause}
- Who of you knows what LSP (langauge server protocol) is? 💬🖥️📋
  {pause}
- Who of you knows what a language server is? 💬🖥️

{pause up-at-unpause=ocaml}

#### OCaml 🐪 {#ocaml}

**Language**

- Functional-first but multi-paradigm (supports imperative and object-oriented styles)
- Static type system with Hindley–Milner type inference
- Advanced features — powerful module system, GADTs, polymorphic variants
- Multicore support and effect handlers

**Platform and Ecosystem**

- Fast, native code generation — targets x86, ARM, RISC-V, etc.
- JavaScript and WebAssembly (via WasmGC) compilation
- Strong tooling ecosystem — editor integration (LSP), build system (dune), package manager (opam), documentation generator (odoc), etc.
- Opam repository — small but mature package ecosystem
- Notable industrial users — Jane Street, Meta, Microsoft, Ahrefs, Citrix, Tezos, Bloomberg, Docker
- MirageOS — library operating system for building secure, minimal unikernels (cloud and IoT deployments)

**Applications and Strengths**

- High dynamic range — OCaml scales from quick scripts and research prototypes to large production systems.
- Compilers & languages — early versions of the Rust compiler, the WebAssembly reference interpreter, and Meta’s Hack language were written in OCaml.
- Frontend development — Ahrefs’ entire frontend is written in OCaml and compiled to JavaScript.
- Systems programming — used in Docker for Mac/Windows for container virtualization; Parsimoni (a Tarides spinoff) launched OCaml-based software into space.
- Hardware design — HardCaml enables FPGA programming in OCaml; it has powered award-winning entries in the ZPrize competition for zero-knowledge cryptography.

{pause up-at-unpause=merlin}

#### OCaml's language server Merlin 🧙‍♀️ {#merlin}

Live demo!

{pause}

You've just seen OCamlLSP live. OCamlLSP is one of the two frontends of OCaml's language server backend Merlin ✨✨ . Let's talk about Merlin:

{pause unreveal=AST}

![](arbol_magico_cadiz.png){ style="width:400px; vertical-align:middle; margin-right:2em;" }
<span id="AST" style="vertical-align:middle;"> ----> Let's talk about ASTs. </span>

{reveal=AST}

{pause}

{#question_frontend}
**Question**: Who here remembers, e.g. from uni, roughly what an AST is and what the compiler frontend does? (lexing, parsing, typing) 🌳

{pause up-at-unpause=question_frontend}

An AST is a representation of the program in the form of a tree.

In OCaml, a statically typed language, there are two ASTs:

- **Parsetree**: the raw syntax tree from parsing source code.
- **Typedtree**: a version of the syntax tree where the compiler has annotated every expression with its inferred type.

{pause}

The compiler frontend builds up these different representations of your program step by step. Merlin does the same.

{pause}

![](pipeline_with_typer.svg)

{pause up}
{#cfd}
{.svg-container include src=merlin_cfd_with_typer.svg #cfd}

<style>
.svg-container svg {
  width: 45%;
  height: auto;
}
</style>

{focus="rect26279-7-2"}

{unfocus}

{pause up}

#### Performance data (in milliseconds)

![](perf_lsp_types_2.png){ style="height:8em;" }

&nbsp; <!-- small spacer -->

![](perf_lsp_2.png){ style="height:8em;" }

&nbsp; <!-- small spacer -->

![](perf_js_2.png){ style="height:8em;" }

{pause up-at-unpause=cfd}

{pause up}

#### Cache mechanisms in Merlin

There are two cache mechanisms:

1. File caches

   Build artifacts are stored in memory once read.

{pause up-at-unpause=typer_cache}

{#typer_cache} 2. Typer cache

{pause}

TODO: Make this nicer!!

![](typer.svg)

{pause}

{#simplification}
That was overly simplified.

Actually, the next item only gets typed if it hasn't changed since the last time Merlin ran. If not, it gets drawn from cache

{pause}

So: When you modify code near the top of a file, Merlin needs to retype most of the file, so queries are slower.
Changes near the end have little impact as almost all previous typing results can be reused.

{pause}

{#take-away}
**Take-away from the typer cache** 🍕: When you modify a long file at the beginning of the file, Merlin can be very slow. If Merlin could speed up queries towards the beginning of a file, that'd be magic!✨

{pause up-at-unpause=take-away}

**Take-away from performance analysis** 🍣: The typer is the main performance bottlenecks. The query analysis can also be quite slow. Partly parallelising the two things would help.

{pause}

**Also** ✨➕✨: Currently, Merlin finishes the whole process for one query before starting the next. If there were a way to cancel in-progress work when new queries arrive, queries could respond even faster. LSP does skip queued queries. If Merlin could also cancel ongoing query processing, that’d be magic!

{pause up}

#### Carine's sections

{pause up}

#### Metrics
