<!--#region:intro-->
# Regular Expression `\R` Escape for ECMAScript

<!--#endregion:intro-->

<!--#region:status-->
## Status

**Stage:** 1  
**Champion:** Ron Buckton ([@rbuckton](https://github.com/rbuckton))  

_For detailed status of this proposal see [TODO](#todo), below._  
<!--#endregion:status-->

<!--#region:authors-->
## Authors

* Ron Buckton ([@rbuckton](https://github.com/rbuckton))  
<!--#endregion:authors-->

<!--#region:motivations-->
# Motivations

> NOTE: See https://github.com/rbuckton/proposal-regexp-features for an overview of
> how this proposal fits into other possible future features for Regular Expressions.

The `\R` escape sequence matches the various sets of code points that match a unicode line terminator, which can be difficult to write correctly.

<!--#endregion:motivations-->

<!--#region:prior-art-->
# Prior Art 

* [Perl](https://rbuckton.github.io/regexp-features/engines/perl.html#feature-line-endings-escape)  
* [PCRE](https://rbuckton.github.io/regexp-features/engines/pcre.html#feature-line-endings-escape)  
* [Boost.Regex](https://rbuckton.github.io/regexp-features/engines/boost.regex.html#feature-line-endings-escape)  
* [Oniguruma](https://rbuckton.github.io/regexp-features/engines/oniguruma.html#feature-line-endings-escape)  
* [ICU](https://rbuckton.github.io/regexp-features/engines/icu.html#feature-line-endings-escape)  
* [Glib/GRegex](https://rbuckton.github.io/regexp-features/engines/glib-gregex.html#feature-line-endings-escape)  

See https://rbuckton.github.io/regexp-features/features/line-endings-escape.html for additional information.

<!--#endregion:prior-art-->

<!--#region:syntax-->
# Syntax

- `\R` &mdash; Matches any line ending character sequence.

> NOTE: Requires the `u` or `v` flags, as `\R` is currently just an escape for `R` without the `u` flag.

> NOTE: Not supported inside of a character class.


<!--#endregion:syntax-->

<!--#region:semantics-->
# Semantics

- In `u` or `v` mode, `\R` is roughly equivalent to the following pattern:
  ```re
  (?>\r\n?|[\x0A-\x0C\x85\u{2028}\u{2029}])
  ```
  - Aligns with `^` and `$` in `mu` mode
- When not in `u` or `v` mode, `\R` will continue to match the literal character `R`.

> NOTE: The above example uses atomic groups `(?>)` to prevent backtracking when matching `\r\n?`. Atomic groups is proposed [here](https://github.com/rbuckton/proposal-regexp-atomic-operators).

<!--#endregion:semantics-->

<!--#region:examples-->
# Examples

```js
// split lines regardless of line termiantor style
const lines = fs.readFileSync("file.txt", "utf8").split(/\R/ug);
```

<!--#endregion:examples-->

<!--#region:api-->
<!-- # API -->

<!--#endregion:api-->

<!--#region:grammar-->
<!-- # Grammar

```grammarkdown
``` -->
<!--#endregion:grammar-->

<!--#region:references-->
<!-- # References

> TODO: Provide links to other specifications, etc.

* [Title](url)   -->
<!--#endregion:references-->

# History

- October 28, 2021 &mdash; Proposed for Stage 1 ([slides](https://1drv.ms/p/s!AjgWTO11Fk-TkfoQmhSpEYYM0spVqg?e=zsP6g4))
  - Outcome: Advanced to Stage 1

<!--#region:todo-->
# TODO

The following is a high-level list of tasks to progress through each stage of the [TC39 proposal process](https://tc39.github.io/process-document/):

### Stage 1 Entrance Criteria

* [x] Identified a "[champion][Champion]" who will advance the addition.  
* [x] [Prose][Prose] outlining the problem or need and the general shape of a solution.  
* [x] Illustrative [examples][Examples] of usage.  
* [ ] ~~High-level [API][API].~~  

### Stage 2 Entrance Criteria

* [x] [Initial specification text][Specification].  
* [ ] ~~[Transpiler support][Transpiler] (_Optional_).~~  

### Stage 3 Entrance Criteria

* [ ] [Complete specification text][Specification].  
* [ ] Designated reviewers have [signed off][Stage3ReviewerSignOff] on the current spec text.  
* [ ] The ECMAScript editor has [signed off][Stage3EditorSignOff] on the current spec text.  

### Stage 4 Entrance Criteria

* [ ] [Test262](https://github.com/tc39/test262) acceptance tests have been written for mainline usage scenarios and [merged][Test262PullRequest].  
* [ ] Two compatible implementations which pass the acceptance tests: [\[1\]][Implementation1], [\[2\]][Implementation2].  
* [ ] A [pull request][Ecma262PullRequest] has been sent to tc39/ecma262 with the integrated spec text.  
* [ ] The ECMAScript editor has signed off on the [pull request][Ecma262PullRequest].  
<!--#endregion:todo-->

<!-- The following links are used throughout the README: -->

[Process]: https://tc39.es/process-document/
[Proposals]: https://github.com/tc39/proposals/
[Grammarkdown]: http://github.com/rbuckton/grammarkdown#readme
[Champion]: #status
[Prose]: #motivations
[Examples]: #examples
[API]: #api
[Specification]: https://tc39.es/proposal-regexp-r-escape

[Transpiler]: #todo
[Stage3ReviewerSignOff]: #todo
[Stage3EditorSignOff]: #todo
[Test262PullRequest]: #todo
[Implementation1]: #todo
[Implementation2]: #todo
[Ecma262PullRequest]: #todo
