---
title: インターネットベースのデバイスを共同管理する
titleSuffix: Configuration Manager
description: 共同管理用に Windows 10 のインターネットベースのデバイスを準備する方法について説明します。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/14/2020
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: d58faa57fa1459bbc8d821d117d20b3f404dc8e0
ms.sourcegitcommit: 7b2f7918d517005850031f30e705e5a512959c3d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84776890"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>共同管理用にインターネットベースのデバイスを準備する方法

この記事では、新しいインターネットベースのデバイスの、共同管理の 2 番目のパスに焦点を当てます。 このシナリオは Azure AD に参加し、自動的に Intune に登録される新しい Windows 10 のデバイスを入手した場合を想定しています。 共同管理状態にするには、Configuration Manager クライアントをインストールします。  

## <a name="windows-autopilot"></a>Windows Autopilot

新しい Windows 10 のデバイスでは、Autopilot サービスを使用して out of box experience (OOBE) を構成することができます。 このプロセスには、デバイスを Azure AD に参加させ、デバイスを Intune に登録する作業が含まれています。  

詳細については、「[Windows Autopilot の概要](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot)」を参照してください。

Azure AD に参加したときにデバイスが Intune に自動的に登録されるように構成するには、 [Microsoft Intune での Windows デバイスの登録](https://docs.microsoft.com/intune/windows-enroll)に関する記事を参照してください。  

### <a name="gather-information-from-configuration-manager"></a>Configuration Manager から情報を収集する

Configuration Manager を使用して、Intune で必要なデバイス情報を収集して報告します。 この情報には、デバイスのシリアル番号、Windows 製品識別子、およびハードウェア ID が含まれます。 これは、Windows Autopilot がサポートされるように、Intune でデバイスを登録するために使用されます。

1. Configuration Manager コンソールの **[監視]** ワークスペースに移動し、 **[レポート]** ノード、 **[レポート]** の順に展開し、 **[ハードウェア - 全般]** ノードを選びます。  

2. レポート **[Windows AutoPilot デバイス情報]** を実行し、結果を表示します。  

3. レポート ビューアーで **[エクスポート]** アイコンを選択して、 **[CSV (コンマ区切り)]** オプションを選択します。  

4. ファイルを保存した後、データを Intune にアップロードします。  

詳細については、[Intune でデバイスを追加する方法](https://docs.microsoft.com/intune/enrollment-autopilot#add-devices)に関するページをご覧ください。

### <a name="autopilot-for-existing-devices"></a>既存のデバイス向け Autopilot
<!--1358333-->

[既存のデバイス向けの Windows Autopilot](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) は、Windows 10 バージョン 1809 以降で利用できます。 この機能を利用すると、単一のネイティブな Configuration Manager タスク シーケンスを使用して、[Windows Autopilot ユーザー駆動モード](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven)用に Windows 7 デバイスを再イメージ化およびプロビジョニングできます。

詳細については、「[Windows Autopilot for existing devices task sequence](../osd/deploy-use/windows-autopilot-for-existing-devices.md)」 (既存のデバイス向け Windows Autopilot のタスク シーケンス) を参照してください。

## <a name="install-the-configuration-manager-client"></a>Configuration Manager クライアントのインストール

2 番目のパスのインターネットベースのデバイスの場合、Intune でアプリを作成する必要があります。 まだ Configuration Manager クライアントではない Windows 10 デバイスにこのアプリを展開します。

> [!NOTE]
> このアプリを Intune のデバイスに割り当てる前に、デバイスによって CMG サーバー認証証明書が信頼されていることを確認する必要があります。 詳細については、[クライアントが信頼する CMG のルート証明書](../core/clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot)に関するページを参照してください。 デバイスによって CMG サーバー認証証明書が信頼されていない場合は、クライアント上の ccmsetup.log で WINHTTP_CALLBACK_STATUS_FLAG_INVALID_CA エラーを確認できます。

### <a name="get-the-command-line-from-configuration-manager"></a>Configuration Manager からコマンド ラインを取得する

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[Cloud Services]** を展開して **[共同管理]** を選択します。  

2. 共同管理オブジェクトを選択してから、リボンで **[プロパティ]** を選択します。  

3. **[有効化]** タブで、コマンド ラインをコピーします。 これを次のプロセスのためにメモ帳に貼り付けて保存します。  

たとえば、次のようなコマンド ラインです。`CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC"`

<!--1358215-->
環境に必要なコマンド ライン プロパティを決定します。  

- すべてのシナリオで次のコマンド ライン プロパティが必要になります。  
  - CCMHOSTNAME  
  - SMSSITECODE  

- PKI ベースのクライアント認証証明書ではなく、クライアント認証で Azure AD を使用する場合は、次のプロパティが必要です。  
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

- クライアントがイントラネットに再度ローミングされる場合は、次のプロパティを使用します。
  - SMSMP  

- 独自の PKI 証明書を使用しており、CRL がインターネットに公開されない場合は、次のパラメーターが必要です。  
  - /noCRLCheck  

    詳細については、[CRL の計画](../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs)に関するページを参照してください

- バージョン 2002 以降では、次のプロパティを使用して、クライアント登録の直後にタスク シーケンスをブートストラップします。
  - PROVISIONTS

    詳しくは、[クライアント インストールのプロパティ - PROVISIONTS](../core/clients/deploy/about-client-installation-properties.md#provisionts) に関するページをご覧ください。

サイトでは、クラウド管理ゲートウェイ (CMG) に対して Azure AD の追加情報が公開されます。 Azure AD に参加しているクライアントは、ccmsetup プロセスの間に、参加している同じテナントを使用して、CMG からこの情報を取得します。 この動作により、複数の Azure AD テナントがある環境での共同管理に対するデバイスの登録がさらに簡略化されます。 必要な ccmsetup プロパティは、**CCMHOSTNAME** と **SMSSITECODE** の 2 つだけです。<!--3607731-->

> [!NOTE]
> Intune から Configuration Manager クライアントを既に展開している場合は、新しいコマンド ラインと新しい MSI で Intune アプリを更新します。 <!-- SCCMDocs-pr issue 3084 -->

次の例には、上記のプロパティのすべてが含まれます。

`CCMSETUPCMD="CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com PROVISIONTS=PRI20001"`

詳細については、「[クライアント インストールのプロパティ](../core/clients/deploy/about-client-installation-properties.md)」を参照してください。

### <a name="create-the-app-in-intune"></a>Intune でアプリを作成する

1. [Microsoft Endpoint Manager 管理センター](https://endpoint.microsoft.com)に移動し、左のナビゲーション ウィンドウを展開します。  

2. **[アプリ]**  >  **[すべてのアプリ]**  >  **[追加]** の順に選択します。  

3. **[その他]** で **[基幹業務アプリ]** を選択します。  

4. **ccmsetup.msi** アプリ パッケージ ファイルをアップロードします。 このファイルを Configuration Manager サイト サーバーの次のフォルダーで探します。`<ConfigMgr installation directory>\bin\i386`  

    > [!Tip]  
    > サイトを更新するときに、Intune でこのアプリも更新してください。  

5. アプリが更新されたら、Configuration Manager からコピーしたコマンド ラインでアプリの情報を構成します。  

> [!IMPORTANT]
> このコマンド ラインをカスタマイズする場合は、長さが 1,024 文字を超えないようにしてください。 コマンド ラインの長さが 1,024 文字を超えると、クライアントのインストールは失敗します。
