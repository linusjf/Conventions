- Use 4 spaces per indentation level. The 4-space rule is optional for continuation lines.

- Continuation lines should align wrapped elements either vertically using Python’s implicit line joining inside parentheses, brackets and braces, or using a hanging indent. When using a hanging indent the following should be considered; there should be no arguments on the first line and further indentation should be used to clearly distinguish itself as a continuation line.

- Spaces are the preferred indentation method. Python disallows mixing tabs and spaces for indentation.

- Limit all lines to a maximum of 79 characters.

- For flowing long blocks of text with fewer structural restrictions (docstrings or comments), the line length should be limited to 72 characters.

- The preferred way of wrapping long lines is by using Python’s implied line continuation inside parentheses, brackets and braces. Long lines can be broken over multiple lines by wrapping expressions in parentheses. These should be used in preference to using a backslash for line continuation. Backslashes may still be appropriate at times. Make sure to indent the continued line appropriately.

- Break before a binary operator.

- Surround top-level function and class definitions with two blank lines.

- Method definitions inside a class are surrounded by a single blank line.

- Extra blank lines may be used (sparingly) to separate groups of related functions. Blank lines may be omitted between a bunch of related one-liners (e.g. a set of dummy implementations).

- Use blank lines in functions, sparingly, to indicate logical sections.

- Code should always use UTF-8, and should not have an encoding declaration.

- All identifiers MUST use ASCII-only identifiers, and SHOULD use English words wherever feasible (in many cases, abbreviations and technical terms are used which aren’t English).

- Imports should usually be on separate lines.

- Imports are always put at the top of the file, just after any module comments and docstrings, and before module globals and constants.

- All module-level constants must be declared at the top of the file, immediately after imports and before any class or function definitions.
  Constants should be named in UPPER_SNAKE_CASE and grouped together for clarity and maintainability.

- Imports should be grouped in the following order:

  1. Standard library imports.
  2. Related third party imports.
  3. Local application/library specific imports.

- Put a blank line between each group of imports.

- Absolute imports are recommended, as they are usually more readable and tend to be better behaved (or at least give better error messages) if the import system is incorrectly configured (such as when a directory inside a package ends up on `sys.path`). However, explicit relative imports are an acceptable alternative to absolute imports, especially when dealing with complex package layouts where using absolute imports would be unnecessarily verbose:

- When importing a class from a class-containing module, it’s usually okay to spell this:

  from myclass import MyClass
  from foo.bar.yourclass import YourClass

  If this spelling causes local name clashes, then spell them explicitly:

  import myclass
  import foo.bar.yourclass

  and use `myclass.MyClass` and `foo.bar.yourclass.YourClass`.

- Wildcard imports (`from <module> import *`) should be avoided, as they make it unclear which names are present in the namespace, confusing both readers and many automated tools.

- Module level “dunders” (i.e. names with two leading and two trailing underscores) such as `__all__`, `__author__`, `__version__`, etc. should be placed after the module docstring but before any import statements _except_ `from __future__` imports. Python mandates that future-imports must appear in the module before any other code except docstrings:

- In Python, single-quoted strings and double-quoted strings are the same. Pick a rule and stick to it. When a string contains single or double quote characters, however, use the other one to avoid backslashes in the string. It improves readability.

- For triple-quoted strings, always use double quote characters to be consistent with the docstring convention in PEP 257.

- Avoid extraneous whitespace in the following situations:

  1. Immediately inside parentheses, brackets or braces.
  1. Between a trailing comma and a following close parenthesis.
  1. Immediately before a comma, semicolon, or colon.
  1. However, in a slice the colon acts like a binary operator, and should have equal amounts on either side (treating it as the operator with the lowest priority). In an extended slice, both colons must have the same amount of spacing applied. Exception: when a slice parameter is omitted, the space is omitted.
  1. Immediately before the open parenthesis that starts the argument list of a function call.
  1. Immediately before the open parenthesis that starts an indexing or slicing.
  1. More than one space around an assignment (or other) operator to align it with another.

- Avoid trailing whitespace anywhere. Because it’s usually invisible, it can be confusing: e.g. a backslash followed by a space and a newline does not count as a line continuation marker. Some editors don’t preserve it and many projects (like CPython itself) have pre-commit hooks that reject it.

- Always surround these binary operators with a single space on either side: assignment (`=`), augmented assignment (`+=`, `-=` etc.), comparisons (`==`, `<`, `>`, `!=`, `<=`, `>=`, `in`, `not in`, `is`, `is not`), Booleans (`and`, `or`, `not`).

- If operators with different priorities are used, consider adding whitespace around the operators with the lowest priority(ies). Use your own judgment; however, never use more than one space, and always have the same amount of whitespace on both sides of a binary operator:

- Function annotations should use the normal rules for colons and always have spaces around the `->` arrow if present.

- Don’t use spaces around the `=` sign when used to indicate a keyword argument, or when used to indicate a default value for an _unannotated_ function parameter.

- When combining an argument annotation with a default value, however, do use spaces around the `=` sign:

- Compound statements (multiple statements on the same line) are generally discouraged.

- While sometimes it’s okay to put an if/for/while with a small body on the same line, never do this for multi-clause statements. Also avoid folding such long lines!

- Trailing commas are usually optional, except they are mandatory when making a tuple of one element. For clarity, it is recommended to surround the latter in (technically redundant) parentheses.

- When trailing commas are redundant, they are often helpful when a version control system is used, when a list of values, arguments or imported items is expected to be extended over time. The pattern is to put each value (etc.) on a line by itself, always adding a trailing comma, and add the close parenthesis/bracket/brace on the next line. However it does not make sense to have a trailing comma on the same line as the closing delimiter (except in the case of singleton tuples).

- Names that are visible to the user as public parts of the API should follow conventions that reflect usage rather than implementation.

- The following naming styles are commonly distinguished:

  1. `b` (single lowercase letter)
  2. `B` (single uppercase letter)
  3. `lowercase`
  4. `lower_case_with_underscores`
  5. `UPPERCASE`
  6. `UPPER_CASE_WITH_UNDERSCORES`
  7. `CapitalizedWords` (or CapWords, or CamelCase – so named because of the bumpy look of its letters. This is also sometimes known as StudlyCaps. Note: When using acronyms in CapWords, capitalize all the letters of the acronym. Thus HTTPServerError is better than HttpServerError.
  8. `mixedCase` (differs from CapitalizedWords by initial lowercase character!)
  9. `Capitalized_Words_With_Underscores` (ugly!)

- There’s also the style of using a short unique prefix to group related names together. This is not used much in Python, but it is mentioned for completeness. For example, the `os.stat()` function returns a tuple whose items traditionally have names like `st_mode`, `st_size`, `st_mtime` and so on. (This is done to emphasize the correspondence with the fields of the POSIX system call struct, which helps programmers familiar with that.)

- In addition, the following special forms using leading or trailing underscores are recognized (these can generally be combined with any case convention):

  1. `_single_leading_underscore`: weak “internal use” indicator. E.g. `from M import *` does not import objects whose names start with an underscore.
  2. `single_trailing_underscore_`: used by convention to avoid conflicts with Python keyword, e.g. :
  3. `__double_leading_underscore`: when naming a class attribute, invokes name mangling (inside class FooBar, `__boo` becomes `_FooBar__boo`; see below).
  4. `__double_leading_and_trailing_underscore__`: “magic” objects or attributes that live in user-controlled namespaces. E.g. `__init__`, `__import__` or `__file__`. Never invent such names; only use them as documented.

- Never use the characters ‘l’ (lowercase letter el), ‘O’ (uppercase letter oh), or ‘I’ (uppercase letter eye) as single character variable names. In some fonts, these characters are indistinguishable from the numerals one and zero. When tempted to use ‘l’, use ‘L’ instead.

- Identifiers used in the standard library must be ASCII compatible.

- Modules should have short, all-lowercase names. Underscores can be used in the module name if it improves readability. Python packages should also have short, all-lowercase names, although the use of underscores is discouraged.

- When an extension module written in C or C++ has an accompanying Python module that provides a higher level (e.g. more object oriented) interface, the C/C++ module has a leading underscore (e.g. `_socket`).

- Class names should normally use the CapWords convention.

- The naming convention for functions may be used instead in cases where the interface is documented and used primarily as a callable. Note that there is a separate convention for builtin names: most builtin names are single words (or two words run together), with the CapWords convention used only for exception names and builtin constants.

- Names of type variables introduced in should normally use CapWords preferring short names: `T`, `AnyStr`, `Num`. It is recommended to add suffixes `_co` or `_contra` to the variables used to declare covariant or contravariant behavior correspondingly:

- Because exceptions should be classes, the class naming convention applies here. However, you should use the suffix “Error” on your exception names (if the exception actually is an error).

- Modules that are designed for use via `from M import *` should use the `__all__` mechanism to prevent exporting globals, or use the older convention of prefixing such globals with an underscore (which you might want to do to indicate these globals are “module non-public”).

- Function names should be lowercase, with words separated by underscores as necessary to improve readability.

- Variable names follow the same convention as function names.

- mixedCase is allowed only in contexts where that’s already the prevailing style (e.g. threading.py), to retain backwards compatibility.

- Always use `self` for the first argument to instance methods.

- Always use `cls` for the first argument to class methods.

- If a function argument’s name clashes with a reserved keyword, it is generally better to append a single trailing underscore rather than use an abbreviation or spelling corruption. Thus `class_` is better than `clss`. (Perhaps better is to avoid such clashes by using a synonym.)

- Use the function naming rules: lowercase with words separated by underscores as necessary to improve readability.

- Use one leading underscore only for non-public methods and instance variables.

- To avoid name clashes with subclasses, use two leading underscores to invoke Python’s name mangling rules.

- Python mangles these names with the class name: if class Foo has an attribute named `__a`, it cannot be accessed by `Foo.__a`. (An insistent user could still gain access by calling `Foo._Foo__a`.) Generally, double leading underscores should be used only to avoid name conflicts with attributes in classes designed to be subclassed.

- Constants are usually defined on a module level and written in all capital letters with underscores separating words. Examples include `MAX_OVERFLOW` and `TOTAL`.

- Always decide whether a class’s methods and instance variables (collectively: “attributes”) should be public or non-public. If in doubt, choose non-public; it’s easier to make it public later than to make a public attribute non-public.

- Public attributes should have no leading underscores.

- If your public attribute name collides with a reserved keyword, append a single trailing underscore to your attribute name. This is preferable to an abbreviation or corrupted spelling. (However, notwithstanding this rule, ‘cls’ is the preferred spelling for any variable or argument which is known to be a class, especially the first argument to a class method.)

- For simple public data attributes, it is best to expose just the attribute name, without complicated accessor/mutator methods. Keep in mind that Python provides an easy path to future enhancement, should you find that a simple data attribute needs to grow functional behavior. In that case, use properties to hide functional implementation behind simple data attribute access syntax.
  Note 1: Try to keep the functional behavior side-effect free, although side-effects such as caching are generally fine.
  Note 2: Avoid using properties for computationally expensive operations; the attribute notation makes the caller believe that access is (relatively) cheap.

- If your class is intended to be subclassed, and you have attributes that you do not want subclasses to use, consider naming them with double leading underscores and no trailing underscores. This invokes Python’s name mangling algorithm, where the name of the class is mangled into the attribute name. This helps avoid attribute name collisions should subclasses inadvertently contain attributes with the same name.
  Note 1: Note that only the simple class name is used in the mangled name, so if a subclass chooses both the same class name and attribute name, you can still get name collisions.
  Note 2: Name mangling can make certain uses, such as debugging and `__getattr__()`, less convenient. However the name mangling algorithm is well documented and easy to perform manually.
  Note 3: Not everyone likes name mangling. Try to balance the need to avoid accidental name clashes with potential use by advanced callers.

- Any backwards compatibility guarantees apply only to public interfaces. Accordingly, it is important that users be able to clearly distinguish between public and internal interfaces.

- Documented interfaces are considered public, unless the documentation explicitly declares them to be provisional or internal interfaces exempt from the usual backwards compatibility guarantees. All undocumented interfaces should be assumed to be internal.

- To better support introspection, modules should explicitly declare the names in their public API using the `__all__` attribute. Setting `__all__` to an empty list indicates that the module has no public API.

- Even with `__all__` set appropriately, internal interfaces (packages, modules, classes, functions, attributes or other names) should still be prefixed with a single leading underscore.

- An interface is also considered internal if any containing namespace (package, module or class) is considered internal.

- Imported names should always be considered an implementation detail. Other modules must not rely on indirect access to such imported names unless they are an explicitly documented part of the containing module’s API, such as `os.path` or a package’s `__init__` module that exposes functionality from submodules.

- Code should be written in a way that does not disadvantage other implementations of Python (PyPy, Jython, IronPython, Cython, Psyco, and such).

- Comparisons to singletons like None should always be done with `is` or `is not`, never the equality operators.
  Also, beware of writing `if x` when you really mean `if x is not None` – e.g. when testing whether a variable or argument that defaults to None was set to some other value. The other value might have a type (such as a container) that could be false in a boolean context!

- Use `is not` operator rather than `not ... is`. While both expressions are functionally identical, the former is more readable and preferred:

- When implementing ordering operations with rich comparisons, it is best to implement all six operations (`__eq__`, `__ne__`, `__lt__`, `__le__`, `__gt__`, `__ge__`) rather than relying on other code to only exercise a particular comparison.

- To minimize the effort involved, the `functools.total_ordering()` decorator provides a tool to generate missing comparison methods.

- PEP 207 indicates that reflexivity rules _are_ assumed by Python. Thus, the interpreter may swap `y > x` with `x < y`, `y >= x` with `x <= y`, and may swap the arguments of `x == y` and `x != y`. The `sort()` and `min()` operations are guaranteed to use the `<` operator and the `max()` function uses the `>` operator. However, it is best to implement all six operations so that confusion doesn’t arise in other contexts.

- Always use a def statement instead of an assignment statement that binds a lambda expression directly to an identifier:

- The first form means that the name of the resulting function object is specifically ‘f’ instead of the generic `<lambda>`. This is more useful for tracebacks and string representations in general. The use of the assignment statement eliminates the sole benefit a lambda expression can offer over an explicit def statement (i.e. that it can be embedded inside a larger expression)

- Derive exceptions from `Exception` rather than `BaseException`. Direct inheritance from `BaseException` is reserved for exceptions where catching them is almost always the wrong thing to do.

- Design exception hierarchies based on the distinctions that code _catching_ the exceptions is likely to need, rather than the locations where the exceptions are raised. Aim to answer the question “What went wrong?” programmatically, rather than only stating that “A problem occurred”.

- Use exception chaining appropriately. `raise X from Y` should be used to indicate explicit replacement without losing the original traceback.

- When deliberately replacing an inner exception (using `raise X from None`), ensure that relevant details are transferred to the new exception (such as preserving the attribute name when converting KeyError to AttributeError, or embedding the text of the original exception in the new exception message).

- When catching exceptions, mention specific exceptions whenever possible instead of using a bare `except:` clause:

- A bare `except:` clause will catch SystemExit and KeyboardInterrupt exceptions, making it harder to interrupt a program with Control-C, and can disguise other problems. If you want to catch all exceptions that signal program errors, use `except Exception:` (bare except is equivalent to `except BaseException:`).

- A good rule of thumb is to limit use of bare ‘except’ clauses to two cases:

  1. If the exception handler will be printing out or logging the traceback; at least the user will be aware that an error has occurred.
  2. If the code needs to do some cleanup work, but then lets the exception propagate upwards with `raise`. `try...finally` can be a better way to handle this case.

- When catching operating system errors, prefer the explicit exception hierarchy introduced in Python 3.3 over introspection of `errno` values.

- Additionally, for all try/except clauses, limit the `try` clause to the absolute minimum amount of code necessary. Again, this avoids masking bugs.

- When a resource is local to a particular section of code, use a `with` statement to ensure it is cleaned up promptly and reliably after use. A try/finally statement is also acceptable.

- Context managers should be invoked through separate functions or methods whenever they do something other than acquire and release resources.

- Be consistent in return statements. Either all return statements in a function should return an expression, or none of them should. If any return statement returns an expression, any return statements where no value is returned should explicitly state this as `return None`, and an explicit return statement should be present at the end of the function (if reachable).

- Use `''.startswith()` and `''.endswith()` instead of string slicing to check for prefixes or suffixes.

- Object type comparisons should always use isinstance() instead of comparing types directly.

- For sequences, (strings, lists, tuples), use the fact that empty sequences are false.

- Don’t write string literals that rely on significant trailing whitespace. Such trailing whitespace is visually indistinguishable and some editors (or more recently, reindent.py) will trim them.

- Don’t compare boolean values to True or False using `==`.

- Use of the flow control statements `return`/`break`/`continue` within the finally suite of a `try...finally`, where the flow control statement would jump outside the finally suite, is discouraged. This is because such statements will implicitly cancel any active exception that is propagating through the finally suite.

- Function annotations should use PEP 484 syntax.
- However, outside the stdlib, experiments within the rules of PEP 484 are now encouraged. For example, marking up a large third party library or application with PEP 484 style type annotations, reviewing how easy it was to add those annotations, and observing whether their presence increases code understandability.
- The Python standard library should be conservative in adopting such annotations, but their use is allowed for new code and for big refactorings.
- For code that wants to make a different use of function annotations it is recommended to put a comment of the form:

  `# type: ignore`

  near the top of the file; this tells type checkers to ignore all annotations.

- Like linters, type checkers are optional, separate tools. Python interpreters by default should not issue any messages due to type checking and should not alter their behavior based on annotations.
- Users who don’t want to use type checkers are free to ignore them. However, it is expected that users of third party library packages may want to run type checkers over those packages. For this purpose PEP 484 recommends the use of stub files: .pyi files that are read by the type checker in preference of the corresponding .py files. Stub files can be distributed with a library, or separately (with the library author’s permission) through the typeshed repo.

- PEP 526 introduced variable annotations. The style recommendations for them are similar to those on function annotations described above.

- Annotations for module level variables, class and instance variables, and local variables should have a single space after the colon.
- There should be no space before the colon.
- If an assignment has a right hand side, then the equality sign should have exactly one space on both sides.
