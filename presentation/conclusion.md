
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

{style="display: flex; position:relative"}
> > ![](images/camel_skatting.gif){width=180px}
>
> > ![](images/camel_humping.gif){width=180px}
>
> > ![](images/camel_balling.gif){width=180px}
>
> > ![](images/camel_yoyoing.gif){width=180px}
>
> > ![](images/camel_super.gif){width=180px}
>
> > ![](images/camel_walking.gif){width=180px}
>
> > ![](images/camel_rolling.gif){width=180px}