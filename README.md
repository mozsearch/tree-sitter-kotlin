# tree-sitter-kotlin

[![CI][ci]](https://github.com/tree-sitter-grammars/tree-sitter-kotlin/actions/workflows/ci.yml)
[![discord][discord]](https://discord.gg/w7nTvsVJhm)
[![matrix][matrix]](https://matrix.to/#/#tree-sitter-chat:matrix.org)
[![crates][crates]](https://crates.io/crates/tree-sitter-kotlin-ng)
[![npm][npm]](https://www.npmjs.com/package/@tree-sitter-grammars/tree-sitter-kotlin)
[![pypi][pypi]](https://pypi.org/project/tree-sitter-kotlin)

Kotlin grammar for [tree-sitter](https://github.com/tree-sitter/tree-sitter).

## This fork

This is [searchfox](https://searchfox.org)'s fork of tree-sitter-kotlin-ng
1.1.0, for its history tokenizer, which tokenizes trees' leaves, and so needs
all of a file's text to be in its tree, and parses Firefox's Kotlin (all of
whose 5939 files parse without errors with it, vs 42 with errors, some losing
thousands of characters to error recovery):
- `;`s are in trees (aliased statement and member separators, which were
  hidden), and `!is`'s `!` and nullable types' `?`s before comments are their
  tokens' (the external scanner skipped them).
- Soft and modifier keywords can be names (ex: `var private = true`,
  `suspend { ... }`, `contains(dynamic)`), where nothing else parses.
- Kotlin 2's multi-dollar interpolation (`$$"..."`), explicit backing fields
  (`field = ...`), and guard conditions in `when` (`is Foo if bar ->`).
- Primary constructors on their class's next line (`class Foo` followed by
  `internal constructor(` or an annotated `constructor(`), annotated getters
  and setters after properties without types and after getters (with a
  zero-width `_accessor_semi`), annotated parenthesized types
  (`@Composable (() -> Unit)`), empty collection literals, and trailing
  commas in type arguments and parameters.

## References

- [Kotlin Grammar](https://kotlinlang.org/docs/reference/grammar.html)

[ci]: https://img.shields.io/github/actions/workflow/status/tree-sitter-grammars/tree-sitter-kotlin/ci.yml?logo=github&label=CI
[discord]: https://img.shields.io/discord/1063097320771698699?logo=discord&label=discord
[matrix]: https://img.shields.io/matrix/tree-sitter-chat%3Amatrix.org?logo=matrix&label=matrix
[npm]: https://img.shields.io/npm/v/@tree-sitter-grammars/tree-sitter-kotlin?logo=npm
[crates]: https://img.shields.io/crates/v/tree-sitter-kotlin-ng?logo=rust
[pypi]: https://img.shields.io/pypi/v/tree-sitter-kotlin?logo=pypi&logoColor=ffd242
