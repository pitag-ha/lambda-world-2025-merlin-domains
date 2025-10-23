```ocaml
type _ Effect.t += Love : unit Effect.t

let foo () =
  Format.printf "I ";
  Effect.perform Love;
  Format.printf " Lambda World!@."

(* Prints "I ♥ Lambda World!"*)
let main () =
  match foo () with
  | () -> ()
  | Effect.effect Love, k ->
    Format.printf "%s" "♥";
    Effect.continue k ()
```