# Matlab Semantics

1. There are many different types of mclasses. Arrays must have a type of one of
  those mclases. If we try to set another value, it will either get implicitely
  converted/coerced to that value, or it will throw an error if conversion is
  not possible.
 
```
a = ones(1,5,'uint8')
a(5)="97"
>>
	The following error occurred converting from string to uint8:
	Conversion to uint8 from string is not possible.	
```
```
a = ones(1,5,'uint8')
a(5)='a'
>>
a=
	1
	1
	1
	1
	97
```
__RESOLUTION__: Verify type coercions. 
2. If a type such as 'uint8' is defined and we try to assign a value that
   clearly overflows the uint8 such as 256.
   The variable gets set to the max int8 number, i.e. 255 
```
a = uint8(256)
>>
a=
	255
```
__RESOLUTION__: Only use the natively supported types in WebAssembly and a
one-to-one correspondance with WASM.
3. Variables of the same name may have different types at different points. i.e. 
	`a = 3;a='c';%this is allowed`
	- To resolve this we must rename the variable at each change of type.
4. Matlab has particular type coercions at some points. i.e for some cases it
   will cast a type from DOUBLE to INT implicitly, like when accessing an array.
   This must be taken care of by the target language.
   SOLUTION: Use type coercions in WASM
5. Things to notice with built-in functions.
	- Should optimize as much as possible. If the function is simple enough.
	  INLINE
	- To support this, make a completely different module that supports all the
	  built-in functions. Leave some sort of 'assume it exists' idea on your
	  compiler, then simply add the function to another module called
	  libmatwably.

__RESOLUTION__: 	For this, we will have to rename all the overloaded functions
					to have consistent naming.
6. Out of bounce in arrays.
	- When reading out of bounce, Matlab throws error
	- When writing out of bounds. Matlab grows array.
__RESOLUTION__: Take into account range analysis created
