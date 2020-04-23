---
title: サイト データの発行
titleSuffix: Configuration Manager
description: Configuration Manager サイトを Active Directory Domain Services に発行する方法について説明します。
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 77ca6711f86250f4a6f937d919893cf95e022567
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700980"
---
# <a name="publish-site-data-for-configuration-manager"></a>Configuration Manager のサイト データの発行

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の Active Directory スキーマを拡張した後で、Active Directory Domain Services (AD DS) に Configuration Manager サイトを発行することができます。 こうすることで、Active Directory コンピューターは、信頼できる発行元からサイトの情報を安全に取得することができます。 サイト情報を AD DS に発行することは Configuration Manager の基本機能に必須というわけではありませんが、管理オーバーヘッドを低減する効果があります。  

-   **AD DS に発行するようにサイトが構成されている場合は**、Active Directory にサイト データを発行することにより、Configuration Manager クライアントが自動的に管理ポイントを検出できるようになります。 クライアントは、グローバル カタログ サーバーに対して LDAP クエリを使用します。  

-   **サイトを AD DS に発行しない場合**、クライアントには、その既定の管理ポイントを特定するための、それに代わるメカニズムが必要となります。  

クライアントでの管理ポイントの検出方法については、[クライアントが Configuration Manager のサイト リソースやサービスを検索する方法](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)に関するページを参照してください。  

## <a name="configure-sites-to-publish-to-ad-ds"></a>AD DS に発行するためのサイトの構成  
 基本的な手順は次のとおりです。  

-   サイト データを発行する各フォレスト内で、[Configuration Manager の Active Directory スキーマを拡張する](../../../../core/plan-design/network/extend-the-active-directory-schema.md)必要があります。 また、**System Management** コンテナーが存在していることを確認します。  

-   データを発行する各プライマリ サイトのコンピューター アカウントには、**システム管理**コンテナーとそのすべての子オブジェクトに対する**フル コントロール**権限を付与する必要があります。  

### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>Configuration Manager サイトが Active Directory フォレストにサイト情報を発行できるようにするには

1.  Configuration Manager コンソールで、 **[管理]** をクリックします。  

2.  **管理**  ワークスペースで、展開 **サイトの構成**, 、 をクリック **サイト**です。 サイト データの発行対象となるサイトを選択します。 **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]** をクリックします。  

3.  サイト プロパティの **[発行]** タブで、このサイトのサイト データの発行先のフォレストを選択します。  

4.  **[OK]** をクリックして構成を保存します。  

### <a name="to-set-up-active-directory-forests-for-publishing"></a>Active Directory フォレストを発行用に設定するには  

1.  Configuration Manager コンソールで、 **[管理]** をクリックします。  

2.  **[管理]** ワークスペースで、 **[階層の構成]** を展開し、 **[Active Directory フォレスト]** をクリックします。 Active Directory フォレストの検索を前に実行している場合は、検出されたフォレストが結果ウィンドウに表示されます。 Active Directory フォレストの探索を実行すると、ローカル フォレストと信頼済みフォレストがすべて探索されます。 信頼されていないフォレストだけを手動で追加します。  

    -   既に検出済みのフォレストをセットアップするには、結果ウィンドウでそのフォレストを選択します。 次に、 **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]** をクリックしてフォレストのプロパティを開きます。 手順 3 に進みます。  

    -   一覧表示されていない新しいフォレストをセットアップするには、 **[ホーム]** タブの **[作成]** グループで、 **[フォレストの追加]** をクリックして **[フォレストの追加]** ダイアログ ボックスを開きます。 手順 3 に進みます。  

3.  **[全般]** タブで、検出するフォレストの構成を完了し、 **[Active Directory フォレスト アカウント]** を指定します。  

    > [!NOTE]  
    >  Active Directory フォレストの探索で、信頼されていないフォレストを検出して、そのフォレストに発行するにはグローバル アカウントが必要です。 サイト サーバーのコンピューター アカウントを使用しない場合は、グローバル アカウントのみ選択できます。  

4.  サイト データをこのフォレストに発行できるようにする場合は、 **[発行]** タブで、必要な構成を行います。  

    > [!NOTE]  
    >  サイトをフォレストに発行できるようにする場合は、Configuration Manager 用にそのフォレストの Active Directory スキーマを拡張する必要があります。 Active Directory フォレスト アカウントには、そのフォレストの System コンテナーに対するフル コントロールのアクセス許可が必要です。  

5.  このフォレストを Active Directory フォレストの探索で使用するための構成が完了したら、 **[OK]** をクリックして構成を保存します。  
