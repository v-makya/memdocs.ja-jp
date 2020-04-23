---
title: Microsoft Intune での Android Enterprise デバイスの問題解決
description: Intune に Android デバイスを登録するときに最も多く発生する問題のうち、一部の問題の解決方法を提案します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/25/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bcc524a69d0fb41da84a2e882b81a205fe7192cc
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "79363331"
---
# <a name="troubleshoot-android-enterprise-device-problems-in-microsoft-intune"></a>Microsoft Intune での Android Enterprise デバイスの問題解決

この記事は、Intune 管理者が Android Enterprise デバイスを Intune に登録するときに発生する問題を理解し、解決するのに役立ちます。

## <a name="apps-on-android-enterprise-devices"></a>Android Enterprise デバイス上のアプリ

### <a name="managed-google-play-apps-that-arent-deployed-through-intune-are-displayed-in-the-work-profile"></a>Intune 経由で配備されていないマネージド Google Play アプリが仕事用プロファイルに表示される
仕事用プロファイルの作成時、デバイス OEM がシステム アプリを仕事用プロファイルで有効にできます。 これは MDM プロバイダーが制御できることではありません。

次の手順で問題を解決します。

  1. ポータル サイトのログを集めます。
  2. 仕事用プロファイルに意図せず表示されるアプリをメモします。
  3. Intune からデバイスの登録を解除し、ポータル サイトをアンインストールします。
  4. [Test DPC](https://play.google.com/store/apps/details?id=com.afwsamples.testdpc) アプリをインストールします。このアプリでは、テスト目的で EMM なしで仕事用プロファイルを作成できます。
  5. [Test DPC](https://play.google.com/store/apps/details?id=com.afwsamples.testdpc) 内の指示に従い、デバイス上で仕事用プロファイルを作成します。
  6. 仕事用プロファイルに表示されるアプリを確認します。 
  7. 同じアプリが Test DPC アプリに表示されるようであれば、それは OEM の意思でそのデバイスにインストールされているアプリです。

### <a name="unapproved-managed-google-play-for-work-store-apps-arent-being-removed-from-the-client-apps-page-in-intune"></a>未承認のマネージド Google Play for Work ストア アプリが Intune の [クライアント アプリ] ページから削除されている
これは通常の動作です。

### <a name="managed-google-play-apps-arent-being-reported-under-the-discovered-apps-blade-in-the-intune-portal"></a>Intune ポータルの [検出されたアプリ] ブレードでマネージド Google Play アプリが報告されていない
これは通常の動作です。 仕事用プロファイルに取り込んであるシステム アプリのみが [検出されたアプリ] ブレードの一覧に入ります。 インストール済みのマネージド Google Play アプリは、 **[管理対象のアプリ]** ブレードで確認できます。

### <a name="are-web-applications-supported-for-work-profile-enrolled-devices"></a>Web アプリケーションは仕事用プロファイルに登録されたデバイスでサポートされていますか。
はい。 詳細については、「[マネージド Google Play Web リンク](../apps/apps-add-android-for-work.md#managed-google-play-web-links)」を参照してください。

## <a name="device-management"></a>デバイス管理

### <a name="file-path-internal-storageandroiddatacommicrosoftwindowsintunecompanyportalfiles-missing-on-work-profile-enrolled-devices"></a>仕事用プロファイルに登録されたデバイスに Internal storage/Android/Data.com.microsoft.windowsintune.companyportal/files というファイル パスがない

  **答え**:これは通常の動作です。 このパスは、デバイスの管理 (レガシ Android 登録) シナリオでのみ作成されます。

  ポータル サイト ログは次の手順で集めます。

  1. バッジが付いたポータル サイト アプリで、 **[メニュー]**  >  **[ヘルプ]**  >  **[メール サポート]** の順にタップし、 **[Send Email & Upload Logs]\(メールの送信 & ログのアップロード\)** をタップします。 
  2. **[ヘルプ要求の送信に使用するアプリ]** を選択するように求められたら、いずれかのメール アプリを選択します。
  3. IT 管理者宛の電子メールが作成されますが、そのメールには Microsoft 製品サポートに提供できるインシデント ID が含まれています。

### <a name="managed-google-play-last-sync-time--hasnt-been-updated-in-days"></a>マネージド Google Play の前回の同期時刻が数日間更新されていない
これは通常の動作です。 手動で行った場合にのみ、同期は始動します。

### <a name="encryption-is-required-when-a-device-is-enrolled-can-it-be-turned-off"></a>デバイスの登録時には暗号化が求められます。 これはオフにできますか。
いいえ。仕事用プロファイルの作成時にデバイスを暗号化することを Google は要求しています。 

### <a name="samsung-devices-are-blocking-the-use-of-third-party-keyboards-like-swiftkey"></a>Samsung のデバイスでは、SwiftKey のようなサードパーティ製キーボードの使用がブロックされます。
Samsung はこの制限を Android 8.0 以降のデバイスから強制適用しました。 Microsoft は現在、この問題に関して Samsung と協議しており、新しい情報が入り次第投稿します。

## <a name="remote-actions"></a>リモート操作

### <a name="wipe-factory-reset-option-isnt-available-for-work-profile-enrolled-device"></a>仕事用プロファイルに登録されたデバイスで [ワイプ (工場出荷時の設定へのリセット)] オプションを使用できない
これは通常の動作です。 仕事用プロファイル シナリオでは、MDM プロバイダーはデバイスを完全制御できません。 使用できる唯一のオプションは [インベントリから削除 (会社データを削除する)] です。仕事用プロファイル全体とそのすべての内容が削除されます。

### <a name="is-device-passcode-reset-supported"></a>デバイス パスコードをリセットできますか。
仕事用プロファイルに登録されたデバイスについては、次の場合にのみ、Android 8.0 以降で仕事用プロファイルのパスコードをリセットできます。
- 仕事用プロファイルのパスコードが管理されている
- エンド ユーザーからリセットが許可されている

専用デバイス (COSU) とフル マネージド デバイスの場合、デバイス パスコードをリセットできます。


## <a name="next-steps"></a>次のステップ

- [Intune のデバイス登録に関するトラブルシューティング](troubleshoot-device-enrollment-in-intune.md)
- [Intune フォーラムで質問する](https://social.technet.microsoft.com/Forums/%7Blang-locale%7D/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)
- [Microsoft Intune サポート チームのブログを読む](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Microsoft Enterprise Mobility and Security チームのブログを読む](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Announcing-the-public-preview-of-Azure-AD-group-based-license/ba-p/245210)