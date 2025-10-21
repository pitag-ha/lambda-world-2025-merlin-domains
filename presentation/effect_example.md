```ocaml
type _ Effect.t += Love : unit t

let foo () =
  Format.printf "I ";
  perform Love;
  Format.printf " Lambda World!@."

(* Prints "I ♥ Lambda World!"*)
let main () =
  match foo () with
  | () -> ()
  | effect Love, k ->
    Format.printf "%s" "♥";
    continue k ()
```