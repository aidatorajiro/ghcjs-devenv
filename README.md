# GHCJS development environment

This docker image is a boilerplate for GHCJS develop environment. It has GHCUp with normal GHC and experimental GHCJS 9.x, necessary libraries and GIR files for `jsaddle-webkit2gtk`, X11 forwarding preset (for testing webkit2gtk), and neovim with coc-nvim (with haskell-language-server support).

## How to setup

Before setup, you need a workspace folder (different from this repository) and put `examples/docker-compose.yml` onto it. Then, run following commands:

1. `mkdir .stack-cache`
1. `mkdir .cabal-cache`
1. `mkdir -p .stack-cache/hooks/`
1. `curl https://raw.githubusercontent.com/haskell/ghcup-hs/master/scripts/hooks/stack/ghc-install.sh > .stack-cache/hooks/ghc-install.sh`
1. `chmod +x .stack-cache/hooks/ghc-install.sh`
1. `echo "system-ghc: false" >> .stack-cache/config.yaml`
1. `docker-compose up`

## How to build a project

Just run `stack build` (for GHC binary) or `cabal build` (for GHCJS binary) within your project.

For cabal with GHCJS, replacement of compiler and other tools is required. To do so, append 

```
with-compiler: javascript-unknown-ghcjs-ghc-9.10.0.20240413
with-hc-pkg: javascript-unknown-ghcjs-ghc-pkg-9.10.0.20240413
```

to the `cabal.project` file and run

```
cabal build --with-hsc2hs=javascript-unknown-ghcjs-hsc2hs-9.10.0.20240413
```

whenever you build.