# plugins for LoongArch64

<p align="center"><a href="README.md">English</a> | <a href="README-zh.md">中文</a></p>

<p align="center"><img src="https://img.shields.io/badge/plugins%20LoongArch64%20%E9%BE%99%E8%8A%AF%E6%9E%B6%E6%9E%84%E5%8F%91%E8%A1%8C%E7%89%88-blue?logo=kubernetes&logoColor=white" alt="plugins LoongArch64 龙芯架构发行版"></p>

通过 CI/CD 构建 [plugins](https://github.com/containernetworking/plugins) 的 **LoongArch64 (loong64)**
架构二进制文件。

## 工作原理

GitHub Actions 工作流克隆指定的 plugins 版本，使用 `GOOS=linux GOARCH=loong64` 交叉编译，并将构建产物上传为工作流
artifact。目标平台：`linux/loong64`。

## 分支命名

推送 `loong64-<plugins 版本>` 格式的分支（如 `loong64-v1.9.1`）即可触发构建。可追加 `+<build>`
（如 `loong64-v1.9.1+0`）携带构建元数据。

## [发布](https://github.com/kubernetes-loong64/plugins-loong64/releases)

推送 `release-loong64-<plugins 版本>` 格式的标签（如 `release-loong64-v1.9.1+0`）即可自动创建 GitHub
Release 并上传构建产物。

`+<build>` 后缀提供构建元数据（如 `+0`、`+1-alpha.1`）。

后缀表示发布阶段：

| 后缀      | 阶段   |
|---------|------|
| `alpha` | 内测版  |
| `beta`  | 公测版  |
| `rc`    | 预发布版 |
| （无后缀）   | 正式版  |

## 发布产物

每个发布包含以下文件：

| 文件            | 描述                    |
|---------------|-----------------------|
| `bridge`      | CNI bridge 插件         |
| `host-device` | CNI host-device 插件    |
| `host-local`  | CNI host-local IPAM 插件 |
| `ipvlan`      | CNI ipvlan 插件         |
| `loopback`    | CNI loopback 插件        |
| `macvlan`     | CNI macvlan 插件         |
| `portmap`     | CNI portmap 插件         |
| `ptp`         | CNI ptp 插件             |
| `static`      | CNI static IPAM 插件     |
| `vlan`        | CNI vlan 插件            |

每个文件都有对应的 `.asc` 分离 GPG 签名。

## 验证发布

- 发布文件使用 GPG 签名。
- 从 [keys.openpgp.org](https://keys.openpgp.org) 下载公钥。
- [FCF8724722CCBF9F51B1FBE376532BE7E3013105](https://keys.openpgp.org/debug?q=FCF8724722CCBF9F51B1FBE376532BE7E3013105)

```shell
gpg --keyserver keys.openpgp.org --recv-keys FCF8724722CCBF9F51B1FBE376532BE7E3013105
echo "FCF8724722CCBF9F51B1FBE376532BE7E3013105:6:" | gpg --import-ownertrust
```

每个发布产物都有对应的 `.asc` 分离签名。验证时，从发布页面下载文件和对应的 `.asc` 签名文件，然后：

```shell
gpg --verify <文件>.asc <文件>
```

## 许可证

[Apache License 2.0](LICENSE)
