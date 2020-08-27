---
title: Windows 自動操縦用自己展開モード
description: 自己展開モードでは、ユーザーの操作なしでデバイスを展開できます。 このモードモードは、キオスク、デジタル看板デバイス、または共有デバイスとして Windows 10 を展開するように設計されています。
keywords: MDM, セットアップ, Windows, Windows 10, OOBE, 管理, 展開, Autopilot, ZTD, ゼロタッチ, パートナー, MSFB, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 5ab51eda0791d42ed49b90e97b25ee66ee72c6dc
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907950"
---
# <a name="windows-autopilot-self-deploying-mode"></a>Windows 自動操縦用自己展開モード

**適用対象: Windows 10 バージョン1903以降**

Windows 自動操縦の自己展開モードでは、ユーザーの操作なしでデバイスを展開できます。 イーサネット接続を使用するデバイスの場合、ユーザー操作は必要ありません。wi-fi 経由で接続されているデバイスの場合、Wi-fi 接続を作成した後 (言語、ロケール、キーボードを選択し、ネットワーク接続を作成した後)、操作は必要ありません。  

自己展開モードでは、デバイスを Azure Active Directory に参加させ、Intune (または別の MDM サービス) にデバイスを登録して、MDM の自動登録に Azure AD を使用します。また、デバイスが完全にプロビジョニングされるまで、[登録のステータス] ページを使用してデスクトップにアクセスできないようにします。 

>[!NOTE]
>自己展開モードでは Active Directory Join または Hybrid Azure AD Join はサポートされません。  すべてのデバイスが Azure Active Directory に参加します。

自己展開モードは、キオスク、デジタル看板デバイス、または共有デバイスとして Windows 10 を展開するように設計されています。 キオスクをセットアップするときに、Microsoft Edge 上に構築されたアプリである新しいキオスクブラウザーを利用できます。これを使用して、カスタマイズされた MDM で管理された閲覧エクスペリエンスを作成できます。 MDM ポリシーと組み合わせてローカルアカウントを作成し、自動的にログオンするように構成すると、デバイスの完全な構成を自動化できます。 これらのオプションの詳細については、「Windows 10 でのキオスク管理の簡素化」を参照してください。  詳細については [、「Intune またはその他の MDM サービスでのキオスクまたはデジタルサインインのセットアップ](/windows/configuration/setup-kiosk-digital-signage#set-up-a-kiosk-or-digital-sign-in-intune-or-other-mdm-service) 」を参照してください。

>[!NOTE]
>現在、自己展開モードでは、ユーザーがデバイスに関連付けられていません (プロセスの一部としてユーザー ID またはパスワードが指定されていないため)。  その結果、一部の Azure AD と Intune の機能 (BitLocker の回復、ポータルサイトからのアプリのインストール、条件付きアクセスなど) は、デバイスにサインインしているユーザーが使用できなくなる可能性があります。 詳細については、「 [Windows 自動操縦のシナリオと機能](windows-autopilot-scenarios.md) 」および「 [自動操縦用デバイスの BitLocker 暗号化アルゴリズムの設定](bitlocker.md)」を参照してください。

![Windows 自動操縦用自己展開モードのユーザーエクスペリエンス](images/self-deploy-welcome.png)

## <a name="requirements"></a>必要条件

自己展開モードでは、デバイスの TPM 2.0 ハードウェアを使用して、組織の Azure AD テナントにデバイスを認証するため、TPM 2.0 のないデバイスをこのモードで使用することはできません。  デバイスでは、TPM デバイスの構成証明もサポートする必要があります。  (新しく製造したすべての Windows デバイスは、これらの要件を満たしている必要があります)。

>[!IMPORTANT]
>TPM 2.0 をサポートしていないデバイスまたは仮想マシン上で、自己展開モードの展開を実行しようとすると、0x800705B4 タイムアウトエラー (Hyper-v 仮想 Tpm はサポートされていません) を使用してデバイスを検証するときに、プロセスが失敗します。 また、Windows 10 version 1809 での TPM デバイスの構成証明の問題により、自己展開モードを使用するには、Windows 10 バージョン1903以降が必要であることにも注意してください。 Windows 10 Enterprise 2019 LTSC は Windows 10 バージョン1809に基づいているため、自己展開モードは Windows 10 Enterprise 2019 LTSC でもサポートされていません。 他の既知のエラーと解決策については、「 [Windows 自動操縦の既知の問題](known-issues.md) 」を参照してください。

自動操縦プロセス中に組織固有のロゴと組織名を表示するには、表示するイメージとテキストを使用して Azure Active Directory 企業ブランドを構成する必要があります。  詳細については [、「クイックスタート: Azure AD のサインインページに会社のブランドを追加する](/azure/active-directory/fundamentals/customize-branding) 」を参照してください。 

## <a name="step-by-step"></a>ステップ バイ ステップ

Windows 自動操縦を使用して自己展開モードの展開を実行するには、次の準備手順を完了する必要があります。

-   必要な設定を使用して、自己展開モード用の自動操縦プロファイルを作成します。  Microsoft Intune では、プロファイルの作成時にこのモードが明示的に選択されます。 (セルフ展開モードでは、ビジネス向けまたはパートナーセンターの Microsoft Store でプロファイルを作成することはできません)。
-   Intune を使用している場合は Azure Active Directory でデバイスグループを作成し、そのグループに自動操縦プロファイルを割り当てます。  デバイスの展開を試行する前に、プロファイルがデバイスに割り当てられていることを確認してください。
-   デバイスを起動し、必要に応じて Wi-fi に接続してから、プロビジョニング処理が完了するまで待ちます。

## <a name="validation"></a>検証

Windows 自動操縦機能を使用して自己展開モードの展開を実行する場合は、次のエンドユーザーエクスペリエンスを確認する必要があります。

-   ネットワークに接続すると、自動操縦プロファイルがダウンロードされます。
-   自動操縦プロファイルが、言語、ロケール、およびキーボードレイアウトを自動的に構成するように構成されている場合は、イーサネット接続が使用可能であれば、これらの OOBE 画面をスキップする必要があります。  それ以外の場合は、手動の手順が必要です。
    -   Windows 10 に複数の言語がプレインストールされている場合、ユーザーは言語を選択する必要があります。
    -   ユーザーは、ロケールとキーボードレイアウトを選択する必要があります。また、必要に応じて2番目のキーボードレイアウトを選択する必要があります。
-   イーサネット経由で接続されている場合、ネットワークプロンプトは必要ありません。  使用可能なイーサネット接続がなく、Wi-fi が組み込まれている場合は、ユーザーがワイヤレスネットワークに接続する必要があります。
-   Windows 10 では、OOBE の重大な更新プログラムがあるかどうかがチェックされ、使用可能なものがあれば自動的にインストールされます (必要に応じて再起動します)。
-   デバイスが Azure Active Directory 参加します。
-   Azure Active Directory 参加した後、デバイスは Intune (またはその他の構成済み MDM サービス) に登録されます。
-   [ [登録ステータス] ページ](enrollment-status.md) が表示されます。
-   展開されたデバイスの設定によって、デバイスは次のいずれかになります。
    -   ログオン画面が表示されたままにして、組織のメンバーが Azure AD 資格情報を指定してログオンできるようにします。
    -   キオスクまたはデジタルの看板として構成されているデバイスについて、ローカルアカウントとして自動的にサインインします。

>[!NOTE]
>キオスク展開の自己展開モードを使用して EAS ポリシーを展開すると、自動ログオン機能が失敗します。 

観察された結果がこれらの予測と一致しない場合は、 [Windows 自動操縦のトラブルシューティング](troubleshooting.md) に関するドキュメントを参照してください。