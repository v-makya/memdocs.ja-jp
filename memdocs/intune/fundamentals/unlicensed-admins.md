---
title: Microsoft Intune のライセンス未付与の管理者
description: ライセンスが与えられていない管理者に Intune にアクセスする許可を与える方法について説明します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: a5f479dcad0c293c547edec24f0f835a4fc987e1
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574832"
---
# <a name="unlicensed-admins"></a>ライセンス未付与の管理者

> [!Important]
> このオプションでは、管理者が Microsoft エンドポイント マネージャーにアクセスするためのライセンス要件のみが削除されます。 Azure Active Directory Premium などの他の機能やサービスの使用で、管理者のライセンスが必要になる場合があります。

Intune ライセンスのない管理者に、Intune または Microsoft エンドポイント マネージャー管理センターのアクセス権を付与することができます。

1. [Microsoft エンドポイント マネージャー管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインし、 **[テナント管理]** 、 **[ロール]** 、 **[Administrator licensing]\(管理者ライセンス\)** の順に移動します。
2. **[ライセンスのない管理者へのアクセスを許可する]**  >  **[はい]** を選択します。
    >[!WARNING]
    >**[はい]** をクリックした後にこの設定を元に戻すことはできません。

3. これ以降、Microsoft エンドポイント マネージャー管理センターにサインインしているユーザーには、Intune のライセンスは必要ありません。 アクセスの範囲は、割り当てられたロールによって定義されます。

Intune では、セキュリティ グループあたり最大 350 人のライセンスのない管理者がサポートされ、直接のメンバーにのみ適用されます。 この上限を超えた管理者には、予測できない動作が発生します。




