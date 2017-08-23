# Install Rust

> 2018-08-23

## 概述

安装 Rust 还是踩了一下坑，觉得有必要记录下

Homebrew 上面也有Rust，但是这么安装的话有两个问题：

1. 没有 rustup， 会对 src 有影响，设置环境变量，然后影响配置 emacs
2. 环境变量不会自动添加


## 正确的打开方式

官网推荐的

```
$ curl https://sh.rustup.rs -sSf | sh

$ rustc --version
$ cargo --version
```
选择默认安装就行了 


## 配置spacemacs的 rust-mode

```cmd
$ cargo install racer
$ rustup component add rust-src

export RUST_SRC_PATH="$(rustc --print sysroot)/lib/rustlib/src/rust/src"

$ cargo install rustfmt
```


## Spacemacs Key bindings


| Key Binding | Description                                 |
|-------------+---------------------------------------------|
| ~SPC m =~   | reformat the buffer                         |
| ~SPC m c .~ | repeat the last Cargo command               |
| ~SPC m c C~ | remove build artifacts with Cargo           |
| ~SPC m c X~ | execute a project example with Cargo        |
| ~SPC m c c~ | compile project with Cargo                  |
| ~SPC m c d~ | generate documentation with Cargo           |
| ~SPC m c e~ | run benchmarks with Cargo                   |
| ~SPC m c f~ | run the current test with Cargo             |
| ~SPC m c i~ | create a new project with Cargo (init)      |
| ~SPC m c n~ | create a new project with Cargo (new)       |
| ~SPC m c o~ | run all tests in current file with Cargo    |
| ~SPC m c s~ | search for packages on crates.io with Cargo |
| ~SPC m c u~ | update dependencies with Cargo              |
| ~SPC m c x~ | execute a project with Cargo                |
| ~SPC m g g~ | jump to definition                          |
| ~SPC m h h~ | describe symbol at point                    |
| ~SPC m t~   | run tests with Cargo                        |


