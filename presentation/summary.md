{pause up #summary}
## Summary

{pause}

{carousel change-page='~n:"all"'}
----
![Merlin's story](images/im3.png){width=1200px}

---
![Merlin's story](images/im3-name.png){width=1200px}

---
![Merlin's story](images/im4.png){width=1200px}
----


{pause up #cancel}
## 🪄 Some parallelism

Between the computation of the pipeline and the query analysis.

{pause}
## ✨ A cancellation mechanism 

> Ability to cancel the current query if a new one comes up.
> 


{#partial pause}
## ⚡️ Early type return

<!-- {reveal="cancel_text"} -->

{style="display: flex; gap: 5rem; position:relative"}
> {split}
> > 
> > {.svg-container-small include src=images/pipeline.svg} 
>
> {split}
> > {.block pause}
> > **Idea**: if you need the type of a top-level item line 10, Merlin does not need to type what comes after.
> >
> > {pause}
> >
> > Work in  most of the time! 
> >
> > Except (e.g. value restriction)
> >
> > {pause}
> > {carousel change-page='~n:"all"'}
> > ----
> > 
> > ---
> > 
> > >```ocaml
> > > let a = ref [] 
> > >
> > >
> > >
> > > 
> > > (* end of buffer *)
> > >```
> > 
> > ---
> > 
> > >```ocaml
> > > let a = ref [] 
> > > (* '_weak1 list ref *)
> > >
> > >
> > > 
> > > (* end of buffer *)
> > >```
> > 
> > ---
> > 
> > >```ocaml
> > > let a = ref [] 
> > > 
> > > 
> > >  a := [ 1 ] 
> > > (* let () = a := [ 1 ] *)
> > > (* end of buffer *)
> > > ```
> > 
> > ---
> > 
> > >```ocaml
> > > let l = ref [] 
> > > (* int list ref *)
> > > 
> > >  a := [ 1 ]
> > >
> > > (* end of buffer *)
> > > ```
> > 
> > ----


{pause up-at-unpause=cancel}


<style>
.svg-container-small svg {
  width: 100%;
  height: auto;
}
</style>