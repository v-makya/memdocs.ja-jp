---
title: Windows 自動操縦用自己展開モード
description: 自己展開モードでは、ユーザーの操作なしでデバイスを展開できます。 このモードは、キオスク、デジタル看板デバイス、または共有デバイスとして Windows 10 を展開するように設計されています。
keywords: MDM, セットアップ, Windows, Windows 10, OOBE, 管理, 展開, Autopilot, ZTD, ゼロタッチ, パートナー, MSFB, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
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
ms.openlocfilehash: 13b45b972ed17d24efedaa048c0e48ea2f2d90d2
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568606"
---
# <a name="windows-autopilot-self-deploying-mode"></a>Windows 自動操縦用自己展開モード

**適用対象: Windows 10 バージョン1903以降**

Windows 自動操縦用自己展開モードでは、ユーザーの操作なしでデバイスを展開できます。 イーサネット接続を使用するデバイスの場合、ユーザー操作は必要ありません。 Wi-fi を使用して接続されているデバイスの場合、ユーザーは以下を実行する必要があります。
- 言語、ロケール、およびキーボードを選択します。
- ネットワーク接続を確立します。 

自己展開モードでは、次のすべてが提供されます。
- デバイスを Azure Active Directory に参加させます。
- MDM の自動登録に Azure AD を使用して Intune (または別の MDM サービス) にデバイスを登録します。
- すべてのポリシー、アプリケーション、証明書、およびネットワークプロファイルがデバイスにプロビジョニングされていることを確認します。
- [登録ステータス] ページを使用して、デバイスが完全にプロビジョニングされるまでアクセスを防止します。

>[!NOTE]
>自己展開モードでは Active Directory Join または Hybrid Azure AD Join はサポートされません。 すべてのデバイスが Azure Active Directory に参加します。

自己展開モードでは、キオスク、デジタル看板デバイス、または共有デバイスとして Windows 10 デバイスを展開できます。

キオスクデバイスをセットアップするときに、 [キオスクブラウザー](https://www.microsoft.com/p/kiosk-browser/9ngb5s5xg2kp?rtc=1&activetab=pivot:overviewtab) を使用できます。 このアプリは Microsoft Edge 上に構築されており、カスタマイズされた MDM で管理された閲覧エクスペリエンスを作成するために使用できます。

MDM ポリシーと自己 deploing モードを組み合わせることによって、デバイスの構成を完全に自動化できます。 MDM ポリシーを使用して、自動的にログオンするように構成されたローカルアカウントを作成します。 詳細については、次を参照してください。
- [Windows 10 によるキオスク管理の簡素化](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/simplifying-kiosk-management-for-it-with-windows-10/ba-p/187691)。
- [Intune またはその他の MDM サービスでキオスクまたはデジタル署名を設定](/windows/configuration/setup-kiosk-digital-signage#set-up-a-kiosk-or-digital-sign-in-intune-or-other-mdm-service)します。

>[!NOTE]
>現在、自己展開モードでは、ユーザーがデバイスに関連付けられていません (プロセスの一部としてユーザー ID またはパスワードが指定されていないため)。 その結果、一部の Azure AD と Intune の機能 (BitLocker の回復、ポータルサイトからのアプリのインストール、条件付きアクセスなど) は、デバイスにサインインしているユーザーが使用できなくなる可能性があります。 詳細については、「 [Windows 自動操縦のシナリオと機能](windows-autopilot-scenarios.md) 」および「 [自動操縦用デバイスの BitLocker 暗号化アルゴリズムの設定](bitlocker.md)」を参照してください。

![Windows 自動操縦用自己展開モードのユーザーエクスペリエンス](images/self-deploy-welcome.png)

## <a name="requirements"></a>必要条件

自己展開モードでは、デバイスの TPM 2.0 ハードウェアを使用して、組織の Azure AD テナントにデバイスを認証します。 このため、TPM 2.0 を搭載していないデバイスをこのモードで使用することはできません。 デバイスは、TPM デバイスの構成証明もサポートする必要があります。 すべての新しい Windows デバイスは、これらの要件を満たしている必要があります。

>[!IMPORTANT]
>TPM 2.0 をサポートしていないデバイスまたは仮想マシン上で、自己展開モードの展開を実行しようとすると、0x800705B4 タイムアウトエラー (Hyper-v 仮想 Tpm はサポートされていません) を使用してデバイスを検証するときに、プロセスが失敗します。 また、Windows 10 version 1809 での TPM デバイスの構成証明の問題により、自己展開モードを使用するには、Windows 10 バージョン1903以降が必要であることにも注意してください。 Windows 10 Enterprise 2019 LTSC は Windows 10 バージョン1809に基づいているため、自己展開モードは Windows 10 Enterprise 2019 LTSC でもサポートされていません。 他の既知のエラーと解決策については、「 [Windows 自動操縦の既知の問題](known-issues.md) 」を参照してください。

自動操縦プロセス中に、組織固有のロゴと組織名を表示することができます。 これを行うには、表示するイメージとテキストを使用して Azure AD 会社のブランド化を構成する必要があります。 詳細については [、「クイックスタート: Azure AD のサインインページに会社のブランドを追加する](/azure/active-directory/fundamentals/customize-branding) 」を参照してください。 

## <a name="step-by-step"></a>ステップ バイ ステップ

自己展開モードの Windows 自動操縦を展開するには、次の準備手順を完了する必要があります。

1. 自己展開モード用の自動操縦プロファイルを作成し、必要な設定を行います。 Microsoft Intune では、プロファイルの作成時にこのモードが明示的に選択されます。 セルフデプロイモードでは、Microsoft Store for Business またはパートナーセンターでプロファイルを作成することはできません。
2. Intune を使用している場合は Azure Active Directory でデバイスグループを作成し、そのグループに自動操縦プロファイルを割り当てます。 デバイスの展開を試行する前に、プロファイルがデバイスに割り当てられていることを確認してください。
3. デバイスを起動し、必要に応じて Wi-fi に接続してから、プロビジョニング処理が完了するまで待ちます。

## <a name="validation"></a>検証

Windows 自動操縦を使用して自己展開モードで展開する場合は、次のエンドユーザーエクスペリエンスを確認する必要があります。

-  ネットワークに接続すると、自動操縦プロファイルがダウンロードされます。
- イーサネットに接続していて、自動操縦プロファイルがスキップするように構成されている場合、次のページは表示されません: 言語、ロケール、およびキーボードレイアウト。 それ以外の場合は、手動の手順が必要です。
  -  Windows 10 に複数の言語がプレインストールされている場合、ユーザーは言語を選択する必要があります。
  -  ユーザーは、ロケールとキーボードレイアウトを選択する必要があります。また、必要に応じて2番目のキーボードレイアウトを選択する必要があります。
-  イーサネット経由で接続されている場合、ネットワークプロンプトは必要ありません。 使用可能なイーサネット接続がなく、Wi-fi が組み込まれている場合は、ユーザーがワイヤレスネットワークに接続する必要があります。
-  Windows 10 では、OOBE の重大な更新プログラムがあるかどうかを確認し、使用可能な場合は自動的にインストールされます (必要に応じて再起動します)。
-  デバイスが Azure Active Directory 参加します。
-  Azure Active Directory 参加した後、デバイスは Intune (またはその他の構成済み MDM サービス) に登録されます。
-  [ [登録ステータス] ページ](enrollment-status.md) が表示されます。
-  展開されたデバイスの設定によって、デバイスは次のいずれかになります。
  -  ログオン画面が表示されたままにして、組織のメンバーが Azure AD 資格情報を指定してログオンできるようにします。
  -  キオスクまたはデジタルの看板として構成されているデバイスについて、ローカルアカウントとして自動的にサインインします。

>[!NOTE]
>キオスク展開の自己展開モードを使用して EAS ポリシーを展開すると、自動ログオン機能が失敗します。 

観測結果がこれらの予測と一致しない場合は、 [Windows 自動操縦のトラブルシューティング](troubleshooting.md) に関するドキュメントを参照してください。
