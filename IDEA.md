# IDEAS

- Mc2for idea of Providing size to create a specialized, optimized version of code
- To analyze results, a few things:
	- Lines of code for generated code.We can maybe include the binary text format information.
	- Execution time and ratio.
- Thinking of SSA form
- Have different module representing lib. So, lib would be the library calls for
  built-ins in wasm
- Create another module to handle all the basic array operations. From creating
  and allocating an array to copying an array, creating an array of ones,
  creating an array of zeros, setting an array element, getting an array
  element, deallocating an array. etc. 
- WASM is not an AST, its a stack machine, check internal representation for stack
  machine and see if its clean to make such a representation in the compiler.
- Using of copy semantics, use of kind analysis, range analysis, value analysis,
  shape analysis.
- Something to look at is the translation to binary format, is it straight
  forward, can we do it? Should we use the wat2wasm tool instead.

