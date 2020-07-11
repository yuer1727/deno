# 贡献

- 阅读[风格指南](./docs_zh/contributing/style_guide.md)。

- 请不要使[benchmarks](https://deno.land/benchmarks.html)变得更差。

- 请在[社区聊天室](https://discord.gg/deno)提问。

- 如果你打算解决一个问题， 请在开始解决 _之前_ 在issue评论中提及。

- 请在论坛中表现您的专业性。我们跟随
  [Rust's code of conduct](https://www.rust-lang.org/policies/code-of-conduct)
  (CoC) 如有问题请发送Email到 ry@tinyclouds.org.

## 开发

关于如何从源代码构建的介结在[这里](./contributing/building_from_source.md).

## 提交一个 Pull Request

在提交之前， 请确保以下事项已完成：

1. 存在一个相关问题，在PR文本中进行了引用。
2. 有一些测试用例可以涵盖这些更改。
3. 确保 `cargo test` 通过。
4. 使用 `./tools/format.py` 格式化代码。
5. 确保 `./tools/lint.py` 通过。

## `third_party` 的修改

[`deno_third_party`](https://github.com/denoland/deno_third_party) 包含大多数
Deno依赖的外部代码，以便在任何时候都能确切地知道使用了哪些第三方库。我们通过体力劳动和私有脚本来维护第三方库。您可能需要 @ry 或者 @piscisaureus 进行更改。


## 添加操作(aka bindings)

我们非常担心在添加新的API时会犯错。当添加一个接口到Deno，应该研究其他平台上的对应接口。请列出如何在Go，Node，Rust和Python中完成此功能。

举个例子, 看看 `Deno.rename()` 如何从被提出到被添加成功
[PR #671](https://github.com/denoland/deno/pull/671)。

## 发布

之前的发布版本的汇总表在[这里](https://github.com/denoland/deno/releases)。

## API文档

记录公共API很重要，我们希望文档与代码内联。这有助于确保代码和文档紧密结合在一起。

### 利用JSDoc

所有的公开暴露的API和类型，无论通过deno模块暴露还
通过全局`window`名称空间暴露，都应该有JSDoc文档。该文档是可以解析的 并且 TypeScript编译器可读，以便提供
给更下游。 JSDoc块位于它们要应用的语句之前，
并以 `/**` 开头，然后以 `*/` 终止。例如：

```ts
/** A simple JSDoc comment */
export const FOO = "foo";
```

在 https://jsdoc.app/ 查阅更多资料。
