# List of tasks that need to done

1. Figure out how to represent arrays internally
2. Figure out how to represent structs internally
3. Figure out how to represent cell-arrays internally
4. Need to figure out in general how to optimize memory in WASM. Inter/Intra
   procedural analysis would be useful here.
5. Need to figure out whether we should be targeting the binary format or the
   wat format
6. We need labels for every loop and keep track of all the structured
   instructions. (Note: Remember that logical &&, || are implemented at a
   low-level using structured flow instructions.)
7. Figure out how to create the wasm AST, or whether we should be even creating
   one in the first place! Depends on how the stack-machine is interpreted and
   what is convenient. Probably will use JastAdd for this purposes and 
8. Array accessing with colon operators