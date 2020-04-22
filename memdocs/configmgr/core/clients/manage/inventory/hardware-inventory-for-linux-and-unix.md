---
title: Linux および UNIX のハードウェア インベントリ
titleSuffix: Configuration Manager
description: Configuration Manager で Linux および UNIX のハードウェア インベントリを使用する方法について説明します。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1bdfb8c6d528c12581f05f86111a1a76d2259faa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695430"
---
# <a name="hardware-inventory-for-linux-and-unix-in-configuration-manager"></a>Configuration Manager における Linux および UNIX のハードウェア インベントリ

*適用対象:Configuration Manager (Current Branch)*

> [!Important]  
> バージョン 1902 以降の Configuration Manager では、Linux または UNIX クライアントはサポートされていません。 
> 
> Linux サーバーを管理するには、Microsoft Azure の管理を検討してください。 Azure ソリューションには広範囲な Linux サポートが含まれており、ほとんどの場合、Linux のエンドツーエンド パッチ管理など、Configuration Manager 以上の機能を備えています。

Linux および UNIX 用の Configuration Manager クライアントは、ハードウェア インベントリをサポートします。 ハードウェア インベントリを収集すると、リソース エクスプローラーまたは Configuration Manager レポートでインベントリの表示を実行したり、この情報を使用して以下の操作が可能になるクエリやコレクションを作成したりできます。  

- ソフトウェアの展開  

- メンテナンス期間の適用  

- カスタム クライアント設定の展開  

Linux および UNIX サーバーのハードウェア インベントリでは、標準ベースの Common Information Model (CIM) サーバーを使用します。 CIM サーバーはソフトウェア サービス (またはデーモン) として実行され、分散管理タスク フォース (DMTF) 標準に基づく管理インフラストラクチャを提供します。 CIM サーバーには、Windows ベースのコンピューターで使用可能な Windows Management Infrastructure (WMI) CIM 機能に類似した機能が備わっています。  

累積的な更新プログラム 1 以降の Linux および UNIX 用クライアントでは、**Open Group** のオープン ソース **omiserver** バージョン 1.0.6 が使用されます。 (累積的な更新プログラム 1 より前の場合、クライアントは **nanowbem** を CIM サーバーとして使用していました。)  

CIM サーバーは、Linux および UNIX 用クライアントの一部としてインストールされます。 Linux および UNIX 用クライアントでは、CIM サーバーと直接通信し、CIM サーバーの WS-MAN インターフェイスは使用されません。 CIM サーバー上の WS-MAN ポートは、クライアントのインストール時には無効です。 Microsoft は、Open Management Infrastructure (OMI) プロジェクトを介してオープン ソースとして利用できる CIM サーバーを開発しました。 Open Management Infrastructure プロジェクトについて詳しくは、「 [Open Group](https://www.opengroup.org/) 」Web サイトをご覧ください。  

Linux および UNIX サーバー上のハードウェア インベントリは、既存の Win32 と WMI のクラスとプロパティを、Linux と UNIX サーバーの同等のクラスとプロパティにマッピングすることによって動作します。 このクラスとプロパティの 1 対 1 のマッピングによって、Linux と UNIX のハードウェア インベントリを Configuration Manager と統合できるようになります。 Linux および UNIX サーバーからのインベントリ データは、Windows ベースのコンピューターからのインベントリと一緒に、Configuration Manager コンソールとレポートに表示されます。 この動作により、一貫性のある異種管理エクスペリエンスが提供されます。  

> [!TIP]  
>  **[オペレーティング システム]** クラスの **[キャプション]** 値を使用して、クエリとコレクション内の各種 Linux および UNIX オペレーティング システムを識別できます。  

##  <a name="configuring-hardware-inventory-for-linux-and-unix-servers"></a><a name="BKMK_ConfigHardwareforLnU"></a> Linux および UNIX サーバーのハードウェア インベントリを構成する  
 ハードウェア インベントリを構成するには、既定のクライアント設定を使用することもできますし、カスタム クライアント デバイス設定を作成することも可能です。 カスタム クライアント デバイス設定を使用する場合は、ご使用の Linux および UNIX サーバーからのみ収集するクラスとプロパティを構成できます。 また、使用している Linux および UNIX サーバーから、完全なインベントリと差分のインベントリを収集するカスタムのスケジュールを指定できます。  

 Linux および UNIX 用のクライアントでは、Linux および UNIX サーバーで使用できる次のハードウェア インベントリ クラスがサポートされています。  

- Win32_BIOS  

- Win32_ComputerSystem  

- Win32_DiskDrive  

- Win32_DiskPartition  

- Win32_NetworkAdapter  

- Win32_NetworkAdapterConfiguration  

- Win32_OperatingSystem  

- Win32_Process  

- Win32_Service  

- Win32Reg_AddRemovePrograms  

- SMS_LogicalDisk  

- SMS_Processor  

これらのインベントリ クラスのすべてのプロパティが、Configuration Manager の Linux および UNIX コンピューターで有効になるわけではありません。  

##  <a name="operations-for-hardware-inventory"></a><a name="BKMK_OperationsforHardwareforLnU"></a> ハードウェア インベントリの操作  
 ご使用の Linux および UNIX サーバーからハードウェア インベントリを収集すると、他のコンピューターから収集したインベントリを表示する場合と同じように、その情報を次のように表示および使用できます。  

- リソース エクスプローラーを使用して、Linux および UNIX サーバーからのハードウェア インベントリに関する詳細情報を表示します。  

- 特定のハードウェア構成に基づいたクエリを作成します。  

- 特定のハードウェア構成に基づいたクエリ ベースのコレクションを作成します。  

- ハードウェア構成に関する特定の詳細情報を表示するレポートを実行します。  

Linux または UNIX サーバー上のハードウェア インベントリは、クライアント設定で構成したスケジュールに従って実行されます。 既定では、このスケジュールは 7 日ごとです。 Linux および UNIX 用クライアントは、完全なインベントリ サイクルと差分インベントリ サイクルの両方をサポートします。  

また Linux または UNIX サーバー上のクライアントにハードウェア インベントリを直ちに実行するように強制することもできます。 ハードウェア インベントリを実行するには、クライアント上で**ルート**資格情報を使用して、ハードウェア インベントリ サイクルを開始する次のコマンドを実行します: `/opt/microsoft/configmgr/bin/ccmexec -rs hinv`  

ハードウェア インベントリの操作は、クライアント ログ ファイル **scxcm.log**に記録されます。  

##  <a name="how-to-use-open-management-infrastructure-to-create-custom-hardware-inventory"></a><a name="BKMK_CustomHINVforLinux"></a> Open Management Infrastructure を使用してカスタムのハードウェア インベントリを作成する方法  
 Linux および UNIX 用クライアントは、Open Management Infrastructure (OMI) を使用して作成できるカスタムのハードウェア インベントリをサポートします。 作成するには、次の手順に従います。  

1.  OMI ソースを使用してカスタム インベントリ プロバイダーを作成します  

2.  新しいプロバイダーを使用してインベントリをレポートするようにコンピューターを構成します  

3.  Configuration Manager で新しいプロバイダーのサポートを有効にする  

###  <a name="create-a-custom-hardware-inventory-provider-for-linux-and-unix-computers"></a><a name="BKMK_LinuxProvider"></a> Linux および UNIX コンピューターのカスタム ハードウェア インベントリを作成する:  
 Linux および UNIX 用の構成マネージャー クライアントのカスタム ハードウェア インベントリ プロバイダーを作成するには、**OMI ソース - v.1.0.6** を使用し、OMI 入門ガイドの指示に従います。 このプロセスには、新しいプロバイダーのスキーマを定義するマネージド オブジェクト フォーマット (MOF) ファイルの作成が含まれます。 後ほど、この MOF ファイルを Configuration Manager にインポートし、新しいカスタム インベントリ クラスのサポートを有効にします。  

 OMI ソース- v.1.0.6 およびソース OMI 入門ガイドはどちらも「 [Open Group](https://github.com/microsoft/omi/blob/master/README.md) 」Web サイトからダウンロードできます。 ダウンロードの場所は、OpenGroup.org の Web サイトの Web ページの **[Documents]** タブで見つけることができます ([Open Management Infrastructure (OMI)](https://go.microsoft.com/fwlink/p/?LinkId=286805))。  

###  <a name="configure-each-computer-that-runs-linux-or-unix-with-the-custom-hardware-inventory-provider"></a><a name="BKMK_AddProvidertoLinux"></a> カスタム ハードウェア インベントリ プロバイダーを使用して Linux または UNIX を実行する各コンピューターを次のように構成します。  
 カスタム インベントリ プロバイダーを作成した後、収集対象のインベントリが含まれる各コンピューターで、プロバイダー ライブラリ ファイルをコピーして登録する必要があります。  

1.  インベントリを収集する各 Linux および UNIX コンピューターに対してプロバイダー ライブラリをコピーします。 プロバイダー ライブラリの名前は、次のようになります (**XYZ_MyProvider.so**)。  

2.  次に、各 Linux および UNIX コンピューター上で、プロバイダー ライブラリを OMI サーバーに登録します。 OMI サーバーは、Linux および UNIX 用の構成マネージャー クライアントをインストールするときにコンピューターにインストールされますが、カスタム プロバイダーは手動で登録する必要があります。 次のコマンド ラインを使用してプロバイダーを登録します: `/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so`  

3.  新しいプロバイダーを登録した後に、 **omicli** ツールを使用してプロバイダーをテストします。 **omicli** ツールは、Linux および UNIX 用の構成マネージャー クライアントをインストールするときに各 Linux および UNIX コンピューターにインストールされます。 たとえば、作成したプロバイダーの名前が **XYZ_MyProvider** の場合、コンピューターで次のコマンドを実行します: **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     **omicli** およびカスタム プロバイダーのテストについては、OMI 入門ガイドをご覧ください。  

> [!TIP]  
>  ソフトウェアの配布を使用して、カスタム プロバイダーを展開して、Linux および UNIX クライアント コンピューターごとに、カスタム プロバイダーを登録します。  

###  <a name="enable-the-new-inventory-class-in-configuration-manager"></a><a name="BKMK_AddLinuxProvidertoCM"></a> Configuration Manager で、新しいインベントリ クラスを次のように有効にします。  
 Linux および UNIX コンピューター上の新しいプロバイダーによって報告されるインベントリについて Configuration Manager でレポートできるようにするには、事前に、カスタム プロバイダーのスキーマが定義されている管理オブジェクト フォーマット (MOF) ファイルをインポートしておく必要があります。  

 カスタム MOF ファイルを Configuration Manager にインポートするには、[ハードウェア インベントリを構成する方法](../../../../core/clients/manage/inventory/configure-hardware-inventory.md)に関するページを参照してください。  
