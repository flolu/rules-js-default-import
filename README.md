<div align="center">
  <h1>rules_js default import broken</h1>
  <p>TypeError: (0 , _sanitizeHtml(...).default) is not a function</p>
</div>

# Solution

The solution was rather simple. Setting `"noInterop": true` in `.swccrc` caused this error. Hence just omitting it or setting it to `false` fixes the issue. Read more about it here: https://swc.rs/docs/configuration/modules#commonjs

# Reproduction

**Requirements**

- Node.js
- pnpm (`npm install -g pnpm`)
- Bazelisk (`npm install -g @bazel/bazelisk`)

**Setup**

- `pnpm i` (Install Node dependencies)

**Error**

- `bazelisk run //:bin` (Run app)

  ```
  INFO: Build completed successfully, 1 total action
  INFO: Running command line: bazel-bin/bin.sh
  /home/flolu/.cache/bazel/_bazel_flolu/1b8803ef8961710fdd5d7b63a7d56904/execroot/__main__/bazel-out/k8-fastbuild/bin/bin.sh.runfiles/__main__/main.js:10
  console.log((0, _sanitizeHtml().default)(html));
                                          ^

  TypeError: (0 , _sanitizeHtml(...).default) is not a function
      at Object.<anonymous> (/home/flolu/.cache/bazel/_bazel_flolu/1b8803ef8961710fdd5d7b63a7d56904/execroot/__main__/bazel-out/k8-fastbuild/bin/bin.sh.runfiles/__main__/main.js:10:41)
      at Module._compile (node:internal/modules/cjs/loader:1101:14)
      at Object.Module._extensions..js (node:internal/modules/cjs/loader:1153:10)
      at Module.load (node:internal/modules/cjs/loader:981:32)
      at Function.Module._load (node:internal/modules/cjs/loader:822:12)
      at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:79:12)
      at node:internal/main/run_main_module:17:47
  ```
