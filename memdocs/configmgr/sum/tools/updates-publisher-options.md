---
title: オプションを構成する
titleSuffix: Configuration Manager
description: System Center Updates Publisher を使用するためのオプションを構成する
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8b6578e32d5ae5a003c485960b556f3b87e8d557
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700070"
---
# <a name="configure-options-for-updates-publisher"></a>Updates Publisher のオプションを構成する

*適用対象: System Center Updates Publisher*

Updates Publisher の操作に影響するオプションおよび関連する設定を確認し、構成します。

Updates Publisher のオプションにアクセスするには、コンソールの左上隅で、 **[Updates Publisher]** **[プロパティ]** タブを開き、 **[オプション]** を選択します。

![Options](media/properties1.png)   


オプションは、次のように分けられています。

-   更新サーバー
-   ConfigMgr サーバー
-   プロキシの設定
-   信頼された発行元
-   詳細設定
-   Updates
-   ログ記録

## <a name="update-server"></a>更新サーバー
[更新プログラムを公開](manage-updates-with-updates-publisher.md#publish-updates-and-bundles-from-the-updates-workspace)するには、その前に、Windows Server Update Services (WSUS) などの更新サーバーと連携するように Updates Publisher を構成する必要があります。 これには、サーバーの指定、コンソールからリモートである場合にこのサーバーに接続する方法、および発行する更新プログラムのデジタル署名に使用する証明書が含まれています。

- **更新サーバーを構成します**。 更新サーバーを構成するときに、Configuration Manager 階層の最上位の WSUS サーバー (更新サーバー) を選択して、発行する更新プログラムにすべての子サイトがアクセスできるようにします。

  更新サーバーが Updates Publisher サーバーからリモートの場合は、サーバーの完全修飾ドメイン名 (FQDN) を指定します。 SSL で接続する場合、既定のポートが 8530 から 8531 に変わります。 設定したポートが更新サーバーで使用されているポートと一致していることを確認してください。

  > [!TIP]  
  > 更新サーバーを構成しない場合でも、ソフトウェア更新プログラムの作成に Updates Publisher を使用できます。

- **署名証明書を構成します**。 署名証明書を構成するには、更新サーバーを構成して正常に接続できている必要があります。

  Updates Publisher では、署名証明書を使用して、更新サーバーに発行されるソフトウェア更新プログラムに署名します。 更新サーバーまたは Updates Publisher を実行しているコンピューターの証明書ストアでデジタル証明書が使用できない場合、発行は失敗します。

  証明書ストアに証明書を追加する方法の詳細については、「[Updates Publisher の証明書とセキュリティ](updates-publisher-security.md)」を参照してください。

  更新サーバーに対するデジタル証明書が自動的に検出されない場合は、次のいずれかを選択します。

  -   **[参照]** : [参照] は、更新サーバーがコンソールを実行するサーバーにインストールされている場合にのみ使用できます。 証明書を選択した後、 **[作成]** を選択して、更新サーバーの WSUS 証明書ストアにその証明書を追加する必要があります。 この方式によって選択する証明書の **.pfx** ファイルのパスワードを入力する必要があります。

  -   **[作成]** : このオプションを使用して、新しい証明書を作成します。 これにより、更新サーバーの WSUS 証明書ストアにも証明書が追加されます。

  **独自の署名証明書を作成する場合は**、次を構成します。

  -   **[秘密キーのエクスポートを許可する]** オプションを有効にします。

  -   **[キー使用法]** にデジタル署名を設定します。

  -   **[キーの最小サイズ]** に 2048 ビット以上の値を設定します。

  WSUS 証明書ストアから証明書を削除するには、 **[削除]** オプションを使用します。 このオプションは、更新サーバーが使用する Updates Publisher コンソールに対してローカルである場合、または **SSL** を使用してリモート更新サーバーに接続しているときに利用可能です。

## <a name="configmgr-server"></a>ConfigMgr サーバー
Updates Publisher と Configuration Manager を合わせて使用する場合は、これらのオプションを使用します。

-   **Configuration Manager サーバーを指定する:** Configuration Manager のサポートを有効にした後で、Configuration Manager 階層から最上位階層サイト サーバーの場所を指定します。 Updates Publisher のインストールからリモートのサーバーの場合は、サイト サーバーの FQDN を指定します。 **[接続のテスト]** を選択してサイト サーバーに接続できることを確認します。

-   **しきい値を構成する:** しきい値は、パブリケーションの種類を [自動] にして更新プログラムを発行する場合に使用されます。 しきい値の値は、メタデータのみではなく、更新プログラムの完全なコンテンツを発行するかを判別するために役立ちます。 パブリケーションの種類について詳しくは、「[更新プログラムをパブリケーションに割り当てる](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication)」を参照してください。

    以下のしきい値のうち一方または両方を使用できます。

    -   **[Requested client count threshold]\(要求したクライアント数のしきい値):** Updates Publisher でこの更新プログラムの完全なセットを自動的に発行する前に、この更新プログラムを要求する必要のあるクライアントの数を定義します。 指定した数のクライアントがこの更新プログラムを要求するまでは、更新プログラムのメタデータのみが発行されます。

    -   **[Package source size threshold (MB)][パッケージ ソースのサイズのしきい値 (MB)]:** これにより、指定したサイズを超える更新プログラムを自動発行できないようにします。 更新プログラムのサイズがこの値を超えている場合は、メタデータのみが発行されます。 指定したサイズよりも小さい更新プログラムは、完全なコンテンツを発行できます。

## <a name="proxy-settings"></a>プロキシの設定
Updates Publisher は、インターネットからソフトウェア カタログをインポートするときや、更新プログラムをインターネットに公開するときに、プロキシ設定を使用します。

-   プロキシ サーバーの FQDN または IP アドレスを指定します。 IPv4 と IPv6 がサポートされます。

-   プロキシ サーバーでインターネット アクセス用にユーザーを認証する場合は、Windows 名を指定する必要があります。 ユニバーサル プリンシパル名 (UPN) はサポートされていません。

## <a name="trusted-publishers"></a>信頼された発行元
更新プログラム カタログをインポートするときは、そのカタログのソース (その証明書に基づく) が、信頼された発行元として追加されます。 同様に、更新プログラムを発行するときは、更新プログラムの証明書のソースが信頼された発行元として追加されます。

各発行者の証明書の詳細を表示でき、信頼された発行元の一覧から発行元を削除できます。

信頼されていない発行元からのコンテンツは、クライアントが更新プログラムをスキャンするときに、クライアント コンピューターで問題を起こす可能性があります。 信頼された発行元からのみコンテンツのみを受け入れる必要があります。

## <a name="advanced"></a>詳細設定
[詳細設定] オプションは、次のとおりです。

-   **[データベースの場所]:** データベース ファイル **scupdb.sdf** の場所を表示および変更します。 このファイルは、Updates Publisher のリポジトリです。

-   **[タイムスタンプ]:** 有効な場合、署名日時を示すタイムスタンプが署名する更新プログラムに追加されます。 証明書が有効なときに署名された更新プログラムは、その署名証明書の期限が切れた後も使用できます。 既定では、署名証明書の期限が切れた後は、ソフトウェア更新プログラムをデプロイできません。

-   **[Check for updates to subscribed catalogs]\(サブスクライズ済みのカタログを調べて更新プログラムを確認する):** Updates Publisher では、起動されるたびに、サブスクライブされているカタログで更新プログラムを確認できます。 カタログの更新が検出されると、 **[更新プログラム ワークスペース]** の **[概要]** ウィンドウに **[最近のアラート]** として詳細が表示されます。

-   **[証明書失効]:** 証明書失効のチェックを有効にするには、このオプションを選択します。

-   **[Local source publishing]\(ローカル ソースの発行):** Updates Publisher は、インターネットからその更新プログラムをダウンロードする前に、発行中の更新プログラムのローカル コピーを使用できます。 この場所は、Updates Publisher を実行しているコンピューター上のフォルダーである必要があります。 この場所は、既定では、**マイ ドキュメント\LocalSourcePublishing** です。 既に 1 つまたは複数の更新プログラムをダウンロードしてあるか、デプロイする更新プログラムに変更を加えたときに、これを使用します。

-   **[Software Updates Cleanup Wizard]\(ソフトウェア更新プログラムのクリーンアップ ウィザード):** 更新プログラムのクリーンアップ ウィザードを起動します。 このウィザードでは、更新サーバーにある一方で Updates Publisher リポジトリにない更新プログラムを期限切れにします。 詳細については、「[参照されていない更新プログラムを期限切れにする](#expire-unreferenced-software-updates)」を参照してください

## <a name="updates"></a>Updates
 Updates Publisher は、開くたびに新しい更新プログラムを自動的に確認できます。 Updates Publisher のプレビュー ビルドを受け取ることも選択できます。

手動で更新プログラムをチェックするには、Updates Publisher コンソールで、![[プロパティ]](media/properties2.png)  
をクリックして、 **[Updates Publisher Properties]\(Updates Publisher のプロパティ)** を開き、 **[Check for update]\(更新プログラムのチェック)** を選択します。

Updates Publisher で新しい更新プログラムを検出すると、 **[更新プログラムを利用可能]** ウィンドウが表示され、選択してインストールできます。 更新プログラムをインストールしない場合は、次回コンソールを開くときに提供されます。

## <a name="logging"></a>ログ記録
Updates Publisher は、Updates Publisher についての基本的な情報を **%WINDIR%\Temp\UpdatesPublisher.log** ログに記録します。

メモ帳または **CMTrace** を使用してログを表示します。 CMTrace は Configuration Manager のログ ファイル ツールで、Configuration Manager のソース メディアの **\SMSSetup\Tools** フォルダーにあります。

ログのサイズとその詳細レベルを変更できます。

データベース ログを有効にすると、Updates Publisher データベースに対して実行されるクエリに関する情報が含まれます。 データベース ログの使用は、Updates Publisher コンピューターのパフォーマンスの低下につながることがあります。

ログ ファイルを表示するには、コンソールで ![[プロパティ]](media/properties2.png) をクリックして **[Updates Publisher Properties]\(Updates Publisher のプロパティ)** を開き、 **[ログ ファイルの表示]** を選択します。

## <a name="expire-unreferenced-software-updates"></a>参照されていないソフトウェア更新プログラムを期限切れにする
**Software Update Cleanup (ソフトウェア更新プログラムのクリーンアップ) ウィザード**を実行すると、更新サーバー上にある一方で Updates Publisher リポジトリにない更新プログラムを期限切れにすることができます。 これが Configuration Manager に通知されて、将来の展開からこれらの更新プログラムが削除されます。

更新プログラムを期限切れにする操作を元に戻すことはできません。 このタスクは、選択したソフトウェア更新プログラムが、組織で不要になったことを確認してからのみ実行してください。

### <a name="to-remove-expired-software-updates"></a>期限切れのソフトウェア更新プログラムを削除するには
1.  Updates Publisher コンソールで ![[プロパティ]](media/properties2.png) をクリックして **[Updates Publisher Properties]\(Updates Publisher のプロパティ)** を開き、 **[オプション]** を選択します。

2.  **[詳細設定]** を選択し、 **[Software Update Clean Wizard]\(ソフトウェア更新プログラムのクリーンアップ ウィザード)** で、 **[開始]** を選択します。

3.  期限切れにするソフトウェア更新プログラムを選択してから **[次へ]** を選択します。

4.  選択内容を確認してから、 **[次へ]** を選択して、選択内容を受け入れ、これらの更新プログラムを期限切れにします。

5.  ウィザードが完了してから **[閉じる]** を選択してウィザードを完了します。
