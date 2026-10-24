# hongguoTV 更新仓库文件

将本目录中的以下两个文件上传到  
`https://github.com/tackeyxy/hongguoTV_Updater` 的 `main` 分支根目录：

- `version.json`
- `hongguoTV.apk`

APP 每次启动会读取：

```text
https://raw.githubusercontent.com/tackeyxy/hongguoTV_Updater/main/version.json
```

失败时自动尝试 `master` 分支以及 `https://v4.gh-proxy.org/` 代理。

## version.json 格式

```json
{
  "versionCode": 2,
  "versionName": "0.2.0",
  "apkUrl": "https://v4.gh-proxy.org/https://github.com/tackeyxy/hongguoTV_Updater/raw/main/hongguoTV.apk",
  "changelog": "更新说明"
}
```

- `versionCode` 必须大于当前安装包的 versionCode，APP 才会提示更新。
- `apkUrl` 可以已经带 `https://v4.gh-proxy.org/` 前缀；如果没带，APP 会自动添加，不会重复添加。
- 新版本弹窗不可取消，只能更新或退出应用，满足强制更新要求。

## 发布新版本

1. 修改 `app/build.gradle.kts` 中的 `versionCode` 和 `versionName`。
2. 执行 `.\gradlew.bat :app:assembleDebug`。
3. 将新的 `app-debug.apk` 覆盖复制为本目录的 `hongguoTV.apk`。
4. 修改 `version.json` 的 `versionCode`、`versionName`、`changelog`。
5. 把 `hongguoTV.apk` 和 `version.json` 推送到更新仓库的 `main` 分支。
