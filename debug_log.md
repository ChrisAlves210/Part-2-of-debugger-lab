# Debug Log

**Explain how you used the VSCode debugger tools to uncover the bugs in Exercise 7. Be specific. What breakpoints did you set? Where did you step to? What made you realize the error?**

_Example: I set a breakpoint on line 5 and stepped until line 12. There, I discovered that the `x` variable had a value of `-3`, whereas it should have had a value of `7`. That made me realize that we should be adding the two numbers `x` and `y`, instead of subtracting._

I ran `exercise-7.py` and saw it print only `fantastic`, rather than the expected full sentence. I set a breakpoint in `replace_substring` at the recursive-case match and stepped over the remainder assignment. The Variables view showed `sentence` still held `'okay, I guess programming is okay.'`, but `remainder_of_sentence` was `''`. That exposed the first bug: the matched prefix was being sliced from `start_str` instead of from `sentence`. The recursive call stack also showed the next invocation receiving the empty string rather than the unprocessed sentence.

I then checked the non-matching case and found that it also recursed on `start_str[1:]` instead of advancing through `sentence[1:]`. I changed both slices to use `sentence`. After the fix, the program prints `fantastic, I guess programming is fantastic.`; the README's example input also produces `foo apple food a bfoofooa`.

I also ran `exercise-5.py` before fixing it and confirmed the uncaught `IndexError` occurs when the inner loop reaches the last list index and evaluates `list_of_nums[i + 1]`. Limiting that loop to `len(list_of_nums) - 1` avoids comparing the final item with a nonexistent next item. With the uncaught-exception breakpoint enabled after the fix, the program completes and prints the sorted list.