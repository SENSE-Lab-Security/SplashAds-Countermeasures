# 🛡️ 开屏广告应对措施

<kbd>中文</kbd> <a href="README.md"><kbd>English</kbd></a>

**开屏广告、摇一摇跳转、自动拉起淘宝/京东……现在有哪些办法可以处理？**

这个项目整理目前公开可查的 **手机广告防御方案（Advertising Defenses）**。无论你遇到的是开屏广告、摇一摇跳转，还是广告自动拉起其他 App，都可以先从自己的问题出发，了解目前有哪些应对方式。

你可以把它当成一份 **手机广告防御方案导航**：先看自己遇到的是什么问题，再了解有哪些可用方案、使用门槛以及各自的局限。

> [!NOTE]
> 本项目只整理和核对公开信息，不代表对任何方案的安全性、效果或兼容性作保证。涉及无障碍、VPN/DNS、Root、LSPosed/Xposed、重签名等能力时，请只使用可信来源，并了解相应权限和风险。
>
> 最近一次集中核验：**2026-09-13**

## 🚀 我该从哪里开始？

| 你遇到的问题 | 可以先看 |
| --- | --- |
| ⏭️ 打开 App 总要等几秒开屏广告 | [自动跳过开屏广告](#auto-skip-splash-ads) |
| 📳 手机稍微一晃就跳淘宝、京东或其他 App | [防“摇一摇 / 扭一扭”跳转](#-防摇一摇--扭一扭跳转) |
| 🚫 希望阻断广告请求，或修改已知广告响应/资源 | [阻断或修改广告资源](#ad-resources) |
| 🔗 广告可以显示，但不想让它自动拉起其他 App | [阻止广告触发的跳转](#ad-navigation) |
| ↩️ 已经跳到其他 App，希望能自动返回 | [跳转后自动返回](#post-navigation-recovery) |
| 🧩 只想去掉某一个 App 里的广告 | [针对特定 App 的工具](#-针对特定-app-的工具) |
| 🍎 我用 iPhone / iPad | [iOS 方案](#-ios-上有哪些办法) |
| 🧑‍💻 我有 Root / LSPosed，愿意折腾 | [高级用户工具](#advanced-user-tools) |
| 📚 我想看全部条目和完整限制信息 | [完整目录](CATALOG.zh-CN.md) |

## 📱 先看看手机系统自己能不能解决

在安装第三方工具之前，**先检查系统有没有现成的权限或跳转控制**。这通常是成本最低的一种方式。

- **华为设备**：部分系统版本可以限制应用获取设备方向，从而减少利用运动传感器触发的广告跳转。见 [Huawei: device orientation permission](entries/151.zh-CN.md)。
- **vivo / iQOO**：部分版本提供运动与方向访问控制，部分固件支持仅在开屏阶段限制。见 [vivo / iQOO: motion and orientation control](entries/149.zh-CN.md)。
- **HONOR**：部分机型/版本提供传感器权限或自动跳转提醒。见 [HONOR: automatic app navigation reminder](entries/153.zh-CN.md) 和 [HONOR: device sensor permission](entries/154.zh-CN.md)。
- **OnePlus**：部分版本提供应用启动阶段的运动权限控制。见 [OnePlus: startup motion permission](entries/166.zh-CN.md)。

不同品牌、机型和系统版本的入口并不完全一致。如果你的系统已经提供类似功能，通常值得优先尝试。

<a id="auto-skip-splash-ads"></a>

## ⏭️ 自动跳过开屏广告

**适合这种情况：** 打开 App 后会先出现几秒广告，页面上通常有“跳过 / 关闭”按钮。

这类方案一般不会阻止广告本身加载，而是 **帮你自动找到并点击“跳过”**。对不想 Root、只想少点几次按钮的 Android 用户来说，这是最容易理解的一类。

| 工具 | 简单理解 | 平台 | 上手难度 |
| --- | --- | --- | --- |
| [李跳跳](entries/005.zh-CN.md) | 通过无障碍服务按规则自动点击“跳过 / 关闭” | Android | 🟢 低门槛 |
| [GKD](entries/001.zh-CN.md) | 按订阅规则自动找到并点击“跳过 / 关闭” | Android | 🟡 中等门槛 |
| [SKIP](entries/002.zh-CN.md) | 根据本地规则自动处理启动页广告 | Android | 🟢 低门槛 |
| [ZeroStart](entries/006.zh-CN.md) | UI 不好识别时，还会尝试离线 OCR 等方式找按钮 | Android | 🟢 低门槛 |
| [PureSkip](entries/007.zh-CN.md) | 使用离线规则处理已适配的启动广告 | Android | 🔴 高门槛 |
| [SplashCleaner-Android](entries/008.zh-CN.md) | 只在 App 启动后的短时间内寻找并点击跳过按钮 | Android | 🟢 低门槛 |
| [madeye/ad-skipper](entries/009.zh-CN.md) | 找不到按钮时可进一步用 OCR / YOLO / VLM 辅助定位 | Android | 内置识别 🟢 / 额外 VLM 🟡 |

**要知道的一点：** 这类方案通常解决的是“帮你点掉广告”，并不等于广告没有加载，也不一定能防摇一摇、滑动或自动跳转。

## 📳 防“摇一摇 / 扭一扭”跳转

**适合这种情况：** 广告本身可能还在，但你只是拿起手机、轻微晃动，甚至没有明显点击意图，就被拉到了购物 App 或其他页面。

这类方案通常从两个方向处理：**不让 App 正常获得运动数据**，或者 **直接阻止摇一摇相关逻辑继续执行**。

| 方案 | 简单理解 | 平台 | 上手难度 |
| --- | --- | --- | --- |
| [NoShakingAD / Bu Xu Tiaozhuan](entries/016.zh-CN.md) | 在开屏的一小段时间里临时限制运动传感器 | Android | 🟡 中等门槛 |
| [Fuck Shake](entries/015.zh-CN.md) | 直接阻止目标 App 的摇一摇相关逻辑 | Android | 🔴 高门槛 |
| [QzxyAdBlock](entries/024.zh-CN.md) | 针对特定 App，同时处理广告和摇一摇跳转 | Android | 🔴 高门槛 |

**这些方案不会自动解决所有广告。** 防住摇一摇以后，点击、滑动、大面积触摸等其他触发方式仍可能存在。

<a id="ad-resources"></a>

## 🚫 阻断或修改广告资源

**适合这种情况：** 你希望更早地介入广告流程——在 App 获取可用广告内容之前或过程中进行处理，而不是等广告显示出来以后再点“跳过”。

这类方案作用在 **资源阶段**。有些通过 DNS、hosts 或本地 VPN 阻断已知广告域名/请求；另一些并不阻断请求，而是 **修改返回数据、移除广告字段，或阻止 App 读取缓存中的广告数据**。因此这里不再简单叫“阻止广告加载”。

| 方案 | 简单理解 | 平台 | 部署难度 |
| --- | --- | --- | --- |
| [AdAway](entries/047.zh-CN.md) | 通过 hosts 或本地 VPN 阻断已知广告域名 | Android | 🟢 低门槛（VPN）/ 🔴 高门槛（Root hosts） |
| [Rethink DNS + Firewall](entries/048.zh-CN.md) | 过滤匹配的 DNS 请求，并可配合按应用防火墙 | Android | 🟢 低门槛 |
| [Blokada 6 / Cloud](entries/127.zh-CN.md) | 通过 DNS / 云端服务过滤已知广告域名 | 跨平台 | 🟢 低门槛 |
| [app2smile rules + Surge / Quantumult X](entries/108.zh-CN.md) | 在兼容 iOS 客户端中改写特定广告 API 的返回数据 | iOS | 🟡 中等门槛 |

**局限也很直接：** 是否有效取决于实际资源路径。广告与正常内容共用域名、已经缓存或内置在 App 中、接口发生变化、证书固定（pinning）或响应格式不匹配，都可能让广告继续出现或继续执行。

<a id="ad-navigation"></a>

## 🔗 阻止广告触发的跳转

**适合这种情况：** 你可以接受广告暂时显示，但不希望一次误触就把你拉到淘宝、京东、浏览器或其他 App。

这类方案作用在 **跳转阶段**：它们可能改写目标链接、阻止特定目标页面/应用被打开，或者在跨 App 跳转前增加一次确认。

| 方案 | 简单理解 | 平台 | 部署难度 |
| --- | --- | --- | --- |
| [FuckAdJump](entries/106.zh-CN.md) | 针对部分淘宝 / 京东 Deep Link，让相应跳转失效 | Android | 🔴 高门槛 |
| [HONOR 自动跳转提醒](entries/153.zh-CN.md) | 对识别出的疑似误触广告跳转增加系统提醒 | Android | 🟢 低门槛 |

当跳转经过对应拦截点时，这类防护不必关心上游到底是点击、滑动、摇一摇还是其他触发方式；但覆盖范围仍取决于防护方案究竟能拦住哪些链接和启动路径。

<a id="post-navigation-recovery"></a>

## ↩️ 跳转后自动返回

**适合这种情况：** 跳转已经发生，你希望防护工具尽快把你带回原来的 App，缩短中断时间。

| 方案 | 简单理解 | 平台 | 部署难度 |
| --- | --- | --- | --- |
| [ShakeGuard](entries/018.zh-CN.md) | 在跳转发生后识别匹配的前台 App 切换，并尝试执行 Back / 返回 | Android | 🔴 高门槛 |

这一类需要和“阻止跳转”明确区分：**它介入时目标 App 已经打开了**，因此无法撤销已经显示的页面或已经发出的网络请求，也不能保证恢复到原 App 的精确页面状态。

## 🧩 针对特定 App 的工具

还有一大类工具并不追求“所有 App 通用”，而是专门适配某一个 App 或少数几个 App。

例如：

- [MiFitnessAdAway](entries/026.zh-CN.md)：针对小米运动健康。
- [bili-hook](entries/027.zh-CN.md)：针对特定版本的哔哩哔哩。
- [CoolApkNoSplash](entries/020.zh-CN.md)：针对酷安的已知开屏路径。
- [XTA-AdKiller](entries/025.zh-CN.md)：针对超级课程表中的多类广告接口。
- [GmailHideAds](entries/032.zh-CN.md)：针对 Gmail 收件箱中的 Sponsored 行。
- [Play Store Adblock](entries/029.zh-CN.md)：针对 Google Play 中的 Sponsored / 推广内容。

这类工具通常是针对 **特定 App 和特定版本做的窄范围适配**；这种针对性不等于它们已经在所有支持版本上通过统一实测。App 一更新，原来的适配就可能失效。

## 🍎 iOS 上有哪些办法？

相比 Android，iOS 上可直接修改其他 App 行为的空间更小，因此这里常见的是 **代理 / DNS / Rewrite 规则**，以及系统或浏览器本身提供的限制能力。

你可以先看：

- [app2smile ad network rules + Surge / Quantumult X](entries/108.zh-CN.md)
- [blackmatrix7 startup](entries/125.zh-CN.md)
- [R-Store](entries/136.zh-CN.md)
- [Moyu Rewrite](entries/138.zh-CN.md)
- [iOS browser app launching and link routing](entries/167.zh-CN.md)
- [iOS URL Filter](entries/168.zh-CN.md)

其中一些方案需要配置代理、证书或规则，并不属于“安装后直接生效”的普通 App。

<a id="advanced-user-tools"></a>

## 🧑‍💻 高级用户工具

如果你已经熟悉 **Root / Magisk、LSPosed / Xposed 等运行时注入框架，以及 APK 修改**，可选范围会大很多。这些工具可以深入到 App 内部逻辑、广告 SDK、Activity / Intent 或传感器回调层面。

常见例子包括：

- [Fuck Shake](entries/015.zh-CN.md)
- [AdPopupBlocker](entries/021.zh-CN.md)
- [LiTianSuo](entries/028.zh-CN.md)
- [FuckAdJump](entries/106.zh-CN.md)
- [Adobo advertising patches](entries/119.zh-CN.md)
- [DTL-X rmads](entries/120.zh-CN.md)

但这类方案也意味着更高的维护和安全成本：版本更新、代码混淆、签名校验、Root 检测都可能影响可用性。

## 🏢 广告平台和 App 开发者能做什么？

仓库里还收录了一些 **面向开发者或广告平台侧的防御控制**。它们不是给普通用户直接安装的工具，而是广告 SDK 或平台提供给开发者的配置项。

例如，部分 SDK 允许开发者关闭摇一摇、旋转或其他运动交互：

- [GroMore Android](entries/141.zh-CN.md)
- [Sigmob Android](entries/143.zh-CN.md)
- [Sigmob iOS](entries/145.zh-CN.md)
- [Taku Android](entries/146.zh-CN.md)
- [Taku iOS](entries/147.zh-CN.md)
- [Tencent GDT Android](entries/150.zh-CN.md)
- [Kuaishou iOS](entries/152.zh-CN.md)

这些条目对普通用户的意义不是“去下载它”，而是帮助理解：**很多广告交互本身就是可以被开发者配置或关闭的。**

## 🧭 部署难度（Deployment Effort）

- **🟢 低门槛（Low）**：安装并授权现成的应用/服务即可使用，或只需开启已有系统设置。
- **🟡 中等门槛（Moderate）**：需要额外配置，例如导入规则、安装证书、调试配对、选择区域，或安装项目提供的修改版应用。
- **🔴 高门槛（High）**：需要 Root / 越狱、运行时注入、APK 修改或源码编译。

## 📚 完整目录

如果你想查看：

- 当前收录的全部条目；
- 每个条目的完整限制；
- 暂未完全核实的历史项目；
- 系统能力、开发者设置和研究原型；

请查看 **[完整目录 CATALOG.zh-CN.md](CATALOG.zh-CN.md)**。

每个条目也都有独立详情页，其中会进一步记录工作方式、适用场景、使用门槛、限制和原始来源。

## 🤝 纠错与贡献

广告防御方案和系统版本变化很快，App 更新也可能让旧规则失效。如果你发现：

- 项目已经停更或恢复维护；
- 某个链接失效；
- 某项方案的实际能力与描述不符；
- 有新的广告防御方案值得收录；

欢迎参考 [CONTRIBUTING.zh-CN.md](CONTRIBUTING.zh-CN.md) 提交线索或修正。

## 📄 许可

目录数据和说明文字采用 [CC BY 4.0](LICENSE-CONTENT)，生成与校验脚本采用 [MIT](LICENSE)。
