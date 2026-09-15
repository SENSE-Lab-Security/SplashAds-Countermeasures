# 🛡️ Splash Ads Countermeasures

<a href="README.zh-CN.md"><kbd>中文</kbd></a> <kbd>English</kbd>

**Splash ads, “shake-to-open” redirects, ads that suddenly launch Taobao or JD… what can you actually do about them?**

This project collects publicly documented **mobile advertising defenses**. Whether you are dealing with a splash ad, a shake-triggered redirect, or an ad that automatically opens another app, you can start from the problem you see and explore the available options.

Think of it as a **guide to mobile advertising defenses**: start with the problem you are facing, then see what options are available, what they require, and what their limitations are.

> [!NOTE]
> This project only organizes and cross-checks public information. It does not guarantee the safety, effectiveness, or compatibility of any defense. For defenses involving Accessibility, VPN/DNS, Root, LSPosed/Xposed, re-signing, or similar capabilities, use trusted sources only and understand the relevant permissions and risks.
>
> Last major verification pass: **2026-09-13**

## 🚀 Where should I start?

| What are you dealing with? | Start here |
| --- | --- |
| ⏭️ You have to wait through a splash ad whenever you open an app | [Automatically skip splash ads](#auto-skip-splash-ads) |
| 📳 A slight movement sends you to Taobao, JD, or another app | [Stop “shake / twist” redirects](#motion-redirects) |
| 🚫 You want to block ad requests or modify known ad responses/resources | [Block or modify ad resources](#ad-resources) |
| 🔗 The ad can stay visible, but you do not want it opening another app | [Prevent ad-triggered navigation](#ad-navigation) |
| ↩️ Another app has already opened and you want to return automatically | [Return after navigation](#post-navigation-recovery) |
| 🧩 You only want to remove ads from one particular app | [App-specific tools](#app-specific) |
| 🍎 You use an iPhone or iPad | [iOS options](#ios-options) |
| 🧑‍💻 You have Root / LSPosed and do not mind tinkering | [Advanced tools](#advanced-user-tools) |
| 📚 You want every entry and its full limitations | [Complete catalog](CATALOG.md) |

## 📱 Check your phone’s built-in controls first

Before installing a third-party tool, **check whether your phone already provides a relevant permission or navigation control**. This is usually the lowest-cost option.

- **Huawei devices**: some system versions let you restrict an app’s access to device orientation, which can reduce ad redirects triggered by motion sensors. See [Huawei: device orientation permission](entries/151.md).
- **vivo / iQOO**: some versions provide motion and orientation access controls, and some firmware can restrict access only during the splash period. See [vivo / iQOO: motion and orientation control](entries/149.md).
- **HONOR**: some models/versions provide sensor permissions or an automatic-navigation reminder. See [HONOR: automatic app navigation reminder](entries/153.md) and [HONOR: device sensor permission](entries/154.md).
- **OnePlus**: some versions provide motion-permission controls during app startup. See [OnePlus: startup motion permission](entries/166.md).

The exact menu and availability vary by brand, model, and system version. If your phone already provides a similar control, it is usually worth trying first.

<a id="auto-skip-splash-ads"></a>

## ⏭️ Automatically skip splash ads

**Best for:** You open an app and see a splash ad for a few seconds, usually with a **Skip / Close** button somewhere on the screen.

These defenses generally do not stop the ad itself from loading. Instead, they **find and press “Skip / Close” for you**. For Android users who do not want to Root their phone and simply want fewer buttons to press, this is one of the easiest categories to understand.

| Tool | In plain English | Platform | Deployment effort |
| --- | --- | --- | --- |
| [Li Tiaotiao](entries/005.md) | Uses Accessibility rules to automatically tap “Skip / Close” | Android | 🟢 Low effort |
| [GKD](entries/001.md) | Uses subscription rules to find and tap “Skip / Close” | Android | 🟡 Moderate effort |
| [SKIP](entries/002.md) | Uses local rules to handle splash ads automatically | Android | 🟢 Low effort |
| [ZeroStart](entries/006.md) | Tries offline OCR and other methods when the UI is difficult to recognize | Android | 🟢 Low effort |
| [PureSkip](entries/007.md) | Uses offline rules for supported splash ads | Android | 🔴 High effort |
| [SplashCleaner-Android](entries/008.md) | Looks for and taps a Skip / Close control only during a short startup window | Android | 🟢 Low effort |
| [madeye/ad-skipper](entries/009.md) | Can use OCR / YOLO / VLM to help locate the target when normal UI matching fails | Android | Built-in recognition 🟢 / additional VLM 🟡 |

**Good to know:** these defenses mainly “press Skip for you.” The ad may still load and appear first, and shake, swipe, or automatic redirects may still exist.

<a id="motion-redirects"></a>

## 📳 Stop “shake / twist” redirects

**Best for:** The ad may still be on screen, but simply picking up or slightly moving the phone—without any obvious intent to click—sends you to a shopping app or another page.

These defenses usually work in one of two ways: **prevent the app from receiving motion data normally**, or **stop the shake-related logic from continuing**.

| Defense | In plain English | Platform | Deployment effort |
| --- | --- | --- | --- |
| [NoShakingAD / Bu Xu Tiaozhuan](entries/016.md) | Temporarily restricts motion sensors during a short splash window | Android | 🟡 Moderate effort |
| [Fuck Shake](entries/015.md) | Stops shake-related logic inside the target app | Android | 🔴 High effort |
| [QzxyAdBlock](entries/024.md) | Handles ads and shake-triggered redirects in a specific app | Android | 🔴 High effort |

**These defenses do not automatically solve every ad problem.** Even after shake triggers are blocked, taps, swipes, large clickable areas, and other trigger paths may still exist.

<a id="ad-resources"></a>

## 🚫 Block or modify ad resources

**Best for:** You want to intervene earlier in the ad pipeline—before or while the app obtains usable ad content—instead of waiting for the ad to appear and then pressing “Skip.”

These defenses operate at the **resource stage**. Some use DNS, hosts files, or a local VPN to block known ad domains/requests; others do not block the request itself, but **modify returned data, remove ad fields, or prevent the app from reading cached ad data**. That is why this category is broader than simply “blocking ad loading.”

| Defense | In plain English | Platform | Deployment effort |
| --- | --- | --- | --- |
| [AdAway](entries/047.md) | Blocks known ad domains through hosts or a local VPN | Android | 🟢 Low effort (VPN) / 🔴 High effort (Root hosts) |
| [Rethink DNS + Firewall](entries/048.md) | Filters matching DNS requests and can combine this with a per-app firewall | Android | 🟢 Low effort |
| [Blokada 6 / Cloud](entries/127.md) | Filters known ad domains through DNS / cloud services | Cross-platform | 🟢 Low effort |
| [app2smile rules + Surge / Quantumult X](entries/108.md) | Rewrites selected ad API responses in compatible iOS clients | iOS | 🟡 Moderate effort |

**The limitation is straightforward:** effectiveness depends on the actual resource path. Ads that share a domain with normal content, are already cached or bundled into the app, use changed endpoints, rely on certificate pinning, or return an unmatched response format may still appear or continue running.

<a id="ad-navigation"></a>

## 🔗 Prevent ad-triggered navigation

**Best for:** You can tolerate the ad being visible, but you do not want one accidental trigger to send you to Taobao, JD, a browser, or another app.

These defenses operate at the **navigation stage**: they may rewrite destination links, prevent certain pages/apps from being opened, or add a confirmation step before a cross-app redirect.

| Defense | In plain English | Platform | Deployment effort |
| --- | --- | --- | --- |
| [FuckAdJump](entries/106.md) | Makes selected Taobao / JD deep links fail | Android | 🔴 High effort |
| [HONOR automatic-navigation reminder](entries/153.md) | Adds a system reminder for suspected accidental ad redirects | Android | 🟢 Low effort |

When navigation passes through the relevant interception point, these defenses do not need to care whether the upstream trigger was a tap, swipe, shake, or something else. Coverage still depends on which links and launch paths the defense can actually intercept.

<a id="post-navigation-recovery"></a>

## ↩️ Return after navigation

**Best for:** The redirect has already happened, and you want the defense to take you back to the original app as quickly as possible and shorten the interruption.

| Defense | In plain English | Platform | Deployment effort |
| --- | --- | --- | --- |
| [ShakeGuard](entries/018.md) | Detects a matching foreground-app transition after navigation and attempts a Back / return action | Android | 🔴 High effort |

This category is deliberately separate from “preventing navigation”: **the destination app has already opened when it intervenes**. It therefore cannot undo pages already shown or network requests already sent, and it cannot guarantee restoration of the exact page state in the original app.

<a id="app-specific"></a>

## 🧩 Tools for specific apps

Another large group of tools does not try to work across every app. Instead, each one targets **a particular app or a small number of apps**.

For example:

- [MiFitnessAdAway](entries/026.md) targets Xiaomi Fitness / Health.
- [bili-hook](entries/027.md) targets specific Bilibili versions.
- [CoolApkNoSplash](entries/020.md) targets known CoolApk splash paths.
- [XTA-AdKiller](entries/025.md) targets several ad interfaces in Super Curriculum Table.
- [GmailHideAds](entries/032.md) targets Sponsored rows in Gmail.
- [Play Store Adblock](entries/029.md) targets Sponsored / promoted content in Google Play.

These tools are usually **narrowly adapted to specific apps and versions**. That specificity does not mean they have been uniformly tested across every supported version. An app update can break the existing adaptation.

<a id="ios-options"></a>

## 🍎 What can you do on iOS?

Compared with Android, iOS gives third-party tools less room to directly modify the behavior of other apps. Common approaches therefore include **proxy / DNS / Rewrite rules**, along with controls provided by the system or browser itself.

You can start with:

- [app2smile ad network rules + Surge / Quantumult X](entries/108.md)
- [blackmatrix7 startup](entries/125.md)
- [R-Store](entries/136.md)
- [Moyu Rewrite](entries/138.md)
- [iOS browser app launching and link routing](entries/167.md)
- [iOS URL Filter](entries/168.md)

Some of these require proxy configuration, certificates, or rule imports; they are not ordinary apps that simply work immediately after installation.

<a id="advanced-user-tools"></a>

## 🧑‍💻 Advanced tools

If you are already familiar with **Root / Magisk, runtime injection frameworks such as LSPosed / Xposed, and APK modification**, many more options become available. These tools can reach into app internals, ad SDKs, Activities / Intents, or sensor callbacks.

Common examples include:

- [Fuck Shake](entries/015.md)
- [AdPopupBlocker](entries/021.md)
- [LiTianSuo](entries/028.md)
- [FuckAdJump](entries/106.md)
- [Adobo advertising patches](entries/119.md)
- [DTL-X rmads](entries/120.md)

These defenses also come with higher maintenance and security costs: version updates, code obfuscation, signature checks, and Root detection can all affect availability.

## 🏢 What can ad platforms and app developers do?

The repository also records **defensive controls available to developers or ad platforms**. These are not tools for ordinary users to install directly; they are configuration options exposed to developers by ad SDKs or platforms.

For example, some SDKs let developers disable shake, rotation, or other motion interactions:

- [GroMore Android](entries/141.md)
- [Sigmob Android](entries/143.md)
- [Sigmob iOS](entries/145.md)
- [Taku Android](entries/146.md)
- [Taku iOS](entries/147.md)
- [Tencent GDT Android](entries/150.md)
- [Kuaishou iOS](entries/152.md)

For ordinary users, the point of these entries is not to “download the SDK,” but to understand that **many ad interactions can be configured or disabled by app developers.**

## 🧭 Deployment effort

- **🟢 Low effort**: install and authorize a ready-to-use app/service, or enable an existing system setting.
- **🟡 Moderate effort**: requires extra setup, such as importing rules, installing a certificate, debugging pairing, selecting a region, or installing a modified app provided by the project.
- **🔴 High effort**: requires Root / jailbreak, runtime injection, APK modification, or source compilation.

## 📚 Complete catalog

If you want to see:

- all currently recorded entries;
- the full limitations for each entry;
- historical projects that have not yet been fully verified;
- system capabilities, developer settings, and research prototypes;

see the **[complete catalog](CATALOG.md)**.

Each entry also has its own detail page, with its working method, applicable scenarios, deployment requirements, limitations, and original source.

## 🤝 Corrections and contributions

Advertising defenses and system versions change quickly, and app updates can also break old rules. If you notice:

- a project has stopped or resumed maintenance;
- a link is broken;
- an entry does not match what the defense actually does;
- a new advertising defense is worth including;

please see [CONTRIBUTING.md](CONTRIBUTING.md) and submit a correction or source.

## 📄 License

Catalog data and explanatory text are licensed under [CC BY 4.0](LICENSE-CONTENT); generation and validation scripts are licensed under [MIT](LICENSE).
