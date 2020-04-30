---
title: Intune ポータル サイトと DISA Purebred を使用して iOS または iPadOS デバイスを登録する
description: iOS または iPadOS デバイスを登録し、DISA Purebred で派生した資格情報認証を設定する方法について説明します。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
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
ms.openlocfilehash: 268ed874be65c9ade7f801b89528d1a23f176ee1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82077803"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-disa-purebred"></a>Intune ポータル サイトと DISA Purebred を使用して iOS または iPadOS デバイスをセットアップする  

組織の電子メール、ファイル、およびアプリに安全にモバイルからアクセスするために、Intune ポータル サイト アプリでデバイスを登録します。 デバイスが登録されると、*マネージド*になります。 組織は、Intune などのモバイル デバイス管理 (MDM) プロバイダーを介してデバイスにポリシーとアプリを割り当てることができます。  

登録時に、派生資格情報もデバイスにインストールします。 組織によっては、ユーザーがリソースにアクセスするとき、またはメールに署名して暗号化するために、認証方法として派生資格情報を使用するよう要求することがあります。 

ユーザーは、スマート カードを使用して次のことを行う場合、派生資格情報を設定する必要があります。

* 学校または職場のアプリ、Wi-Fi、仮想プライベート ネットワーク (VPN) にサインインする
* S/MIME 証明書を使用して学校または職場のメールに署名して暗号化する  

この記事では、次のことについて説明します。  

   * Intune ポータル サイトを使用してモバイルの iOS デバイスまたは iPadOS デバイスを登録する。  
   * 組織の派生資格情報プロバイダー DISA Purebred (https:\//cyber.mil/pki-pke/purebred/) から派生資格情報を取得する。  

## <a name="what-are-derived-credentials"></a>派生資格情報とは  
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

また、セットアップの間に、Purebred エージェントまたは担当者に問い合わせる必要があります。      

## <a name="enroll-device"></a>デバイスを登録する  
1. モバイル デバイスで iOS または iPadOS 用の Intune ポータル サイト アプリを開き、職場のアカウントでサインインします。  

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
    b. **[開く]** をクリックして Purebred アプリを開きます。  

    ![Intune ポータル サイトの [モバイル スマート カード アクセスのセットアップ] 画面のスクリーンショットの例。](./media/smart-card-open-disa-purebred.png)  
9. Intune ポータル サイトで Purebred 登録アプリを開く許可を求められたら、 **[開く]** を選択します。   

    ![Intune ポータル サイトで DISA Purebred アプリを開くプロンプトのスクリーンショットの例。](./media/open-app-prompt-disa-purbred.png)  
10. アプリが動いたら、組織の Purebred エージェントと協力して、Purebred の事前登録構成プロファイルを構成してダウンロードします。   
11. 設定アプリで **[General]\(全般\)**  >  **[Profiles & Device Management]\(プロファイルとデバイスの管理\)**  >  **[Install Profile]\(プロファイルのインストール\)** に移動し、 **[Install]\(インストール\)** をタップします。  
12. デバイスのパスコードを入力します。  
13. プロファイルをインストールします。 インストールを開始するには、 **[Install]\(インストール\)** を 2 回以上タップすることが必要な場合があります。 
14. Purebred 登録アプリに戻ります。 Purebred エージェントの指示に従って続行します。  
 
15. 構成プロファイルをダウンロードした後、設定アプリで **[General]\(全般\)**  >  **[Profiles & Device Management]\(プロファイルとデバイスの管理\)**  >  **[Install Profile]\(プロファイルのインストール\)** に移動し、 **[Install]\(インストール\)** をタップします。   
16.  デバイスのパスコードを入力します。
17. プロファイルをインストールします。 インストールを開始するには、 **[Install]\(インストール\)** を 2 回以上タップすることが必要な場合があります。 
18. インストールが完了したら、Intune ポータル サイト アプリに戻ります。  
19.  **[モバイル スマート カード アクセスのセットアップ]** 画面で、 **[続行]** をタップします。  

20. **[証明書のインポート]** 画面で、DISA Purebred から入手した派生資格情報を取得してインポートします。  

    a. **[続行]** をタップします。   

    ![Intune ポータル サイトのインポート証明書設定画面のスクリーンショットの例。](./media/import-certificate-disa-purebred.png)  
    b. iCloud Drive で **[Browse]\(参照\)**  >  **[Locations]\(場所\)** に移動し、 **[More Locations]\(その他の場所\)** をタップします。  

    ![iCloud Drive ドライブの [参照] メニューで [その他の場所] オプションが強調して示されているスクリーンショットの例。](./media/icloud-drive-more-locations.png)  
    c. スイッチをタップして **[Purebred Key Chain]\(Purebred キー チェーン\)** を有効にします。  

    ![iCloud Drive ドライブの参照ビューで Purebred キー チェーン スイッチが有効になっているスクリーンショットの例。](./media/icloud-drive-enable-purebred-keychain.png)   

    d. **[Purebred Credential Package]\(Purebred 資格情報パッケージ\)** をタップします。  

    ![iOS 画面の選択可能な Purebred 資格情報パッケージ オプションのスクリーンショットの例。](./media/purebred-credential-package.png)  
    f. 証明書の一覧が表示されます。 1 つを選択し、 **[Import key]\(キーのインポート\)** をタップします。  

    ![選択可能な証明書の一覧で 1 つが既に選択されているスクリーンショットの例。](./media/import-purebred-keychain.png) 
21. Intune ポータル サイト アプリに戻り、デバイスのセットアップが完了するのを待ちます。   

## <a name="next-steps"></a>次のステップ  
登録が完了すると、メール、Wi-Fi、組織で使用できるようになっているアプリなど、職場のリソースにアクセスできるようになります。 Intune ポータル サイトでアプリを取得、検索、インストール、アンインストールする方法の詳細については、以下を参照してください。

* [ポータル サイト Web サイトからアプリを管理する](manage-apps-cpweb.md)  
* [デバイスで管理対象アプリを使用する](use-managed-apps-on-your-device-ios.md)  

サポートが必要な場合は、 社内サポートに問い合わせてください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。
