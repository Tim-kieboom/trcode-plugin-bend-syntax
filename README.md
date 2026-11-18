# Bend syntax for TerminalCode

Syntax highlighting for [Bend 2](https://github.com/bendlang/bend) (`.bend`) as a [TerminalCode](https://github.com/Tim-kieboom/TerminalCode) plugin. (Bend 1, the older Python-like language of HigherOrderCO/Bend, has another grammar and is not covered.)

It is a language and nothing else: there is no code in it and no pane. The plugin is

- `bend.wasm`, the tree-sitter grammar built for WebAssembly (about 5 MB: the grammar is big, and the editor compiles it when a Bend file is opened, which takes about a tenth of a second in a release build),
- `manifest.toml`, which says which files are Bend (`[language]`: `extensions`, `comment`, `grammar_name`) and has the highlight query as text.

TerminalCode loads the grammar in its sandbox (plugin API 1.12, TerminalCode 0.11.0 or later) and colors the
files with the query, using the colors of your theme (`syntax.keyword`, `syntax.string`, ... in the theme file).

## Use

"Plugins: Manage", install **Bend**, and turn it on. Bend files are colored when they are opened, and
`ctrl+/` comments a line with `#`.

## Where the grammar comes from

The grammar and the query are those of [Soulthym/tree-sitter-bend2](https://github.com/Soulthym/tree-sitter-bend2) at v0.3.0 (3819b83)
(MIT, `LICENSE-GRAMMAR`), which follows Bend 2.0.36. The module was built from that revision with the tree-sitter CLI:

```sh
git clone https://github.com/Soulthym/tree-sitter-bend2 && cd tree-sitter-bend2
git checkout v0.3.0
tree-sitter build --wasm -o bend.wasm
```

A new version of the grammar needs a new `version` in `manifest.toml` and a release (the module is the file the
installer checks). The query is copied into the manifest with its patterns in the opposite order (TerminalCode takes
the first of two patterns on the same text; the grammar's file is written for the last), with some capture names
renamed to ones themes have.

## Licence

The plugin is MIT or Apache-2.0, as the other plugins; the grammar is MIT (`LICENSE-GRAMMAR`).
