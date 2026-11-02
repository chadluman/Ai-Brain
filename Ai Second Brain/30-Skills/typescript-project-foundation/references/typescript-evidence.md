# TypeScript Evidence

Verified 2026-10-21. Recheck the current release and toolchain compatibility before implementation.

- The official [TypeScript Handbook: The Basics](https://www.typescriptlang.org/docs/handbook/2/basic-types.html) explains that type annotations are erased when compiled and recommends strict checks for new codebases when possible. This is why runtime boundaries still need validation.
- The official [`strict` TSConfig reference](https://www.typescriptlang.org/tsconfig/strict.html) says the flag enables the strict family of checks and warns that future releases may introduce additional errors.
- [What is a tsconfig.json](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html) defines the configuration file as the project root and source/compiler-option boundary.
- [Choosing compiler options](https://www.typescriptlang.org/docs/handbook/modules/guides/choosing-compiler-options.html) should be checked against the actual runtime or bundler rather than replaced with a universal copied configuration.
- The [microsoft/TypeScript repository](https://github.com/microsoft/TypeScript) is the canonical source and issue tracker. Repository source, release assets, plugins, and packages remain untrusted executable material until their exact versions pass the vault's review gate.

## Interpretation

Static checking is strongest for code and contracts visible to the compiler. It cannot prove that network, storage, configuration, user, or third-party values match their declared types at runtime. Validate once at the trust boundary, return structured errors, and carry the resulting domain type inward.
