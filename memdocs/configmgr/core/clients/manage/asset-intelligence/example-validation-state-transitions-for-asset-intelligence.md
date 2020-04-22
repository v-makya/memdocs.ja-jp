---
title: 検証状態遷移の例
titleSuffix: Configuration Manager
description: Configuration Manager での資産インテリジェンスの検証状態移行の例について説明します。
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6230a6e5-a1f6-459b-84f1-07fbde0e70f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2af9243d6720d5821c641e5c80589457a33b638e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695080"
---
# <a name="example-validation-state-transitions-for-asset-intelligence"></a>資産インテリジェンスの検証状態移行の例

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の資産インテリジェンスの検証の状態は固定したものではなく、資産インテリジェンス カタログに保持されたデータに影響を与える管理操作によって変化することがあります。 このトピックでは、考えられる検証状態の変化について例を挙げて説明します。

##  <a name="uncategorized-catalog-item-is-categorized-by-the-administrative-user"></a><a name="BKMK_UncategorizedIsCategorized"></a> カテゴリ化されていないカタログ項目が管理ユーザーによってカテゴリ化される  

|**状態の変化**|**状態の変化の説明**|  
|--------------------------|--------------------------------------|  
|**カテゴリ化されていない**|System Center Online または管理ユーザーによってカテゴリ化されたことがない、インベントリされたソフトウェア タイトルが、資産インテリジェンス カタログに入力されます。|  
|**カテゴリ化されていない** に **ユーザー定義**|カテゴリ化されていない項目が、管理ユーザーによってカテゴリ化されます。|  

##  <a name="categorized-catalog-item-is-recategorized-by-the-administrative-user"></a><a name="BKMK_CategorizedIsReCategorized"></a> カテゴリ化されたカタログ項目が管理ユーザーによって再カテゴリ化される  

|**状態の変化**|**状態の変化の説明**|  
|--------------------------|--------------------------------------|  
|**検証済み**|カタログ項目は、System Center Online の調査員によって定義され、資産インテリジェンス カタログ内に存在しています。|  
|**カテゴリ化されていない** から **検証済み**|検証されていない項目が、管理ユーザーによってカテゴリ化されます。|  

> [!NOTE]  
>  System Center Online から取得したカテゴリ化情報はデータベースに格納されて削除できないため、管理ユーザーは、後で System Center Online のカテゴリ化を復元することができます。  

##  <a name="user-defined-catalog-item-is-recategorized-by-system-center-online"></a><a name="BKMK_UserDefinedIsRecategorized"></a> ユーザー定義のカタログ項目が System Center Online によって再カテゴリ化される  

|**状態の変化**|**状態の変化の説明**|  
|--------------------------|--------------------------------------|  
|**カテゴリ化されていない**|インベントリされたソフトウェア タイトルが、System Center Online または管理ユーザーによってカテゴリ化されたことのない資産インテリジェンス カタログに入力されます。|  
|**ユーザー定義の**|カテゴリ化されていない項目が、管理ユーザーによってカテゴリ化されます。|  
|**ユーザー定義済み** から **更新可能**|ユーザー定義のカタログ項目は、その後の資産インテリジェンス カタログの手動一括更新中に、System Center Online によって異なったカテゴリ化がされています。<br /><br /> 管理ユーザーは **[ソフトウェア詳細の不一致の解決]** ダイアログ ボックスを使用して、新しいカテゴリ化情報と以前のユーザー定義済みの値のいずれを使用するのかを決定できます。|  
|**更新可能** から **検証済み**|管理ユーザーは **[ソフトウェア詳細の不一致の解決]** ダイアログ ボックスを使用して、前回のカタログ更新中に System Center Online から受信した新しいカテゴリ化情報を使用します。|  
|または||  
|**更新可能** から **検証済み**|管理ユーザーは **[ソフトウェア詳細の不一致の解決]** ダイアログ ボックスを使用して、以前のユーザー定義済みの値を使用します。|  

> [!NOTE]  
>  System Center Online から取得したカテゴリ化情報はデータベースに格納されて削除できないため、管理ユーザーは、後で System Center Online のカテゴリ化を復元することができます。  

##  <a name="uncategorized-catalog-item-is-submitted-to-system-center-online-for-categorization"></a><a name="BKMK_UncategorizedIsSubmitted"></a> カテゴリ化されていないカタログ項目が、カテゴリ化のために System Center Online に送信される  

|**状態の変化**|**状態の変化の説明**|  
|--------------------------|--------------------------------------|  
|**カテゴリ化されていない**|インベントリされたソフトウェア タイトルが、System Center Online または管理ユーザーによってカテゴリ化されたことのない資産インテリジェンス データベースに入力されます。|  
|**カテゴリ化されていない** から **保留中**|カテゴリ化されていない項目が、管理ユーザーによるカテゴリ化のために System Center Online に送信されます。|  
|**保留中** から **検証済み**|この項目は System Center Online によってカテゴリ化されています。 管理ユーザーは、一括カタログ更新または資産インテリジェンス カタログの同期化を使用して、この項目を資産インテリジェンス カタログにインポートします。 資産インテリジェンス同期ポイント サイト システムの役割を使用すると、両方を使用できます。|  

##  <a name="user-defined-catalog-item-is-submitted-to-system-center-online-for-categorization"></a><a name="BKMK_UserDefinedIsSubmitted"></a> ユーザー定義のカタログ項目が、カテゴリ化のために System Center Online に送信される  

|**状態の変化**|**状態の変化の説明**|  
|--------------------------|--------------------------------------|  
|**カテゴリ化されていない**|インベントリされたソフトウェア タイトルが、System Center Online または管理ユーザーによってカテゴリ化されたことのない資産インテリジェンス データベースに入力されます。|  
|**検証済み**|ユーザーがカテゴリ化されていない項目がカテゴリ化しました。|  
|**ユーザー定義済み** から **保留中**|ユーザー定義のカタログ項目を、カテゴリ化のために System Center Online に送信します。|  
|**保留中** から **更新可能**|ユーザー定義のカタログ項目が、その後のカタログ同期時に System Center Online により、異なるようにカテゴリ化されました。 **[競合の解決]** 操作を使用して、新しいカテゴリ化情報または以前のユーザー定義値を使用するかどうかを決定することができます。 競合の解決の詳細については、「 [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)」を参照してください。|  
|**更新可能** から **検証済み**|**[競合の解決]** 操作を使用して、前回のカタログ更新中に System Center Online から受信した新しいカテゴリ化情報を選択します。 競合の解決の詳細については、「[ソフトウェア詳細の競合の解決](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)」をご覧ください。|  
|または||  
|**更新可能** から **検証済み**|**[競合の解決]** 操作を使用して、以前のユーザー定義値の使用を選択します。 競合の解決の詳細については、「[ソフトウェア詳細の競合の解決](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)」をご覧ください。|  

> [!NOTE]  
>  System Center Online から取得したカテゴリ化情報はデータベースに格納されて削除できないため、後で System Center Online のカテゴリ化を復元することができます。  
