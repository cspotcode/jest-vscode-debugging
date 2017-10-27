This repo shows two ways to test code in Jest with VSCode debugging support:

One is a conventional Jest setup, where code is transpiled at test runtime via Jest loaders.

The other runs a normal build first, then tests the generated code.

## Notes:

Sourcemaps must be inline and must refer to external sources.  The sourcemap is inline; the source code is not.  This is because:

A. Jest does not support external sourcemaps.  
B. VSCode can't open a source file unless it lives on disc.

Jest loaders should do this automatically; no additional config required.  When pre-compiling via a build script, we must configure this ourselves.

Jest caching should be irrelevant because VSCode never looks on disc for generated code or sourcemaps; it gets both straight from node via the inspector protocol.
Essentially, VSCode receives the executing, transpiled code via node's inspector protocol, parses out the sourcemap, and reads the source path on disc.  Only the source needs to be discoverable on disc so that VSCode can open it in the editor.

