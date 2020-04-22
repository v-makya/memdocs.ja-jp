---
title: Linux および UNIX クライアントを管理する
titleSuffix: Configuration Manager
description: Configuration Manager で Linux および UNIX サーバーのクライアントを管理します。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 716441bd146e9172b3f183c497fcaa4036ad0084
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690050"
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Configuration Manager で Linux および UNIX サーバーのクライアントを管理する方法

*適用対象:Configuration Manager (Current Branch)*

> [!Important]  
> バージョン 1902 以降の Configuration Manager では、Linux または UNIX クライアントはサポートされていません。 
> 
> Linux サーバーを管理するには、Microsoft Azure の管理を検討してください。 Azure ソリューションには広範囲な Linux サポートが含まれており、ほとんどの場合、Linux のエンドツーエンド パッチ管理など、Configuration Manager 以上の機能を備えています。

Configuration Manager で Linux および UNIX サーバーを管理する場合、サーバーを管理しやすいように、コレクション、メンテナンス期間、およびクライアント設定を構成できます。 また、Linux および UNIX 用の Configuration Manager クライアントにはユーザー インターフェイスがありませんが、クライアントにクライアント ポリシーの手動ポーリングを強制することもできます。

##  <a name="collections-of-linux-and-unix-servers"></a><a name="BKMK_CollectionsforLnU"></a> Linux および UNIX サーバーのコレクション  
 コレクションを使用して Linux および UNIX サーバーのグループを管理する方法は、コレクションで他のクライアントの種類を管理する方法と同じです。 コレクションとして使用できるのは、ダイレクト メンバーシップ コレクションまたはクエリ ベースのコレクションです。 クエリ ベースのコレクションでは、クライアント オペレーティング システム、ハードウェア構成、またはサイト データベースに格納されているクライアントに関するその他の詳細情報を識別します。 たとえば、Linux および UNIX サーバーを含むコレクションを使用すると、次の設定を管理できます。  

- クライアント設定  

- ソフトウェアの展開  

- メンテナンス期間の適用  

  Linux または UNIX クライアントをそのオペレーティング システムまたはディストリビューションによって特定するには、そのクライアントから[ハードウェア インベントリ](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md)を収集しておく必要があります。  

  ハードウェア インベントリの既定のクライアント設定には、クライアント コンピューターのオペレーティング システムに関する情報が含まれます。 **オペレーティング システム** クラスの **キャプション** プロパティを使用すると、Linux または UNIX サーバーのオペレーティング システムを特定できます。  

  Linux および UNIX 用の Configuration Manager クライアントを実行しているコンピューターに関する詳細は、Configuration Manager コンソールの **[資産とコンプライアンス]** ワークスペースの **[デバイス]** ノードで確認できます。 Configuration Manager コンソールの **[資産とコンプライアンス]** ワークスペースでは、 **[オペレーティング システム]** 列に、各コンピューターのオペレーティング システムの名前が表示されます。  

  既定では、Linux および UNIX サーバーは、 **[すべてのシステム]** コレクションのメンバーです。 Linux および UNIX サーバーのみが含まれるカスタム コレクション、またはそのコレクションのサブセットを作成することをお勧めします。 カスタム コレクションでは、展開の成功を正確に判断できるように、ソフトウェアを展開する、同じようなコンピューターのグループにクライアント設定を割り当てるなどの操作を管理できます。   

  Linux および UNIX サーバーのカスタム コレクションを作成する場合は、オペレーティング システム属性のキャプション属性が含まれるメンバーシップの規則クエリを追加します。 コレクションの作成に関する詳細については、[コレクションの作成方法](../../../core/clients/manage/collections/create-collections.md)に関するページを参照してください。  

##  <a name="maintenance-windows-for-linux-and-unix-servers"></a><a name="BKMK_MaintenanceWindowsforLnU"></a> Linux および UNIX サーバーのメンテナンス期間  
 Linux および UNIX サーバー用の Configuration Manager クライアントでは、[メンテナンス期間](../../../core/clients/manage/collections/use-maintenance-windows.md)を使用できます。 このサポートは、Windows ベースのクライアントから変更されていません。  

##  <a name="client-settings-for-linux-and-unix-servers"></a><a name="BKMK_ClientSettingsforLnU"></a> Linux および UNIX サーバーのクライアント設定s  
 Linux および UNIX サーバーに適用される[クライアント設定](../../../core/clients/deploy/configure-client-settings.md)は、他のクライアントの設定と同じ方法で構成できます。  

 既定では、 **[既定のクライアント エージェント設定]** が Linux および UNIX サーバーに適用されます。 また、カスタムのクライアント設定を作成し、特定のクライアントのコレクションに展開できます。  

 Linux および UNIX クライアントにのみ適用される追加のクライアント設定はありません。 ただし、Linux および UNIX クライアントに適用されない既定のクライアント設定は存在します。 Linux と UNIX のクライアントは、それがサポートする機能の設定のみを適用します。  

 たとえば、リモート コントロール設定を有効にし、構成するカスタムのクライアント デバイス設定は、Linux サーバーと UNIX サーバーでは無視されます。Linux と UNIX のクライアントはリモート コントロールをサポートしないためです。  

##  <a name="computer-policy-for-linux-and-unix-servers"></a><a name="BKMK_PolicyforLnU"> Linux および UNIX サーバーのコンピューター ポリシー  
 Linux および UNIX サーバーのクライアントは、そのサイトを定期的にポーリングしてコンピューター ポリシーを確認し、要求された構成に関する詳細情報を取得して、展開をチェックします。  

 Linux または UNIX サーバーのクライアントにコンピューター ポリシーのポーリングを直ちに実行するように強制することもできます。 それを実行するには、サーバーで **ルート** 資格情報を使用して、 **/opt/microsoft/configmgr/bin/ccmexec -rs policy**コマンドを実行します。  

 コンピューター ポリシーのポーリングの詳細が、共有クライアントのログ ファイル **scxcm.log**に入力されます。  

> [!NOTE]  
>  Linux および UNIX 用の Configuration Manager クライアントによって、ユーザー ポリシーの要求や処理が実行されることはありません。  

##  <a name="how-to-manage-certificates-on-the-client-for-linux-and-unix"></a><a name="BKMK_ManageLinuxCerts"></a> Linux および UNIX 用クライアントで証明書を管理する方法  
 Linux および UNIX 用のクライアントをインストールした後、 **certutil** ツールを使用して、新しい PKI 証明書でクライアントを更新し、新しい証明書失効リスト (CRL) をインポートできます。 Linux および UNIX 用のクライアントをインストールするとき、このツールは `/opt/microsoft/configmgr/bin/certutil` に配置されます。 

 証明書を管理するには、各クライアントで、次のいずれかのオプションを指定して certutil を実行します。  

|オプション|説明|  
|------------|----------------------|  
|`importPFX`|このオプションを使用すると、証明書を指定して、クライアントが現在使用している証明書と置き換えることができます。<br /><br /> `-importPFX` を使用する場合は、`-password` コマンド ライン パラメーターを使って、PKCS#12 ファイルに関連付けられているパスワードを指定する必要もあります。<br /><br /> 追加のルート証明書の要件を指定するには、`-rootcerts` を使用します。<br /><br /> 例: `certutil -importPFX <path to the PKCS#12 certificate> -password <certificate password> [-rootcerts <comma-separated list of certificates>]`|  
|`importsitecert`|このオプションを使用すると、管理サーバー上にあるサイト サーバー署名証明書を更新できます。<br /><br /> 例: `certutil -importsitecert <path to the DER certificate>`|  
|`importcrl`|このオプションを使用すると、1 つ以上の CRL ファイル パスを指定してクライアント上の CRL を更新できます。<br /><br /> 例: `certutil -importcrl <comma separated CRL file paths>`|  
