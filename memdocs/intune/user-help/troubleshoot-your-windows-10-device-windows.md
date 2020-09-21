---
title: Windows 10 デバイスでの職場または学校へのアクセスのトラブルシューティング | Microsoft Intune
description: 登録済みの Windows 10 デバイスでのアクセスまたはアカウント接続に関する問題を解決します。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/09/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 4ab630b6-47ff-443b-a2a5-be23388bcea7
searchScope:
- User help
ROBOTS: ''
ms.reviewer: amanh
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 7c96bef7c1be004714f0b06dd47c9c28850118da
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643429"
---
# <a name="troubleshoot-windows-10-device-access"></a>Windows 10 デバイスでのアクセスのトラブルシューティング
この記事では、登録済みの Windows 10 デバイスでのアクセスの問題を解決する方法について説明します。 

## <a name="check-wi-fi-connection"></a>Wi-Fi 接続を確認する  

職場または学校のリソースにアクセスするには、Wi-Fi への接続が必要です。 Wi-Fi に接続していることを確認してから、もう一度リソースにアクセスしてみてください。  

## <a name="add-work-or-school-account-in-settings-app"></a>設定アプリに職場または学校のアカウントを追加する  
これらの手順は、デバイスを登録するために使用したものと同じです。 ただし、お使いのアカウントが**設定**アプリに表示されない場合は、これらの手順をもう一度実行する必要があります。  

1. **[設定]** アプリを開きます。 
2. **[アカウント]** を選択します。
3. 次の手順は、使用している Windows 10 のバージョンによって異なります。 
    * バージョン 1607 以降: **[職場または学校にアクセスする]** を選択します。
    * バージョン 1511 以前: **[職場のアクセス]** を選びます。  
4. お使いのアカウントを確認します。 それが表示されていない場合は、 **[接続]** プラス記号ボタンを選択して追加します。 
5. 職場または学校の資格情報でサインインします。 
6. 画面の指示に従って、接続を完了します。  
7. 完了すると、お使いのアカウントが接続として追加されます。 組織が利用可能にしているすべてのリソースにアクセスできます。   

## <a name="contact-it-support-for-access-requirements"></a>アクセス要件を IT サポートに問い合わせる  
設定アプリに職場または学校のアカウントが表示されていれば、お使いのデバイスとアカウントは既に接続されています。 IT サポート担当者に連絡して、アクセス問題に対するヘルプを求めてください。 特定のリソースにアクセスできないようにしている制限や要件が適用されている場合があります。  

## <a name="error-messages"></a>エラー メッセージ  

### <a name="we-couldnt-auto-discover-a-management-endpoint-matching-the-username-entered-please-check-your-username-and-try-again-if-you-know-the-url-to-your-management-endpoint-please-enter-it"></a>入力されたユーザー名と一致する管理エンドポイントを自動検出できませんでした。 ユーザー名を確認して、やり直してください。 管理エンドポイントの URL がわかっている場合は、それを入力してください。

**原因**:指定された URL (管理エンドポイントとも呼ばれます) とアカウントを検証できませんでした。  

#### <a name="resolution"></a>解決策
1. ユーザー名とパスワードを再入力します。 
2. それでもうまくいかない場合は、IT サポート担当者に連絡して、正しい URL を入手してください (例: www.yourcompany.onmicrosoft.com)。 
3. メッセージが表示されたら、提供された URL を入力します。 

### <a name="it-looks-like-youre-not-connected-make-sure-youre-connected-to-the-network"></a>接続されていないようです。 ネットワークに接続していることを確認します。

**原因**:デバイスが Wi-Fi に接続されていません。職場または学校のアカウントを追加するには、接続が必要です。     

#### <a name="resolution"></a>解決策
1. デバイスのツールバーまたは設定から、 **[ネットワークの状態]** 地球アイコンを選択します。
2. [Wi-Fi ネットワーク] > **[接続]** を選択します。  
3. お使いのアカウントにもう一度接続してみてください。  


## <a name="next-steps"></a>次のステップ  

サポートが必要な場合は、 IT サポート担当者にお問い合わせください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。
