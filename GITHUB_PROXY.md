# GitHub 代理配置

Scoop 现在支持通过代理下载 GitHub 资源，这对于网络访问受限的用户非常有用。

## 启用 GitHub 代理

要启用 GitHub 代理，请运行以下命令：

```powershell
# 启用 GitHub 代理
scoop config github_proxy_enabled true

# 设置代理 URL（可选，默认为 https://gh-proxy.org/）
scoop config github_proxy_url "https://gh-proxy.org/"
```

## 使用自定义代理

您也可以使用其他的 GitHub 代理服务：

```powershell
# 设置自定义代理 URL
scoop config github_proxy_url "https://ghproxy.com/"
scoop config github_proxy_enabled true
```

## 禁用 GitHub 代理

如果要禁用代理功能：

```powershell
scoop config github_proxy_enabled false
```

## 支持的 GitHub 链接类型

此代理功能适用于所有从 GitHub 下载的资源，包括：
- GitHub Releases 下载链接
- GitHub 存档文件 (archive/master.zip 等)
- 其他直接从 GitHub 获取的资源

当启用此功能后，类似 `https://github.com/user/repo/archive/master.zip` 的链接会被自动转换为 `https://gh-proxy.org/https://github.com/user/repo/archive/master.zip`。