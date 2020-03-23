---
title: Intune ポータル サイトと Intercede を使用して iOS または iPadOS デバイスを登録する
description: iOS または iPadOS デバイスを登録し、Intercede で派生した資格情報認証を設定する方法について説明します。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 1bd216049c5dbda7c044949f9fa39c3b7bd56f9d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79337240"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-intercede"></a>Intune ポータル サイトと Intercede を使用して iOS または iPadOS デバイスをセットアップする

組織の電子メール、ファイル、およびアプリに安全にモバイルからアクセスするために、Intune ポータル サイト アプリでデバイスを登録します。  デバイスが登録されると、*マネージド*になります。 組織は、Intune などのモバイル デバイス管理 (MDM) プロバイダーを介してデバイスにポリシーとアプリを割り当てることができます。  

登録時に、派生資格情報もデバイスにインストールします。 組織によっては、ユーザーがリソースにアクセスするとき、またはメールに署名して暗号化するために、認証方法として派生資格情報を使用するよう要求することがあります。 

ユーザーは、スマート カードを使用して次のことを行う場合、派生資格情報を設定する必要があります。

* 学校または職場のアプリ、Wi-Fi、仮想プライベート ネットワーク (VPN) にサインインする
* S/MIME 証明書を使用して学校または職場のメールに署名して暗号化する  

この記事では、次のことについて説明します。  

* Intune ポータル サイトを使用してモバイルの iOS デバイスまたは iPadOS デバイスを登録する。  
* 組織の派生資格情報プロバイダー [Intercede](https://www.intercede.com/) から派生資格情報を取得する。   


## <a name="what-are-derived-credentials"></a>派生資格情報とは  
派生資格情報とは、スマート カードの資格情報から派生し、デバイスにインストールされる証明書です。 これにより、未承認ユーザーによる機密情報へのアクセスを防ぎながら、作業リソースへのリモート アクセスが許可されます。  

派生資格情報は次の目的に使用されます。 
* 学校または職場のアプリ、Wi-Fi、VPN にサインインする学生と従業員を認証する
* S/MIME 証明書で学校または職場のメールに署名して暗号化する  

派生資格情報は、Special Publication (SP) 800-157 に含まれている Derived Personal Identity Verification (PIV) 資格情報に対する米国標準技術研究所 (NIST) ガイドラインの実装です。  

## <a name="prerequisites"></a>[前提条件]

 登録を完了するには、次のものが必要です。

* 学校または職場で提供されたスマート カード
* スマート カードを使用してサインインできるコンピューターまたはセルフサービス キオスクへのアクセス
* モバイル デバイス
* デバイスにインストールされた iOS および iPadOS 用の Intune ポータル サイト アプリ


## <a name="enroll-device"></a>デバイスを登録する  
1. モバイル デバイスで iOS または iPadOS 用の Intune ポータル サイト アプリを開き、職場のアカウントでサインインします。  
2. 画面に表示されるコードを書き留めます。  

    ![メッセージとコードが画面に表示された Intune ポータル サイト アプリの画像の例。](./media/copy-code-intercede.png)  
1. スマート カード対応のデバイスに切り替えて、 https://microsoft.com/devicelogin にアクセスします。 

1. 前に書き留めたコードを入力します。
 
2. スマート カードを挿入してサインインします。   

3. モバイル デバイスで Intune ポータル サイト アプリに戻り、画面の指示に従ってデバイスを登録します。  
4. 登録が完了すると、Intune ポータル サイトによって、スマート カードをセットアップするよう通知されます。 通知をタップします。 通知が表示されない場合は、メールを確認してください。   

    ![デバイスのホーム画面に Intune ポータル サイトのプッシュ通知が表示されたスクリーンショットの例。](./media/action-required-in-app-intercede.png)  

5. **[モバイル スマート カード アクセスのセットアップ]** 画面で次のようにします。  
    」を参照します。 組織のセットアップ手順へのリンクをタップします。 組織で追加の手順が提供されていない場合は、この記事が表示されます。  
    b. **[開始]** をタップします。  

    ![Intune ポータル サイトの [モバイル スマート カード アクセスのセットアップ] 画面のスクリーンショットの例。](./media/smart-card-info-intercede.png)  

6. スマート カード対応デバイスまたはセルフサービス キオスクに切り替え、MyID アプリを開きます。 職場の資格情報を使用してサインインします。  
7. ID を要求するオプションを選択します。 
8. 使用するプロファイルの確認を求めるメッセージが表示されたら、モバイル資格情報でアクティブ化するためのオプションを選択します。 QR コードが表示されます。  
9. モバイル デバイスに戻ります。 Intune ポータル サイトの **[QR コードの取得]** 画面で、 **[続行]** をタップします。  

    ![Intune ポータル サイトの [QR コードの取得] 画面のスクリーンショットの例。](./media/get-qr-code-intercede.png) 
 
10. **[カメラを使用する]**  >  **[OK]** をタップします。  

    ![Intune ポータル サイトでカメラのアクセス許可を求めるメッセージのスクリーンショットの例。](./media/allow-cp-camera-access-intercede.png)  

11. スマート カード対応デバイスに表示された QR コードの画像をスキャンします。 
12. Intune ポータル サイトによるデバイスのセットアップが完了するまで待ちます。  

## <a name="next-steps"></a>次のステップ  
登録が完了すると、メール、Wi-Fi、組織で使用できるようになっているアプリなど、職場のリソースにアクセスできるようになります。 Intune ポータル サイトでアプリを取得、検索、インストール、アンインストールする方法の詳細については、以下を参照してください。

* [ポータル サイト Web サイトからアプリを管理する](manage-apps-cpweb.md)  
* [デバイスで管理対象アプリを使用する](use-managed-apps-on-your-device-ios.md)  

サポートが必要な場合は、 社内サポートに問い合わせてください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。
