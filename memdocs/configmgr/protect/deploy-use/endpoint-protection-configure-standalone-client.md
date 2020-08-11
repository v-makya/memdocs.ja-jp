---
title: スタンドアロン クライアントでの Endpoint Protection の構成
titleSuffix: Configuration Manager
description: スタンドアロン クライアントで Endpoint Protection を構成する方法を説明します。
ms.date: 07/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f8d116879b0a85f3276d848b01c69d575b8b69fd
ms.sourcegitcommit: 41b2b50d5870dc127a8848a6657d56112f92515a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87758314"
---
# <a name="configure-endpoint-protection-on-a-standalone-client"></a>スタンドアロン クライアントでの Endpoint Protection の構成

*適用対象:Configuration Manager (Current Branch)*

組織に、Microsoft Endpoint Configuration Manager で管理または保護できないスタンドアロン クライアントが多数存在する場合があります。 エンドポイント保護を設置しないと、これらのスタンドアロン クライアントはマルウェア攻撃を受けやすくなる可能性があります。 このようなスタンドアロン クライアントを保護するために、このトピックで説明するように、Endpoint Protection を使用して手動でそれらを構成できます。

スタンドアロン クライアントで Endpoint Protection を手動で構成するには、以下を行います。

- [スタンドアロン クライアントのマルウェア対策ポリシーを作成する](#create-an-antimalware-policy-for-the-standalone-client)
- [Endpoint Protection クライアント インストール パッケージをスタンドアロン クライアントに転送する](#transfer-endpoint-protection-client-installation-package-to-the-standalone-client)
- [スタンドアロン クライアント上で Endpoint Protection をインストールする](#install-endpoint-protection-on-the-standalone-client)

## <a name="prerequisites"></a>前提条件

スタンドアロン クライアントに Endpoint Protection を構成するための前提条件は次のとおりです。

- Endpoint Protection クライアント インストール パッケージ **scepinstall.exe** にアクセスできる必要があります。 このパッケージは、**C:\Program Files\Microsoft Configuration Manager\Client** フォルダーにあります。 
- [Endpoint Protection クライアント用の 2017 年 1 月のマルウェア対策プラットフォーム更新プログラム](https://support.microsoft.com/help/3209361/january-2017-anti-malware-platform-update-for-endpoint-protection-clie)がインストールされていることを確認します。 

## <a name="create-an-antimalware-policy-for-the-standalone-client"></a>スタンドアロン クライアントのマルウェア対策ポリシーを作成する

この手順では、Configuration Manager コンソールでカスタムのマルウェア対策ポリシーを作成し、それをスタンドアロン クライアントに転送します。

マルウェア対策ポリシーの作成時に、スタンドアロン クライアント上でポリシー定義を最新の状態に保つために、定義の更新ソースを構成する必要があります。 スタンドアロン クライアントがインターネットに接続されている場合は、定義の更新ソースを [Microsoft Update](endpoint-definitions-microsoft-updates.md) および [Microsoft マルウェア対策センター](endpoint-definitions-protection-center.md)として構成できます。 または、定義の配布ソースとして[ネットワーク共有](endpoint-definitions-network.md)を選択し、最新の定義更新パッケージを使用してこれを定期的に更新します。 

スタンドアロン クライアントのマルウェア対策ポリシーを作成するには、以下の手順を実行します。

1. **Configuration Manager** コンソールで、 **[資産とコンプライアンス]** をクリックします。
2. **[資産とコンプライアンス]** ワークスペースで **[Endpoint Protection]** を展開してから、 **[マルウェア対策ポリシー]** をクリックします。
3. **ホーム** ] タブで、 **作成** グループで、[ **マルウェア対策ポリシーを作成する**です。
4. **全般** のセクション、 **マルウェア対策ポリシーを作成する**  ダイアログ ボックスで、名前と、ポリシーの説明を入力します。
5. **マルウェア対策ポリシーを作成する**  ダイアログ ボックスで、クリックして、マルウェア対策ポリシーに必要な設定を構成 **OK**です。 構成できる設定の一覧については、「[マルウェア対策ポリシーの一覧](endpoint-antimalware-policies.md#list-of-antimalware-policy-settings)」をご覧ください。
    > [!NOTE]
    > **定義の更新**設定では、スタンドアロン クライアントがインターネットに接続されている場合は、 **[Microsoft Update から配信された更新プログラム]** と **[Microsoft Malware Protection Center から配信された更新プログラム]** を選択します。  
    > または、 **[UNC ファイル共有から更新する]** を選択して、ネットワーク共有経由でポリシー定義を配布します。 次に、ネットワーク共有上の定義の更新ファイルの場所を示す UNC パスを 1 つまたは複数追加します。

6. 新しく作成されたポリシーを XML としてエクスポートします。
    1. **[マルウェア対策ポリシー]** の一覧で、目的のポリシーを右クリックします。
    1. **[エクスポート]** を選択します。
    1. ポリシーを XML として保存します (**standalone.xml** など)。
7. 新しいマルウェア対策ポリシー XML を、Endpoint Protection の構成先のスタンドアロン クライアントに転送します。

## <a name="transfer-endpoint-protection-client-installation-package-to-the-standalone-client"></a>Endpoint Protection クライアント インストール パッケージをスタンドアロン クライアントに転送する

この手順では、Configuration Manager サーバーから Endpoint Protection クライアント インストール パッケージ (**scepinstall.exe**) をコピーし、それをスタンドアロン クライアントに転送します。

1. Configuration Manager サーバーにログインします。
2. Configuration Manager インストール フォルダーの **Client** フォルダーに移動します (**C:\Program Files\Microsoft Configuration Manager\Client**)。
3. **scepinstall.exe** をコピーします。
4. **scepinstall.exe** を、Endpoint Protection クライアント ソフトウェアのインストール先のスタンドアロン クライアントに転送します。

## <a name="install-endpoint-protection-on-the-standalone-client"></a>スタンドアロン クライアント上で Endpoint Protection をインストールする
この手順では、スタンドアロン クライアント上のコマンド プロンプトから、インストーラー パッケージ (**scepinstall.exe**) とマルウェア対策ポリシー (両方とも以前に Configuration Manager サーバーから転送されたもの) を実行します。

スタンドアロン クライアントで Endpoint Protection をインストールするには、次の手順を実行します。

1. スタンドアロン クライアントで、コマンド プロンプトを管理者として開きます。
2. **scepinstall.exe** インストーラー ファイルを保存したフォルダーにディレクトリを変更します。
3. 次のコマンドを入力して、マルウェア対策ポリシーを使用して **scepinstall.exe** を実行します。

    ```cmd
    scepinstall.exe /policy <full path>\<policy file>
    ```

    `full path` をマルウェア対策ポリシー XML ファイルを保存したパスに置き換え、`policy file` をマルウェア対策ポリシー ファイル名に置き換えます。
 
    インストーラーが展開され、インストール ウィザードが起動します。

4. 画面に表示される指示に従って、クライアントのインストールを完了します。

    インストール ウィザードの最後の画面では、最新の更新プログラムを取得した後に、潜在的な脅威がないかコンピューターをスキャンするオプションが既定で選択されます。 スキャンをスキップするには、チェックボックスをオフにします。

## <a name="change-antimalware-policy-settings-on-a-standalone-endpoint-protection-client"></a>スタンドアロン Endpoint Protection クライアントでマルウェア対策ポリシーの設定を変更する

スタンドアロン Endpoint Protection クライアントでマルウェア対策ポリシーを変更または更新するには、次のようにします。 

1. [スタンドアロン クライアントのマルウェア対策ポリシーを作成します](#create-an-antimalware-policy-for-the-standalone-client)。
2. スタンドアロン クライアントで次のコマンドを実行します。

```cmd
C:\Program Files\Microsoft Security Client\ConfigSecurityPolicy.exe <full path>\<policy file>
```

`full path` を新しいマルウェア対策ポリシー XML ファイルを保存したパスに置き換え、`policy file` をマルウェア対策ポリシー ファイル名に置き換えます。

## <a name="next-steps"></a>次の手順

Endpoint Protection を使用して構成マネージャー クライアント コンピューターのセキュリティとマルウェアを管理する方法については、「[Endpoint Protection の構成](endpoint-protection-configure.md)」をご覧ください。