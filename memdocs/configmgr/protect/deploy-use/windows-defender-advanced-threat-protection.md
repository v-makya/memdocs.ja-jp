---
title: Microsoft Defender Advanced Threat Protection
titleSuffix: Configuration Manager
description: 企業が高度な攻撃に対応するための新しいサービスである Microsoft Defender Advanced Threat Protection を管理および監視する方法について説明します。
ms.date: 04/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a635ae36875984537c18c4850a3526d57ffceb31
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210147"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

*適用対象:Configuration Manager (Current Branch)*

Endpoint Protection は、[Microsoft Defender Advanced Threat Protection (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (以前は Windows Defender ATP と呼ばれていました) を管理および監視するのに役立ちます。 Microsoft Defender ATP は、企業が自社ネットワークに対する高度な攻撃を検出して調査し、対処するのに役立ちます。 Configuration Manager ポリシーは、Windows 10 クライアントのオンボードと監視に役立ちます。

Microsoft Defender ATP は、[Windows Defender セキュリティ センター](https://securitycenter.windows.com)のサービスです。 Configuration Manager は、クライアントのオンボード構成ファイルを追加して展開することにより、展開の状態と Microsoft Defender ATP エージェントの正常性を監視できます。 Microsoft Defender ATP は、Configuration Manager クライアントを実行している PC または [Microsoft Intune によって管理](https://docs.microsoft.com/intune/protect/advanced-threat-protection)されている PC でサポートされています。

## <a name="prerequisites"></a>[前提条件]

- Microsoft Defender Advanced Threat Protection オンライン サービスのサブスクリプション  
- Configuration Manager クライアントが実行されているクライアント コンピューター
- 以下の「[サポートされているクライアント オペレーティング システム](#bkmk_os)」セクションに記載されている OS を使用しているクライアント。

### <a name="supported-client-operating-systems"></a><a name="bkmk_os"></a> サポートされているクライアント オペレーティング システム
実行している Configuration Manager のバージョンに基づいて、次のクライアント オペレーティング システムをオンボードできます。

#### <a name="configuration-manager-version-1910-and-prior"></a>Configuration Manager バージョン 1910 以前

- Windows 10 バージョン 1607 以降を実行しているクライアント コンピューター

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager バージョン 2002 以降
<!--5229962-->
- Windows 7 SP1
- Windows 8.1
- Windows 10 バージョン 1607 以降
- Windows Server 2008 R2 SP1
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016 バージョン 1803
- Windows Server 2019

## <a name="create-an-onboarding-configuration-file"></a>オンボード構成ファイルの作成

1. [Microsoft Defender ATP オンライン サービス](https://securitycenter.windows.com/)にアクセスしてサインインします。
1. **[設定]** の **[コンピューターの管理]** を選択し、 **[オンボード]** を選択します。
1. 一覧から、オンボードするオペレーティング システムを選択します。
   - Windows 10、Windows Server 1803、および Windows Server 2019 をオンボードしている場合:
      1. **[Configuration Manager (current branch) version 1606]** を選択し、 **[パッケージのダウンロード]** を選択します。
      1. 圧縮済みアーカイブ (.zip) ファイルをダウンロードして内容を抽出します。
   - 別の Windows オペレーティング システムをオンボードしている場合: 
      1. 一覧から、オンボードするオペレーティング システムを選択します。 たとえば、 **[Windows 7 と Windows 8.1]** または **[Windows Server 2008 R2 SP1、2012 R2、2016]** のいずれかを選択します。
      1. プロセスが完了したら、 **[接続の構成]** セクションから **[ワークスペース キー]** と **[ワークスペース ID]** の値をコピーします。

> [!IMPORTANT]
> - Microsoft Defender ATP 構成ファイルには、セキュリティで保護する必要がある機密情報が含まれています。

## <a name="onboard-devices"></a>デバイスのオンボード

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[Endpoint Protection]**  >  **[Windows Defender ATP ポリシー]** の順に移動し、 **[Windows Defender ATP ポリシーの作成]** を選択します。 Microsoft Defender ATP ポリシー ウィザードが開きます。  
1. Microsoft Defender ATP ポリシーの **[名前]** と **[説明]** を入力し、 **[オンボード]** を選択します。
1. 組織の Microsoft Defender ATP のクラウド サービス テナントによって提供される構成ファイルを**参照**します。
   - **Windows 7 と 8.1** または **Windows Server 2008 R2 SP1、2012 R2、および 2016**では、**ワークスペース キー** と **ワークスペース ID** を指定します。
   - Configuration Manager バージョン 2002 では、Windows Server 2019 および Windows Server 1803 以降のデバイスのみをオンボードする場合でも、**ワークスペース キー**と**ワークスペース ID** が必要になります。 これらの値を取得するには、[Microsoft Defender ATP オンライン サービス](https://securitycenter.windows.com/)から **[設定]**  >  **[オンボード]**  >  **[Windows 7 と Windows 8.1]** を選択します。 <!--7054188-->
1. マネージド デバイスから分析用に収集され共有されるファイルのサンプルを指定します。  

   - **なし**

   - **すべてのファイルの種類**  
1. 概要を確認して、ウィザードを完了します。  

**[展開]** を選択して、Microsoft Defender ATP ポリシーのターゲットをクライアントにします。

## <a name="monitor"></a>モニター

1. Configuration Manager コンソールで、 **[監視]**  >  **[セキュリティ]** の順に移動し、 **[Windows Defender ATP]** を選択します。  

1. Microsoft Defender Advanced Threat Protection ダッシュボードを確認します。  

    - **Windows Defender エージェントの展開の状態**: アクティブな Microsoft Defender ATP ポリシーがオンボードされている管理対象のクライアント コンピューターの数と割合  

    - **Windows Defender ATP Agent Health**: 自身の Microsoft Defender ATP エージェントの状態を報告しているコンピューター クライアントの割合  

        - **正常**: 正常に機能しています  

        - **非アクティブ**: 期間中にサービスに送信されるデータがありません  

        - **エージェントの状態**: Windows でエージェントのシステム サービスが実行されていません。  

        - **非オンボード**: ポリシーは適用されましたが、エージェントがポリシー オンボードを報告していません  

## <a name="create-an-offboarding-configuration-file"></a>オフボード構成ファイルの作成  

1. [Microsoft Defender ATP オンライン サービス](https://securitycenter.windows.com/)にサインインします。

1. **[設定]** の **[コンピューターの管理]** を選択し、 **[オンボード]** を選択します。  

1. **[Configuration Manager (current branch) version 1606]** を選択し、 **[Endpoint offboarding]\(エンドポイント オフボード\)** を選択します。  

1. 圧縮済みアーカイブ (.zip) ファイルをダウンロードして内容を抽出します。 オフボード ファイルは、30 日間有効です。

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[Endpoint Protection]**  >  **[Windows Defender ATP ポリシー]** の順に移動し、 **[Windows Defender ATP ポリシーの作成]** を選択します。 Microsoft Defender ATP ポリシー ウィザードが開きます。  

1. Microsoft Defender ATP ポリシーの **[名前]** と **[説明]** を入力し、 **[オフボード]** を選択します。

1. 組織の Microsoft Defender ATP のクラウド サービス テナントによって提供される構成ファイルを**参照**します。

1. 概要を確認して、ウィザードを完了します。  

**[展開]** を選択して、Microsoft Defender ATP ポリシーのターゲットをクライアントにします。  

> [!IMPORTANT]
> Microsoft Defender ATP 構成ファイルには、セキュリティで保護する必要がある機密情報が含まれています。

## <a name="next-steps"></a>次のステップ

- [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Microsoft Defender Advanced Threat Protection のオンボードの問題のトラブルシューティング](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
