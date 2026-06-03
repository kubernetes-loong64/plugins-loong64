# plugins for LoongArch64

<p align="center"><a href="README.md">English</a> | <a href="README-zh.md">中文</a></p>

<p align="center"><img src="https://img.shields.io/badge/plugins%20LoongArch64%20%E9%BE%99%E8%8A%AF%E6%9E%B6%E6%9E%84%E5%8F%91%E8%A1%8C%E7%89%88-blue?logo=kubernetes&logoColor=white" alt="plugins LoongArch64 龙芯架构发行版"></p>

Build [plugins](https://github.com/containernetworking/plugins) binaries for the **LoongArch64 (loong64)**
architecture via CI/CD.

## How it works

A GitHub Actions workflow clones the specified plugins version, cross-compiles with
`GOOS=linux GOARCH=loong64`, and uploads the built binaries as workflow artifacts. Target platform: `linux/loong64`.

## Branch naming

Push a branch named `loong64-<plugins-version>` (e.g. `loong64-v1.9.1`) to trigger a build. Append `+<build>`
(e.g. `loong64-v1.9.1+0`) to include build metadata.

## [Release](https://github.com/kubernetes-loong64/plugins-loong64/releases)

Push a tag matching `release-loong64-<plugins-version>` (e.g. `release-loong64-v1.9.1+0`) to publish
a GitHub Release with the built binaries.

The `+<build>` suffix provides build metadata (e.g. `+0`, `+1-alpha.1`).

The suffix in the build metadata indicates the release stage:

| Suffix  | Stage         |
|---------|---------------|
| `alpha` | Internal beta |
| `beta`  | Public beta   |
| `rc`    | Pre-release   |
| (none)  | Stable        |

## Release artifacts

Each release includes the following files:

| File          | Description                  |
|---------------|------------------------------|
| `bridge`      | CNI bridge plugin            |
| `host-device` | CNI host-device plugin       |
| `host-local`  | CNI host-local IPAM plugin   |
| `ipvlan`      | CNI ipvlan plugin            |
| `loopback`    | CNI loopback plugin          |
| `macvlan`     | CNI macvlan plugin           |
| `portmap`     | CNI portmap plugin           |
| `ptp`         | CNI ptp plugin               |
| `static`      | CNI static IPAM plugin       |
| `vlan`        | CNI vlan plugin              |

Each file has a corresponding `.asc` detached GPG signature.

## Verify releases

- Releases are signed with GPG.
- Download the public key from [keys.openpgp.org](https://keys.openpgp.org).
- [FCF8724722CCBF9F51B1FBE376532BE7E3013105](https://keys.openpgp.org/debug?q=FCF8724722CCBF9F51B1FBE376532BE7E3013105)

```shell
gpg --keyserver keys.openpgp.org --recv-keys FCF8724722CCBF9F51B1FBE376532BE7E3013105
echo "FCF8724722CCBF9F51B1FBE376532BE7E3013105:6:" | gpg --import-ownertrust
```

Each release artifact has a corresponding `.asc` detached signature. To verify, download both the file and its `.asc`
signature from the release, then:

```shell
gpg --verify <file>.asc <file>
```

## License

[Apache License 2.0](LICENSE)
