When a function is called, a new Execution Context [[Concepts#Execution Context]] is created and placed in the Execution Stack.

Same as the Global Exec Context [[10. The Global env and the Global Object]] it has its variables and functions, it also has the Creation and Execute phases.

If a function `a` calls a function `b` inside its code, during the Execute Phase of the `a` function, when it encounters the `b` function call, it will create another Exe Context for `b` and stack it in the Execution Stack. When `b` Exec Context finished, the Execution Stack will return to `a` Exec Context.