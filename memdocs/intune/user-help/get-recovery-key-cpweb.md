---
title: Intune ポータル サイト Web サイトから macOS デバイスの回復キーを取得する
description: 登録済みの管理された macOS デバイスの回復キーを表示します。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/04/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 5a15f3a05f96333eba19cf69c5778e6c8bd04f59
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79336759"
---
# <a name="get-a-recovery-key-for-a-macos-device"></a>macOS デバイスの回復キーを取得する

ポータル サイト Web サイトを使用して、ロックされた macOS デバイスの回復キーを取得します。 デバイスのパスワードを忘れた場合は、別のデバイスからポータル サイトにサインインして、キーを取得することができます。  

## <a name="get-recovery-key-from-company-portal-website"></a>ポータル サイト Web サイトから回復キーを取得する

このオプションは、FileVault を使用して組織によって暗号化されたデバイスで使用できます。 個人が暗号化したデバイスでは使用できません。

1. 任意のデバイス上で、**ポータル サイト Web サイト**にサインインし、 **[メニュー]** ボタン、[[デバイス]](https://portal.manage.microsoft.com) の順に選択します。  
2. 暗号化された macOS デバイスを選択します。  
3. **[回復キーを取得する]** を選択します。  

    ![[回復キーを取得する] セクションを強調表示しているポータル サイト Web サイトのスクリーンショット。](./media/1907-recovery2-cpweb-intune.PNG)  

4. 回復キーが表示されます。

    ![回復キーを表示しているポータル サイト Web サイトのスクリーンショット。](./media/1907-recovery-cpweb-intune.PNG)  

    セキュリティ上の理由から、キーは 5 分後に消えます。 キーを再度表示するには、 **[回復キーの取得]** を選択します。

キーが見つからず、デバイスが適切に暗号化されている場合は、組織のサポート担当者にお問い合わせください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。  

## <a name="get-recovery-key-from-company-portal-app-for-ios"></a>iOS 用のポータル サイト アプリから回復キーを取得する

iOS 用のポータル サイト アプリを使用して個人用回復キー (FileVault キー) を取得できます。 個人用回復キーを持つデバイスは、Intune に登録され、Intune により FileVault を使用して暗号化されている必要があります。 個人が暗号化したデバイスでは、このオプションを使用できません。 

ポータル サイト アプリを使用して、Safari Web ビューを開き、個人用回復キーを取得することができます。 

1. ポータル サイトを開きます。
2. **[回復キーを取得する]** をクリックします。

    ![回復キーを表示している iOS のポータル サイト アプリのスクリーンショット](./media/get-recovery-key-cpweb-02.png)  

Safari Web ビューにポータル サイト Web サイトが開き、キーが表示されます。 

## <a name="it-pro-support"></a>IT プロフェッショナル サポート

IT サポート担当者が macOS デバイスの FileVault 暗号化を構成して管理する場合は、「[Intune でデバイスの暗号化を使用する](/intune/protect/encrypt-devices)」を参照してください。

## <a name="next-steps"></a>次のステップ

ポータル サイト Web サイトから他に何ができるかを調べます。 アクションの一覧については、「[Intune ポータル サイト Web サイトの使用](using-the-intune-company-portal-website.md)」を参照してください。  

サポートが必要な場合は、 IT サポート担当者にお問い合わせください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。  
