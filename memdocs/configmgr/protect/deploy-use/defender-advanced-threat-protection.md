---
title: Microsoft Defender Advanced Threat Protection
titleSuffix: Configuration Manager
description: 企業が高度な攻撃に対応するための新しいサービスである Microsoft Defender Advanced Threat Protection を管理および監視する方法について説明します。
ms.date: 06/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cbf7dd3e35db8d2020e96e2511017e43863f724e
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85613463"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

*適用対象:Configuration Manager (Current Branch)*

Endpoint Protection は、[Microsoft Defender Advanced Threat Protection (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (以前は Windows Defender ATP と呼ばれていました) を管理および監視するのに役立ちます。 Microsoft Defender ATP は、企業が自社ネットワークに対する高度な攻撃を検出して調査し、対処するのに役立ちます。 Configuration Manager ポリシーは、Windows 10 クライアントのオンボードと監視に役立ちます。

Microsoft Defender ATP は、[Microsoft Defender セキュリティ センター](https://securitycenter.windows.com)のサービスです。 Configuration Manager は、クライアントのオンボード構成ファイルを追加して展開することにより、展開の状態と Microsoft Defender ATP エージェントの正常性を監視できます。 Microsoft Defender ATP は、Configuration Manager クライアントを実行している PC または [Microsoft Intune によって管理](https://docs.microsoft.com/intune/protect/advanced-threat-protection)されている PC でサポートされています。

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
Configuration Manager バージョン 2002 以降では、次のオペレーティング システムをオンボードできます。

- Windows 8.1
- Windows 10 バージョン 1607 以降
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016、バージョン 1803 以降
- Windows Server 2019

## <a name="about-onboarding-to-atp-with-configuration-manager"></a>Configuration Manager を使用した ATP へのオンボードについて

ATP へのオンボードのニーズは、オペレーティング システムによって異なります。 Windows 8.1 およびその他の下位レベルのオペレーティング システムのデバイスでは、**ワークスペース キー**と**ワークスペース ID** をオンボードする必要があります。 Windows Server バージョン 1803 などの上位レベルのデバイスには、オンボード構成ファイルが必要です。 オンボードされたデバイスで必要な場合、Microsoft Monitoring Agent (MMA) も Configuration Manager によりインストールされますが、エージェントは自動的に更新されません。

上位レベルのオペレーティング システムには次のものが含まれます。
- Windows 10 バージョン 1607 以降
- Windows Server 2016、バージョン 1803 以降
- Windows Server 2019

下位レベルのオペレーティング システムには次のものが含まれます。
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016、バージョン 1709 以前

Configuration Manager を使用してデバイスを ATP にオンボードする場合は、ATP ポリシーをターゲット コレクションまたは複数のコレクションに展開します。 ターゲット コレクションには、サポートされている任意の数のオペレーティング システムを実行しているデバイスが含まれる場合があります。 これらのデバイスのオンボードの手順は、オペレーティング システムが上位レベル、下位レベル、またはその両方であるデバイスが含まれるコレクションを対象としているかどうかによって異なります。

- ターゲット コレクションに上位レベルと下位レベルの両方のデバイスが含まれる場合は、手順に従って、[サポートされている任意のオペレーティング システムを実行しているデバイスをオンボード](#bkmk_any_os)します (推奨)。
- 上位レベルのデバイスのみがコレクションに含まれている場合は、[上位レベルのオンボード手順](#bkmk_uplevel)を使用できます。
- 下位レベルのデバイスのみがコレクションに含まれる場合は、[下位レベルのオンボード手順](#bkmk_downlevel)を使用できます。

> [!Warning]
> - ターゲット コレクションに上位レベルのデバイスが含まれる場合に下位レベルのデバイスの手順を使用すると、上位レベルのデバイスはオンボードされません。
> - ターゲット コレクションに下位レベルのデバイスが含まれる場合に上位レベルのデバイスの手順を使用すると、下位レベルのデバイスはオンボードされません。

## <a name="onboard-devices-with-any-supported-operating-system-to-atp-recommended"></a><a name="bkmk_any_os"></a> サポートされているオペレーティング システムを実行しているデバイスを ATP にオンボードする (推奨)
 [サポートされているオペレーティング システム](#bkmk_os)のいずれかを実行しているデバイスを ATP にオンボードするには、Configuration Manager に構成ファイル、**ワークスペース キー**、**ワークスペース ID** を指定します。

### <a name="get-the-configuration-file-workspace-id-and-workspace-key"></a>構成ファイル、ワークスペース ID、ワークスペース キーを取得する

1. [Microsoft Defender ATP オンライン サービス](https://securitycenter.windows.com/)にアクセスしてサインインします。
1. **[設定]** を選択し、 **[デバイス管理]** 見出しの下にある **[オンボード]** を選択します。
1. オペレーティング システムとして、 **[Windows 10]** を選択します。
1. 展開方法として、 **[Microsoft Endpoint Configuration Manager current branch and later]\(Microsoft Endpoint Configuration Manager Current Branch 以降\)** を選択します。
1. **[パッケージをダウンロード]** をクリックします。
   
   :::image type="content" source="media/5229962-onboarding-configuration.png" alt-text="オンボード構成ファイルのダウンロード" lightbox="media/5229962-onboarding-configuration.png":::
1. 圧縮済みアーカイブ (.zip) ファイルをダウンロードして内容を抽出します。
1. **[設定]** を選択し、 **[デバイス管理]** 見出しの下にある **[オンボード]** を選択します。
1. オペレーティング システムとして、一覧から **Windows 7 SP1 と 8.1** または **Windows Server 2008 R2 Sp1、2012 R2、および 2016** を選択します。
   - 選択したオプションに関係なく、**ワークスペース キー**と**ワークスペース ID** は同じになります。
1. **[接続の構成]** セクションから **[ワークスペース キー]** と **[ワークスペース ID]** の値をコピーします。

   > [!IMPORTANT]
   > Microsoft Defender ATP 構成ファイルには、セキュリティで保護する必要がある機密情報が含まれています。


### <a name="onboard-the-devices"></a>デバイスをオンボードする

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[Endpoint Protection]**  >  **[Microsoft Defender ATP ポリシー]** の順に移動します。
1. **[Microsoft Defender ATP ポリシーの作成]** を選択して、Microsoft Defender ATP ポリシー ウィザードを開きます。 
1. Microsoft Defender ATP ポリシーの **[名前]** と **[説明]** を入力し、 **[オンボード]** を選択します。
1. ダウンロードした .zip ファイルから抽出した構成ファイルを**参照**します。
1. **[ワークスペース キー]** と **[ワークスペース ID]** を入力し、 **[次へ]** をクリックします。

   :::image type="content" source="media/5229962-create-atp-policy-wizard.png" alt-text="Microsoft Defender ATP ポリシーの作成ウィザード" lightbox="media/5229962-create-atp-policy-wizard.png":::

1. マネージド デバイスから分析用に収集され共有されるファイルのサンプルを指定します。  
   - **なし**
   - **すべてのファイルの種類**  
1. 概要を確認して、ウィザードを完了します。  
1. 選択したポリシーを右クリックし、 **[展開]** を選択して、Microsoft Defender ATP ポリシーのターゲットをクライアントにします。

## <a name="onboard-devices-running-up-level-operating-systems-to-atp"></a><a name="bkmk_uplevel"></a> 上位レベルのオペレーティング システムを実行しているデバイスを ATP にオンボードする

上位レベルのクライアントでは、ATP にオンボードするためのオンボード構成ファイルが必要です。 上位レベルのオペレーティング システムには次のものが含まれます。
- Windows 10 バージョン 1607 以降 
- Windows Server 2016、バージョン 1803 以降
- Windows Server 2019

ターゲット コレクションに上位レベルと下位レベルの両方のデバイスが含まれる場合、または不明な場合は、手順に従って、[サポートされている任意のオペレーティング システムを実行しているデバイスをオンボードします (推奨)](#bkmk_any_os)。

### <a name="get-an-onboarding-configuration-file-for-up-level-devices"></a>上位レベルのデバイスのオンボード構成ファイルを取得する

1. [Microsoft Defender ATP オンライン サービス](https://securitycenter.windows.com/)にアクセスしてサインインします。
1. **[設定]** を選択し、 **[デバイス管理]** 見出しの下にある **[オンボード]** を選択します。
1. オペレーティング システムとして、 **[Windows 10]** を選択します。
1. 展開方法として、 **[Microsoft Endpoint Configuration Manager current branch and later]\(Microsoft Endpoint Configuration Manager Current Branch 以降\)** を選択します。
1. **[パッケージをダウンロード]** をクリックします。
1. 圧縮済みアーカイブ (.zip) ファイルをダウンロードして内容を抽出します。

> [!IMPORTANT]
> Microsoft Defender ATP 構成ファイルには、セキュリティで保護する必要がある機密情報が含まれています。


### <a name="onboard-the-up-level-devices"></a>上位レベルのデバイスをオンボードする

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[Endpoint Protection]**  >  **[Microsoft Defender ATP ポリシー]** の順に移動し、 **[Microsoft Defender ATP ポリシーの作成]** を選択します。 Microsoft Defender ATP ポリシー ウィザードが開きます。  
1. Microsoft Defender ATP ポリシーの **[名前]** と **[説明]** を入力し、 **[オンボード]** を選択します。
1. ダウンロードした .zip ファイルから抽出した構成ファイルを**参照**します。
   > [!Note]
   > Configuration Manager バージョン 2002 では、上位レベルのデバイスのみをオンボードする場合でも、**ワークスペース キー**と**ワークスペース ID** が必要になります。 これらの値を取得するには、[Microsoft Defender ATP オンライン サービス](https://securitycenter.windows.com/)から **[設定]**  >  **[オンボード]**  >  **[Windows 7 と Windows 8.1]** を選択します。 <!--7054188-->
1. マネージド デバイスから分析用に収集され共有されるファイルのサンプルを指定します。  
   - **なし**
   - **すべてのファイルの種類**  
1. 概要を確認して、ウィザードを完了します。  
1. 選択したポリシーを右クリックし、 **[展開]** を選択して、Microsoft Defender ATP ポリシーのターゲットをクライアントにします。

## <a name="onboard-devices-running-down-level-operating-systems-to-atp"></a><a name="bkmk_downlevel"></a> 下位レベルのオペレーティング システムを実行しているデバイスを ATP にオンボードする

下位レベルのクライアントには、ATP のオンボードに **ワークスペースキー**と**ワークスペース ID** が必要です。 下位レベルのオペレーティング システムには次のものが含まれます。
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016、バージョン 1709 以前

ターゲット コレクションに上位レベルと下位レベルの両方のデバイスが含まれる場合、または不明な場合は、手順に従って、[サポートされている任意のオペレーティング システムを実行しているデバイスをオンボードします (推奨)](#bkmk_any_os)。

### <a name="get-the-workspace-id-and-workspace-key-for-down-level-devices"></a>下位レベルのデバイスのワークスペース ID とワークスペース キーを取得する

1. [Microsoft Defender ATP オンライン サービス](https://securitycenter.windows.com/)にアクセスしてサインインします。
1. **[設定]** を選択し、 **[デバイス管理]** 見出しの下にある **[オンボード]** を選択します。
1. オペレーティング システムとして、一覧から **Windows 7 SP1 と 8.1** または **Windows Server 2008 R2 Sp1、2012 R2、および 2016** を選択します。
   - 選択したオプションに関係なく、**ワークスペース キー**と**ワークスペース ID** は同じになります。
1. **[接続の構成]** セクションから **[ワークスペース キー]** と **[ワークスペース ID]** の値をコピーします。

### <a name="onboard-the-down-level-devices"></a>下位レベルのデバイスをオンボードする

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[Endpoint Protection]**  >  **[Microsoft Defender ATP ポリシー]** の順に移動し、 **[Microsoft Defender ATP ポリシーの作成]** を選択します。 Microsoft Defender ATP ポリシー ウィザードが開きます。  
1. Microsoft Defender ATP ポリシーの **[名前]** と **[説明]** を入力し、 **[オンボード]** を選択します。
1. **ワークスペース キー**と**ワークスペース ID** を指定します。
   > [!Note]
   > - Configuration Manager バージョン 2002 では、下位レベルのデバイスのみをオンボードする場合でも、構成ファイルが必要になります。 これらの値を取得するには、[Microsoft Defender ATP オンライン サービス](https://securitycenter.windows.com/)から **[設定]**  >  **[オンボード]**  >  **[Windows 10]** を選択します。 <!--7054188--> 
   > - Microsoft Defender ATP 構成ファイルには、セキュリティで保護する必要がある機密情報が含まれています。
1. マネージド デバイスから分析用に収集され共有されるファイルのサンプルを指定します。  
   - **なし**
   - **すべてのファイルの種類**  
1. 概要を確認して、ウィザードを完了します。  
1. 選択したポリシーを右クリックし、 **[展開]** を選択して、Microsoft Defender ATP ポリシーのターゲットをクライアントにします。


## <a name="monitor"></a>モニター

1. Configuration Manager コンソールで、 **[監視]**  >  **[セキュリティ]** の順に移動し、 **[Microsoft Defender ATP]** を選択します。  

1. Microsoft Defender Advanced Threat Protection ダッシュボードを確認します。  

    - **Microsoft Defender ATP エージェントのオンボードの状態**:アクティブな Microsoft Defender ATP ポリシーがオンボードされている管理対象のクライアント コンピューターの数と割合  

    - **Microsoft Defender ATP エージェントの正常性**:自身の Microsoft Defender ATP エージェントの状態を報告しているコンピューター クライアントの割合  

        - **正常**: 正常に機能しています  

        - **非アクティブ**: 期間中にサービスに送信されるデータがありません  

        - **エージェントの状態**: Windows でエージェントのシステム サービスが実行されていません。  

        - **非オンボード**: ポリシーは適用されましたが、エージェントがポリシー オンボードを報告していません  

## <a name="create-an-offboarding-configuration-file"></a>オフボード構成ファイルの作成  

1. [Microsoft Defender ATP オンライン サービス](https://securitycenter.windows.com/)にサインインします。
1. **[設定]** を選択し、 **[デバイス管理]** 見出しの下にある **[オフボード]** を選択します。
1. オペレーティング システムとして、 **[Windows 10]** 、展開方法として、 **[Microsoft Endpoint Configuration Manager current branch and later]\(Microsoft Endpoint Configuration Manager Current Branch 以降\)** を選択します。
   - **Windows 10** オプションを使用すると、確実にコレクション内のすべてのデバイスがオフボードされ、必要に応じて MMA がアンインストールされます。
1. 圧縮済みアーカイブ (.zip) ファイルをダウンロードして内容を抽出します。 オフボード ファイルは、30 日間有効です。

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[Endpoint Protection]**  >  **[Microsoft Defender ATP ポリシー]** の順に移動し、 **[Microsoft Defender ATP ポリシーの作成]** を選択します。 Microsoft Defender ATP ポリシー ウィザードが開きます。  

1. Microsoft Defender ATP ポリシーの **[名前]** と **[説明]** を入力し、 **[オフボード]** を選択します。

1. ダウンロードした .zip ファイルから抽出した構成ファイルを**参照**します。

1. 概要を確認して、ウィザードを完了します。  

**[展開]** を選択して、Microsoft Defender ATP ポリシーのターゲットをクライアントにします。  

> [!IMPORTANT]
> Microsoft Defender ATP 構成ファイルには、セキュリティで保護する必要がある機密情報が含まれています。

## <a name="next-steps"></a>次のステップ

- [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Microsoft Defender Advanced Threat Protection のオンボードの問題のトラブルシューティング](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
