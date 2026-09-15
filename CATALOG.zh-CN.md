# 完整目录

<kbd>中文</kbd> <a href="CATALOG.md"><kbd>English</kbd></a>

本目录共记录 146 个条目：其中 108 个是主要防护条目（93 个与开屏广告相关，15 个针对其他广告形式），另有 22 个证据或可获取性有限的候选条目、12 个需要开发者或广告平台配合的机制，以及 4 个通用平台能力。

> [!IMPORTANT]
> 收录不代表推荐。工具效果、兼容性和维护状态可能随版本变化；涉及无障碍权限、VPN/DNS、Root、Xposed、重签名或实验性代码的条目，请先确认来源、权限和风险。

- 条目数：146
- 分类数量：🛠️ 开屏相关工具、规则与研究原型 88 条；📱 用户可开启的厂商广告控制 5 条；🧩 其他广告形式的防护工具 15 条；🧪 实现或可获取性仍待核实的候选条目 22 条；🏢 需要应用开发者或广告平台配合的机制 12 条；⚙️ 与广告防护相关的通用平台能力 4 条
- 内容核验基线：2026-09-13
- 本目录用途：提供可核对的工具信息，不构成安装、购买或安全建议
- 厂商设置、开发者配合机制和系统能力不一定是普通用户可以独立安装的工具
- 候选条目只作为补充线索，不纳入普通用户工具推荐

## 🛠️ 开屏相关工具、规则与研究原型

| 方案 | 平台 | 部署难度 | 部署要求 | 能做什么 | 可获取性/限制 |
| --- | --- | --- | --- | --- | --- |
| [GKD with specified advertising subscriptions](entries/001.zh-CN.md) | Android | 🟡 中等门槛 | Accessibility / 无障碍 | 利用 无障碍服务 读取页面 UI 节点并按订阅规则匹配“跳过/关闭”，再用无障碍点击/手势自动跳过广告。 | 已确认部署路径；广告仍会先加载并显示；规则依赖 UI 节点和页面结构，App 改版、Canvas/WebView 或自绘界面可能让匹配失效。 |
| [SKIP](entries/002.zh-CN.md) | Android | 内置或本地规则: 🟢 低门槛；导入订阅规则: 🟡 中等门槛 | Accessibility / 无障碍 | 利用 无障碍服务 感知启动页和可访问控件，并按本地/订阅规则定位跳过按钮后自动点击。 | 已确认部署路径；不阻止广告加载或摇一摇等触发；规则随 App UI 变化可能失效，自绘控件也可能无法被无障碍树识别。 |
| [AdSkip / Android-Touch-Helper](entries/003.zh-CN.md) | Android | 🟡 中等门槛 | Accessibility / 无障碍 | 利用 无障碍服务 按关键词、UI 控件或坐标识别目标，并通过无障碍点击自动处理开屏广告。 | 已确认部署路径；依赖页面可识别和规则维护；固定坐标对布局变化敏感，自绘 UI 也可能无法稳定匹配。 |
| [Li Tiaotiao (original version and rule ecosystem)](entries/005.zh-CN.md) | Android | 原版内置规则: 🟢 低门槛；手动导入社区规则: 🟡 中等门槛 | Accessibility / 无障碍 | 利用 无障碍服务 读取开屏页的可访问 UI，并按规则定位“跳过/关闭”控件后自动点击。 | 已停止维护；广告仍会先显示；依赖页面节点和规则适配。项目已于 2023 年宣布无限期停止更新。 |
| [ZeroStart](entries/006.zh-CN.md) | Android | 🟢 低门槛 | Accessibility / 无障碍 | 结合 UI 树、离线 OCR 和位置启发式识别开屏广告，强调防误触和老年用户场景。 | 已确认部署路径；截图/OCR 会增加识别时间；真实广告覆盖率和对误触/摇一摇场景的效果仍需要实测。 |
| [PureSkip](entries/007.zh-CN.md) | Android | 🔴 高门槛 | Accessibility / 无障碍；Source Build / 源码构建 | 采用离线确定性规则和按应用策略自动跳过已适配启动广告。 | 维护/兼容性不明确；适配范围由现有规则决定，App 页面结构变化后需要更新规则。 |
| [SplashCleaner-Android](entries/008.zh-CN.md) | Android | 🟢 低门槛 | Accessibility / 无障碍 | 利用 无障碍服务 感知 App 启动，并在短暂启动扫描窗口内按本地规则查找跳过/关闭控件后自动点击。 | 已确认部署路径；不阻断广告网络请求，广告仍可能先显示；如果跳过按钮不在无障碍树里或出现时间超出扫描窗口，就可能漏掉。 |
| [madeye/ad-skipper](entries/009.zh-CN.md) | Android | 内置节点、文字和图像识别: 🟢 低门槛；额外下载并配置 VLM: 🟡 中等门槛 | Accessibility / 无障碍 | 先用 Accessibility 节点找跳过按钮，失败时再用截图 + OCR/YOLO/VLM 定位，并通过无障碍手势点击。 | 已确认部署路径；视觉识别比纯 UI 节点匹配更慢，也可能误检/漏检；对于一出现就迅速触发跳转的广告，识别完成时可能已经太晚。 |
| [ADSkip (Promisin)](entries/010.zh-CN.md) | Android | 🟡 中等门槛 | Accessibility / 无障碍 | 按应用配置控件、坐标、点击位置和延时，自动跳过开屏广告。 | 维护/兼容性不明确；规则需要人工配置和维护，坐标点击对页面布局变化比较敏感；项目本身也较旧。 |
| [SkipAds (KonghuanSmart)](entries/011.zh-CN.md) | Android | 🔴 高门槛 | Accessibility / 无障碍；Source Build / 源码构建 | 基于无障碍服务自动跳过广告，可配置应用白名单。 | 维护/兼容性不明确；公开文档和适配范围较少，当前覆盖面与长期稳定性仍需进一步验证。 |
| [TapClick (formerly ADGO)](entries/012.zh-CN.md) | Android | 🟡 中等门槛 | Accessibility / 无障碍 | 通过无障碍控件、关键词或坐标规则自动跳过开屏广告并关闭弹窗。 | 已确认部署路径；原始仓库和维护状态不够清晰，多份镜像/分支之间的关系也需要核实。 |
| [Fuck Shake](entries/015.zh-CN.md) | Android | 🔴 高门槛 | Runtime Injection / 运行时注入 | 利用 Xposed Hook 目标 App 的摇一摇/传感器相关注册或回调，使 shake 信号无法继续进入广告跳转逻辑。 | 维护/兼容性不明确；主要切断 shake/运动触发，对点击、滑动、自动跳转等其他路径没有直接作用；App 内部 shake 实现变化后 Hook 也可能失效。 |
| [NoShakingAD / Bu Xu Tiaozhuan](entries/016.zh-CN.md) | Android | 🟡 中等门槛 | Accessibility / 无障碍；Debugging / 调试（Shizuku） | 利用 无障碍服务 判断目标 App 刚启动，再通过 Shizuku 调用 SensorService 的 restricted mode/白名单机制，在开屏时间窗内临时屏蔽运动传感器。 | 已确认部署路径；主要针对启动阶段的运动传感器触发，点击/滑动广告仍会存在；时间窗或 SensorService 控制范围不合适时，正常传感器功能也可能短暂受影响。 |
| [ShakeGuard](entries/018.zh-CN.md) | Android | 🔴 高门槛 | Accessibility / 无障碍；Source Build / 源码构建 | 跳转后识别异常目标应用并通过无障碍服务自动返回。 | 维护/兼容性不明确；属于跳转后的补救，目标页面可能已经短暂出现，跳转前发生的请求或数据交换也不会被撤销。 |
| [CleanSplash](entries/019.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入；Source Build / 源码构建 | 针对菜鸟、Bilibili 和 QQ 的摇一摇开屏广告实现版本特定 Hook。 | 维护/兼容性不明确；只覆盖已适配的菜鸟、Bilibili、QQ 及对应版本；目标 App 更新后相关 Hook 点可能失效。 |
| [CoolApkNoSplash](entries/020.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 已确认部署路径；只针对酷安和已知 SplashAdActivity 启动路径；如果开屏广告改用其他组件或实现，原 Hook 可能失效。 |
| [AdPopupBlocker](entries/021.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 通过 LSPosed 规则拦截已确认的开屏或插屏广告调用链。 | 已确认部署路径；依赖逐 App 逆向得到的规则，覆盖面由已有规则决定；应用或 SDK 改版后调用点可能变化。 |
| [AutoClickerPurifier: advertising features](entries/023.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入；Source Build / 源码构建 | 面向“自动点击器”应用的 LSPosed 模块，跳过其开屏广告并移除横幅。 | 已确认部署路径；只针对特定自动点击器 App，而且项目还包含非广告功能，不能把所有行为都归为广告防护。 |
| [QzxyAdBlock](entries/024.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 面向趣智校园 6.5.28，移除开屏和页面广告并屏蔽摇一摇跳转。 | 已确认部署路径；只支持特定趣智校园版本；资源 ID、广告 SDK 或调用链变化后需要重新定位。 |
| [MiFitnessAdAway](entries/026.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 利用 libxposed/LSPosed Hook 小米运动健康中的图片/视频开屏广告和推广代码，在加载/展示阶段修改执行结果。 | 已确认部署路径；只适用于小米运动健康的已适配版本；App 内部广告方法变化后需要重新定位 Hook 点。 |
| [bili-hook: advertising subset](entries/027.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 面向哔哩哔哩 7.4.0 的去广告与画质解锁模块，可去除普通开屏及多个页面广告。 | 已确认部署路径；严格依赖特定旧版 Bilibili 的内部实现，不是通用开屏广告方案。 |
| [Li Tiansuo / LiTianSuo](entries/028.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 利用 Xposed/LSPosed Hook 开屏 Activity、Splash 容器和第三方广告 SDK 初始化，在广告组件创建/SDK 启动前阻断。 | 已确认部署路径；依赖逐 App/SDK 的内部类和方法；代码混淆、版本更新、动态加载或 native 实现都会降低 Hook 稳定性。 |
| [MinMinGuard](entries/039.zh-CN.md) | Android | 🔴 高门槛 | Runtime Injection / 运行时注入 | 利用 Xposed Hook App 的 View 创建/布局过程，识别并移除广告 View，同时回收原本占用的页面空间。 | 已停止维护；不是开屏广告专用；项目已归档，现代自绘 UI、WebView 或新广告框架可能无法按旧规则识别。 |
| [AdBlocker Reborn](entries/040.zh-CN.md) | Android | 🔴 高门槛 | Runtime Injection / 运行时注入 | 利用 Xposed 在 Activity、View、WebView、Receiver、hosts 等多个位置加入 Hook/过滤，从不同入口阻断广告组件、请求或展示。 | 维护/兼容性不明确；属于较老的多点 Hook 方案，现代 Android/App 的兼容性有限；多个 Hook 点也更容易随系统或 App 更新失效。 |
| [Xposed-GodMode: ad element blocking](entries/041.zh-CN.md) | Android | 🔴 高门槛 | Runtime Injection / 运行时注入 | 允许用户选择并屏蔽应用内控件，例如广告或干扰按钮。 | 维护/兼容性不明确；需要用户自己选择要隐藏的 View；页面结构变化或动态生成内容会让已保存规则失效，而且网络/触发逻辑仍可能继续运行。 |
| [HyperCeiler: advertising features](entries/045.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 系统和应用界面定制模块，候选包含部分系统推荐/广告净化能力。 | 已确认部署路径；功能很多且高度依赖 ROM/版本；广告相关能力需要逐项核实，不能用一个通用工作流概括。 |
| [Cemiuiler: historical advertising features](entries/046.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 旧版 MIUI 系统增强模块，候选包含部分系统应用界面净化能力。 | 已停止维护；不是专用广告工具，而且 ROM/Android 版本限制明显；广告相关能力需要按具体功能项核实。 |
| [AdAway](entries/047.zh-CN.md) | Android | 本地 VPN: 🟢 低门槛；Root hosts: 🔴 高门槛 | Root；VPN / DNS / 代理 | 利用系统 hosts 或 Android 本地 VPN 接管域名解析，并用广告域名黑名单阻断匹配请求。 | 已确认部署路径；依赖广告域名可被单独识别；广告与正常业务共域、已经缓存或直接打包在 App 内时效果有限。 |
| [Rethink DNS + Firewall: advertising domain rules](entries/048.zh-CN.md) | Android | 🟢 低门槛 | VPN / DNS / 代理 | 提供 DNS 黑名单、本地 VPN、按应用防火墙、流量日志和可选 WireGuard。 | 已确认部署路径；不能可靠区分与业务共用域名的广告；本地 VPN 模式还会与其他 VPN 竞争同一系统槽位。 |
| [NetGuard: hosts-based ad filtering in non-Play builds](entries/049.zh-CN.md) | Android | 🟢 低门槛 | VPN / DNS / 代理 | 利用 Android VpnService 接管各 App 网络连接，并用按 App 防火墙与 hosts 规则阻断指定连接或广告域名。 | 已确认部署路径；主要是通用防火墙，不理解开屏广告语义；共享域名和缓存广告仍可能通过，本地 VPN 模式会占用 VPN 槽位。 |
| [DNS66](entries/050.zh-CN.md) | Android | 🟢 低门槛 | VPN / DNS / 代理 | 利用 Android VpnService 只接管 DNS 查询，并用 hosts/blocklist 阻止广告域名解析。 | 已停止维护；项目较老且已归档；只能处理 DNS 层可区分的广告，对第一方、缓存或内置广告无效。 |
| [personalDNSfilter](entries/051.zh-CN.md) | Android | 🟢 低门槛 | VPN / DNS / 代理 | 利用本地 DNS 代理/VPN 接收查询，并用过滤列表在域名解析阶段阻断广告/跟踪域名。 | 已确认部署路径；只影响需要经过 DNS 解析的网络广告；缓存内容或与正常业务共域的广告难以单独过滤。 |
| [TrackerControl: advertising-related network filtering](entries/052.zh-CN.md) | Android | 🟢 低门槛 | VPN / DNS / 代理 | 利用本地 VPN 观察 App 连接的网络端点，并用广告/跟踪数据库分类后阻断对应连接。 | 已确认部署路径；重点是跟踪器/第三方端点控制；第一方或与正常业务共享基础设施的广告较难区分。 |
| [Blokada 5](entries/053.zh-CN.md) | Android | 🟢 低门槛 | VPN / DNS / 代理 | 利用本地或云端 DNS/VPN 路径识别广告和追踪域名，并在网络资源加载前阻断命中请求。 | 已确认部署路径；不同版本的过滤架构并不相同；第一方、共享域名和缓存广告仍可能出现。 |
| [AdGuard for Android](entries/054.zh-CN.md) | Android | 本地 VPN/DNS 过滤: 🟢 低门槛；HTTPS 内容过滤和证书配置: 🟡 中等门槛 | VPN / DNS / 代理 | 利用 Android 本地 VPN/Private DNS 接管网络请求，并用广告/跟踪过滤规则在资源下载前阻断匹配流量。 | 已确认部署路径；不是开屏广告专用；第一方/共享域名、已缓存或打包进 App 的广告较难处理，本地 VPN 模式还可能与其他 VPN 冲突。 |
| [NextDNS: ad filtering](entries/055.zh-CN.md) | Android | 🟢 低门槛 | VPN / DNS / 代理 | 云端加密 DNS 防火墙，支持广告/追踪列表、日志和按配置控制。 | 已确认部署路径；DNS 层看不到页面/请求内容语义，第一方共享域名、缓存和内置广告仍会绕过。 |
| [InviZible: ad-filtering resolver configuration](entries/057.zh-CN.md) | Android | VPN/DNS 解析器: 🟢 低门槛；Root 网络控制: 🔴 高门槛 | Root；VPN / DNS / 代理 | 利用 DNSCrypt、防火墙等网络能力接管 DNS/流量，并按规则阻断不需要的广告或跟踪连接。 | 已确认部署路径；不是专门的开屏广告工具，配置复杂；广告与正常业务共域、缓存广告等仍无法解决。 |
| [BlockAds](entries/058.zh-CN.md) | Android | 本地 VPN: 🟢 低门槛；Root 代理/iptables: 🔴 高门槛 | Root；VPN / DNS / 代理 | 利用本地 VPN 或 Root 代理/iptables 接管流量，并根据广告域名规则阻断匹配连接。 | 已确认部署路径；依赖域名/网络特征可被单独区分；已缓存、内置或第一方广告仍可能绕过。 |
| [Athena: DNS ad filtering](entries/059.zh-CN.md) | Android | 本地 VPN/DNS: 🟢 低门槛；Shizuku: 🟡 中等门槛；Root: 🔴 高门槛 | Debugging / 调试（Shizuku）；VPN / DNS / 代理 | 结合 DNS 过滤和按应用防火墙，支持 VPN、Root 和 Shizuku 模式。 | 已确认部署路径；近期项目，模式差异和实际覆盖需实测。 |
| [DNSNet](entries/062.zh-CN.md) | Android | 🟢 低门槛 | VPN / DNS / 代理 | 利用 Android 本地 VPN 接管 DNS 查询，并按广告/内容域名规则阻断匹配解析。 | 已确认部署路径；近期项目，独立评测和长期维护状态尚不充分。 |
| [Daedalus + AdAway / anti-AD rules (historical implementation)](entries/064.zh-CN.md) | Android | 🟡 中等门槛 | VPN / DNS / 代理 | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 维护/兼容性不明确；维护和新系统兼容性需复核；仅能处理 DNS/域名层。源码可获取；较旧。 |
| [AdLock: mobile ad filtering](entries/066.zh-CN.md) | 跨平台 | 本地 VPN/DNS 过滤: 🟢 低门槛；HTTPS 内容过滤和证书配置: 🟡 中等门槛 | VPN / DNS / 代理 | 利用本地 VPN、DNS 或平台内容过滤能力匹配广告/跟踪请求，并在资源加载前阻断连接。 | 已确认部署路径；闭源；不能仅凭产品宣传推断它对摇一摇或所有原生 App 广告都有效。 |
| [Lockdown Privacy: advertising domain blocking](entries/067.zh-CN.md) | iOS | 🟢 低门槛 | VPN / DNS / 代理 | 使用本地防火墙阻断所有应用中的已知追踪器、广告和恶意域名。 | 已确认部署路径；基于域名列表，无法处理第一方或内置广告；与其他 VPN 配置可能冲突。 |
| [AdGuard for iOS](entries/069.zh-CN.md) | iOS；浏览器 | 🟢 低门槛 | VPN / DNS / 代理 | 提供 Safari 内容拦截、反追踪以及可配置加密 DNS 和自定义过滤订阅。 | 已确认部署路径；Safari 内容拦截只作用于浏览器；跨应用过滤主要依赖 DNS，因此仍受域名粒度限制。 |
| [Wipr 2: Filtr extension](entries/071.zh-CN.md) | iOS；浏览器 | 🟢 低门槛 | System Setting / 系统设置 | Safari 内容拦截器，阻止网页广告、追踪器和干扰元素。 | 已确认部署路径；仅限浏览器内容，不处理原生应用广告和传感器跳转。 |
| [AdBlock (FutureMind): DNS proxy](entries/072.zh-CN.md) | iOS；浏览器 | 🟢 低门槛 | VPN / DNS / 代理 | 使用本地 DNS 代理/VPN 思路进行跨应用域名过滤的商业产品。 | 已确认部署路径；闭源且主要依赖域名过滤，第一方、缓存或内置广告无法保证覆盖；当前产品状态也需继续核实。 |
| [AdGuard DNS: ad-filtering service](entries/075.zh-CN.md) | 路由器/DNS | 🟢 低门槛 | VPN / DNS / 代理 | 托管加密 DNS 服务，可按规则阻止广告、追踪器和恶意域名。 | 已确认部署路径；需信任第三方 DNS 服务，无法识别内容层和共用域名广告。 |
| [Control D: Ads & Trackers filtering](entries/076.zh-CN.md) | 路由器/DNS | 🟢 低门槛 | VPN / DNS / 代理 | 可配置的托管 DNS 过滤服务，支持广告、追踪器和类别规则。 | 已确认部署路径；不是移动广告专用，效果受域名分类和加密 DNS 绕过影响。 |
| [Proton VPN: NetShield ad filtering](entries/080.zh-CN.md) | 跨平台 | 🟢 低门槛 | VPN / DNS / 代理 | Proton VPN 连接期间通过 DNS 过滤恶意软件、广告和追踪域名。 | 已确认部署路径；本质仍是域名级过滤，第一方/共域、缓存或内置广告无法可靠处理；具体过滤能力也可能随平台版本不同。 |
| [Mullvad: advertising DNS filtering](entries/081.zh-CN.md) | 跨平台 | 🟢 低门槛 | VPN / DNS / 代理 | Mullvad 提供可选的广告、追踪、恶意软件等内容阻止 DNS 主机名。 | 已确认部署路径；只在 DNS 层判断域名，无法处理同域、缓存或 App 内置广告，也不干预传感器/跳转逻辑。 |
| [IVPN: AntiTracker](entries/082.zh-CN.md) | 跨平台 | 🟢 低门槛 | VPN / DNS / 代理 | IVPN 的 DNS 级 AntiTracker 在 VPN 隧道中阻断广告和追踪域名。 | 已确认部署路径；依赖域名列表，无法识别广告 UI、传感器触发或与正常业务共域的广告。 |
| [Windscribe: R.O.B.E.R.T. ad filtering](entries/083.zh-CN.md) | 跨平台 | 🟢 低门槛 | VPN / DNS / 代理 | Windscribe 账号侧的 DNS 过滤系统，可阻止广告、追踪器和自定义类别。 | 已确认部署路径；依赖服务端域名分类，无法处理同域、缓存或内置广告，也不理解 App 内的触发/跳转语义。 |
| [Private Internet Access: MACE](entries/084.zh-CN.md) | 跨平台 | 🟢 低门槛 | VPN / DNS / 代理 | PIA VPN 提供的 DNS 级广告、追踪器和恶意域名阻断功能。 | 已确认部署路径；只做域名级阻断，第一方或与正常业务共域的广告仍可能出现；不同平台的可用能力可能不一致。 |
| [NordVPN: mobile ad filtering](entries/085.zh-CN.md) | 跨平台 | 🟢 低门槛 | VPN / DNS / 代理 | NordVPN 的威胁防护功能包含广告和恶意域名阻断，具体能力随平台变化。 | 已确认部署路径；不同平台的功能层级并不一致，不能把桌面端的内容扫描能力直接外推到移动端；移动端仍主要受域名/网络层粒度限制。 |
| [Surfshark: CleanWeb mobile ad filtering](entries/086.zh-CN.md) | 跨平台 | 🟢 低门槛 | VPN / DNS / 代理 | Surfshark VPN 的 CleanWeb 功能用于阻止广告、追踪器和恶意站点。 | 已确认部署路径；主要依赖 DNS/网络规则，无法处理已经加载、与业务共域或直接内置在 App 中的广告。 |
| [dongqiudi-adblock](entries/087.zh-CN.md) | Android | 🔴 高门槛 | Root | 面向懂球帝应用的 Magisk 模块，组合文件权限、网络和 DNS 规则处理开屏及信息流广告。 | 已确认部署路径；只针对懂球帝；守护进程、缓存目录权限和 iptables 规则有兼容风险。 |
| [SplashGuard (33lilil)](entries/088.zh-CN.md) | Android | 🔴 高门槛 | Accessibility / 无障碍；Source Build / 源码构建 | 源码中声明无障碍服务、白名单和规则界面，用于识别并关闭或跳过开屏广告。 | 维护/兼容性不明确；当前主要从 Manifest 和源码结构确认其无障碍/规则能力，缺少成熟产品文档和独立评测，实际覆盖范围仍不清楚。 |
| [AdSkipHelper](entries/089.zh-CN.md) | Android | 🔴 高门槛 | Accessibility / 无障碍；Source Build / 源码构建 | 利用 AccessibilityService 监听 UI 事件并按预设规则识别目标节点，再通过无障碍点击自动跳过广告。 | 维护/兼容性不明确；更偏教学/原型而非成熟产品；依赖规则和可访问 UI，稳定性与维护性有限。 |
| [mirad-tech/Skip](entries/093.zh-CN.md) | Android | 🟢 低门槛 | Accessibility / 无障碍 | 利用 无障碍服务 读取 UI 树并寻找符合条件的 skip/close 控件，找到后直接调用无障碍点击。 | 已确认部署路径；只对可被无障碍识别的控件有效；不阻止广告加载，也不处理摇一摇等触发逻辑。 |
| [obaby/skip_ads_android](entries/095.zh-CN.md) | Android | 🟢 低门槛 | Accessibility / 无障碍；Additional Model / 额外模型 | 利用屏幕截图和 YOLOv5/TFLite/TorchScript 检测“跳过”按钮位置，再通过坐标自动点击。 | 维护/兼容性不明确；属于原型方案；效果依赖训练数据和模型泛化能力，可能有计算延迟，也无法阻止广告本身加载。 |
| [AdClose](entries/096.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 利用 LSPosed/Xposed Hook 广告 SDK、网络和 SensorManager 等调用，在广告初始化/加载或 shake 监听阶段直接截断逻辑。 | 已确认部署路径；通常需要 Root + LSPosed/Xposed；App/SDK 更新、代码混淆、动态加载或 native 实现都可能让 Hook 失效，需要持续适配。 |
| [FanqieHook (advertising features)](entries/097.zh-CN.md) | Android | 🔴 高门槛 | Runtime Injection / 运行时注入 | 利用 LSPosed 注入特定 App，并 Hook 已知广告方法/数据路径，在开屏、Banner 或视频广告执行前修改或跳过逻辑。 | 已确认部署路径；高度依赖目标 App 的版本和内部实现；App 更新后 Hook 点可能变化，需要重新适配。需要 Root/LSPosed。 |
| [PureNGA: advertising subset](entries/098.zh-CN.md) | Android | Xposed/LSPosed: 🔴 高门槛；修改后的 APK: 🔴 高门槛 | Root；Runtime Injection / 运行时注入；APK Modification / APK 修改 | 利用 Xposed/LSPosed/LSPatch Hook NGA 内部的广告方法或数据流，在开屏/信息流内容展示前过滤或跳过广告逻辑。 | 已确认部署路径；只适用于特定 App；目标 App 更新后可能失效。使用 Xposed/LSPosed 通常有较高部署门槛。 |
| [ReWeibo: Weibo Lite advertising subset](entries/100.zh-CN.md) | Android | 🔴 高门槛 | Runtime Injection / 运行时注入 | 利用 Xposed/LSPosed Hook 微博内部的广告函数/数据流，在开屏或信息流广告进入展示前修改或过滤结果。 | 已确认部署路径；依赖目标 App 版本；需要 Root/LSPosed。App 更新或广告实现变化后可能需要维护 Hook 规则。 |
| [BetterHeybox (advertising features)](entries/101.zh-CN.md) | Android | 🔴 高门槛 | Runtime Injection / 运行时注入 | 利用 LSPosed Hook 特定 App 的已知广告入口和运行时函数，在广告代码执行时提前返回或修改结果。 | 已确认部署路径；需要 Root/LSPosed，且只对已适配的 App/版本有效；应用更新后可能失效。 |
| [TheMessWorld: Pangguai Life splash subset](entries/102.zh-CN.md) | Android | 🔴 高门槛 | Runtime Injection / 运行时注入 | 利用 Xposed/LSPosed Hook 特定 App 的开屏广告关键调用，在运行时提前返回或修改结果以绕过展示。 | 已停止维护；项目规模较小，具体支持的 App/版本需进一步核实；需要 Root/LSPosed，更新后可能失效。 |
| [Fuck AD](entries/103.zh-CN.md) | Android | 无障碍自动跳过: 🟢 低门槛；无障碍 + Shizuku 点击: 🟡 中等门槛；Root + Xposed/LSPosed: 🔴 高门槛 | Root；Runtime Injection / 运行时注入；Accessibility / 无障碍；Debugging / 调试（Shizuku） | 利用 Xposed/LSPosed 按 App Hook 广告 SDK、普通 UI 或 Flutter 通道等不同入口，在命中广告逻辑后阻断或自动跳过。 | 已确认部署路径；不是统一通用方案，依赖逐 App 适配；需要 Root/LSPosed。具体支持范围和行为在使用前应进一步核实。 |
| [Kuan Jinghua / Coolapk Purifier](entries/104.zh-CN.md) | Android | 🔴 高门槛 | Runtime Injection / 运行时注入 | 利用 DexKit 在当前酷安版本中定位广告方法，再由 LSPosed 运行时 Hook 这些方法以抑制开屏/信息流广告。 | 已确认部署路径；需要 Root/LSPosed；虽然 DexKit 有助于适配版本变化，但目标 App 大改后仍可能失效。 |
| [FuckAdJump](entries/106.zh-CN.md) | Android | 🔴 高门槛 | Runtime Injection / 运行时注入 | LSPosed 模块，不移除广告本身，而是 Hook URI 解析并使淘宝/京东特定 Deep Link 失效，从而阻止广告把用户拉起到淘宝或京东 App。 | 维护/兼容性不明确；只覆盖项目明确处理的淘宝/京东 URI scheme；需要 LSPosed/Xposed。若目标应用改用其他 scheme、普通 HTTP/App Link、显式 Intent 或其他跳转路径，可能不受该 Hook 影响；广告本身不会被移除。 |
| [app2smile ad network rules + Surge / Quantumult X](entries/108.zh-CN.md) | iOS | 🟡 中等门槛 | VPN / DNS / 代理 | 通过 HTTP(S) MITM + Rewrite / Map Local 匹配广告 API，可直接改写请求/响应或伪造本地空响应，使广告数据在进入 App 前被删除或替换。 | 已确认部署路径；需要配置规则和 MITM 证书；证书固定（certificate pinning）、QUIC/非 HTTP 流量或未进入 Surge HTTP engine 的连接可能无法改写；规则通常需要按 App/API 维护。 |
| [One Patch: touch blocking for ad regions](entries/113.zh-CN.md) | Android | 🟡 中等门槛 | Overlay / 悬浮层 | Android 触摸屏蔽工具，在指定矩形区域放置 Overlay 并吞掉触摸事件，可用于屏蔽易误触的 UI 区域，包括 sticky ads。 | 已确认部署路径；不是广告识别工具，需要用户手动设定区域；会同时屏蔽该区域内的正常交互。系统手势区、键盘及调用 HIDE_OVERLAY_WINDOWS 的 App 等场景可能无法覆盖。 |
| [Adobo: advertising patches (loadable by Morphe)](entries/119.zh-CN.md) | Android | 🔴 高门槛 | APK Modification / APK 修改 | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 已确认部署路径；Morphe Manager 本身不是广告专用，去广告能力由 Adobo Patches 提供；支持范围依赖 patch 与 App/SDK 版本。静态修改可能影响签名、更新和兼容性。 |
| [DTL-X: rmads feature](entries/120.zh-CN.md) | Android | 🔴 高门槛 | APK Modification / APK 修改 | 基于 apktool + smali 的 Python APK reverse/patch 工具，README 明确提供多种 rmads 去广告方法，可修改 Manifest、权限、广告 ID 与广告 loader 后重新打包。 | 已确认部署路径；通用逆向/补丁工具而非广告专用 App，但 README 明确提供 rmads 功能。某些方法（如移除 INTERNET 权限）粒度很粗，会同时影响正常联网；重打包也可能触发签名/完整性校验。 |
| [Li Tiaotiao rules](entries/121.zh-CN.md) | Android | 🟡 中等门槛 | 需要按原始资料配置相应的平台或运行环境 | 提供界面匹配和跳过操作规则 | 已确认部署路径；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [AWAvenue Ads Rule / Qiufeng Advertising Rules](entries/124.zh-CN.md) | 待核验 | 导入 VPN/域名过滤规则: 🟡 中等门槛；Root hosts 规则: 🔴 高门槛 | 需要按原始资料配置相应的平台或运行环境 | 提供广告服务器和广告库的域名规则 | 已确认部署路径；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [blackmatrix7 startup](entries/125.zh-CN.md) | iOS | 🟡 中等门槛 | VPN / DNS / 代理 | 移除开屏广告字段，并修改展示时长、尺寸和过期时间 | 已确认部署路径；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [Block This (historical implementation)](entries/126.zh-CN.md) | Android | 🟢 低门槛 | VPN / DNS / 代理 | 将域名查询发送到作者配置的远程广告过滤服务 | 已停止维护；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [Blokada 6 / Cloud](entries/127.zh-CN.md) | 跨平台 | 🟢 低门槛 | 需要按原始资料配置相应的平台或运行环境 | 通过云端解析服务过滤广告域名 | 已确认部署路径；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [CAD viewer patch](entries/128.zh-CN.md) | Android | 安装项目提供的修改版 APK: 🟡 中等门槛；自行修改、重签名和安装 APK: 🔴 高门槛 | APK Modification / APK 修改 | 移除匹配的广告组件，并将启动入口改为主界面 | 已确认部署路径；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [ChaoxingLaunchAdBlock](entries/129.zh-CN.md) | iOS | 🔴 高门槛 | Jailbreak / 越狱；Runtime Injection / 运行时注入 | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 已确认部署路径；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [fmz200/wool_scripts: advertising subset](entries/130.zh-CN.md) | iOS | 🟡 中等门槛 | VPN / DNS / 代理 | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 已确认部署路径；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [FuckApp (formerly listed as ``Zheng Nengliang''): advertising subset](entries/131.zh-CN.md) | Android | 🔴 高门槛 | Runtime Injection / 运行时注入 | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 已确认部署路径；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [Lain-Patches: Disable Ads subset](entries/132.zh-CN.md) | Android | 🔴 高门槛 | Source Build / 源码构建 | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 已确认部署路径；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [Lin-arm/GKD_subscription advertising subset](entries/134.zh-CN.md) | Android | 🟡 中等门槛 | Executed by GKD | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 已确认部署路径；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [R-Store](entries/136.zh-CN.md) | iOS | 🟡 中等门槛 | VPN / DNS / 代理 | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 已确认部署路径；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [VindroidH/SkipAds](entries/137.zh-CN.md) | Android | 🟢 低门槛 | Accessibility / 无障碍 | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 已确认部署路径；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [Moyu Rewrite: advertising subset](entries/138.zh-CN.md) | iOS | 🟡 中等门槛 | VPN / DNS / 代理 | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 已确认部署路径；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [Lei Tiaotiao](entries/139.zh-CN.md) | Android | 🟢 低门槛 | Accessibility / 无障碍 | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 维护/兼容性不明确；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |

## 📱 用户可开启的厂商广告控制

| 设置/控制项 | 适用平台或范围 | 部署难度 | 部署要求 | 能做什么 | 限制 |
| --- | --- | --- | --- | --- | --- |
| [OPPO: motion and orientation permission](entries/142.zh-CN.md) | Android | 🟢 低门槛 | 记录在官方指南中的用户设置 | 按应用限制运动或方向传感器的访问 | 官方指南没有提供完整的机型和固件兼容列表。 |
| [vivo / iQOO: motion and orientation control](entries/149.zh-CN.md) | Android | 🟢 低门槛 | 用户设置; 支持该选项的机型和固件 | 限制运动数据访问；部分固件只支持在开屏广告期间阻止 | 效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [Huawei: device orientation permission](entries/151.zh-CN.md) | 待核验 | 🟢 低门槛 | 用户设置; 对应的 HarmonyOS 版本 | 按应用限制方向传感器访问 | 应用本身的正常方向功能也会受到限制。 |
| [HONOR: automatic app navigation reminder](entries/153.zh-CN.md) | Android | 🟢 低门槛 | 厂商系统支持和用户设置 | 检测到疑似误触跳转时增加提醒 | 覆盖范围取决于系统能否识别误触，以及对应的跳转是否经过检查。 |
| [HONOR: device sensor permission](entries/154.zh-CN.md) | Android | 🟢 低门槛 | 用户设置; HONOR 100 / 100 Pro 8.0.0.150 版本说明 | 按应用限制运动和方向传感器访问 | 版本证据只适用于列出的机型，正常的运动相关功能也可能受到影响。 |

## 🧩 其他广告形式的防护工具

| 方案 | 平台 | 部署难度 | 部署要求 | 能做什么 | 可获取性/限制 |
| --- | --- | --- | --- | --- | --- |
| [Klick'r / Smart AutoClicker: user-configured ad dismissal](entries/013.zh-CN.md) | Android | 🟡 中等门槛 | Accessibility / 无障碍 | 根据屏幕图像出现与否触发点击，可配置为识别并点击广告跳过按钮。 | 已确认部署路径；它是通用自动化工具，不自带广告语义；是否能稳定跳过广告取决于用户配置的图像条件和页面变化。 |
| [Ad Skipper (anar-bastanov)](entries/014.zh-CN.md) | Android | 🟢 低门槛 | Accessibility / 无障碍 | 在官方 YouTube 应用出现可跳过广告按钮时使用无障碍服务自动点击。 | 已确认部署路径；只针对 YouTube 可跳过广告，不处理开屏广告或不可跳过广告。 |
| [XTA-AdKiller](entries/025.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 为超级课程表拦截开屏、横幅、信息流、插屏、原生和激励广告接口。 | 已确认部署路径；只面向超级课程表及已识别广告接口；目标版本变化后适配可能失效。 |
| [Play Store Adblock](entries/029.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 移除 Google Play 商店中的广告、Sponsored 应用和推广推荐。 | 已确认部署路径；只处理 Google Play 内部的 Sponsored/推广内容，不会影响其他 App 的开屏广告。 |
| [amznkiller](entries/030.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 隐藏 Amazon Shopping 应用的广告、Sponsored 卡片、视频轮播和广告位。 | 已确认部署路径；只针对 Amazon Shopping 的已适配广告/推荐组件，应用改版后内部数据或 View 结构可能变化。 |
| [Discover Feed Filter](entries/031.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 已确认部署路径；只处理 Google Discover/Google App 的推广内容，不是开屏广告或跨 App 跳转防护。 |
| [GmailHideAds](entries/032.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 在 Gmail 收件箱广告行布局测量前移除 Sponsored 会话行。 | 已确认部署路径；只针对 Gmail 收件箱的 Sponsored 行；布局或混淆代码变化可能让定位失效。 |
| [ThreadsHideAds](entries/033.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 从 Threads 信息流中移除 Sponsored 插入项。 | 已确认部署路径；只处理 Threads 信息流里的 Sponsored 插入项，不覆盖开屏广告或其他 App。 |
| [TwitterHideAds](entries/034.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 在 X/Twitter 的时间线、详情、搜索和视频标签中过滤 promoted 内容。 | 已确认部署路径；只处理 X/Twitter 内已适配的 promoted 内容；时间线结构或混淆代码变化时需要更新。 |
| [UnclutterIG (historical implementation)](entries/035.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 隐藏 Instagram 信息流和 Stories 中的广告及推广内容。 | 维护/兼容性不明确；只针对 Instagram 已适配的 Feed/Stories 广告；内部数据结构变化后可能失效。 |
| [MapsAdBlock](entries/037.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | 在 Google Maps 解析响应后移除赞助卡片、推广图钉、广告建议和预订广告。 | 已确认部署路径；只针对 Google Maps 中已适配的赞助内容；不是网络级或开屏广告防御。 |
| [ad-free: audio ad handling](entries/038.zh-CN.md) | Android | 🟢 低门槛 | Notification Access / 通知访问 | 通过检测 Spotify 广告并控制播放/静音等方式减少广告干扰。 | 已确认部署路径；只针对 Spotify 音频广告，不处理移动应用开屏广告、传感器触发或跨应用跳转。 |
| [QAuxiliary: advertising features](entries/044.zh-CN.md) | Android | 🔴 高门槛 | Root；Runtime Injection / 运行时注入 | QQ/TIM 功能增强模块，可能包含界面净化和广告相关开关。 | 已确认部署路径；不是专用广告工具；需要先确认具体版本里到底有哪些广告/净化功能，不能把整个项目都算作广告防护。 |
| [AdSkipper (GimleLarpes)](entries/090.zh-CN.md) | Android | 🔴 高门槛 | Accessibility / 无障碍；Source Build / 源码构建 | 针对 YouTube 资源 ID 检测广告、自动静音，并在跳过按钮可点击时执行无障碍点击。 | 维护/兼容性不明确；只针对 YouTube 的特定 resource ID；界面更新后容易失效，而且广告仍会先播放到出现可跳过控件的阶段。 |
| [AdAuto (Hongguo Short Drama ad skipping)](entries/122.zh-CN.md) | Android | 🟢 低门槛 | Accessibility / 无障碍；Overlay / 悬浮层 | 根据广告文字、倒计时和播放状态关闭广告或向上滑动 | 已确认部署路径；效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |

## 🧪 实现或可获取性仍待核实的候选条目

| 条目 | 平台 | 部署难度 | 能做什么 | 暂不纳入主清单的原因 | 可获取性 |
| --- | --- | --- | --- | --- | --- |
| [AdSkipper (decemberpei)](entries/004.zh-CN.md) | Android | 🟢 低门槛 | 检测可见的 Skip 按钮并通过无障碍服务自动点击。 | 主要覆盖有可识别 Skip/Close 控件的广告；闭源/商店版本的具体识别规则和数据处理方式不容易审计。 | 已确认部署路径 |
| [Rule Imprison (permissions and state handling awaiting verification)](entries/017.zh-CN.md) | Android | 🔴 高门槛 | 公开资料曾描述其与广告处理有关，但目前不作为主目录工具。 | 现有公开资料不足以确认实现方式、版本范围或当前可用性。 | 维护/兼容性不明确 |
| [AdSkipTweak (dismissal flow awaiting verification)](entries/022.zh-CN.md) | iOS | 🔴 高门槛 | 公开资料曾描述其与广告处理有关，但目前不作为主目录工具。 | 现有公开资料不足以确认实现方式、版本范围或当前可用性。 | 维护/兼容性不明确 |
| [JohnnyAdBlock (compatibility awaiting verification)](entries/042.zh-CN.md) | Android | 🔴 高门槛 | 公开资料曾描述其与广告处理有关，但目前不作为主目录工具。 | 现有公开资料不足以确认实现方式、版本范围或当前可用性。 | 维护/兼容性不明确 |
| [BiliRoamingX: advertising patches](entries/043.zh-CN.md) | Android | 🔴 高门槛 | Bilibili 功能增强 Xposed 模块，含若干界面净化候选能力。 | 主 README 没有明确给出广告功能和对应 Hook 点，正式引用前需要定位具体功能项或源码证据。 | 维护/兼容性不明确 |
| [AdClear Content Blocker (current product)](entries/065.zh-CN.md) | Android | 🟢 低门槛 | 公开资料曾描述其与广告处理有关，但目前不作为主目录工具。 | 现有公开资料不足以确认实现方式、版本范围或当前可用性。 | 已确认部署路径 |
| [DNSCloak + AdGuard Home ad filtering](entries/068.zh-CN.md) | iOS | 🔴 高门槛 | 为 dnscrypt-proxy 2 提供 iOS 图形界面，可选择具备广告过滤的 DNS 解析器。 | 本身不定义广告规则，过滤效果取决于解析器；项目技术栈较旧。 | 维护/兼容性不明确 |
| [zoffelf/skipad (implementation unverified)](entries/092.zh-CN.md) | Android | 🔴 高门槛 | 公开资料曾描述其与广告处理有关，但目前不作为主目录工具。 | 公开代码目录缺少应用实现和所述构建流程，因此只能作为未核实线索。 | 维护/兼容性不明确 |
| [Tmall Campus / Quzhi Campus ad removal](entries/099.zh-CN.md) | Android | 🔴 高门槛 | 资料描述了直接进入主界面、隐藏广告和拦截广告加载等功能 | 现有公开资料不足以确认实现方式、版本范围或当前可用性。 | 维护/兼容性不明确 |
| [ReVanced Manager + specific advertising patches (source and versions awaiting verification)](entries/118.zh-CN.md) | Android | 🔴 高门槛 | 公开资料曾描述其与广告处理有关，但目前不作为主目录工具。 | 现有公开资料不足以确认实现方式、版本范围或当前可用性。 | 维护/兼容性不明确 |
| [Adhell3 (historical source)](entries/123.zh-CN.md) | Android | 🔴 高门槛 | 向 Samsung 网络控制功能写入广告域名和连接规则 | 效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 | 已停止维护 |
| [NoMoAds (research prototype)](entries/135.zh-CN.md) | Android | ❓ 待核验 | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 | 当前无法获取 |
| [adX / adX Launcher](entries/155.zh-CN.md) | Android | ❓ 待核验 | 公开资料曾描述其与广告处理有关，但目前不作为主目录工具。 | 内部修改机制未公开，因此仅作为等待实现核验的候选线索。 | 待核验 |
| [Ding Xiaotiao](entries/156.zh-CN.md) | Android | ❓ 待核验 | 下载记录和同期资料显示其曾被用于跳过广告 | 包身份和实现方式尚未确认，相关下载渠道此前已经关闭。 | 待核验 |
| [Yi Zhi Chan](entries/157.zh-CN.md) | Android | ❓ 待核验 | 分发记录中列出的广告跳过应用 | 原始说明网站已无法访问，安装包与功能描述之间的对应关系仍未核实。 | 待核验 |
| [Zhihui Dao](entries/158.zh-CN.md) | 待核验 | ❓ 待核验 | 分发记录中的应用，但广告相关功能尚未核实 | 尚未确认它与“Chanshi”的更名关系，因此不能直接采用后者的实现描述。 | 待核验 |
| [Qing Qidong](entries/159.zh-CN.md) | Android | ❓ 待核验 | 公开资料曾描述其与广告处理有关，但目前不作为主目录工具。 | 广告用途主要来自历史资料，当前广告实现仍未核实。 | 维护/兼容性不明确 |
| [Kelee Plugin Center / ProxyResource](entries/160.zh-CN.md) | iOS | 导入 Loon 插件规则: 🟡 中等门槛；需要应用重签名的插件: 🔴 高门槛 | 为多个应用和小程序提供广告插件配置项 | 部分配置无法获取；腾讯视频插件已声明停止维护并存在版本限制。 | 维护/兼容性不明确 |
| [Yao Ni Ming San Qian: advertising subset (mechanism unverified)](entries/161.zh-CN.md) | Android | 🔴 高门槛 | 资料列出了抖音、快手等应用中的广告处理功能，其中包括部分开屏广告 | 公开分发目录缺少实现代码，具体处理操作仍未核实。 | 维护/兼容性不明确 |
| [LinkedInAdblockerXposed (unfinished prototype)](entries/162.zh-CN.md) | Android | 🔴 高门槛 | 定位 LinkedIn 的点击方法并安装 Hook，目标是处理应用内广告。 | 检查到的前后回调目前为空，尚未实现广告移除；因此不计作已实现的防护，也不会仅根据项目目标推断其具备展示控制能力。 | 维护/兼容性不明确 |
| [QQTamer / QQ Keeper: historical advertising subset](entries/163.zh-CN.md) | Android | 🔴 高门槛 | 资料描述了拦截 QQ 指定的开屏缓存使用和广告跳转 | 现有公开资料不足以确认实现方式、版本范围或当前可用性。 | 维护/兼容性不明确 |
| [Dasheng Jinghua](entries/164.zh-CN.md) | Android | 🔴 高门槛 | 资料列出了页面替换、界面屏蔽以及请求和文件规则 | 现有公开资料不足以确认实现方式、版本范围或当前可用性。 | 维护/兼容性不明确 |

## 🏢 需要应用开发者或广告平台配合的机制

| 机制/控制项 | 适用平台或范围 | 部署难度 | 部署要求 | 能做什么 | 限制 |
| --- | --- | --- | --- | --- | --- |
| [AdblockAndroid: developer integration library](entries/111.zh-CN.md) | Android | 🧑‍💻 仅限开发者/平台方 | 开发者 / 平台配置 | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 属于开发库而非独立系统级 blocker，需要集成到目标 App/浏览器的 WebView；不能直接处理原生 Android View 广告、传感器触发或跨 App 跳转。 |
| [libadblockplus-android: AdblockWebView](entries/133.zh-CN.md) | Android | 🧑‍💻 仅限开发者/平台方 | 开发者 / 平台配置 | 用于处理广告请求、广告界面或广告跳转，具体范围取决于项目支持的应用和版本。 | 效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [Google Confirmed Click](entries/140.zh-CN.md) | 待核验 | 🧑‍💻 仅限开发者/平台方 | 由 Google 针对特定广告位启用 | 在进入广告目标页面前增加一次确认 | 仅适用于 Google Ads 广告需求；对具体开屏广告形式的覆盖范围仍需评估。 |
| [GroMore Android](entries/141.zh-CN.md) | Android | 🧑‍💻 仅限开发者/平台方 | 开发者 / 平台配置 | 通过 setSplashShakeButton 配置开屏广告是否响应摇一摇 | 文档没有列出完整的广告来源覆盖范围或默认值。 |
| [Sigmob Android](entries/143.zh-CN.md) | Android | 🧑‍💻 仅限开发者/平台方 | 开发者 / 平台配置 | 通过 setSensorStatus(false) 禁止 SDK 使用传感器 | 效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [Sigmob HarmonyOS](entries/144.zh-CN.md) | 待核验 | 🧑‍💻 仅限开发者/平台方 | 开发者 / 平台配置 | 通过 isCanUseSensor 控制 SDK 是否可以访问传感器 | 效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [Sigmob iOS](entries/145.zh-CN.md) | iOS | 🧑‍💻 仅限开发者/平台方 | 开发者 / 平台配置 | 通过 isCanUseMotionManager 禁用运动交互组件 | 该接口只覆盖交互组件，其他广告交互仍可能存在。 |
| [Taku Android](entries/146.zh-CN.md) | Android | 🧑‍💻 仅限开发者/平台方 | 开发者 / 平台配置 | 配置是否允许摇一摇、旋转和滑动等交互 | 效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [Taku iOS](entries/147.zh-CN.md) | iOS | 🧑‍💻 仅限开发者/平台方 | 开发者 / 平台配置 | 配置广告来源的运动交互功能 | 效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [ToBid Android](entries/148.zh-CN.md) | Android | 🧑‍💻 仅限开发者/平台方 | 开发者 / 平台配置 | 把传感器采集开关传递给支持的广告来源 | 效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [Tencent GDT Android](entries/150.zh-CN.md) | Android | 🧑‍💻 仅限开发者/平台方 | 开发者 / 平台配置 | 通过 shakable=``0'' 禁用开屏广告摇一摇 | 省略该参数或设置为 1 都不会阻止摇一摇；文档也无法明确该参数首次出现的版本。 |
| [Kuaishou iOS](entries/152.zh-CN.md) | iOS | 🧑‍💻 仅限开发者/平台方 | 开发者 / 平台配置 | 通过 disableShake 禁用开屏广告摇一摇 | 默认不会阻止；只影响指定的交互方式。 |

## ⚙️ 与广告防护相关的通用平台能力

| 系统/浏览器能力 | 平台 | 部署难度 | 部署要求 | 能做什么 | 局限 |
| --- | --- | --- | --- | --- | --- |
| [AOSP Sensors off](entries/165.zh-CN.md) | Android | 🟢 低门槛 | 开发者 / 平台配置 | 全局停止传递对应的传感器事件 | 效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [OnePlus: startup motion permission](entries/166.zh-CN.md) | Android | 🟢 低门槛 | 官方说明适用于 10T 14.0.0.712 / 9R 14.0.0.603 | 在应用启动期间拒绝运动和方向传感器访问 | 这是通用的启动权限，官方资料没有将其限定为广告控制功能。 |
| [iOS browser app launching and link routing](entries/167.zh-CN.md) | iOS；浏览器 | 🟢 低门槛 | System Setting / 系统设置 | 浏览器可以对打开外部应用进行确认、允许或拒绝，系统再根据关联关系处理链接 | 效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |
| [iOS URL Filter](entries/168.zh-CN.md) | iOS | 🧑‍💻 仅限开发者/平台方 | 开发者 / 平台配置 | 系统根据地址数据集允许或拒绝网络请求 | 效果取决于应用版本、规则覆盖范围和运行环境；使用前请核对原始来源。 |

## 🧭 部署难度（Deployment Effort）

- **🟢 低门槛**：安装并授权现成的应用/服务即可使用，或只需开启已有系统设置。
- **🟡 中等门槛**：需要额外配置，例如导入规则、选择区域、安装证书、完成调试配对或安装修改版应用。
- **🔴 高门槛**：需要 Root/越狱、运行时注入、APK 修改或源码编译。
- **仅限开发者/平台方**：需要集成 SDK、修改宿主应用或由广告平台启用，不是普通用户可以独立部署的工具。
- **信息不足**：现有公开资料不足以确认一条可操作的部署路径。

部署难度按具体部署路径判断。同一条目如果有多种路径，会分别标注；是否付费不改变难度等级，部署难度也与安全性、可获取性和实测效果分开记录。

## 🏷️ 可获取性与维护状态

- **已确认部署路径**: 已找到可识别的安装包、服务、配置或源码构建路径；这不等于已验证当前兼容性或实际防护效果。
- **维护/兼容性不明确**: 维护状态或当前版本兼容性不清楚，使用前需要核对来源和版本。
- **已停止维护**: 项目已经停更或归档；历史机制仍可记录，但不代表当前版本仍可使用。
- **当前无法获取**: 目前无法从记录的来源获得可用版本或完整材料。
- **待核验**: 现有公开资料不足以确认实现方式、部署路径或当前可用性。

## 使用门槛提示

- **Root / Jailbreak（越狱）**：系统权限条件，与运行时注入是不同的部署要求。
- **Runtime Injection / 运行时注入**：例如 Xposed / LSPosed，在应用运行时改变其行为；它不等同于 APK 修改。
- **APK Modification / APK 修改**：修改安装包，并需要兼容的补丁、签名和重新安装流程。
- **Accessibility / 无障碍**：可能读取界面信息并执行自动操作，请只对可信来源授权。
- **Debugging / 调试**：部分路径通过 Shizuku 等方式获得调试授权，与无障碍权限分开。
- **VPN / DNS / 代理**：可能接管部分网络连接或域名解析；HTTPS 改写还可能需要证书信任。
- **Source Build / 源码构建**：需要编译防护工具本身，与修改目标 APK 是不同要求。


## 维护与许可

目录数据和说明文字采用 [CC BY 4.0](LICENSE-CONTENT)，生成与校验脚本采用 [MIT](LICENSE)。纠错线索请参阅 [CONTRIBUTING.zh-CN.md](CONTRIBUTING.zh-CN.md)。
