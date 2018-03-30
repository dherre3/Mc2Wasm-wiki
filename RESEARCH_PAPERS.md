# RESEARCH

- Xu Li and Laurie Hendren - _"Mc2For: A tool for aumatically translation MATLAB to FORTRAN 95"_
	- Summary & Ideas:
		- Translation from MATLAB to Fortran 95.
		- Use of Range analysis to minimize the overhead of array bound checks
		  in matlab
		- Shape analysis, estimates the shape and extend of array dimensions
		  using a DSL.
		- Inline of built-in functions
		- Creating a second module for all built-in functions whereby we allow
		  "holes" in functions and assume that is supported by the library.


- L. D Rose and P. Padue "Techiniques for the Translation of MATLAB Programs
  into Fortran 90"
  		- Use of SSA, in order to simplify translation. i.e. All assignments
		  have a different name.
- Zakai, A., 2011, October. _"Emscripten: an LLVM-to-JavaScript compiler."_
 In Proceedings of the ACM international conference companion on Object oriented programming systems languages and applications companion (pp. 301-312). ACM.
- Haas, Andreas, et al. _"Bringing the web up to speed with WebAssembly."_ 
Proceedings of the 38th ACM SIGPLAN Conference on Programming Language Design and Implementation. ACM, 2017.
