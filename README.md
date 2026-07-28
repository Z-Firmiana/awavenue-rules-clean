# AWAvenue Rules (Cleaned)

自动从 [TG-Twilight/AWAvenue-Ads-Rule](https://github.com/TG-Twilight/AWAvenue-Ads-Rule) 同步并清洗的拦截规则，提供 hosts 与 AdGuard 两种格式。

## 订阅地址

把 `<USER>` / `<REPO>` 换成你的 GitHub 用户名和仓库名。

- **hosts 格式**（系统级，Windows / macOS / Linux）：
  ```
  https://raw.githubusercontent.com/<USER>/<REPO>/main/hosts.txt
  ```
- **AdGuard 格式**（AdGuard Android / Windows / 浏览器扩展）：
  ```
  https://raw.githubusercontent.com/<USER>/<REPO>/main/adguard.txt
  ```

## 清洗规则

| 项目 | hosts 版本 | AdGuard 版本 |
|------|-----------|--------------|
| 头部注释符 `!` | 替换为 `#`（hosts 唯一合法注释符） | 删除 |
| localhost 条目 | **保留**（原样不动） | 无 |
| 空行 | **保留**（原样不动） | 删除 |
| 行尾空白 | 不处理 | 去除 |
| 规则本体 | 原样保留 | 原样保留 |
| 文件编码 | UTF-8 无 BOM，LF 换行 | UTF-8 无 BOM，LF 换行 |

设计原则：hosts 版本只做注释符转换，**完整保留上游所有信息**；AdGuard 版本清除全部注释和空行，只留纯规则。

## 更新频率

每天北京时间 10:00 自动同步，也可在 Actions 页面手动触发。

## 使用方法

### Windows hosts

1. 以管理员身份打开记事本
2. 打开 `C:\Windows\System32\drivers\etc\hosts`
3. 将 `hosts.txt` 内容追加到末尾
4. 保存后执行 `ipconfig /flushdns`

### macOS / Linux hosts

```bash
sudo sh -c 'curl -fsSL https://raw.githubusercontent.com/<USER>/<REPO>/main/hosts.txt >> /etc/hosts'
sudo dscacheutil -flushcache 2>/dev/null || sudo systemctl restart systemd-resolved
```

### AdGuard

在 AdGuard 的过滤器 → 添加订阅，填入对应格式的订阅地址即可。
