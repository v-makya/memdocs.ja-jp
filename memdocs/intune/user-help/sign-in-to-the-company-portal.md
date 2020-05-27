---
title: ポータル サイト アプリにサインインする方法 | Microsoft Docs
description: 複数のプラットフォームでポータル サイト アプリにサインインする方法を確認します。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/31/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: cfd214bc-f072-4808-af2e-a3cbf7af9bca
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 59555c8bb9a35d5b70b46836f2298bf3ed342b2d
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881831"
---
# <a name="sign-in-to-company-portal"></a>ポータル サイトにサインインする  

ポータル サイト アプリにサインインする方法は 3 つあります。

* 仕事用メール アドレスとパスワードを使ってサインインする。  
* 証明書ベースの認証を使ってサインインする。  
* 別のデバイスからサインインする。    


## <a name="sign-in-with-your-email-address-and-password"></a>メール アドレスとパスワードを使ったサインイン
次の手順では、iOS 用のポータル サイトのスクリーンショットを示します。  

1. お使いのデバイスでアプリを開いて、 **[サインイン]** をタップします。  

   ![ポータル サイトのサインイン ページのサンプル スクリーンショット。](./media/intune-ios-cp-signin-1908.png)


2. **職場または学校のアカウント**を入力して、 **[次へ]** をタップします。

   ![画面は同じですが電子メールとパスワードではなく、電子メールのみを入力するように要求されます。](./media/cp_ios_aad_signin_after_1804_002.png)

3. パスワードを入力し、 **[サインイン]** をタップします。

   ![電子メールが承認されると、パスワードの入力が要求されます。](./media/cp_ios_aad_signin_after_1804_003.png)

4. アプリによって資格情報が確認されます。 完了後、組織のリソースにアクセスして、利用可能なアプリをインストールできます。  

   ![認証プロセスが終了すると、ポータル サイト アプリでサインインが行われ、読み込みバーが表示されます。](./media/cp_ios_aad_signin_after_1804_004.png)

## <a name="sign-in-with-certificate-based-authentication"></a>証明書ベースの認証を使ってサインインする
このサインイン オプションは、組織で証明書ベースの認証が許可されていて、使用可能な証明書がある場合にのみ表示されます。  

1. デバイス上でポータル サイト アプリを開きます。  

2. **職場または学校アカウント**を入力します。  

3. **[Sign in with a certificate]\(証明書を使用してサインイン\)** をタップします。  

4. **[続行]** をタップして証明書を使用します。  

## <a name="sign-in-from-another-device"></a>別のデバイスからサインインする

会社がコンピューターへのアクセスにスマートカードを使用している場合は、別のデバイスからサインインして認証しなければならない可能性があります。  

1. デバイス上でポータル サイト アプリを開きます。 職場のリソースにアクセスするために使用するデバイスであることを確認します。       

1. **[別のデバイスからサインインする]** を選択します。  

   ![ポータル サイトのサインイン ページで、メール アドレスの入力がユーザーに求められます。  [次へ] ボタンと [別のデバイスからサインインする] リンクが表示されます。 "アカウントにアクセスできない場合" のリンクもあります。 下部にあるリンクから Microsoft のプライバシーと Cookie に関する情報にアクセスできます。](./media/cp_ios_aad_signin_after_1804_005.png)

2. ポータル サイトにサインインするための、一意のワンタイム コードを受け取ります。 コードをコピーします。

   ![会社のコンピューターから固有のパスワードで https://microsoft.com/devicelogin ページにアクセスし、コードを使用してサインインするように指示されます。](./media/cp_ios_aad_signin_after_1804_006.png)

3. 他のデバイス (認証に使用しているデバイス) で、ブラウザーを開き、[https://microsoft.com/devicelogin](https://microsoft.com/devicelogin) にアクセスします。 コードを入力するか、貼り付けます。  

   ![ポータル サイト アプリの画像ではなく会社のコンピューターのブラウザーの画像です。 [デバイス ログイン] ページが表示され、ポータル サイト アプリで取得したコードを入力するように要求されます。](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_004.png)

4. __[続行]__ を選択して、ポータル サイトから職場のデバイスにサインインできるようにします。   

   ![固有のコードをフィールドに入力すると、[デバイス ログイン] サイトから、Intune ポータル サイトがサインインを許可してよい適切なアプリであることを確認されます。](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_005.png) 

5. コードが確認されたら、ウィンドウを閉じることができます。  

   ![デバイスでポータル サイト アプリへのログインが完了したことと、このページを閉じることができることを示す確認ページ。](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_006.png)

6. ポータル サイト アプリを通じて職場のデバイスにサインインします。  

   ![認証プロセスが終了すると、ポータル サイト アプリはサインインを行い、進捗を示す読み込みバーが表示されます。](./media/cp_ios_aad_signin_after_1804_007.png)

サポートが必要な場合は、 社内サポートに問い合わせてください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。  
