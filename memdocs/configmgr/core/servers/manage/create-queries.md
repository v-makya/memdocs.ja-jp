---
title: クエリを作成する
titleSuffix: Configuration Manager
description: Configuration Manager でクエリを作成してインポートする方法を紹介します。 クエリの例とヒントが含まれています。
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d15252c3b3c93c7e90e517c502c4c3dd2dfcf20
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700046"
---
# <a name="create-queries-in-configuration-manager"></a>Configuration Manager でのクエリの作成

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager でのクエリの作成およびインポート方法について説明します。  

##  <a name="create-a-query"></a><a name="BKMK_Create"></a> クエリの作成  
 Configuration Manager でクエリを作成するには、次の手順に従います。  

1.  Configuration Manager コンソールで、 **[監視]** を選択します。  

2.  **[監視]** ワークスペースで、 **[クエリ]** を選択します。 **[ホーム]** タブの **[作成]** グループで、 **[クエリの作成]** を選択します。  

3.  **[クエリの作成ウィザード]** の **[全般]** タブで、クエリに対する一意の名前と、必要に応じてコメントを指定します。  

4.  既存のクエリをインポートして新しいクエリのベースとして使用するには、 **[クエリ ステートメントのインポート]** を選択します。 **[クエリの参照]** ダイアログ ボックスで、インポートするクエリを選択してから、 **[OK]** を選択します。  

5.  **[オブジェクトの種類]** 一覧で、クエリが返すオブジェクトの種類を選択します。 次の表に、検索可能なオブジェクトの種類の例をいくつか示します。  

    |オブジェクトの種類|[説明]|  
    |-----------------|-----------------|  
    |**[システム リソース]**|デバイスの NetBIOS 名、クライアントのバージョン、クライアントの IP アドレス、Active Directory Domain Services の情報のような、一般的なシステム属性を検索するために使用します。|  
    |**[ユーザー リソース]**|ユーザー名、ユーザー グループ名、セキュリティ グループ名のような、一般的なユーザー情報を検索するために使用します。|  
    |**展開**|展開名、スケジュール、展開先となったコレクションのような、展開の一般的な属性を検索するために使用します。|  

6.  **[クエリ ステートメントの編集]** を選択して、 **[&lt;クエリ名\> ステートメントのプロパティ]** ダイアログ ボックスを開きます。  

7.  **[&lt;クエリ名\> ステートメントのプロパティ]** ダイアログ ボックスの **[全般]** タブで、クエリによって返される属性と、その表示方法を指定します。 **[新規]** アイコンを選択して、新しい属性を追加します。 **[クエリ言語を表示する]** を選択して、WMI Query Language (WQL) でクエリを直接入力または編集することもできます。 WMI クエリの例については、この記事の「[Example WQL queries](#BKMK_Example)」セクションをご覧ください。  

    > [!TIP]  
    > 独自の WQL クエリを作成するために、次のリファレンス ドキュメントをご利用いただけます。  
    >   
    > -   [WQL (WMI 用の SQL)](/windows/win32/wmisdk/wql-sql-for-wmi)  
    > -   [WHERE 句](/windows/win32/wmisdk/where-clause)  
    > -   [WQL オペレーター](/windows/win32/wmisdk/wql-operators)  

8.  **[&lt;クエリ名\> ステートメントのプロパティ]** ダイアログ ボックスの **[条件]** タブで、クエリ結果の絞り込みに使用する条件を指定します。 たとえば、サイト コード **XYZ** を含むリソースのみが返されるようにすることができます。 1 つのクエリに複数の条件を構成することができます。  

    > [!IMPORTANT]  
    > 条件が含まれないクエリを作成した場合、そのクエリは、 **[すべてのシステム]** コレクションのすべてのデバイスを返します。  

9. **[&lt;クエリ名\> ステートメントのプロパティ]** ダイアログ ボックスの **[結合]** タブで、2 つの異なる属性からのデータをクエリ結果に結合させることができます。 クエリ結果に 2 つの異なる属性を選択すると、Configuration Manager は自動的にクエリの結合を作成しますが、 **[結合]** タブには、より詳細なオプションが用意されています。 Configuration Manager では、次の属性クラスがサポートされています。  

    |結合の種類|[説明]|  
    |---------------|-----------------|  
    |内部|一致する結果のみを表示します。 自動的に作成される結合で常に使用されます。|  
    |左|基本属性についてはすべての結果を表示し、結合の属性については一致する結果だけを表示します。|  
    |権限|結合の属性についてはすべての結果を表示し、基本属性については一致する結果だけを表示します。|  
    |完全|基本属性と結合の属性の両方について、すべての結果を表示します。|  

     結合操作を使用する方法の詳細については、SQL Server のドキュメントをご覧ください。  

10. **[OK]** をクリックして **[&lt;クエリ名\> ステートメントのプロパティ]** ダイアログ ボックスを閉じます。  

11. **[クエリの作成ウィザード]** の **[全般]** タブで、クエリ結果をコレクションのメンバーに制限しないか、指定したコレクションのメンバーに制限するか、またはクエリを実行するたびにコレクションの入力を求めるかを指定します。  

12. ウィザードを完了すると、クエリが作成されます。 新しいクエリは、 **[監視]** ワークスペースの **[クエリ]** ノードに表示されます。  

##  <a name="import-a-query"></a><a name="BKMK_Import"></a> クエリのインポート  
 Configuration Manager にクエリをインポートするには、次の手順に従います。 クエリのエクスポート方法については、「[クエリの管理方法](../../../core/servers/manage/manage-queries.md)」を参照してください。  

1.  Configuration Manager コンソールで、 **[監視]** を選択します。  

2.  **[監視]** ワークスペースで、 **[クエリ]** を選択します。 **[ホーム]** タブの **[作成]** グループで、 **[オブジェクトのインポート]** を選択します。  

3.  **[オブジェクトのインポート ウィザード]** の **[MOF ファイル名]** ページで、 **[参照]** を選択して、インポートするクエリを含む管理オブジェクト フォーマット (MOF) ファイルを選択します。  

4.  インポートされるクエリの情報を確認してから、ウィザードを完了します。 新しいクエリは、 **[監視]** ワークスペースの **[クエリ]** ノード上に表示されます。  

##  <a name="example-wql-queries"></a><a name="BKMK_Example"></a> Example WQL queries

このセクションでは、階層で使用したり、他の目的のために変更したりできる WQL クエリの例を示します。 これらのクエリを使用するには、 **[クエリ ステートメントのプロパティ]** ダイアログ ボックスで **[クエリ言語を表示する]** を選択します。 次に、クエリをコピーして **[クエリ ステートメント]** フィールドに貼り付けます。  

> [!TIP]  
> 任意の文字列を表すには、ワイルドカード文字 `%` を使用します。 たとえば、`%Visio%` は、Microsoft Office Visio 2010 を返します。  

### <a name="computers-that-run-windows-10"></a>Windows 10 を稼働しているコンピューター

Windows 7 を実行しているすべてのコンピューターの NetBIOS 名とオペレーティング システムのバージョンを返すには、次のクエリを使用します。  

``` WQL
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from
SMS_R_System where
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 10%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>特定のソフトウェア パッケージがインストールされているコンピューター  

特定のソフトウェア パッケージがインストールされているすべてのコンピューターの NetBIOS 名とソフトウェア パッケージ名を返すには、次のクエリを使用します。 この例では、いずれかのバージョンの Microsoft Visio がインストールされているすべてのコンピューターが返されます。 `Microsoft%Visio%` を、クエリで照会するソフトウェア パッケージに置き換えます。  

> [!TIP]  
> このクエリは、Windows コントロール パネルのプログラムの一覧に表示される名前を使用して、ソフトウェア パッケージを検索します。  

``` WQL
select SMS_R_System.NetbiosName,
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =
SMS_R_System.ResourceId where
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Microsoft%Visio%"  
```  

### <a name="computers-in-a-specific-active-directory-domain-services-organizational-unit"></a>特定の Active Directory Domain Services 組織単位に含まれるコンピューター

指定した組織単位 (OU) 内のすべてのコンピューターの NetBIOS 名と OU 名を返すには、次のクエリを使用します。 テキスト `OU Name` を、クエリで照会する OU の名前に置き換えます。  

``` WQL
select SMS_R_System.NetbiosName,
SMS_R_System.SystemOUName from
SMS_R_System where
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>特定の NetBIOS 名のコンピューター

特定の文字列で始まるすべてのコンピューターの NetBIOS 名を返すには、次のクエリを使用します。 この例では、クエリは、`ABC` で始まる NetBIOS 名を持つすべてのコンピューターを返します。  

``` WQL
select SMS_R_System.NetbiosName from
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="devices-of-a-specific-type"></a><a name="BKMK_DeviceType"></a> 特定の種類のデバイス

デバイスの種類は、Configuration Manager データベースのリソース クラス **sms_r_system** および属性名 **AgentEdition** の下に格納されます。 指定したデバイスの種類のエージェント エディションと一致するデバイスのみを取得するには、次のクエリを使用します。  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

&lt;Device ID\> には次のいずれかの値を使用します。  

|デバイスの種類|AgentEdition の値|  
|-----------------|---------------------------|  
|Windows デスクトップまたはラップトップ コンピューター|0|  
|Windows ARM ベースのデバイス (Windows RT を実行)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Mac コンピューター|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|Intel system on a chip|12|  
|Unix および Linux サーバー|13|  
|Microsoft HoloLens (MDM)|15|
|Microsoft Surface Hub (MDM)|16|

> [!NOTE]
> この表に記載されていない値は、サポートされなくなったデバイスに関連付けられています。

<!-- removed with hybrid EOL
|iOS|8|  
|iPad|9|  
|iPod touch|10|  
|Android|11|  
|Apple macOS (MDM)|14|
|Android for Work|17|
 -->

たとえば、Mac コンピューターだけが返されるようにする場合は、次のクエリを使用します。  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="next-steps"></a>次のステップ

[クエリを管理する方法](manage-queries.md)