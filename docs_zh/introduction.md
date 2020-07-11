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

Deno的目标是给现代的程序员提供一个高生产力和安全的脚本环境。

Deno作为单个可执行文件分发。[15MB左右的压缩可执行文件](https://github.com/denoland/deno/releases)可以单独运行无需其它依赖。Deno明确承担了运行时和程序包管理器的角色。它使用加载模块的标准浏览器兼容协议：URL。

除此之外，Deno是实用程序脚本的绝佳替代品，
历史上是用bash或python编写的。

## 目标

- 只提供一个单独的可执行文件 (`deno`)。
- 提供默认安全
  - 除非特殊允许，脚本不可以访问文件系统，环境变量或者网络。
- 与浏览器兼容：完全用JavaScript编写且不使用全局Deno名称空间（或对其进行功能测试）的Deno程序的子集，也应该能够在现代Web浏览器中运行而无需更改。
- 提供内置工具，例如单元测试，代码格式化和改善开发人员体验。
- 不会将V8概念暴露到用户领域。
- 可以提供高效的HTTP服务。

## 与Node.js对比

- Deno不再使用`npm`
  - 它使用模块引用，比如:URL或者文件路径。
- Deno不再在它的模块管理解决方案算法里使用`package.json`。
- 在Deno里的所有异步行为返回一个promise。 因此Deno提供了与Node不一样的API。
- Deno需要显式授权文件系统、网络和环境变量的访问权限。
- Deno进程经常崩溃在未捕获的错误。
- 使用"ES Modules"  和不再支持`require()`。第三方模块通过URL导入：
  ```javascript
  import * as log from "https://deno.land/std/log/mod.ts";
  ```

## 其他关键的表现

- 远程代码是在第一次执行时拉取和缓存，且不更新。除非程序启动时指定 `--reload` 标记。(因此在飞行模式时，代码仍然可以执行。)
- Modules/files 从远程URL加载，旨在不可变性、可缓存性。
