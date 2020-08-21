---
title: 分類と製品の構成
titleSuffix: Configuration Manager
description: Configuration Manager コンソールで次の手順を利用し、同期させるソフトウェア更新プログラムの分類と製品を構成します。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: 7dc3ef2ceb22f1c15c96127c593965ea31bdd7eb
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696822"
---
# <a name="configure-classifications-and-products-to-synchronize"></a>同期する分類と製品の構成  

*適用対象:Configuration Manager (Current Branch)*

ソフトウェアの更新ポイント コンポーネントのプロパティで指定した設定に基づき、Configuration Manager で、同期プロセス中にソフトウェア更新メタデータが取得されます。 ソフトウェア更新を初めて同期した後、あるいは新しい製品や分類がリリースされるとき、プロパティに進み、新しい項目を選択する必要があります。 次の手順を使用し、同期させる分類と製品を構成します。  

> [!NOTE]  
> このセクションの手順は、最上位サイトの場合のみ従ってください。  

## <a name="to-configure-classifications-and-products-to-synchronize"></a>同期させる分類と製品を構成する方法  

1. **Configuration Manager** コンソールで、 **[管理]** 、 **[サイトの構成]** 、 **[サイト]** に移動します。

2. 中央管理サイトまたはスタンドアロン プライマリ サイトを選択します。  

3. **[ホーム]** タブの **[設定]** グループで **[サイト コンポーネントの構成]** をクリックし、 **[ソフトウェアの更新ポイント]** を選択します。

4. **[分類]** タブで、ソフトウェア更新プログラムを同期させるソフトウェア更新プログラムの分類を指定します。  

    すべてのソフトウェア更新プログラムは、各種の更新プログラムを整理するための更新プログラムの分類により定義されます。 同期プロセス中に、指定した分類のソフトウェアの更新プログラムのメタデータが同期されます。 Configuration Manager には次の更新プログラムの分類でソフトウェアの更新を同期する機能が用意されています。  

     - **重要な更新**:重要でセキュリティに関係しない不具合に対応する特定の問題に対して一般にリリースされた修正プログラムを指定します。  
     - **定義ファイルの更新:** 製品の定義データベースに追加される、頻繁に一般に公開されるソフトウェア更新プログラムを指定します。  
     - **Feature Pack**:最初に製品リリースに先立って配布され、通常は次回の製品版リリースに含まれる、製品の新機能を指定します。  
     - **セキュリティ更新プログラム:** 製品固有でセキュリティに関係する脆弱性に対して、一般にリリースされた修正を指定します。  
     - **Service Pack**:製品に適用されるすべての修正プログラム、セキュリティ更新プログラム、重要な更新プログラム、および更新プログラムを累積したテスト済みのセットを指定します。 さらに、Service Pack には、製品のリリース以降に内部で見つかった問題に対する追加の修正プログラムが含まれる場合もあります。  
     - **ツール**:1 つ以上のタスクを完了するのに役立つユーティリティまたは機能を指定します。  
     - **更新プログラムのロールアップ**:修正プログラム、セキュリティ更新プログラム、重要な更新プログラム、他の更新プログラムを展開しやすいようにパッケージにしたテスト済みのセットを指定します。 更新プログラムのロールアップは、通常、セキュリティまたは製品コンポーネントなど特定の領域に対応します。  
     - **更新プログラム**:特定の問題に対して一般にリリースされた修正プログラムを指定します。 更新プログラムは、重大ではない非セキュリティ関連のバグに対処します。  
     - **アップグレード**:Windows 10 の機能のアップグレードを指定します。 ソフトウェアの更新ポイントとサイトは最低限 WSUS 6.2 と[修正プログラム 3095113](https://support.microsoft.com/kb/3095113) を実行して、**アップグレード**の分類を取得する必要があります。 この更新プログラムおよび**アップグレード**用のその他の更新プログラムのインストールの詳細については、「[ソフトウェア更新プログラムの前提条件](../plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012)」を参照してください。
    
    > [!NOTE]
    > **[Microsoft Surface のドライバーとファームウェアの更新プログラムを含める]** チェックボックスをオンにして、Microsoft Surface ドライバーを同期することができます。<!--1098490--> Surface ドライバーを正常に同期するには、すべてのソフトウェアの更新ポイントで Windows Server 2016 以降を実行している必要があります。 Surface ドライバーを有効にした後、Windows Server 2012 を実行するコンピューターにソフトウェアで更新ポイントを有効にすると、ドライバーの更新プログラムのスキャン結果が不正確になります。 これにより、不適切なコンプライアンス データが Configuration Manager コンソールと Configuration Manager レポートに表示されます。 詳細については、「[Configuration Manager を使用して Surface ドライバーを管理する](../deploy-use/surface-drivers.md)」を参照してください。

5. **[製品]** タブで、ソフトウェア更新プログラムを同期させる製品の更新の分類を指定し、 **[閉じる]** をクリックします。  

    - Configuration Manager は、ソフトウェアの更新ポイントを初めてインストールするときに選択できる製品と製品ファミリのリストを保存します。 Configuration Manager のリリース後にリリースされる製品と製品ファミリは、選択できる使用可能な製品と製品ファミリのリストを更新する、ソフトウェア更新プログラムの同期を完了するまでは選択できない可能性があります。  

    - 各ソフトウェア更新プログラムのメタデータは、更新プログラムが適用される製品を定義します。 製品とは、オペレーティング システムまたはアプリケーションの特定エディションのことです (Windows Server 2012 など)。 製品ファミリは、個々の製品が派生する基礎となるオペレーティング システムまたはアプリケーションです。 製品ファミリの例として Windows があり、Windows Server 2012 はそのメンバーです。 製品ファミリまたは製品ファミリ内の個別製品を指定できます。 選択する製品が多くなるほど、ソフトウェア更新プログラムを同期させるのに必要な時間が長くなります。  

    - ソフトウェア更新プログラムが複数の製品に適用可能な状態で、少なくとも 1 つの製品の同期を選択した場合、選択されていない製品も含めてすべての製品が Configuration Manager コンソールに表示されます。 たとえば、選択しているオペレーティング システムが Windows Server 2012 のみで、ソフトウェア更新プログラムが Windows 8 と Windows Server 2012 に適用される場合、Configuration Manager コンソールには両方の製品が表示されます。  

    > [!NOTE]  
    > **Windows 10 バージョン 1903 以降**は、以前のバージョンのように **Windows 10** の一部としてではなく、独自の製品として Microsoft Update に追加されました。 この変更により、クライアントでこれらの更新プログラムが確実に表示されるようにするための多くの手動のステップが発生しました。 Configuration Manager バージョン 1906 で、新製品に対して手動で行う必要がある手順の数を減らすことができました。 <!--4682946-->
    >
    > Configuration Manager バージョン 1906 に更新し、同期のために **Windows 10** 製品が選択されていると、次のアクションが自動的に行われます。
    > - **Windows 10 バージョン 1903 以降**の製品が同期のために追加されます。
    > - **Windows 10** 製品を含む[自動展開規則](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)が、**Windows 10 バージョン 1903 以降**が含まれるように更新されます。
    > - **Windows 10 バージョン 1903 以降**の製品を含めるため、[サービス プラン](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)が更新されます。


## <a name="configuring-products-for-versions-of-windows-10"></a>Windows 10 のバージョンの製品の構成

### <a name="windows-10-version-1909"></a>Windows 10 バージョン1909

Windows 10 バージョン 1909 では、Windows 10 バージョン 1903 と共通のコア オペレーティング システムを共有しています。 これらのバージョンはどちらも、同じ累積的な更新プログラムで提供されています。 Windows 10 バージョン 1909 の詳細については、[windows 10 バージョン 1909 配信オプション](https://aka.ms/1909mechanics)に関するブログ記事を参照してください。

Windows 10 バージョン 1909 と Windows 10 の両方で、バージョン 1903 クライアントが Configuration Manager から更新プログラムをインストールするようにするには、次のようにします。

- Windows 10 の 1909 と 1903 の両方のバージョンの更新プログラムを承認します。
  - 更新プログラムのタイトルと適用規則は、OS のバージョンごとに異なります。
  - OS のバージョンとアーキテクチャごとに各更新プログラムを承認すると、管理者の通常の承認プロセスが維持されます。
- 累積的な更新プログラムのインストール ファイルは、Windows 10 の 1909 と 1903 の両方のバージョンで同じです。
  - Configuration Manager では、更新プログラムのソース ファイルが 1 回だけダウンロードされます。

#### <a name="feature-updates-for-windows-10-version-1909"></a>Windows 10 バージョン 1909 の機能更新プログラム

Windows 10 バージョン 1909 の機能更新プログラムを承認すると、いくつかの異なるオプションが表示されます。

- Windows 10 バージョン 1903 クライアントには、2019 年 11 月 12 日にリリースされた[有効化パッケージ](https://support.microsoft.com/en-us/help/4517245/feature-update-via-windows-10-version-1909-enablement-package)が提供されています。
  - 有効化パッケージは簡単にインストールできる小さなファイルで、Windows 10 バージョン 1909 の機能をアクティブ化し、デバイスを再起動します。
  - 有効化パッケージの前提条件は次のとおりです。
    - 2019 年 10 月 8 日にリリースされた [KB4517389](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4517389) の最小累積更新プログラム。
    - 2019 年 9 月 24 日にリリースされた [KB4520390](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4520390) の最小サービス スタック更新プログラム。
  - この更新プログラムは、他の機能更新プログラムと同様に、`https:\\catalog.update.microsoft.com` からのインポートには使用できません。
  - 更新プログラムは、**Windows 10 バージョン 1903 以降**の製品および**アップグレード**分類が同期用に選択されている場合、WSUS と自動的に同期されます。
  - Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースにアクセスし、 **[Windows 10 のサービス]** を展開して、 **[すべての Windows 10 更新プログラム]** ノードを選択します。 "有効化" または "4517245" という語句を検索します。

    > [!TIP]
    > これらは機能更新プログラムであるため、 **[すべてのソフトウェア更新プログラム]** ノードにはありません。

- Windows 10 バージョン 1809 以前のクライアントは、単一の直接機能更新プログラムを使用してアップグレードされます。
  - これは、Windows 10 で今までに実行した機能更新プログラム用の他のすべてのインストールと同じです。

> [!NOTE]
> インストールに使用されたパスに関係なく、有効化パッケージと Windows 10 バージョン 1909 の従来の機能更新プログラムはどちらも "インストール済み" としてレポートに表示されます。

### <a name="windows-10-version-1903-and-later"></a>Windows 10 バージョン 1903 以降

**Windows 10 バージョン 1903 以降**は、以前のバージョンのように **Windows 10** の一部としてではなく、独自の製品として Microsoft Update に追加されました。 この変更により、クライアントでこれらの更新プログラムが確実に表示されるようにするための多くの手動のステップが発生しました。 Configuration Manager バージョン 1906 で、新製品に対して手動で行う必要がある手順の数を減らすことができました。 <!--4682946-->

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1906"></a>Windows 10 バージョン 1903 以降で Configuration Manager バージョン 1906 を使用する
Configuration Manager バージョン 1906 に更新し、同期のために **Windows 10** 製品が選択されていると、次のアクションが自動的に行われます。
- **Windows 10 バージョン 1903 以降**の製品が同期のために追加されます。
- **Windows 10** 製品を含む[自動展開規則](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)が、**Windows 10 バージョン 1903 以降**が含まれるように更新されます。
- **Windows 10 バージョン 1903 以降**の製品を含めるため、[サービス プラン](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)が更新されます。

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1902"></a>Windows 10 バージョン 1903 以降で Configuration Manager バージョン 1902 を使用する
Windows 10 バージョン 1903 クライアントで Configuration Manager 1902 を使用している場合は、次のことを行う必要があります。
- 同期のために **Windows 10 バージョン 1903 以降**の製品を選択します。
- Windows 10 バージョン 1903 クライアントの[自動展開規則](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)を更新します。
- Windows 10 バージョン 1903 クライアントの[サービス プラン](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)を更新します。

## <a name="windows-insider-program"></a><a name="bkmk_WIfB"></a> Windows Insider Program
<!--3556023-->
2019 年 9 月以降、Configuration Manager を使って、Windows Insider Preview ビルドを実行しているデバイスの点検と更新を行えるようになりました。 この変更によって、ご自身の通常のプロセスを変更したり、Windows Update for Business を有効にしたりすることなく、これらのデバイスを管理できるようになります。 他の Windows 10 更新プログラムまたはアップグレードと同様に、Windows Insider Preview ビルドの機能更新プログラムと累積的な更新プログラムを Configuration Manager にダウンロードできます。 詳細については、[プレリリースの Windows 10 機能更新プログラムを WSUS に公開する](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Publishing-pre-release-Windows-10-feature-updates-to-WSUS/ba-p/845054)に関するブログ記事を参照してください。

Configuration Manager での Windows Insider のサポートの詳細については、[Windows 10 のサポート](../../core/plan-design/configs/support-for-windows-10.md#bkmk_WIfB-support)に関するページを参照してください。

### <a name="prerequisites"></a>[前提条件]

- [ソフトウェア更新プログラムの管理](../plan-design/plan-for-software-updates.md)用に構成された、Configuration Manager バージョン 1906 以降。
- [Windows Insider Preview ビルド](/windows-insider/at-work-pro/wip-4-biz-get-started)を実行している Windows 10 デバイス。
- Windows Insider デバイスを含むコレクション。

### <a name="enable-windows-insider-upgrades-and-updates"></a>Windows Insider のアップグレードと更新プログラムを有効にする

Windows Insider のアップグレードと更新プログラム用に製品と分類を有効にする必要があります。 Windows Insider の機能更新プログラム、累積的な更新プログラム、およびその他の更新プログラムは、**Windows Insider プレリリース**製品カテゴリにあります。

1. **Configuration Manager** コンソールで、 **[管理]** 、 >  **[サイトの構成]** 、 >  **[サイト]** に移動します。
2. 中央管理サイトまたはスタンドアロン プライマリ サイトを選択します。  
3. **[ホーム]** タブの **[設定]** グループで **[サイト コンポーネントの構成]** をクリックし、 **[ソフトウェアの更新ポイント]** を選択します。
4. **[製品]** タブで、次の製品が同期対象として選択されていることを確認します。
    - Windows Insider プレリリース
    - Windows 10 バージョン 1903 以降
5. **[分類]** タブで、次の分類が同期対象として選択されていることを確認します。
    - アップグレード
    - セキュリティ更新プログラム
    - 更新プログラム (オプション)
6. **[OK]** をクリックして、 **[ソフトウェアの更新ポイント コンポーネントのプロパティ]** を閉じます。

### <a name="upgrading-windows-insider-devices"></a>Windows Insider デバイスのアップグレード

Windows Insider のアップグレードが同期されると、 **[ソフトウェア ライブラリ]**  >  **[Windows 10 のサービス]**  >  **[すべての Windows 10 更新プログラム]** から確認できます。

![Windows 10 のサービスの Windows Insider 機能更新プログラム](media/3556023-windows-insiders-pre-release-feature-update.png)

他のアップグレードと同じように、Windows Insider の機能更新プログラムをターゲット コレクションに展開します。 ただし、これらの機能更新プログラムを展開するときは、次の点に注意してください。

- これらのアップグレードは、アーキテクチャ、エディション、および言語が一致するすべての Windows 10 クライアント 1903 以前に適用されます。
- ライセンス条項がある場合、インストールするためには、展開で条項に同意する必要があります。
- [クライアント設定のスレッドの優先順位](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority)を使用することを検討してください。
- 動的更新により、最新の累積的な更新プログラムを含む重要な更新プログラムが Microsoft Update から直接自動的にインストールされます。 この動作は、Windows 10 バージョン 1903 の機能更新プログラムで開始されました。 
  - 明示的に[クライアント設定の動的更新を無効](../../core/clients/deploy/about-client-settings.md#bkmk_du)にできます。[setupconfig.ini ファイル](/windows-hardware/manufacture/desktop/windows-setup-command-line-options)を使用して無効にすることもできます。 
  - 詳細については、[Windows 10 の動的更新](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847)に関するブログ記事を参照してください。

アップグレードを展開する方法の詳細については、[サービスとしての Windows の管理](../../osd/deploy-use/manage-windows-as-a-service.md)に関するページを参照してください。


### <a name="keeping-insider-devices-up-to-date"></a>Insider デバイスを最新の状態に保つ

Windows Insider の累積的な更新プログラムは、WSUS および Configuration Manager 用拡張機能によって利用可能になります。 これらの累積的な更新プログラムは、Windows 10 バージョン 1903 の累積的な更新プログラムと同様の頻度でリリースされます。 Windows Insider の累積的な更新プログラムは、**Windows Insider プレリリース**製品カテゴリに含まれており、**セキュリティ更新プログラム**または**更新プログラム**として分類されています。 [自動展開規則](../deploy-use/automatically-deploy-software-updates.md)や[段階的な展開](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json)など、通常のソフトウェア更新プロセスを使用して、Windows Insider の累積的な更新プログラムを展開できます。

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a> 延長セキュリティ更新プログラムと Configuration Manager

[延長セキュリティ更新プログラム (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) は、特定のレガシ Microsoft 製品をサポート終了後に実行する必要があるお客様のための最後の手段となります。 これには、製品の延長サポート期間が終了してから最長 3 年間、重大または重要なセキュリティ更新プログラム ([Microsoft Security Response Center (MSRC)](https://www.microsoft.com/msrc) によって定義されています) が含まれます。

既にサポート ライフサイクルが終了している製品は、Configuration Manager ではサポートされません。 これには、ESU プログラムの対象となるすべての製品が含まれます。 たとえば、Windows 7 です。 ESU プログラムでリリースされたセキュリティ更新プログラムは、Windows Server Update Services (WSUS) に発行されます。 これらの更新プログラムは、Configuration Manager コンソールに表示されます。 ESU プログラムの対象となる製品は、Configuration Manager での使用がサポートされなくなりましたが、[最新リリース バージョンの Configuration Manager の現在のブランチ](../../core/servers/manage/updates.md#version-details)を使用して、プログラムでリリースされた Windows セキュリティ更新プログラムを展開およびインストールできます。 Windows 7 を稼働しているデバイスに Windows 10 を展開するために、最新のリリース バージョンを使用することもできます。

Windows ソフトウェア更新プログラムの管理または OS 展開に関係のないクライアント管理機能は、ESU プログラムの対象となるオペレーティング システムではテストされなくなり、引き続き機能することが保証されません。 クライアント管理のサポートを受けるには、できるだけ早く現在のバージョンのオペレーティング システムにアップグレードまたは移行することを強くお勧めします。


## <a name="next-steps"></a>次のステップ

ソフトウェア更新プログラムの同期を開始し、新しい基準でソフトウェア更新プログラムを取得します。 詳細については、「[ソフトウェア更新プログラムの同期](synchronize-software-updates.md)」を参照してください。