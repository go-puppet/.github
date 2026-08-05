<p align="center"><img src="https://raw.githubusercontent.com/go-puppet/brand/main/social/go-puppet.png" alt="go-puppet" width="640"></p>

<h1 align="center">go-puppet</h1>
<p align="center"><strong>The Puppet language in pure Go — lexer, parser, Puppet::Pops AST, evaluator and catalog compiler, no cgo.</strong></p>

<p align="center">
  🌐 <a href="https://go-puppet.github.io">Website</a> ·
  📚 <a href="https://go-puppet.github.io/docs/">Documentation</a>
</p>

<p align="center">
  <a href="https://go-puppet.github.io/docs/"><img alt="Docs" src="https://img.shields.io/badge/docs-mkdocs--material-FBBF24?style=flat-square"></a>
  <a href="https://github.com/go-puppet/puppet/blob/main/LICENSE"><img alt="License: BSD-3-Clause" src="https://img.shields.io/badge/license-BSD--3--Clause-blue?style=flat-square"></a>
  <img alt="Go 1.26.4+" src="https://img.shields.io/badge/go-1.26.4%2B-00ADD8?style=flat-square&logo=go&logoColor=white">
  <img alt="Coverage 100%" src="https://img.shields.io/badge/coverage-100%25-1a7f37?style=flat-square">
</p>

---

**go-puppet** is a **pure-Go (no cgo) implementation of the [Puppet](https://www.puppet.com/docs/puppet/latest/puppet_language.html)
language**. It parses Puppet 8 manifests into a faithful `Puppet::Pops`-style
AST and compiles them to a **catalog** — a resource graph with containment and
relationship edges, serializable to Puppet catalog JSON.

It builds on the Puppet-family libraries — the type system is
**[go-pcore](https://github.com/go-pcore)**, data binding is
**[go-hiera](https://github.com/go-hiera)**, and facts are
**[go-facter](https://github.com/go-facter)** — and never reimplements them. A
function/type registry seam lets **go-ruby-puppet** contribute Ruby-defined
custom functions.

## Repositories

| Repo | What it is |
|------|------------|
| [**puppet**](https://github.com/go-puppet/puppet) | the library: `lexer`, `parser`, `ast`, `eval`, `catalog`, `hcl` — parse a manifest (Puppet `.pp` or Terraform-style HCL2) and compile it to a catalog |
| [**docs**](https://github.com/go-puppet/docs) | MkDocs Material documentation, versioned with [mike], served at [/docs/](https://go-puppet.github.io/docs/) |
| [**go-puppet.github.io**](https://github.com/go-puppet/go-puppet.github.io) | the Hugo landing page |
| [**brand**](https://github.com/go-puppet/brand) | logos and brand assets |

## Principles

- **Pure Go, zero cgo.** Cross-compiles and embeds anywhere; a static binary by
  default, green across the six 64-bit Go targets.
- **Faithful to Puppet 8 / Pops.** Node kinds, grammar, precedence and evaluator
  semantics track the Puppet specification.
- **No reinvention.** Types → go-pcore, data → go-hiera, facts → go-facter.
- **100% test coverage** is the target, enforced as a CI gate, including every
  parse- and eval-error branch.

## Status

**v0.1 — lexer, parser, AST, evaluator and catalog compiler complete.** The
Puppet 8 front-end (literals & interpolation, heredocs, data-type expressions,
the full operator ladder, selectors, conditionals, resources, class/define/node/
function definitions, calls with lambdas, relationship chaining) and an evaluator
(scopes, class/defined-type instantiation, iteration, a built-in function set,
`lookup()` via go-hiera, facts via go-facter) that compiles to a Puppet catalog —
at 100% coverage, `gofmt` + `go vet` clean, CI green across amd64, arm64, riscv64,
loong64, ppc64le and s390x. EPP/ERB templates, resource defaults/overrides/
collectors, exported resources, the plan/apply language, an extensive stdlib and a
Terraform-style HCL2 front-end (`hcl.Parse` → the same catalog) are all
implemented; Pcore type constructors beyond the scalar core and the HCL2 v0.2
expression set are still in progress.

BSD-3-Clause.

[mike]: https://github.com/jimporter/mike
