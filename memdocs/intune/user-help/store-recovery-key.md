---
title: ポータル サイトの Web サイトを介して回復キーを Intune に格納する
description: ポータル サイトの Web サイトからデバイスの回復キーをアップロードして格納します。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/17/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: annochiva
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: f0a674753ff23fca509bd21e6b52101104a6803f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910793"
---
# <a name="store-your-personal-filevault-key"></a>個人の FileVault キーを格納する 

個人の暗号化された macOS デバイスの FileVault キーを格納します。 暗号化の要件を満たすだけでなく、キーを Intune に格納すると、次のことが可能になります。 

* 任意のデバイスから簡単かつ迅速にキーの取得またはローテーションを行うことができます。 
* キーを取得またはローテーションする必要があり、アプリまたは Web サイトにアクセスして自分で操作できない場合は、サポート担当者にお問い合わせください。


## <a name="retrieve-or-rotate-the-key"></a>キーの取得またはローテーション

デバイスからロックアウトされた場合は、次の場所からキーを取得できます。
   
- ポータル Web サイト
- iOS/iPadOS 用ポータル サイト アプリ 
- Android 用ポータル サイト アプリ
- Intune アプリ
 
 Intune への管理者アクセス権を持つ IT サポート担当者は、デバイスからロックアウトされた場合に、個人の回復キーをローテーションすることができます。また、彼らはキーを表示できますが、企業が所有するデバイスに属するもののみが表示されます。 IT サポート担当者が、個人用デバイスに属する回復キーを表示することはできません。   


## <a name="do-i-need-to-store-my-key"></a>キーを格納する必要はありますか?  
IT サポート担当者から、個人の回復キーをアップロードする必要があるかどうかが通知されます。 組織の IT 部門が通常あなたと通信する方法である場合、iOS/iPadOS または Android 用のポータル サイトアプリから通知を受け取ることがあります。 

次のいずれかのカテゴリに該当する場合にのみ、回復キーをアップロードすることをお勧めします。
* ご自分のデバイスを、組織に登録する前に暗号化した。 
* macOS のシステム設定でデバイスを手動で暗号化した。   

組織のポリシーによっては、キーをアップロードするまで、デバイス上の企業リソースへのアクセスがブロックされる場合があります。  

## <a name="upload-personal-recovery-key"></a>個人用回復キーをアップロードする 
暗号化された Mac デバイスの個人用 FileVault キーを保存するには、次の手順を行います。  


1. [ポータル サイトの Web サイト](https://portal.manage.microsoft.com)に移動し、職場または学校アカウントでサインインします。 
2. 暗号化されたデバイスを選択します。
3. **[Store recovery key]\(回復キーの保存\)** を選択します。  
4. 24 文字の英数字の FileVault キーを入力します。  
5. キーをもう一度入力します。 次に、 **[保存]** を選択します。
6. ポータル サイトでは、個人用回復キーの検証、ローテーション、および保存が試行されます。 キーが保存された後は、それ以上の操作は必要ありません。 アップロードが完了する前に Web サイトを離れると、次回サインインしたときにデバイスの詳細ページでその状態を確認できます。  

このプロセス中に表示されるメッセージの詳細については、「[ポータル サイトのメッセージ](store-recovery-key.md#company-portal-messages)」を参照してください。  

## <a name="company-portal-messages"></a>ポータル サイトのメッセージ

|メッセージ  |意味  |
|---------|---------|
|キーは一致している必要があります。 キーを確認して、もう一度お試しください。     | **[回復キーの確認]** ボックスの下に表示され、キーが相互に一致していないことが通知されます。 両方のフィールドにキーを再入力してから、もう一度保存してみてください。        |
|Couldn't update recovery key for device. (デバイスの回復キーを更新できませんでした。)| 画面の上部にトースト通知として表示され、ポータル サイトで回復キーを格納できなかったことが示されます。 詳細については、暗号化されたデバイスを選択します。 次の手順については、ページの上部にあるメッセージを参照してください。 |
|We were unable to upload your recovery key. (回復キーをアップロードできませんでした。) Check that you entered the correct key and try again. (正しいキーを入力したことを確認してから、もう一度やり直してください。) If the problem persists, try to manually rotate your key. (問題が引き続き発生する場合は、キーを手動でローテーションしてみてください。) タップすると、詳細を確認できます。     | デバイスの詳細ページに表示され、いくつかの意味があります。まず入力したキーが正しくないため、ポータル サイトではキーのローテーションと保存を実行できませんでした。 正しいキーを持っていることを確認してから、もう一度やり直してください。 2 つ目の可能性は、デバイスがしばらくの間に組織にチェックインされていないことです。 組織の最新の更新プログラムを同期するには、デバイス > **[状態]**  >  **[アクセスの確認]** を選択します。 その後、回復キーをもう一度保存してみてください。 最後に、問題が解決しない場合は、組織が FileVault を有効にしていない可能性があります。 IT サポート担当者に連絡し、デバイスを同期しても、FileVault キーを保存できないことを知らせてください。         |
|回復キーが更新されました。 デバイスからロックアウトされ、キーを取得する必要がある場合は、ポータル サイトにサインインし、 **[回復キーを取得する]** を選択します。    | デバイスの詳細ページに表示されます。 保存したキーは正常にローテーションされ、新しい個人用回復キーが格納されます。    |



## <a name="it-pro-support"></a>IT プロフェッショナル サポート

あなたが IT サポート担当者であり、組織内の Mac デバイス用に FileVault 暗号化を構成して管理する場合は、[「Intune で macOS 用の FileVault ディスク暗号化を使用する」](../protect/encrypt-devices-filevault.md)を参照してください。  

## <a name="next-steps"></a>次のステップ

いつでもポータル サイトの Web サイト、Intune アプリ、iOS および Android 向けのポータル サイト アプリからキーを取得し、それを使用して Mac デバイスにアクセスすることができます。 回復キーを取得する方法については、[回復キーの取得](get-recovery-key-cpweb.md)に関するページを参照してください。

ポータル サイト Web サイトで他に何ができるかを調べましょう。 アクションの一覧については、「[Intune ポータル サイト Web サイトの使用](using-the-intune-company-portal-website.md)」を参照してください。  

サポートが必要な場合は、 IT サポート担当者にお問い合わせください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。