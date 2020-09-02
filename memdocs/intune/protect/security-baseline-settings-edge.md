---
title: Microsoft Edge 用の Intune セキュリティ ベースラインの設定
titleSuffix: Microsoft Intune
description: Microsoft Edge ブラウザーを管理するために、Intune でサポートされるセキュリティ ベースラインの設定
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
zone_pivot_groups: edge-baseline-versions
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8fd6943be69f66d4cd6fde2e9c08bec9323005a5
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914431"
---
<!-- Pivots in use: 
::: zone pivot="edge-october-2019"
::: zone-end

::: zone pivot="edge-april-2020"
::: zone-end

::: zone pivot="edge-october-2019,edge-april-2020"
::: zone-end
-->

# <a name="microsoft-edge-baseline-settings-for-intune"></a>Intune 用の Microsoft Edge ベースラインの設定

Microsoft Intune でサポートされている Microsoft Edge Web ブラウザーのベースラインの設定を確認します。 Microsoft Edge ベースラインの既定値は、Microsoft Edge ブラウザーの推奨される構成を表しており、他のセキュリティ ベースラインのベースラインの既定値と一致しない場合があります。

::: zone pivot="edge-october-2019"

> [!NOTE]
> 2019 年 10 月の Microsoft Edge のベースラインは、パブリック プレビュー段階にあります。

::: zone-end
::: zone pivot="edge-april-2020"

以前のバージョンからのこのバージョンのベースラインの変更点を確認するには、このベースラインの *[バージョン]* ウィンドウを表示すると使用可能になる [[ベースラインの比較]](../protect/security-baselines.md#compare-baseline-versions) 操作を使用します。 以前のバージョンからのこのバージョンのベースラインの変更点を確認するには、このベースラインの *[バージョン]* ウィンドウを表示すると使用可能になる [[ベースラインの比較]](../protect/security-baselines.md#compare-baseline-versions) 操作を使用します。

::: zone-end
::: zone pivot="edge-october-2019,edge-april-2020"

## <a name="microsoft-edge"></a>Microsoft Edge

::: zone-end
::: zone pivot="edge-april-2020"

- **サポートされている認証スキーム**  
  サポートする HTTP 認証スキームを指定します。 ポリシーを構成するには、*basic*、*digest*、*ntlm*、*negotiate* のいずれかの値を使用します。 複数の値はコンマで区切ります。 このポリシーを構成しないと、4 つのスキームがすべて使用されます。

  - **有効** (*既定*) - 選択したスキームが使用されます。
  - **[無効]**
  - **未構成** - 4 つすべてのスキームが使用されます。
  
  *[有効]* に設定した場合、次の設定を構成して、使用する認証を選択できます。

  - **サポートされている認証スキーム**  
    次のオプションから選択します。
    - **基本**
    - **ダイジェスト**
    - **NTLM** *(既定で選択されます)*
    - **ネゴシエート** *(既定で選択されます)*

- **既定の Adobe Flash 設定**  
  CSP:[Browser/AllowFlash](/windows/client-management/mdm/policy-csp-browser#browser-allowflash)、[Browser/AllowFlashClickToRun](/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)

  次の設定へのアクセスを有効にして、Adobe Flash プラグインを実行するための動作を構成できます。  

  - **有効** (*既定*)
  - **[無効]**
  - **未構成**

  *[有効]* に設定すると、次の設定を構成できます。

  - **既定の Adobe Flash 設定**

    - **Adobe Flash プラグインをブロックする** (*既定*) - すべてのサイトで Adobe Flash をブロックします
    - **クリックして再生** - Adobe Flash が実行されますが、ユーザーはそれを起動するためのオプションを選択する必要があります。

- **インストールできない拡張機能の制御**  
  ユーザーが Microsoft Edge にインストールできない拡張機能を指定するリストの使用を有効にします。 リストが使用されている場合、以前にインストールされたリストの設定はすべて無効になり、ユーザーはそれらを有効にできません。 ブロックする拡張機能のリストから項目を削除すると、その拡張機能は、以前にインストールされていたすべての場所で自動的に再度有効になります。

  - **有効** (*既定*) - 拡張機能をブロックするためにリストの使用を有効にします。
  - **[無効]**
  - **未構成** - ユーザーは任意の拡張機能を Microsoft Edge にインストールできます。
  
  *[有効]* に設定すると、ブロックする拡張機能のリストを定義する次の設定を構成できます。

  - **ユーザーがインストールできないようする必要のある拡張機能の ID (すべての場合は *)**

    **[追加]** を選択し、追加の拡張機能を指定します。 **\*** は既定で選択されています。

- **ユーザーレベルのネイティブ メッセージング ホストを許可する (管理者権限なしでインストールされる)**  
  ネイティブ メッセージング ホストのユーザー レベルのインストールを有効にします。

  - **Enabled**
  - **無効** (*既定*) - Microsoft Edge では、システム レベルでインストールされているネイティブ メッセージング ホストのみが使用されます。
  - **未構成** - 既定で、Microsoft Edge では、ユーザーレベルのネイティブ メッセージング ホストを使用できます。

- **パスワード マネージャーへのパスワードの保存を有効にする**  
  Microsoft Edge CSP: [Browser/AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Microsoft Edge でユーザー パスワードを保存できるようにします。

  - **有効** - ユーザーは Microsoft Edge でパスワードを保存できます。 次回サイトにアクセスしたときには、Microsoft Edge でパスワードが自動的に入力されます。 ユーザーは、Microsoft Edge でこのポリシーを変更または上書きできません。
  - **無効** (*既定*) - ユーザーは新しいパスワードを保存できませんが、以前に保存したパスワードを使用し続けることができます。 ユーザーは、Microsoft Edge でこのポリシーを変更または上書きできません。
  - **未構成** - ユーザーはパスワードを保存でき、この機能をオフにできます。

- **サイトの Microsoft Defender SmartScreen プロンプトをバイパスしない**  
  CSP:[Browser/PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  悪意のある可能性がある Web サイトに関する Microsoft Defender SmartScreen の警告をユーザーがオーバーライドできるかどうかを決定できます。

  - **有効** (*既定*) - ユーザーは Microsoft Defender SmartScreen の警告を無視できず、サイトへの移動をブロックされます。
  - **無効** - ユーザーは Microsoft Defender SmartScreen の警告を無視することができ、サイトに移動できます。
  - **未構成** - ユーザーは Microsoft Defender SmartScreen の警告を無視することができ、サイトに移動できます

- **ダウンロードに関する Microsoft Defender SmartScreen の警告をバイパスしない**  
  CSP:[Browser/PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  未確認のダウンロードに関する Microsoft Defender SmartScreen の警告をユーザーがオーバーライドできるかどうかを指定します。

  - **有効** (*既定*) - ユーザーは Microsoft Defender SmartScreen 警告を無視できず、未確認のダウンロードを完了できません。
  - **無効** - ユーザーは Microsoft Defender SmartScreen の警告を無視することができ、未確認のダウンロードを完了できます。
  - **未構成** - ユーザーは Microsoft Defender SmartScreen の警告を無視することができ、未確認のダウンロードを完了できます。

- **すべてのサイトでサイト分離を有効にする**  
  サイト分離を構成して、すべてのサイトを分離する既定の動作をユーザーがオプトアウトするのを防ぎます。
  
  - **有効** (*既定*) - 各サイトが独自のプロセスで実行される既定の動作を、ユーザーはオプトアウトできません。
  - **無効** - ユーザーはサイト分離をオプトアウトできます。 サイト分離はオフになっていません。
  - **未構成** - ユーザーはサイト分離をオプトアウトできます。 サイト分離はオフになっていません。

  Microsoft Edge では、[IsolateOrigins](/deployedge/microsoft-edge-policies#isolateorigins) ポリシーがサポートされており、さらに細かいオリジンを分離することもできます。  Intune では、IsolateOrigins ポリシーの構成がサポートされていません。
  
- **Microsoft Defender SmartScreen の構成**  
  CSP:[Browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)  
  
  Microsoft Defender SmartScreen では、ユーザーをフィッシング詐欺や悪意のあるソフトウェアから保護するのに役立つ警告メッセージが提供されます。 既定では、Microsoft Defender SmartScreen は有効になっています。
  
  - **有効** (*既定*) - Microsoft Defender SmartScreen は有効になり、ユーザーはこれを無効にできません。
  - **無効** - Microsoft Defender SmartScreen は無効になり、ユーザーはこれを有効にできません。
  - **未構成** - ユーザーは Microsoft Defender SmartScreen を使用するかどうかを選択できます。

  このポリシーは、Microsoft Active Director ドメインに参加している Windows インスタンス、あるいはデバイス管理用に登録されている Windows 10 Pro または Enterprise インスタンスでのみ使用できます。

- **望ましくない可能性のあるアプリをブロックするよう Microsoft Defender SmartScreen を構成する**  
    望ましくない可能性のあるアプリをブロックするために Microsoft Defender SmartScreen の動作を構成します。 Microsoft Defender SmartScreen では、Web サイトでホストされているアドウェア、コイン マイナー、バンドルウェア、その他の低評価のアプリからユーザーを保護するのに役立つ警告メッセージを提供できます。 Microsoft Defender SmartScreen における望ましくない可能性のあるアプリのブロックは既定で無効になります。

  - **有効** (*既定*) - 望ましくない可能性のあるアプリがブロックされます。
  - **無効** - 望ましくない可能性のあるアプリがブロックされません。
  - **未構成** - ユーザーは Microsoft Defender SmartScreen で望ましくない可能性のあるアプリのブロックを使用するかどうかを選択できます。

  このポリシーは、Microsoft Active Director ドメインに参加している Windows インスタンス、あるいはデバイス管理用に登録されている Windows 10 Pro または Enterprise インスタンスでのみ使用できます。

- **SSL 警告ページから続行することをユーザーに許可する**  
   CSP:[Browser/PreventCertErrorOverrides](/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  ユーザーが SSL エラーのあるサイトにアクセスすると、Microsoft Edge で警告ページが表示されます。
  - **有効** - ユーザーは警告ページをクリックして進むことができます。
  - **無効** (*既定*) - ユーザーはすべての警告ページをクリックして進むことがブロックされます。
  - **未構成** - ユーザーはこれらの警告ページをクリックして進むことができます。

- **SSL の最小バージョンが有効**  
  サポートされる最小バージョンの SSL を設定するオプションを有効にします。

  - **有効** (*既定*) - 使用する最小バージョンの TLS を指定する次の設定へのアクセスを有効にします。
  - **[無効]**
  - **未構成** - Microsoft Edge では既定の最小バージョンの *TLS 1.0* が使用されます。

  *[有効]* に設定すると、次の設定を使用して、TLS を構成できます。

  - **[SSL の最小バージョンが有効]** 使用する TLS の最小バージョンを設定します。 Microsoft Edge では、指定したバージョンよりも古いすべてのバージョンの SSL/TLS が使用されません。
    - **TLS 1.0**
    - **TLS 1.1**
    - **TLS 1.2** (*既定*)

::: zone-end

::: zone pivot="edge-october-2019"

- **サイトの Microsoft Defender SmartScreen プロンプトをバイパスしない**  
  **既定値**:Enabled  
  Microsoft Edge CSP: [Browser/PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  このポリシー設定では、悪意のある可能性がある Web サイトに関する Microsoft Defender SmartScreen の警告をユーザーがオーバーライドできるかどうかを決定できます。 
  - この設定を有効にすると、ユーザーは Microsoft Defender SmartScreen の警告を無視できず、サイトへの移動をブロックされます。 
  - この設定を無効にするか構成しないと、ユーザーは Microsoft Defender SmartScreen の警告を無視することができ、サイトに移動できます。

- **SSL の最小バージョンが有効**  
  **既定値**:Enabled  

  サポートされる最小バージョンの SSL を設定します。 このポリシーを "*未構成*" に設定すると、Microsoft Edge では既定の最小バージョン *TLS 1.0* が使用されます。 "*有効*" に設定したときは、次の値から最小バージョンを選択できます。

  - TLS 1.0
  - TLS 1.1
  - TLS 1.2

  - **SSL の最小バージョンが有効**  
    **既定値**:TLS 1.2

- **ダウンロードに関する Microsoft Defender SmartScreen の警告をバイパスしない**  
  **既定値**:Enabled  
  Microsoft Edge CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  このポリシーを使用すると、未確認のダウンロードに関する Microsoft Defender SmartScreen の警告をユーザーがオーバーライドできるかどうかを指定できます。
  - このポリシーを有効にすると、組織内のユーザーは Microsoft Defender SmartScreen 警告を無視できず、未確認のダウンロードを完了できません。
  - このポリシーを無効にするか構成しないと、ユーザーは Microsoft Defender SmartScreen の警告を無視することができ、未確認のダウンロードを完了できます。

- **SSL 警告ページから続行することをユーザーに許可する**  
  **既定値**:無効  
  Microsoft Edge CSP: [Browser/PreventCertErrorOverrides](/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  ユーザーが SSL エラーのあるサイトにアクセスすると、Microsoft Edge で警告ページが表示されます。 このポリシーを "*有効*" または "*未構成*" に設定すると、ユーザーはこれらの警告ページをクリックして通過できます。 このポリシーを "*無効*" にすると、ユーザーは警告ページを通過できなくなります。 

- **既定の Adobe Flash 設定**  
  **既定値**:Enabled  
  Microsoft Edge CSP: [Browser/AllowFlash](/windows/client-management/mdm/policy-csp-browser#browser-allowflash)、[Browser/AllowFlashClickToRun](/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)  

  "PluginsAllowedForUrls" または "PluginsBlockedForUrls" でカバーされていない Web サイトで Adobe Flash プラグインを自動的に実行できるかどうかを指定します。 

  - "BlockPlugins" を選択すると、すべてのサイトで Adobe Flash がブロックされます
  - "ClickToPlay" を選択すると、Adobe Flash を実行できますが、開始するにはユーザーがプレースホルダーをクリックする必要があります。
  
  どのような場合でも、"PluginsAllowedForUrls" および "PluginsBlockedForUrls" ポリシーは "DefaultPluginsSetting" より優先されます。 自動再生は、"PluginsAllowedForUrls" ポリシーで明示的にリストされているドメインに対してのみ許可されます。 
   すべてのサイトで自動再生を有効にする場合は、このリストに http://* と https://* を追加することを検討してください。

  - このポリシーを "*未構成*" に設定すると、ユーザーはこの設定を手動で変更できます。 * 2 = Adobe Flash プラグインをブロックする、* 3 = クリックして再生する、以前の "1" オプションでは "すべて許可" に設定されますが、この機能は現在は "PluginsAllowedForUrls" ポリシーによってのみ処理されます。 "1" を使用している既存のポリシーは、"クリックして再生" モードで動作します。  

  - **既定の Adobe Flash 設定**  
    **既定値**:Adobe Flash プラグインをブロックする

- **すべてのサイトでサイト分離を有効にする**  
  **既定値**:Enabled  

  "SitePerProcess" ポリシーを使用すると、すべてのサイトを分離する既定の動作をユーザーがオプトアウトするのを防ぐことができます。 また、IsolateOrigins ポリシーを使用して、さらに細かいオリジンを分離することもできます。

  - このポリシーを "*有効*" に設定すると、各サイトが独自のプロセスで実行される既定の動作を、ユーザーはオプトアウトできません。 
  - "*無効*" または "*未構成*" を使用すると、ユーザーはサイトの分離をオプトアウトできます。 (たとえば、edge://flags で "Disable site isolation" (サイトの分離を無効にする) エントリを使用することにより)。ポリシーを無効にしたり、構成しなかったりしても、サイトの分離は無効になりません。

- **サポートされている認証スキーム**  
  **既定値**:Enabled  

  サポートする HTTP 認証スキームを指定します。 ポリシーを構成するには、"basic"、"digest"、"ntlm"、"negotiate" のいずれかの値を使用します。 複数の値はコンマで区切ります。 このポリシーを構成しないと、4 つのスキームがすべて使用されます。

  - **サポートされている認証スキーム**  
    次のオプションから選択します。
    - 基本
    - ダイジェスト
    - NTLM *(既定で選択されています)*
    - ネゴシエート *(既定で選択されます)*

- **パスワード マネージャーへのパスワードの保存を有効にする**  
  **既定値**:無効  
  Microsoft Edge CSP: [Browser/AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Microsoft Edge でユーザー パスワードを保存できるようにします。
  - このポリシーを有効にすると、ユーザーは Microsoft Edge でパスワードを保存できます。 次回サイトにアクセスしたときには、Microsoft Edge でパスワードが自動的に入力されます。
  - このポリシーを無効にすると、ユーザーは新しいパスワードを保存できませんが、以前に保存したパスワードを使用することはできます。
  
  このポリシーを "*有効*" または "*無効*" にすると、ユーザーは Microsoft Edge でこのポリシーを変更またはオーバーライドできません。
  
  これを "*未構成*" に設定すると、ユーザーはパスワードを保存でき、この機能をオフにすることもできます。

- **インストールできない拡張機能の制御**  
  **既定値**:Enabled  

  ユーザーが Microsoft Edge にインストールできない特定の拡張機能のリストを指定します。 このポリシーを展開すると、このリストに含まれる拡張機能で以前にインストールされたものはすべて無効になり、ユーザーはこれらの拡張機能を有効にできなくなります。 ブロックする拡張機能のリストから項目を削除すると、その拡張機能は、以前にインストールされていたすべての場所で自動的に再度有効になります。
  
  許可リストに明示的に記載されていないすべての拡張機能をブロックするには、 **\*** を使用します。 このポリシーを "*未構成*" に設定すると、ユーザーは任意の拡張機能を Microsoft Edge にインストールできます。
  
  値の例: extension_id1 extension_id2。  
  <br>
  - **ユーザーがインストールできないようする必要のある拡張機能の ID (すべての場合は *)**  
    **[追加]** を選択し、追加の拡張機能を指定します。 **\*** は既定で選択されています。

- **Microsoft Defender SmartScreen の構成**  
  **既定値**:Enabled  
  Microsoft Edge CSP: [Browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  このポリシー設定を使用すると、Microsoft Defender SmartScreen を有効にするかどうかを構成できます。 Microsoft Defender SmartScreen では、ユーザーをフィッシング詐欺や悪意のあるソフトウェアから保護するのに役立つ警告メッセージが提供されます。
  
  - 既定では、Microsoft Defender SmartScreen は有効になっています。 この設定を有効にすると、Microsoft Defender SmartScreen は有効になり、ユーザーはこれを無効にできません。
  - この設定を無効にすると、Microsoft Defender SmartScreen は無効になり、ユーザーはこれを有効にできません。
  - "*未構成*" に設定すると、ユーザーは Microsoft Defender SmartScreen を使用するかどうかを選択できます。
  
  このポリシーは、Microsoft Active Director ドメインに参加している Windows インスタンス、あるいはデバイス管理用に登録されている Windows 10 Pro または Enterprise インスタンスでのみ使用できます。

- **ユーザーレベルのネイティブ メッセージング ホストを許可する (管理者権限なしでインストールされる)**  
  **既定値**:無効

  ネイティブ メッセージング ホストのユーザー レベルのインストールを有効にします。 
  - このポリシーを無効にすると、Microsoft Edge では、システム レベルでインストールされているネイティブ メッセージング ホストのみが使用されます。 このポリシーを構成しないと、既定では、Microsoft Edge でユーザー レベルのネイティブ メッセージング ホストの使用が許可されます。

::: zone-end

## <a name="next-steps"></a>次のステップ

- [セキュリティ ベースラインに関する詳細](security-baselines.md)
- [競合を回避する](security-baselines.md#avoid-conflicts)
- [Intune でのポリシーとプロファイルのトラブルシューティング](../configuration/troubleshoot-policies-in-microsoft-intune.md)