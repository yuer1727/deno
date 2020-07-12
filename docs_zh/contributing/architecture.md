## 内部细节

### Deno比喻Linux

|                       **Linux** | **Deno**                                     |
| ------------------------------: | :------------------------------------------- |
|                       Processes | Web Workers                                  |
|                        Syscalls | Ops                                          |
|           File descriptors (fd) | [Resource ids (rid)](architecture#resources) |
|                       Scheduler | Tokio                                        |
| Userland: libc++ / glib / boost | https://deno.land/std/                       |
|                 /proc/\$\$/stat | [Deno.metrics()](architecture#metrics)       |
|                       man pages | deno types                                   |

#### 资源

资源又称`rid`，是Deno版的文件描述符。他们被用来引用打开的文件、套接字和其它概念的整型值。它可以查询系统打开了多少资源，对测试非常有用。

```ts
console.log(Deno.resources());
// { 0: "stdin", 1: "stdout", 2: "stderr" }
Deno.close(0);
console.log(Deno.resources());
// { 1: "stdout", 2: "stderr" }
```

#### 指标

指标是Deno的各种统计数据的内部计数器。

```shell
> console.table(Deno.metrics())
┌──────────────────┬────────┐
│     (index)      │ Values │
├──────────────────┼────────┤
│  opsDispatched   │   9    │
│   opsCompleted   │   9    │
│ bytesSentControl │  504   │
│  bytesSentData   │   0    │
│  bytesReceived   │  856   │
└──────────────────┴────────┘
```

### 原理示意图

![architectural schematic](https://deno.land/images/schematic_v0.2.png)
