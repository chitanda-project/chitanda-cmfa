<div align="center">

<img src="https://raw.githubusercontent.com/chitanda-project/chitanda/main/public/avatar.webp" alt="Chitanda" width="120" />

# 🌸 Chitanda CMFA (Chitanda for Android)

**次世代 Android 向け高性能プロキシクライアント**

[![Release](https://img.shields.io/github/v/release/chitanda-project/chitanda-cmfa?color=green&style=flat-square)](https://github.com/chitanda-project/chitanda-cmfa/releases)
[![Build](https://github.com/chitanda-project/chitanda-cmfa/actions/workflows/build-release.yaml/badge.svg)](https://github.com/chitanda-project/chitanda-cmfa/actions)
[![Official Website](https://img.shields.io/badge/Official-chitanda.net-blue?style=flat-square)](https://chitanda.net)

<p align="center">
  <b>Chitanda CMFA</b> は、Android 端末向けに最適化された公式プロキシクライアントです。<br>
  次世代プロキシコア <b><a href="https://github.com/chitanda-project/chitanda">Chitanda Core (Mihomo)</a></b> を内蔵し、ネイティブ <b>Chitanda プロトコル</b> による超高速・低遅延なセキュア通信を提供します。
</p>

</div>

> [!WARNING]
> ### ⚠️ 免責事項 (Disclaimer)
> 本プロジェクトおよび関連リソースは、学術研究、ネットワークセキュリティ検証、および正当な管理運用を目的として公開・提供されています。
> 
> 1. **法令遵守の義務**：本ソフトウェアおよび関連コードを利用する際は、**必ずご利用者ご自身の所在国・地域の法令および規則を遵守してください**。
> 2. **利用の禁止**：本ソフトウェアの利用が所在国または地域の法令・規則に違反する場合、**いかなる目的であっても本ソフトウェアのダウンロード、インストール、実行、および二次配布を行わないでください**。
> 3. **免責条項**：開発者およびプロジェクト保守管理者は、本ソフトウェアの使用、誤用、またはそれに関連して生じたいかなる損害、法的紛争、および責任についても一切の責任を負いません。

---

### Requirement

- Android 5.0+ (minimum)
- Android 7.0+ (recommend)
- `armeabi-v7a` , `arm64-v8a`, `x86` or `x86_64` Architecture

### Build

1. Update submodules

   ```bash
   git submodule update --init --recursive
   ```

2. Install **OpenJDK 11**, **Android SDK**, **CMake** and **Golang**

3. Create `local.properties` in project root with

   ```properties
   sdk.dir=/path/to/android-sdk
   ```

4. (Optional) Custom app package name. Add the following configuration to `local.properties`.

   ```properties
   # config your ownn applicationId, or it will be 'com.github.metacubex.clash'
   custom.application.id=com.my.compile.clash
   # remove application id suffix, or the applicaion id will be 'com.github.metacubex.clash.alpha'
   remove.suffix=true

5. Create `signing.properties` in project root with

   ```properties
   keystore.path=/path/to/keystore/file
   keystore.password=<key store password>
   key.alias=<key alias>
   key.password=<key password>
   ```

6. Build

   ```bash
   ./gradlew app:assembleAlphaRelease
   ```

### Automation

APP package name is `com.github.metacubex.clash.meta`

- Toggle Clash.Meta service status
  - Send intent to activity `com.github.kr328.clash.ExternalControlActivity` with action `com.github.metacubex.clash.meta.action.TOGGLE_CLASH`
- Start Clash.Meta service
  - Send intent to activity `com.github.kr328.clash.ExternalControlActivity` with action `com.github.metacubex.clash.meta.action.START_CLASH`
- Stop Clash.Meta service
  - Send intent to activity `com.github.kr328.clash.ExternalControlActivity` with action `com.github.metacubex.clash.meta.action.STOP_CLASH`
- Import a profile
  - URL Scheme `clash://install-config?url=<encoded URI>` or `clashmeta://install-config?url=<encoded URI>`

### Contribution and Project Maintenance

#### Meta Kernel

- CMFA uses the kernel from `android-real` branch under `MetaCubeX/Clash.Meta`, which is a merge of the main `Alpha` branch and `android-open`.
  - If you want to contribute to the kernel, make PRs to `Alpha` branch of the Meta kernel repository.
  - If you want to contribute Android-specific patches to the kernel, make PRs to  `android-open` branch of the Meta kernel repository.

#### Maintenance

- When `MetaCubeX/Clash.Meta` kernel is updated to a new version, the `Update Dependencies` actions in this repo will be triggered automatically.
  - It will pull the new version of the meta kernel, update all the golang dependencies, and create a PR without manual intervention.
  - If there is any compile error in PR, you need to fix it before merging. Alternatively, you may merge the PR directly.
- Manually triggering `Build Pre-Release` actions will compile and publish a `PreRelease` version.
- Manually triggering `Build Release` actions will compile, tag and publish a `Release` version.
  - You must fill the blank `Release Tag` with the tag you want to release in the format of `v1.2.3`.
  - `versionName` and `versionCode` in `build.gradle.kts` will be automatically bumped to the tag you filled above.
