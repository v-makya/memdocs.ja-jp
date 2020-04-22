---
title: Intune 用に Android デバイスを暗号化する | Microsoft Docs
description: Intune で必要なときに Android デバイスの暗号化を有効にする手順です
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/31/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: d9e074def368927504c3f3c1761ec21b3ab62d22
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "80696275"
---
# <a name="encrypting-your-android-device"></a>Android デバイスの暗号化

デバイスを暗号化すると、デバイスをなくしたり盗まれたりした場合に、ファイルとフォルダーが不正アクセスから保護されます。 これにより、パスコードを持たない人物がデバイス上のデータにアクセスしたり、読み取ったりできなくなります。 

学校や職場のリソースにアクセスするための前提条件として、組織から次を求められる場合があります。

* [デバイスを暗号化する](#encrypt-device)
* [安全な起動を有効にする](#enable-secure-startup)
* [スタートアップ パスコード、PIN、またはその他の認証方法を設定する](#set-startup-passcode)  

> [!Note]
> Huawei、Vivo、OPPO 製の特定の Android デバイスは暗号化できません。 詳細については、「[デバイスの暗号化がアプリに認識されない](your-device-appears-encrypted-but-cp-says-otherwise-android.md)」をご覧ください。  

## <a name="encrypt-device"></a>デバイスの暗号化

デバイスを暗号化するには、次の手順に従います。 デバイスが数回再起動される場合があります。 

暗号化オプションに関する名前と場所は、お使いのデバイスの製造元と Android のバージョンによって異なります。 

1. **[設定]** アプリを開きます。
2. アプリの検索バーに「**セキュリティ**」または「**暗号化**」と入力し、関連する設定を検索します。
3. デバイスを暗号化するオプションをタップします。 画面の指示に従います。  
4. プロンプトが表示されたら、ロック画面のパスワード、PIN、またはその他の認証方法 (組織で許可されている場合) を設定してください。 
5. 設定を再確認するには、ポータル サイトまたは Microsoft Intune アプリを開きます。
    * ポータル サイトのユーザー:デバイスを選択し、 **[デバイス設定の確認]** をタップします。 
    * Microsoft Intune のユーザー: ページが更新されるまで待つ必要がありますが、更新されると、暗号化の状態が準拠に変わっているはずです。 

## <a name="enable-secure-startup"></a>安全な起動を有効にする

暗号化ポリシーの一環として、安全な起動を有効にするように組織から求められる場合があります。 この機能を使用すると、電話を起動する前にパスワードまたは PIN の入力を要求することで、デバイスをさらに保護することができます。 さらなる認証オプションを利用できる場合もありますが、それらは組織で何が許可されているかによって異なります。 

安全な起動オプションに関する名前と場所は、お使いのデバイスの製造元と Android のバージョンによって異なります。 一部のデバイス上では、この設定は **[Strong protection]\(強力な保護\)** と呼ばれる場合があります。 

1. **[設定]** アプリを開きます。
2. アプリの検索バーに「**安全な起動**」と入力します。
3. **[安全な起動]**  >  **[Require PIN when device turns on]\(デバイスの電源をオンにするときに PIN を要求する\)** の順にタップします。
4. プロンプトが表示されたら、お使いのデバイスの PIN を入力します。   
5. 設定を再確認するには、ポータル サイトまたは Microsoft Intune アプリを開きます。
    * ポータル サイトのユーザー:デバイスを選択し、 **[デバイス設定の確認]** をタップします。 
    * Microsoft Intune のユーザー: ページが更新されるまで待つ必要がありますが、更新されると、暗号化の状態が準拠に変わっているはずです。  


## <a name="set-startup-passcode"></a>スタートアップ パスコードを設定する   
[デバイスの暗号化](#encrypt-device)と[安全な起動の有効化](#enable-secure-startup)を行うと、デバイスの PIN、パスワード、またはその他の認証方法 (組織で許可されている場合) を設定するように求められます。 必要な手順はこれで終了です。 

ロック画面の種類を選択または変更するには:

1. **[設定]** アプリを開きます。
2. アプリの検索バーに「**画面のロック**」と入力します。
3. **[Screen lock type]\(画面のロックの種類\)** をタップします。
4. 使用する画面のロックの種類をタップし、画面上の指示に従って確認します。  

## <a name="troubleshoot"></a>トラブルシューティング    
**問題**:暗号化ボタンが無効です。   

**やってみること**: 
* デバイスが完全に充電され、電源に接続されていることを確認します。 暗号化には時間がかかる場合があるため、完全なバッテリが必要です。   

**問題**:デバイスの暗号化が必要であるというメッセージが引き続き表示されます。  

**対処方法**:
   *  デバイスで[ロック画面を設定](#set-startup-passcode)します。 
   * [安全な起動を有効にします](#enable-secure-startup)。

サポートが必要な場合は、 会社のサポートに問い合わせるか (連絡先情報については[ポータル Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください)、または <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">Microsoft Android チーム</a>にご連絡ください。  
