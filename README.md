# A Simple Workflow to Setup Agda for GitHub Actions

Example Workflow Config:
`.github/workflows/agda.yaml`
```yaml
name: Build

on:
  push:
  pull_request:

jobs:
  build:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        agda-ref: ["v2.6.2"]
        ghc-ver: ["8.10.7"]
        stdlib-ref: ["v1.7"]

    steps:
    - name: Setup Agda
      uses: fangyi-zhou/setup-agda-action@v0.1.0
      with:
        # Git reference of agda/agda to checkout
        agda-ref: ${{ matrix.agda-ref }}
        # GHC version
        ghc-version: ${{ matrix.ghc-ver }}
        # Git reference of agda/agda-stdlib to checkout (optional)
        stdlib-ref: ${{ matrix.stdlib-ref }}

    - name: Checkout my library
      uses: actions/checkout@v2
      with:
        path: main

    - name: Typecheck my library
      run: |
        cd main
        agda Everything.agda
```
