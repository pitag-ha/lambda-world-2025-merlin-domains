{#beginning}
<h1 style="text-align: center;">When magic meets multicore</h1>
<h3 style="margin-top: -15px; text-align: center">OCaml and its elegant era of parallelism</h3>

<!-- # When magic meets multicore
# OCaml and its elegant era of parallelism -->

{pause}

<br>

#### Content {#summary}

- Merlin, OCaml's language server.
- A few performance issues.
- OCaml multicore for performance improvements.









<!-- {.block #cool title="The point of this demo" pause}
>
> foo
> 

{pause #vrai-sommaire up=cool} -->


<!-- <br> -->

{pause}

#### Structure {#structure}

The talk will be structured into three parts:

{pause style="text-align:center" #comment-presenter up-at-unpause=structure}

{style="display: flex; position:relative"}
> {#part1 slip include src="merlin.md"}
>
> {up=vrai-sommaire}
>
> {#part3 include src=multicore.md slip enter}
>
> {step}
>
> {enter #part4 include src="multicore_merlin.md" slip}
>
> {pause up-at-unpause=beginning}
>

{pause}

**Bonus:** We'll point out interesting aspects of OCaml as we go.




















<!-- > {#merci pause}
> > {#merci-2}
> > > # Merci de votre attention !
> > >
> > > - Site du projet : <https://github.com/panglesd/slipshow/>
> > >
> > > - Documentation : <https://slipshow.readthedocs.io/>
> > >
> > > - Source de ces slides : <https://choum.net/panglesd/slides/campus_du_libre.md>
> > >
> > > - Sliphub : <https://sliphub.choum.net/>







<style>
#merci {
  position:absolute;
  padding-right:200px;
  padding-left:200px;
  padding-top: 50px;
  padding-bottom: 50px;
  background-color: yellowgreen;
  top: 303px;
  border-radius: 30px;
}
#merci-2 {
  animation: growShrink 2s infinite;
}
@keyframes growShrink {
    0%, 100% {
      transform: scale(1); /* Original size */
    }
    50% {
      transform: scale(1.15); /* Enlarged size */
    }
  }
</style>


<style>
.flex {
  display: flex;
    justify-content: space-evenly;
}
.grow {
  flex-grow: 1;
}

.touche code {
  margin-left: 10px;
  display: inline-block;
  border: 3px solid black;
  padding: 9px;
  border-radius: 12px;
  width: 20px;
  height: 29px;
}
.touche.space code {
  width: 90px;
}
</style>



<style>
#youhou {
    font-size:1.5em
}
code {
  background-color:#f3f3f3;
}
</style> -->

