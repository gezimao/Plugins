# Dalamud 自定义仓库发布说明

这个目录就是一份可直接托管到公网静态站点的仓库骨架。

## 目录结构

```text
custom-repo/
  repo.json
  store-entry.template.json
  plugins/
    Dalamud.LoadingImage/
      latest.zip
      icon.png
    DisPlacePlugin/
      latest.zip
      icon.png
```

## 你需要做的事

1. 把 `custom-repo` 整个目录上传到一个公网可访问的静态地址。
2. 把 `repo.json` 里的 `__BASE_URL__` 全部替换成你的真实基础地址。
3. 在 Dalamud 的自定义仓库里填写：

```text
https://你的地址/repo.json
```

例如，如果你最终托管地址是：

```text
https://example.com/dalamud
```

那么：

- 仓库地址应填写为 `https://example.com/dalamud/repo.json`
- 插件下载地址应为 `https://example.com/dalamud/plugins/Dalamud.LoadingImage/latest.zip`

## 新增一个插件时要填写什么

你可以复制 `store-entry.template.json` 里的对象，并补这些字段：

- `Author`: 插件作者
- `Name`: 插件显示名
- `InternalName`: 插件内部名，必须唯一，通常与程序集/项目名一致
- `AssemblyVersion`: 插件版本号，更新版本时要递增
- `Description`: 详细描述
- `Punchline`: 简短描述
- `RepoUrl`: 源码仓库地址
- `ApplicableVersion`: 通常填 `any`
- `DalamudApiLevel`: 例如 `15`
- `IsHide`: 是否隐藏，通常 `false`
- `IsTestingExclusive`: 是否仅测试源显示，通常 `false`
- `IconUrl`: 可选，插件图标直链
- `ImageUrls`: 可选，插件截图直链数组
- `DownloadLinkInstall`: 安装直链
- `DownloadLinkUpdate`: 更新直链，通常和安装直链相同
- `LastUpdate`: Unix 时间戳字符串

## 插件产物放哪里

建议每个插件都放到：

```text
plugins/<InternalName>/latest.zip
```

例如当前插件：

```text
plugins/Dalamud.LoadingImage/latest.zip
```

当前仓库也已经包含：

```text
plugins/DisPlacePlugin/latest.zip
```

如果要额外托管图标或截图，也建议放在同一目录：

```text
plugins/<InternalName>/icon.png
plugins/<InternalName>/screenshot-1.png
```

## 更新插件时怎么做

1. 重新构建插件，得到新的 `latest.zip`
2. 覆盖 `plugins/<InternalName>/latest.zip`
3. 修改 `repo.json` 中对应插件的：
   - `AssemblyVersion`
   - `DalamudApiLevel`（如果 API 变了）
   - `LastUpdate`
   - `DownloadLinkUpdate`（如果路径改了）
4. 重新上传 `custom-repo` 目录

## 多插件仓库

`repo.json` 顶层是一个数组。要放多个插件，就继续往数组里追加对象。

## GitHub 托管

这个仓库额外准备了一个 `docs/` 目录，适合直接启用 GitHub Pages。

你只需要：

1. 新建一个 GitHub 仓库
2. 把当前目录内容推上去
3. 在 GitHub 仓库设置里打开 Pages
4. 选择从 `main` 分支的 `/docs` 目录发布
5. 记下最终站点地址，例如：

```text
https://<your-name>.github.io/<repo-name>
```

6. 把 `docs/repo.json` 和 `custom-repo/repo.json` 里的 `__BASE_URL__` 替换为这个地址
7. 再次提交并推送

然后用户在 Dalamud 里填写：

```text
https://<your-name>.github.io/<repo-name>/repo.json
```
