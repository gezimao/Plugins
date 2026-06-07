# GitHub Pages 托管说明

这个目录已经整理成 GitHub Pages 可直接托管的结构。

## 发布步骤

1. 创建 GitHub 仓库
2. 把当前项目推送到该仓库
3. 打开仓库 `Settings > Pages`
4. 选择 `Deploy from a branch`
5. Branch 选 `main`
6. Folder 选 `/docs`
7. 保存后等待 GitHub Pages 分配站点地址

站点地址通常是：

```text
https://<github-user>.github.io/<repo-name>
```

## 发布前要改的内容

这个仓库对应的 GitHub Pages 基础地址应为：

```text
https://gezimao.github.io/Plugins/docs
```

下面两个文件现在已经按这个地址填好：

- `docs/repo.json`
- `custom-repo/repo.json`

## Dalamud 里填写什么

在 Dalamud 自定义仓库中填写：

```text
https://<github-user>.github.io/<repo-name>/repo.json
```
