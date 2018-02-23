# WebAssembly research and features

- Big motivation of WebAssembly is the quick decoding/encoding, validation of
  Wasm code. 
- Why not a full stack machine?
	- Structure if/else statements make the code more predictable and allow
	  verification of code with one pass of the compiler.
	- Because it has to then do a fixed point analysis, which requires for the
	  code to have iterations.
