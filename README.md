This repo holds the slipshow for a talk that @lyrm and I are going to give at Lambda World 2025. 

## Links to the talk

https://lambda.world/speakers/?speaker=Sonja%20Heinze  
https://lambda.world/speakers/?speaker=Carine%20Morel

## Abstract

> "Merlin" is certainly a magician -- but it's also the backend for OCaml's language server.
> It allows OCamlers to get superb editor support, such as seeing OCaml's type inference,
> navigating to a definition, constructing or destructing sum type values, and much more.
> In a different vein, OCaml multicore is certainly very interesting from a runtime design
> perspective -- but it also offers elegant ways to improve performance practically. It was
> introduced in 2022, bringing genuine parallelism to OCaml by extending the runtime with
> support for multiple domains (lightweight threads mapped to CPU cores). How do these
> two -Merlin and OCaml multicore- fit together? We've been working on improving the
> responsiveness of OCaml's editor support by offloading Merlin's type-checking logic to a
> background domain. In this talk, we'll give a small tour through that work. We'll start
> with a high-level overview of Merlin and of OCaml multicore concepts such as domains and
> effect handlers. Then, we'll explain how we used these concepts to improve Merlin's
> performance. You don't need any prior knowledge of OCaml to follow this talk. We hope
> to get you curious about OCaml and its ecosystem.
