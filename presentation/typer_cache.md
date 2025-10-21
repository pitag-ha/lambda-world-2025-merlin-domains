#### Typer cache

{pause}


{carousel change-page='~n:"all"'}
-----
![](typer.svg)

---

![](typer_with_cache.svg)

-----

{pause}

-> When you modify code near the top of a file, Merlin needs to retype most of the file, so queries are slower.
Changes near the end have little impact as almost all previous typing results can be reused.
