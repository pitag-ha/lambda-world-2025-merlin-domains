
```ocaml
type _ Effect.t += PartialResult : Typetree.item list -> unit t

let rec typing_loop is_right_pos env typed_items parsetree =
  match parsetree with
  | [] -> []
  | item :: nparsetree ->
    let new_env, typed_item = type_item env item in
    let ntyped_items = typed_item :: typed_items in

    if is_right_pos item then (
      perform (PartialResult ntyped_items);
      typing_loop is_right_pos new_env ntyped_items nparsetree)
    else typing_loop is_right_pos new_env ntyped_items nparsetree

let make_pipeline config pos =
  let file = read config in
  let parsetree = parse file in
  let exp_parsetree = expand_ppx parsetree in
  let typer_result =
    match typing_loop pos [] [] exp_parsetree with
    | typed_items -> typed_items
    | effect PartialResult typed_items, k ->
      let result =
        { file; parsetree = exp_parsetree; typer_result = typed_items }
      in
      share result;
      continue k ()
  in
  { file; parsetree = exp_parsetree; typer_result }
```

<!-- 
```ocaml
type style = Emo | Text
type _ Effect.t += Love : style -> unit t | World : unit t

let foo () =
  Format.printf "I ";
  perform (Love Emo);
  Format.printf " Lambda World!@."

(* Prints "I ♥ Lambda World!"*)
let main () =
  match foo () with
  | () -> ()
  | effect World, k -> Format.printf "World"; continue k ()
  | effect Love style, k ->
    let str = match style with | Emo -> "♥" | Text -> "love"
    in
    Format.printf "%s" str;
    continue k ()
``` 
-->