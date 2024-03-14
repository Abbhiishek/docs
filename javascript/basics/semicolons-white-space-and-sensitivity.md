# Semicolons, white space and sensitivity

### Semicolons

Every statement in a JavaScript program is optionally terminated using semicolons.

I said optionally, because the JavaScript interpreter is smart enough to introduce semicolons for you.

In most cases, you can omit semicolons altogether from your programs.

This fact is very controversial, and you’ll always find code that uses semicolons and code that does not.

My personal preference is to always avoid semicolons unless strictly necessary.

### White space

JavaScript does not consider white space meaningful. Spaces and line breaks can be added in any fashion you might like, even though this is _in theory_.

In practice, you will most likely keep a well defined style and adhere to what people commonly use.

For example, I like to always use 2 characters to indent.

### Case sensitivity

JavaScript is case sensitive.

A variable named `something` is different from `Something`.

A variable named `AGE` is different from `age` and from ‘aGe’.
