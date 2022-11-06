# Javascript
## let, var, const
* `var` 
    * TL;DR: don't use it, prefer `let` and `const`
    * var scope is global when outside a function, local when inside a function. 
    * can be re-declared
    * problematic when a local var shadows a global var since it will overwrite the global one when called
* `let`
    * let is only block scoped (within curly braces)
    * can be updated, but not re-declared within the same scope
* `const`
    * block scoped
    * can't be updated or re-declared
