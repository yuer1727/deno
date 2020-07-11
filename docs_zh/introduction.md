# 介绍

Deno是一个JavaScript/TypeScript带有默认安全和伟大的开发者经验的运行时。

Deno被构建在V8, Rust和Tokio之上。

## 功能亮点

- 默认安全。不涉及文件系统、网络或者环境变量的访问(除非显式开启)。
- 开箱即用地支持TypeScript。
- 提供单独的可执行文件(`deno`)。
- 拥有许多内建工具，例如一个依赖检查器 (`deno info`) 和一个代码格式化工具 (`deno fmt`)。
- 拥有[一系列被审核过的标准模块](https://github.com/denoland/deno/tree/master/std)与Deno一起工作。 
- 脚本可以被捆绑到一个JavaScript文件。

## Deno哲学

Deno aims to be a productive and secure scripting environment for the modern
programmer.

Deno will always be distributed as a single executable. Given a URL to a Deno
program, it is runnable with nothing more than
[the ~15 megabyte zipped executable](https://github.com/denoland/deno/releases).
Deno explicitly takes on the role of both runtime and package manager. It uses a
standard browser-compatible protocol for loading modules: URLs.

Among other things, Deno is a great replacement for utility scripts that may
have been historically written with bash or python.

## 目标

- Only ship a single executable (`deno`).
- Provide Secure Defaults
  - Unless specifically allowed, scripts can't access files, the environment, or
    the network.
- Browser compatible: The subset of Deno programs which are written completely
  in JavaScript and do not use the global `Deno` namespace (or feature test for
  it), ought to also be able to be run in a modern web browser without change.
- Provide built-in tooling like unit testing, code formatting, and linting to
  improve developer experience.
- Does not leak V8 concepts into user land.
- Be able to serve HTTP efficiently

## 与Node.js对比

- Deno does not use `npm`
  - It uses modules referenced as URLs or file paths
- Deno does not use `package.json` in its module resolution algorithm.
- All async actions in Deno return a promise. Thus Deno provides different APIs
  than Node.
- Deno requires explicit permissions for file, network, and environment access.
- Deno always dies on uncaught errors.
- Uses "ES Modules" and does not support `require()`. Third party modules are
  imported via URLs:

  ```javascript
  import * as log from "https://deno.land/std/log/mod.ts";
  ```

## 其他关键的表现

- Remote code is fetched and cached on first execution, and never updated until
  the code is run with the `--reload` flag. (So, this will still work on an
  airplane.)
- Modules/files loaded from remote URLs are intended to be immutable and
  cacheable.
