OByteLib
========

OCaml bytecode library tools.
Useful to read, write and evaluate OCaml bytecode files.

# Warning

I simply told obytelib to accept 4.12.0 OCaml bytecode files. While it seems to work I can provide no guarantees that it actually does.

Example
=======

```
open OByteLib

let usage () =
  Printf.eprintf "Usage: %s <input.byte>\n" Sys.argv.(0);
  exit 1
    
let inpath =
  match Sys.argv with
  | [| _; inpath |] -> inpath
  | _ -> usage ()
  
let () =
  match Filename.extension inpath with
  | ".byte" ->
    let bytefile = Bytefile.read inpath in (* Load the given bytecode file *)
    Bytefile.print stdout bytefile;        (* Pretty-print its contents    *)
    Interp.eval_bytefile bytefile;         (* Evaluate its code            *)
  | ".cmo" ->
    let cmofile = Cmofile.read inpath in   (* Load the given .cmo file     *)
    Cmofile.print stdout cmofile           (* Pretty-print its contents    *)
  | _ ->
    usage ()
```
