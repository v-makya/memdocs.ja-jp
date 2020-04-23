---
title: Linux および UNIX クライアントのアップグレード
titleSuffix: Configuration Manager
description: Configuration Manager で Linux または UNIX サーバーのクライアントをアップグレードします。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f71a36dff92f888d595538ff2fd483d7c212358f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696820"
---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Configuration Manager で Linux および UNIX サーバーのクライアントをアップグレードする方法

*適用対象:Configuration Manager (Current Branch)*

> [!Important]  
> バージョン 1902 以降の Configuration Manager では、Linux または UNIX クライアントはサポートされていません。 
> 
> Linux サーバーを管理するには、Microsoft Azure の管理を検討してください。 Azure ソリューションには広範囲な Linux サポートが含まれており、ほとんどの場合、Linux のエンドツーエンド パッチ管理など、Configuration Manager 以上の機能を備えています。

コンピューター上の Linux および UNIX 用のクライアントのバージョンを現在のクライアントをアンインストールせずに新しいクライアントのバージョンにアップグレードできます。 これを行うには、 **-keepdb** コマンド ライン プロパティを使用しながら、新しいクライアント インストール パッケージをコンピューターにインストールします。 Linux および UNIX 用のクライアントをインストールすると、既存のクライアント データが新しいクライアント ファイルで上書きされます。 ただし、 **-keepdb** コマンド ライン プロパティによって、クライアントの一意の識別子 (GUID)、情報のローカル データベース、証明書ストアの保持がインストール プロセスに指示されます。 この情報が新しいクライアントのインストールに使用されます。  

 たとえば、Linux および UNIX 用の Configuration Manager クライアントの最初のリリースのクライアントを実行している RHEL5 x64 コンピューターがあるとします。 このクライアントを累積的な更新プログラム 1 からクライアントのバージョンにアップグレードするには、 **-keepdb** コマンド ライン スイッチを付加して、**install** スクリプトを手動で実行し、累積的な更新プログラム 1 から該当するクライアント パッケージをインストールします。 次のコマンド ラインの例を参照してください。  

`./install -mp <hostname\> -sitecode <code\> -keepdb ccm-Universal-x64.<build\>.tar`  



## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Linux および UNIX サーバーでソフトウェアの展開を使用してクライアントをアップグレードする方法  
 ソフトウェアの展開を使用して、Linux および UNIX 用のクライアントを新しいクライアントのバージョンにアップグレードすることができます。 ただし、新しいクライアントのインストールで最初に現在のクライアントをアンインストールする必要があるため、Configuration Manager クライアントは新しいクライアントをインストールするインストール スクリプトを直接実行できません。 このアクションにより、新しいクライアントのインストールが開始される前に、インストール スクリプトを実行する Configuration Manager クライアント プロセスが終了します。 ソフトウェアの展開を使用した新しいクライアントのインストールを成功させるには、インストールを将来の時刻に開始して、オペレーティング システムの組み込みのスケジューリング機能によって実行されるようにスケジュールする必要があります。  

 ソフトウェアの展開を使用して、最初にクライアント コンピューターに新しいクライアント インストール パッケージのファイルをコピーします。 次に、クライアント インストール プロセスをスケジュールするスクリプトを展開して実行します。 このスクリプトは、オペレーティング システムの組み込みの **at** コマンドを使用してインストール プロセスの開始を遅らせます。 スクリプトが実行されると、その操作はコンピューター上の Configuration Manager クライアントではなく、クライアント オペレーティング システムによって管理されます。 この動作により、最初に Configuration Manager クライアントをアンインストールするスクリプトでコマンド ラインが呼び出されてから、新しいクライアントがインストールされます。 これらのアクションで、Linux または UNIX コンピューター上のクライアントのアップグレード プロセスが完了します。 アップグレードの完了後は、アップグレードされたクライアントの管理が Configuration Manager によって継続されます。  

 次の手順を使用して、Linux および UNIX 用のクライアントをアップグレードするようにソフトウェアの展開を構成します。 次の手順と例では、クライアントの最初のリリースを実行している RHEL5 x64 コンピューターを累積的な更新プログラム 1 のクライアントのバージョンにアップグレードします。  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Linux および UNIX サーバーでソフトウェアの展開を使用してクライアントをアップグレードするには  

1. 新しいクライアント インストール パッケージを、アップグレードする Configuration Manager クライアントを実行しているコンピューターにコピーします。  

    たとえば、クライアント コンピューター上の場所 ( **/tmp/PATCH**) に、クライアント インストール パッケージを配置して、累積的な更新プログラム 1 用のスクリプトをインストールします。  

2. Configuration Manager クライアントのアップグレードを管理するスクリプトを作成します。 次に、手順 1 のクライアント インストール ファイルと同じクライアント コンピューター上のフォルダーにスクリプトのコピーを配置します。  

    このスクリプトには、特定の名前を付ける必要はありません。 クライアント コンピューター上のローカル フォルダーにあるクライアント インストール ファイルを使用し、 **-keepdb** コマンド ライン プロパティを指定してクライアント インストール パッケージをインストールするのに十分なコマンド ラインを含める必要があります。 現在のクライアントの一意の識別子を、インストールしている新しいクライアントでも使用する場合は、 **-keepdb** コマンド ライン プロパティを使用します。  

    たとえば、次の行を含む、**upgrade.sh** という名前のスクリプトを作成します。  

   ```  
   #!/bin/sh  
   #  
   /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

   ```  

    次に、それをクライアント コンピューター上の **/tmp/PATCH** フォルダーにコピーします。

3. ソフトウェアの展開を使用して、各クライアントにコンピューターの組み込みの **at** コマンドを使用して **upgrade.sh** スクリプトを少し遅らせて実行するように指示します。  

    たとえば、次のコマンド ラインを使用してスクリプトを実行します。**at -f /tmp/upgrade.sh -m now + 5 minutes**  

   **upgrade.sh** スクリプトの実行が正常にスケジュールされたら、クライアントはソフトウェアの展開が正常に完了したことを示すステータス メッセージを送信します。 ただし、実際のクライアントのインストールは、遅延後に、コンピューターによって管理されます。 クライアントのアップグレードが完了したら、クライアント コンピューター上の **/var/opt/microsoft/scxcm.log** ファイルを調査してインストールを確認します。 Configuration Manager コンソールの **[資産とコンプライアンス]** ワークスペースの **[デバイス]** ノードでクライアントの詳細を表示することで、クライアントがインストールされ、サイトと通信していることを確認します。  
