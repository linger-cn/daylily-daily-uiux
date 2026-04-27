# daylily-daily-uiux

本仓库承载 **Daylily Daily** 相关 UI/UX 原型与协作文档；需求规格通过 Git 子模块挂载在 `req-specs/`。

## 克隆前准备

- 已安装 **Git 2.13+**（建议较新版本，子模块体验更好）。
- 若使用 SSH 克隆（本组织常用 `git@lingr.github.com:...`），请确保：
  - 本机 SSH 密钥已加入对应代码托管账户；
  - `~/.ssh/config` 中已配置可解析 `lingr.github.com` 的 `Host`（由团队统一提供或按内部文档配置）。
- 子模块仓库同样需要你有 **读权限**；若仅克隆主仓库而不初始化子模块，则不会访问子模块远程。

以下命令中的 `<REPO_URL>` 请替换为你在用的主仓库地址，例如：

```bash
git@lingr.github.com:linger-cn/daylily-daily-uiux.git
```

若你使用 HTTPS，请将示例中的 SSH URL 换成团队提供的 HTTPS 地址。

---

## 场景一：首次完整克隆（推荐，一次拿到主仓库 + 子模块）

适用于日常开发、需要同时查看原型与需求规格。

```bash
git clone --recurse-submodules <REPO_URL>
cd daylily-daily-uiux
```

说明：

- `--recurse-submodules` 会在克隆主仓库后自动初始化并拉取 `req-specs`。
- 若子模块较多或网络不稳定，可加 `--progress` 观察进度。

验证：

```bash
git submodule status
# req-specs 行前应为空格（已检出），不应长时间为减号“-”
ls req-specs
```

---

## 场景二：已经 `git clone` 了主仓库，但忘了带子模块

适用于先执行了普通 `clone`，发现 `req-specs` 为空或只有占位。

```bash
cd daylily-daily-uiux
git submodule update --init --recursive
```

若只想初始化子模块、不递归更深子模块（当前通常足够）：

```bash
git submodule update --init
```

---

## 场景三：浅克隆主仓库，再按需拉子模块

适用于 CI 或只想先占磁盘、后补历史。

```bash
git clone --depth 1 <REPO_URL>
cd daylily-daily-uiux
git submodule update --init --recursive
```

注意：浅克隆后若要对子模块做深度开发或需要完整历史，可能需要在子模块目录内另行 `git fetch --unshallow`（按需）。

---

## 场景四：只需要主仓库，不需要 `req-specs`

适用于只做原型 HTML/CSS、不读需求仓库的成员。

```bash
git clone <REPO_URL>
cd daylily-daily-uiux
# 不要执行 submodule update；保持 req-specs 未检出即可
```

说明：主仓库仍会记录子模块应指向的提交；本地未初始化时 `req-specs` 可能为空目录或不存在（取决于 Git 版本与克隆方式）。若 Git 提示子模块未检出，可忽略，除非你确实需要该目录内容。

---

## 场景五：子模块克隆失败（权限、主机名、换协议）

常见原因与处理：

1. **SSH 权限被拒绝**  
   检查密钥、账户权限，以及 `ssh -T git@lingr.github.com`（或团队文档中的测试命令）是否通过。

2. **需要改用 HTTPS 拉子模块**  
   在克隆主仓库后，可覆盖子模块 URL 再初始化（示例，URL 以团队实际为准）：

   ```bash
   cd daylily-daily-uiux
   git config submodule.req-specs.url https://example.com/linger-cn/daylily-daily-req-specs.git
   git submodule sync --recursive
   git submodule update --init --recursive
   ```

3. **公司代理 / 防火墙**  
   按网络规范配置 `git config --global http.proxy` 或使用内部镜像地址（由基础设施团队提供）。

---

## 场景六：拉取主仓库更新时，一并更新子模块

每次在主分支或功能分支上 `git pull` 后，建议同步子模块到主仓库记录的提交：

```bash
git pull
git submodule update --init --recursive
```

若子模块在远端有独立更新，而主仓库尚未 bump 子模块指针，需要进入子模块目录在**子模块自己的分支策略**下 `git pull`（与产品流程一致时再操作）。

---

## 场景七：CI / 脚本化无交互克隆

在流水线中推荐使用：

```bash
git clone --recurse-submodules <REPO_URL> daylily-daily-uiux
cd daylily-daily-uiux
```

若流水线使用浅克隆：

```bash
git clone --depth 1 --recurse-submodules <REPO_URL> daylily-daily-uiux
```

确保 CI 凭据对主仓库与子模块均有效（同一 SSH 密钥或分别配置的 token）。

---

## 场景八：`req-specs` 目录异常、想强制对齐记录版本

当子模块目录被误删、冲突或本地魔改导致状态混乱时：

```bash
cd daylily-daily-uiux
git submodule deinit -f req-specs
rm -rf .git/modules/req-specs   # 谨慎：会清除该子模块本地 Git 元数据
git submodule update --init --recursive
```

执行前请确认没有仅在子模块内且未备份的本地提交；若有，请先在 `req-specs` 内用分支或 patch 保存。

---

## 仓库内文档索引

| 路径 | 说明 |
|------|------|
| [MONOREPO_STRUCTURE.md](./MONOREPO_STRUCTURE.md) | 本仓库 Monorepo 规范（中文） |
| [AGENTS.md](./AGENTS.md) | 原型目录与协作约束 |
| `prototypes/` | 各产品线页面原型 |
| `req-specs/` | 需求规格子模块（独立仓库） |
| `docs/superpowers/` | 设计说明与实施计划等 |

---

## 贡献与分支约定

本仓库协作流程要求 **不在 `main` 上直接提交**；请从 `main` 拉出功能分支修改后通过 Pull Request 合并。具体步骤见团队 Git 工作流说明。
