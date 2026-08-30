# BetterHeybox

![BetterHeybox](https://socialify.git.ci/Mrmiaomrzh/BetterHeybox/image?font=Source+Code+Pro&forks=1&issues=1&language=1&name=1&pattern=Floating+Cogs&pulls=1&stargazers=1&theme=Auto)

增强小黑盒（Heybox）的 LSPosed 模块。
> [!CAUTION]
> **免责声明**
> - 本应用与清枫(北京)科技有限公司**无任何关联**，亦未经其授权或认可  
> - 本项目仅用于**学习与研究**小黑盒 APP 的部分技术原理，**严禁**用于任何商业或非法用途  
> - 请在下载后 **24 小时内**删除本应用及相关文件  
> - **禁止**在 **小黑盒 / HeyBox** 平台内发布、讨论或传播本模块的内容，违者后果自负  

## Note
本应用基于 [小黑盒 1.3.393](https://github.com/Mrmiaomrzh/BetterHeybox/releases/download/v0.2.0/heybox_1.3.393.apk) 完成，低于此版本出现的问题不会进行处理

## 主仓库
完整源码、技术栈、工程结构、构建与使用说明见主仓库：
**[Mrmiaomrzh/BetterHeybox](https://github.com/Mrmiaomrzh/BetterHeybox)**

## 功能

所有功能开关均可在小黑盒「我的 → 设置 → 通用设置」中的 `BetterHeybox 设置` 入口直接打开模块面板，

### 广告过滤

| 类型 |
|------|
| 屏蔽开屏广告 |
| 屏蔽信息流广告 |
| 屏蔽气泡广告 |
| 屏蔽角标广告 |
| 屏蔽推广贴 |

### 界面增强

- **底部导航栏优化**（需重启小黑盒生效）：隐藏底栏tab项

### 帖子增强

- **解除复制**：Hook 小黑盒自定义 `TextSelectHandler` 的长按拦截，
  恢复安卓系统标准文本选择
- **拖动跨行选择修复**：文本选择激活时放行滚动容器的触摸拦截，选择手柄可跨行拖动
- **图片系统分享**：图片查看器中长按图片，在原有分享面板追加「系统分享」动作，
  下载当前图片后**优先保存到系统相册**（可被相册真正查看、可被任意 App 分享），
  自动识别 jpg/png/gif/webp/bmp 真实格式并修正 MIME；可通过「系统分享图片」开关关闭
- **净化分享链接**：复制链接 / 分享到 QQ、微信等渠道时，自动去掉小黑盒链接上的
  h_camp、h_session_id、h_src、new_post_share_style 等追踪参数
  （如 `...web/share?h_camp=link&h_session_id=xxx&link_id=abc&new_post_share_style=true`
  净化为 `...web/share?link_id=abc`；仅处理小黑盒域名，保留 link_id / id / hkey
  等功能参数，链接照常打开）；默认开启，可通过「净化分享链接」开关关闭，
  去除内容会记录到模块日志

### 视频下载

- **下载入口**：视频帖右上角圆形 Monet 渐变悬浮按钮
- **底部下载面板**：
  - 准备：标题 / 来源 / 预计大小 → 「开始下载」
  - 下载中：实时百分比、已下载/总大小、当前速度 → 「暂停下载」「取消下载」
  - 暂停：「继续下载」
  - 完成：保存路径 → 「播放」「分享」「完成」
  - 失败：错误原因 → 「重新下载」
- **后台下载**：面板可随时关闭，下载继续进行；悬浮按钮进度环持续反馈
- **全类型视频**：正文 / 信息流 / 故事 / 游戏卡片均可；mp4 直链与 HLS（m3u8）分片流均支持
- **断点续传**  
- **自动转封装 MP4**：HLS 合并后自动无损转封装为 MP4
- **智能命名**：文件名优先使用**帖子标题**，HLS 通用名（segs/index）自动回退时间戳；
  重名自动加 `(n)` 后缀，绝不覆盖
- **保存位置**：默认相册 `Movies/BetterHeybox`；设置「保存位置」可调起**系统文件选择器**
  选择任意文件夹，完成通知显示实际保存路径
- **通知栏反馈**：进度（含暂停/取消）、完成（播放/分享/删除 + 保存路径）、失败（重试/取消）
- **系统分享**：完成后一键分享视频文件  

### 每日任务

- **自动完成每日分享任务**：自动完成小黑盒每日任务的 **3 种分享任务**
  - 任务一：**分享任意帖子**（配置帖子链接）
  - 任务二：**分享游戏详情**（配置游戏详情链接）
  - 任务三：**分享游戏评价**（配置游戏评价链接）
- **3 个独立链接设置**：帖子链接 / 游戏详情链接 / 游戏评价链接，各自独立配置；
  未配置的任务自动跳过；每日状态按日期记录，跨天重置
- **分享渠道可配置**：内嵌面板/独立设置页「分享渠道」可选 **QQ / QQ空间**、**微信 / 朋友圈** 或 **微博**，
  自动分享按所选渠道在分享面板点击对应按钮并伪造成功回调（默认 QQ；抖音因无分享成功回调暂不支持）
- **清除今日打卡**：打卡失败或想重新执行时，点击「清除今日打卡」清除今日已完成状态并立即重新尝试

#### 链接格式（3 个分享链接均支持以下任意一种）

| 类型 | 示例 |
|------|------|
| 分享链接（带 link_id） | `https://api.xiaoheihe.cn/v3/bbs/app/api/web/share?link_id=123456` |
| 网页链接（xiaoheihe.cn） | `https://xiaoheihe.cn/a/123456` |
| 深链协议（heybox://） | `heybox://v3/bbs/app/api/web/share?link_id=123456` |

> 链接经小黑盒 RouterActivity 自动路由到对应帖子/游戏页；未配置的类型自动跳过。  
> **获取方式**：在小黑盒 App 打开目标帖子 → 分享 → 复制链接，取分享链接或网页链接均可；
> 游戏/频道页同理复制分享链接  

### 通用

- **版本前置检测**：检测小黑盒版本是否为受支持版本 `1.3.393` / `1.3.394`，不匹配时显示提示
- **伪装通知权限**：让小黑盒认为通知权限已开启，获得**签到加成**  
- **屏蔽更新**：提供可选开关，屏蔽小黑盒更新   
- **记录日志**：提供「记录日志」开关，开启后自动把模块运行日志写入文件

### 更新兼容（DexKit 自动分析）

小黑盒更新常会打乱混淆名，模块通过 [DexKit](https://github.com/LuckyPray/DexKit) 字节码特征分析
自动重新定位，不必等模块发版适配：

- **原生弹窗自动定位**：以 HeyBoxDialog 内的品牌常量字符串为锚点定位对话框类；
  Builder 的标题/正文、View 槽位、正向/负向按钮等同签名混淆方法，用 alpha=0 的
  「隐形探针」按实际渲染位置自动分类；
  分享渠道 / 链接编辑 / 导入确认 / 保存位置等弹窗全部走该通道，解析失败自动回退系统弹窗
- **设置页启发式定位**：binding 字段按 ViewBinding 接口形态判定

## 致谢
- [LSPosed](https://github.com/LSPosed/LSPosed)
- [Libxposed api](https://github.com/libxposed/api) — Apache-2.0，现代 Xposed 模块 API
- [Dexkit](https://github.com/LuckyPray/DexKit) — Apache-2.0，字节码特征分析

### 部分功能灵感来源
- [假装开启小黑盒通知权限](https://github.com/Xposed-Modules-Repo/com.chrxw.justenablednotification)
- [SoulFrog](https://github.com/xmnh/SoulFrog)
