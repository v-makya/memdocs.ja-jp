---
title: Intune ポータル サイトと Entrust Datacard を使用して iOS または iPadOS デバイスを登録する
description: iOS または iPadOS デバイスを登録し、Entrust Datacard で派生資格情報認証を設定します。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/08/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: e849936e7e0686af3377fd4d10182d3a4eb84458
ms.sourcegitcommit: 678104677ad36b789630befdc5e0f1efc572c14b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86137430"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-entrust-datacard"></a>Intune ポータル サイトと Entrust Datacard を使用して iOS または iPadOS デバイスを設定する

組織の電子メール、ファイル、およびアプリに安全にモバイルからアクセスするために、Intune ポータル サイト アプリでデバイスを登録します。 デバイスが登録されると、*マネージド*になります。 組織は、Intune などのモバイル デバイス管理 (MDM) プロバイダーを介してデバイスにポリシーとアプリを割り当てることができます。  

登録時に、派生資格情報もデバイスにインストールします。 組織によっては、ユーザーがリソースにアクセスするとき、またはメールに署名して暗号化するために、認証方法として派生資格情報を使用するよう要求することがあります。 

ユーザーは、スマート カードを使用して次のことを行う場合、派生資格情報を設定する必要があります。  

* 学校または職場のアプリ、Wi-Fi、仮想プライベート ネットワーク (VPN) にサインインする
* S/MIME 証明書を使用して学校または職場のメールに署名して暗号化する  

この記事では、次のことについて説明します。  

   * Intune ポータル サイトを使用してモバイルの iOS デバイスまたは iPadOS デバイスを登録する。  
   * 組織の派生資格情報プロバイダー [Entrust Datacard](https://www.entrustdatacard.com/) から派生資格情報を取得する。  

### <a name="what-are-derived-credentials"></a>派生資格情報とは  
派生資格情報とは、ご自分のスマート カードの資格情報から派生し、デバイスにインストールされる証明書です。 これにより、未承認ユーザーによる機密情報へのアクセスを防ぎながら、作業リソースへのリモート アクセスが許可されます。  

派生資格情報は次の目的に使用されます。 
* 学校または職場のアプリ、Wi-Fi、VPN にサインインする学生と従業員を認証する
* S/MIME 証明書で学校または職場のメールに署名して暗号化する

派生資格情報は、Special Publication (SP) 800-157 に含まれている Derived Personal Identity Verification (PIV) 資格情報に対する米国標準技術研究所 (NIST) ガイドラインの実装です。  

## <a name="prerequisites"></a>[前提条件]

 登録を完了するには、次のものが必要です。

* 学校または職場で提供されたスマート カード
* スマート カードを使用してサインインできるコンピューターまたはキオスクへのアクセス
* モバイル デバイス
* デバイスにインストールされた iOS および iPadOS 用の Intune ポータル サイト アプリ  


## <a name="enroll-device"></a>デバイスを登録する  
1. モバイル デバイスで iOS または iPadOS 用の Intune ポータル サイト アプリを開き、別のデバイスからサインインするオプションを選択します。  

2. 画面に表示されたコードを書き留めます。  

    ![メッセージとコードが画面に表示された Intune ポータル サイト アプリの画像の例。](./media/copy-code-intercede.png)   

3. スマート カード対応のデバイスに切り替えて、 https://microsoft.com/devicelogin にアクセスします。 
4. 前に書き留めたコードを入力します。  

    ![Intune ポータル サイト Web サイトの "コード入力" プロンプトのスクリーンショットの例。](./media/enter-code-intercede.png)   

5. スマート カードを挿入してサインインします。   
6. モバイル デバイスで Intune ポータル サイト アプリに戻り、画面の指示に従ってデバイスを登録します。  
7. 登録が完了すると、Intune ポータル サイトによって、スマート カードをセットアップするよう通知されます。 通知をタップします。 通知が表示されない場合は、メールを確認してください。   

    ![デバイスのホーム画面に Intune ポータル サイトのプッシュ通知が表示されたスクリーンショットの例。](./media/action-required-in-app-intercede.png)  

8. **[モバイル スマート カード アクセスのセットアップ]** 画面で次のようにします。   
    a. 組織のセットアップ手順へのリンクをタップします。 組織で追加の手順が提供されていない場合は、この記事が表示されます。  
    b. **[開始]** をタップします。  

    ![Intune ポータル サイトの [モバイル スマート カード アクセスのセットアップ] 画面のスクリーンショットの例。](./media/smart-card-info-intercede.png)

9. スマート カード対応のデバイスに切り替えて、IdentityGuard を開きます。 
10. スマート資格情報のサインイン領域を見つけて、サインイン ボタンを選択します。  
11. 証明書の選択を求められたら、スマート カードの資格情報を選択します。 次に、 **[OK]** を選択します。 
12. スマート カードの PIN を入力します。  
13. アクションの一覧から選択するように求められます。 派生バイル スマート資格情報に登録できるものを選択します。 リンクまたはボタンに、 **[I'd like to enroll for a derived mobile smart card credential]\(派生モバイル スマート カード資格情報で登録する\)** と表示される場合があります。  
14. スマート資格情報対応のアプリケーションを正常にダウンロードしてインストールしたことを選択します。 次の画面に進みます。   
15. 派生スマート カード資格情報に関する情報を入力します。  
    a. ID 名には任意の名前を入力します (例: *Entrust Derived Cred*)。  
    b. ドロップダウン メニューで、 **[Entrust IdentityGudard Mobile Smart Credential]\(Entrust IdentityGudard モバイル スマート資格情報\)** を選択します。  
    c. 次の画面に進みます。 その下に、数値のパスワードを含む QR コードが表示されます。  

16. モバイル デバイスに戻ります。 Intune ポータル サイトの **[QR コードの取得]** 画面で、 **[続行]** をタップします。 

    ![Intune ポータル サイトの [QR コードの取得] 画面のスクリーンショットの例。](./media/get-qr-code-intercede.png)  
17. **[カメラを使用する]**  >  **[OK]** をタップします。  

    ![Intune ポータル サイトでカメラのアクセス許可を求めるメッセージのスクリーンショットの例。](./media/allow-cp-camera-access-intercede.png)  
18. スマート カード対応デバイスに表示された QR コードの画像をスキャンします。  
19. QR コードの下に表示された数字のパスワードを入力します。  

    ![Intune ポータル サイトの [パスワードが必要] 画面で [パスワード] フィールドに入力したスクリーンショットの例。](./media/enter-password-derived-credentials.png)   

20. Intune ポータル サイトによるデバイスのセットアップが完了するまで待ちます。  


## <a name="next-steps"></a>次のステップ  
登録が完了すると、メール、Wi-Fi、組織で使用できるようになっているアプリなど、職場のリソースにアクセスできるようになります。 Intune ポータル サイトでアプリを取得、検索、インストール、アンインストールする方法の詳細については、以下を参照してください。

* [ポータル サイト Web サイトからアプリを管理する](manage-apps-cpweb.md)  
* [デバイスで管理対象アプリを使用する](use-managed-apps-on-your-device-ios.md)  

サポートが必要な場合は、 社内サポートに問い合わせてください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。  
