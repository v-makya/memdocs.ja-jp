---
title: Microsoft 接続キャッシュ
titleSuffix: Configuration Manager
description: 配信の最適化のローカル キャッシュ サーバーとして Configuration Manager の配布ポイントを使用する
ms.date: 05/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4dead573e1744a5c8b84ff954e85be43af644486
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83878490"
---
# <a name="microsoft-connected-cache-in-configuration-manager"></a>Configuration Manager における Microsoft 接続済みキャッシュ

*適用対象:Configuration Manager (Current Branch)*

<!--3555764-->

バージョン 1906 以降、配布ポイントに Microsoft 接続済みキャッシュ サーバーをインストールできます。 このコンテンツをオンプレミスでキャッシュすることによって、クライアントは配信の最適化機能から恩恵を受けることができますが、お客様が WAN リンクを保護するのに役立てることができます。

> [!NOTE]
> バージョン 1910 以降、この機能は、**Microsoft 接続済みキャッシュ**という名前になりました。 以前は、"配信の最適化のネットワーク内キャッシュ" という名前でした。

このキャッシュ サーバーは、配信の最適化によってダウンロードされたコンテンツに対して、オンデマンドの透過型キャッシュとして機能します。 クライアント設定を使用して、このサーバーがローカルの Configuration Manager 境界グループのメンバーにのみ提供されるようにします。

このキャッシュは、Configuration Manager の配布ポイントのコンテンツとは別のものです。 配布ポイントの役割と同じドライブを選択した場合は、コンテンツは個別に格納されます。

> [!Note]  
> 接続済みキャッシュ サーバーは、Windows Server にインストールされているアプリケーションです。 このアプリケーションはまだ開発中です。

## <a name="how-it-works"></a>しくみ

接続済みキャッシュ サーバーを使用するようにクライアントを構成すると、クライアントはインターネットから Microsoft クラウドで管理されたコンテンツを要求しなくなります。 クライアントは、このコンテンツを、配布ポイントにインストールされたキャッシュ サーバーから要求します。 オンプレミス サーバーは、アプリケーション要求ルーティング処理 (ARR) の IIS 機能を使用して、このコンテンツをキャッシュします。 キャッシュ サーバーは、同じコンテンツに対するその後のすべての要求にすばやく応答することができます。 接続済みキャッシュ サーバーを使用できない場合、またはコンテンツがまだキャッシュされていない場合、クライアントはコンテンツをインターネットからダウンロードします。 また、クライアントは、配信の最適化を使用するため、コンテンツの一部を自身のネットワーク内のピアからダウンロードします。

![接続済みキャッシュのしくみの図](media/3555764-microsoft-connected-cache.png)

1. クライアントは、更新をチェックして、コンテンツ配信ネットワーク (CDN) のアドレスを取得します。

2. Configuration Manager は、キャッシュ サーバー名など、クライアントの配信の最適化 (DO) 設定を構成します。

3. クライアント A は、DO キャッシュ サーバーからコンテンツを要求します。

4. キャッシュにコンテンツが含まれていない場合、DO キャッシュ サーバーは CDN からコンテンツを取得します。

5. キャッシュ サーバーが応答に失敗すると、クライアントは CDN からコンテンツをダウンロードします。

6. クライアントは、DO を使用してピアからコンテンツの一部を取得します。

## <a name="prerequisites-and-limitations"></a>前提条件と制限事項

- *オンプレミス*の配布ポイントには、次の構成が必要です。

  - Windows Server 2012、Windows Server 2012 R2、Windows Server 2016、または Windows Server 2019 を実行

  - 既定の Web サイトはポート 80 で有効

  - IIS [アプリケーション要求ルーティング処理](https://docs.microsoft.com/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) (ARR) 機能をプレインストールしないでください。 接続済みキャッシュにより、ARR のインストールとその設定の構成が行われます。 Microsoft は、接続済みキャッシュによる ARR の構成が、サーバー上でこの機能を使用する他のアプリケーションと競合しないことを保証することはできません。

  - 配布ポイントには、Microsoft クラウドへのインターネット アクセスが必要です。 特定の URL は、特定のクラウド対応のコンテンツによって異なる場合があります。 詳細については、「[Internet access requirements (インターネット アクセスの要件)](../network/internet-endpoints.md)」を参照してください。

  - バージョン 2002 以降は、接続済みキャッシュ アプリケーションで非認証のプロキシ サーバーをインターネット アクセスに使用できます。 詳しくは、「[サイト システム サーバー用にプロキシを構成する](../network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)」をご覧ください。<!-- 5856396 -->

- Windows 10 バージョン 1709 以降を実行しているクライアント

## <a name="enable-connected-cache"></a>接続済みキャッシュを有効にする

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動して、 **[配布ポイント]** ノードを選択します。

1. "*オンプレミス*" の配布ポイントを選択して、リボンで **[プロパティ]** を選択します。

1. 配布ポイントの役割のプロパティの **[全般]** タブで、次の設定を構成します。  

    1. **[Microsoft 接続済みキャッシュ サーバーとして使用するためにこの配布ポイントを有効にする]** オプションを有効にします  

        ライセンス条項を表示して同意します。

    2. **使用するローカル ドライブ**: キャッシュ用に使用するディスクを選択します。 既定値は **[自動]** で、最も多くの空き領域を含むディスクを使用します。<sup>[注 1](#bkmk_note1)</sup>  

        > [!Note]  
        > このドライブは後で変更できます。 キャッシュされたコンテンツは、新しいドライブにコピーしない限り消失します。

    3. **ディスク領域**: GB 単位で予約するディスク領域の容量または合計ディスク領域の割合を選択します。 既定値は 100 GB です。

        > [!Note]  
        > ほとんどの場合、既定のキャッシュ サイズで十分です。 キャッシュ サイズは後で調整できます。
        >
        > ディスクのキャッシュ サイズが割り当てられているディスク容量を超えた場合、ARR では組み込みのヒューリスティックに基づいてコンテンツを削除することで領域を解放します。<!-- SCCMDocs#2045 -->

    4. **接続済みキャッシュ サーバーを無効にする場合にキャッシュを保持する**: キャッシュ サーバーを削除して、このオプションを有効にした場合、サーバーでディスク上のキャッシュのコンテンツが保持されます。  

1. クライアント設定の **[配信の最適化]** グループで、 **[Configuration Manager で管理されるデバイスで、コンテンツのダウンロードに Microsoft 接続済みキャッシュ サーバーを使用できるようにします]** を設定します。  

### <a name="note-1-about-drive-selection"></a><a name="bkmk_note1"></a> 注 1:ドライブの選択について

**[自動]** を選択した場合、Configuration Manager で接続済みキャッシュ コンポーネントがインストールされるとき、**no_sms_on_drive.sms** ファイルが優先されます。 たとえば、配布ポイントにファイル `C:\no_sms_on_drive.sms` があります。 C: ドライブの空き容量が最も多い場合でも、Configuration Manager では、そのキャッシュに別のドライブを使用するように接続済みキャッシュが構成されます。

既に **no_sms_on_drive.sms** ファイルが含まれている特定のドライブを選択すると、Configuration Manager ではファイルが無視されます。 そのドライブを使用するように接続済みキャッシュを構成することは、明示的な意図です。 たとえば、配布ポイントにファイル `F:\no_sms_on_drive.sms` があります。 **F:** ドライブを使用するように配布ポイントのプロパティを明示的に構成すると、Configuration Manager では、そのキャッシュに F: ドライブを使用するように接続済みキャッシュが構成されます。

接続済みキャッシュをインストールした後にドライブを変更するには:

- 特定のドライブ文字を使用するように配布ポイントのプロパティを手動で構成します。

- 自動に設定されている場合、最初に **no_sms_on_drive.sms** ファイルを作成します。 次に、構成変更をトリガーするように配布ポイントのプロパティにいくつかの変更を加えます。

### <a name="automation"></a>オートメーション

<!-- SCCMDocs#1911 -->

Configuration Manager SDK を使用して、配布ポイントで Microsoft 接続キャッシュ設定の構成を自動化することができます。 すべてのサイトの役割の場合と同様に、[SMS_SCI_SysResUse WMI クラス](../../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md)を使用します。 詳しくは、[サイトの役割のプログラミング](../../../develop/osd/about-operating-system-deployment-site-role-configuration.md#programming-the-site-roles)に関するページを参照してください。

配布ポイントの **SMS_SCI_SysResUse** インスタンスを更新する場合は、次のプロパティを設定します。

- **AgreeDOINCLicense**: ライセンス条項に同意するには、`1` に設定します。
- **Flags**: 有効 `|= 4`、無効 `&= ~4`
- **DiskSpaceDOINC**: `Percentage` または `GB` に設定します
- **RetainDOINCCache**: `0` または `1` に設定します
- **LocalDriveDOINC**: `Automatic`、または特定ドライブのドライブ文字 (`C:` や `D:` など) に設定します

## <a name="verify"></a>確認事項

クライアントがクラウドで管理されたコンテンツをダウンロードするときに、配布ポイントにインストールされたキャッシュ サーバーから配信の最適化を使用します。 クラウドで管理されたコンテンツには、次の種類が含まれています。

- Microsoft Store アプリ
- オンデマンドの Windows 機能 (言語など)
- [Windows Update for Business ポリシー](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)を有効にする場合: Windows 10 の機能と品質更新プログラム
- [共同管理ワークロード](../../../comanage/workloads.md)の場合:
  - Windows Update for Business: Windows 10 の機能と品質更新プログラム
  - Office クイック実行アプリ: Office アプリと更新プログラム
  - クライアント アプリ: Microsoft Store アプリと更新プログラム
  - エンドポイント保護:Windows Defender の定義更新プログラム

Windows 10 バージョン 1809 以降で、**Get-DeliveryOptimizationStatus** Windows PowerShell コマンドレットを使ってこの動作を確認します。 コマンドレットの出力で、**BytesFromCacheServer** の値を確認します。 詳細については、「[配信の最適化を監視する](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-setup#monitor-delivery-optimization)」をご覧ください。

キャッシュ サーバーによって任意の HTTP エラーが返された場合、配信の最適化クライアントは元のクラウド ソースに戻されます。

詳細については、「[Configuration Manager における Microsoft 接続済みキャッシュのトラブルシューティング](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md)」を参照してください。

## <a name="support-for-intune-win32-apps"></a><a name="bkmk_intune"></a> Intune Win32 アプリのサポート

<!--5032900-->

バージョン 1910 以降、Configuration Manager 配布ポイントで接続済みキャッシュを有効にすると、Microsoft Intune Win32 アプリを共同管理クライアントに提供できます。

### <a name="prerequisites"></a>[前提条件]

#### <a name="client"></a>クライアント

- クライアントを最新バージョンに更新します。

- クライアント デバイスには、少なくとも 4 GB のメモリが必要です。

    > [!TIP]
    > 次のグループ ポリシー設定を使用します。[コンピューターの構成] > [管理用テンプレート] > [Windows コンポーネント] > [配信の最適化] > **[ピア キャッシュの使用に必要な最小 RAM 容量 (GB)]** 。

#### <a name="site"></a>サイト

- 配布ポイント上で Connected Cache を有効にします。 詳細については、[Microsoft 接続済みキャッシュ](microsoft-connected-cache.md)に関するページを参照してください。

- クライアントと Connected Cache 対応の配布ポイントは、同じ境界グループに存在する必要があります。

- [ **[配信の最適化]** ](../../clients/deploy/about-client-settings.md#delivery-optimization) グループで、次のクライアント設定を有効にします。

  - **配信の最適化グループ ID に Configuration Manager 境界グループを使用します**
  - **Configuration Manager で管理されるデバイスで、コンテンツのダウンロードに Microsoft の接続済みキャッシュ サーバーを使用できるようにします**

- **共同管理デバイス向けのクライアント アプリ**のプレリリース機能を有効にします。 詳細については、「[プレリリース機能](../../servers/manage/pre-release-features.md)」を参照してください。

- 共同管理を有効にし、 **[クライアント アプリ]** ワークロードを **Pilot Intune** または **Intune** に切り替えます。 詳細については、以下の記事を参照してください。

  - [ワークロード - クライアント アプリ](../../../comanage/workloads.md#client-apps)
  - [共同管理を有効にする方法](../../../comanage/how-to-enable.md)
  - [ワークロードを Intune に切り替える](../../../comanage/how-to-switch-workloads.md)

    パイロットの場合は、クライアント アプリのパイロット コレクションにクライアントを追加します。

#### <a name="intune"></a>Intune

- この機能では、Intune Win32 アプリの種類のみがサポートされます。

  - この目的のために、Intune で新しいアプリを作成して割り当て (展開) します。 (Intune バージョン 1811 より前に作成されたアプリは機能しません。)詳細については、[Intune の Win32 アプリの管理](https://docs.microsoft.com/intune/apps/apps-win32-app-management)に関する記事を参照してください。

  - アプリのサイズは 100 MB 以上である必要があります。
  
    > [!TIP]
    > 次のグループ ポリシー設定を使用します。[コンピューターの構成] > [管理用テンプレート] > [Windows コンポーネント] > [配信の最適化] > **[最小ピア キャッシュ コンテンツ ファイル サイズ (MB)]** 。

## <a name="see-also"></a>関連項目

[Windows 10 更新プログラムの配信の最適化](../../../sum/deploy-use/optimize-windows-10-update-delivery.md)

[Configuration Manager における Microsoft 接続済みキャッシュのトラブルシューティング](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md)
