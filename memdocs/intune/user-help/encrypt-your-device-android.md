---
title: Intune 用に Android デバイスを暗号化する | Microsoft Docs
description: Intune で必要なときに Android デバイスの暗号化を有効にする手順です
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ee2d220e308b406251f049e1c17422f89ee36534
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79348784"
---
# <a name="encrypting-your-android-device"></a>Android デバイスの暗号化

デバイスを暗号化すると、デバイスをなくしたり盗まれたりした場合に、ファイルとフォルダーが不正アクセスから保護されます。 デバイスの暗号化を有効にすると、正しいパスワードまたは PIN を持つユーザーのみが、デバイスにサインインできるようになります。 

学校や職場のリソースにアクセスするための前提条件として、Android デバイスの暗号化が組織で要求されている場合があります。 一部の新しい Android デバイスは、何もしなくても既定で暗号化されます。  

## <a name="turn-on-encryption"></a>暗号化を有効にする

Intune ポータル サイトまたは Microsoft Intune アプリで、デバイスの暗号化を求められた場合は、次の手順のようにします。 

> [!Note]
> Huawei、Vivo、OPPO 製の特定の Android デバイスは暗号化できません。 詳細については、[こちら](your-device-appears-encrypted-but-cp-says-otherwise-android.md)を参照してください。  

1. デバイスの画面のロックを設定します。  
    」を参照します。 **[設定]**  >  **[ロック画面とセキュリティ]**  >  **[Screen lock type]\(画面のロックの種類\)** に移動します。  
    b. **[暗証番号 (PIN)]** 、 **[パスワード]** 、 **[パターン]** のいずれかを選択します。  
    c. 表示される指示に従って、画面のロックを構成します。  

2. **[Lock screen and security]\(ロック画面とセキュリティ\)** に戻り、 **[Secure startup]\(安全なスタートアップ\)** を選択します。
3. **[Require PIN when device turns on]\(デバイスの電源をオンにするときに PIN を要求する\)**  >  **[OK]** を選択 ます。
4. PIN を入力して確認し、デバイスを暗号化します。
5. Intune ポータル サイトまたは Microsoft Intune アプリを開きます。
    * ポータル サイトのユーザー:デバイスを選択し、 **[デバイス設定の確認]** をタップします。 
    * Microsoft Intune のユーザー: ページが更新されるまで待つ必要がありますが、更新されると、暗号化の状態が準拠に変わっているはずです。  

Android 4.4 以前が実行されているデバイスには、 **[Secure startup]\(安全なスタートアップ\)** オプションがない可能性があります。 その場合は、次の手順のようにしてデバイスを暗号化します。

1. **[Settings]\(設定\)**  >  **[Security]\(セキュリティ\)**  >  **[Encrypt Device]\(デバイスの暗号化\)** に移動します。 表示されるラベルは、Android デバイスによって異なります。 **[Encrypt Device]\(デバイスの暗号化\)** オプションが表示されない場合は、以下の場所を調べます。
    * **[Storage]\(ストレージ\)**  >  **[Storage encryption]\(ストレージの暗号化\)**
    * **[Storage]\(ストレージ\)**  >  **[Lock screen and security]\(ロック画面とセキュリティ\)**  >  **[Other security settings]\(その他のセキュリティ設定\)** 

2. 画面の指示に従います。 暗号化中、デバイスが何度か再起動する可能性があります。
3. Intune ポータル サイトまたは Microsoft Intune アプリを開きます。
    * ポータル サイトのユーザー:デバイスを選択し、 **[デバイス設定の確認]** をタップします。  
    * Microsoft Intune のユーザー: ページが更新されるまで待つ必要がありますが、更新されると、暗号化の状態が準拠に変わっているはずです。

## <a name="troubleshoot"></a>トラブルシューティング  
**問題**:デバイスを既に暗号化してあるのに、次のようになります

- 暗号化ボタンが無効です。
- 暗号化が必要であるというメッセージが引き続き表示されます。
- Intune ポータル サイトまたは Microsoft Intune アプリを使用しようとすると、エラーが表示されます。

**対処方法**

- デバイスが課金され、接続されていることを確認します。  
- デバイスで PIN やパスワードが設定されていることを確認します。  

サポートが必要な場合は、 会社のサポートに問い合わせるか (連絡先情報については[ポータル Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください)、または <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">Microsoft Android チーム</a>にご連絡ください。  
