---
title: Microsoft Intune アプリと DISA Purebred を使用して Android デバイスを登録する
description: DISA Purebred を使用して、Android デバイスを登録し、派生資格情報認証を設定する方法について説明します。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/15/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: 584392891320f96eed16863225ffb323dc240594
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83880616"
---
# <a name="set-up-android-device-with-the-microsoft-intune-app-and-disa-purebred"></a>Microsoft Intune アプリと DISA Purebred を使用して Android デバイスを設定する

組織の電子メール、ファイル、およびアプリにモバイルから安全にアクセスするために、Microsoft Intune アプリでデバイスを登録します。 デバイスが登録されると、*マネージド*になります。 組織は、Intune などのモバイル デバイス管理 (MDM) プロバイダーを介してデバイスにポリシーとアプリを割り当てることができます。  

登録時に、派生資格情報もデバイスにインストールします。 組織によっては、ユーザーがリソースにアクセスするとき、またはメールに署名して暗号化するために、認証方法として派生資格情報を使用するよう要求することがあります。

ユーザーは、スマート カードを使用して次のことを行う場合、派生資格情報を設定する必要があります。

* 学校または職場のアプリ、Wi-Fi、仮想プライベート ネットワーク (VPN) にサインインする
* S/MIME 証明書を使用して学校または職場のメールに署名して暗号化する

この記事では、次のことについて説明します。

* Intune アプリを使用して Android モバイル デバイスを登録する
* 組織の派生資格情報プロバイダーである [DISA Purebred](https://public.cyber.mil/pki-pke/purebred/) から派生資格情報をインストールして、スマート カードを設定する

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
* Android 7.0 以降が動作している新しいデバイスまたは出荷時の設定に戻したデバイス 
* ご自分のデバイスに Microsoft Intune アプリがインストールされていること
* デバイスにインストールされている Purebred アプリ (アプリはデバイスのセットアップ直後に自動的にインストールされます。 インストールされない場合は、IT サポート担当者にお問い合わせください。)

また、セットアップの間に、Purebred エージェントまたは担当者に問い合わせる必要があります。

## <a name="enroll-device"></a>デバイスを登録する  

1. 新しいデバイスまたは出荷時の設定に戻したデバイスの電源を入れます。  
2. **[ようこそ]** 画面で、言語を選択します。 QR コードまたは NFC で登録するように指示されている場合は、方法に一致する以下の手順に従います。  
     * NFC:お使いの NFC 対応デバイスをプログラマー デバイスに対してタップし、組織のネットワークに接続します。 画面の指示に従います。 Chrome のサービス利用規約の画面が表示されたら、ステップ 5 に進みます。  

     * QR コード:「[QR コードでの登録](#qr-code-enrollment)」の手順を完了します。  

     別の方法を使用するように指示されている場合は、ステップ 3 に進みます。    

3. Wi-Fi に接続し、 **[次へ]** をタップします。 登録方法と一致する手順に従います。 

    * トークン:Google のサインイン画面が表示されたら、「[トークンでの登録](#token-enrollment)」の手順を完了します。  
    * Google Zero Touch:Wi-Fi に接続すると、組織によってデバイスが認識されます。 ステップ 4 に進み、画面の指示に従ってセットアップを完了します。    
 
       ![Google Zero Touch を使用した場合に表示される Google 契約条件画面の例の画像。[Accept & Continue]\(同意して続行\) ボタンが強調表示されている。](./media/google-zero-touch-intune-app-01.png)   
   
4. Google の契約条件を確認します。 次に、 **[ACCEPT & CONTINUE]\(同意して続行\)** をタップします。  

      ![Google 契約条件画面の例の画像。[Accept & Continue]\(同意して続行\) ボタンが強調表示されている。](./media/fully-managed-intune-app-04.png)   

5. Chrome のサービス利用規約を確認します。 次に、 **[ACCEPT & CONTINUE]\(同意して続行\)** をタップします。  

   ![Chrome サービス利用規約画面の例の画像。[Accept & Continue]\(同意して続行\) ボタンが強調表示されている。](./media/fully-managed-intune-app-06.png)   

6. サインイン画面で、 **[サインイン オプション]** 、 **[別のデバイスからサインインする]** の順にタップします。 

7. 画面に表示されたコードを書き留めます。  

8. スマート カード対応のデバイスに切り替えて、画面に表示されている Web アドレスにアクセスします。 

9. 前に書き留めたコードを入力します。

   > [!div class="mx-imgBorder"]
   > ![Intune ポータル サイト Web サイトの "コード入力" プロンプトのスクリーンショット。](./media/enter-code-intercede.png)

10. スマート カードを挿入してサインインします。 

11. サインイン画面で、職場または学校アカウントを選択します。 次に、モバイル デバイスに戻ります。 

12. 組織の要件によっては、画面のロックや暗号化などの設定の更新を求められる場合があります。 これらのプロンプトが表示された場合は、 **[設定]** をタップして、画面の指示に従います。  

       ![職場の携帯電話の設定画面の例の画像。[設定] ボタンが強調表示されている。](./media/fully-managed-intune-app-10.png)   

13. 仕事用アプリをデバイスにインストールするには、 **[インストール]** をタップします。 インストールが完了したら、 **[次へ]** をタップします。  

       ![職場の携帯電話の設定画面の例の画像。[インストール] ボタンが強調表示されている。](./media/fully-managed-intune-app-11.png)   

14. **[START] (スタート)** をタップして Microsoft Intune アプリを開きます。 

    ![[スタート] ボタンが強調表示されている職場の携帯電話の設定画面の例の画像。](./media/fully-managed-intune-app-17.png)   

15. モバイル デバイスで Intune アプリに戻り、登録が完了するまで画面の指示に従います。 

    ![[完了] ボタンが強調して示されているアクセス セットアップのデバイス登録画面の例の画像。](./media/fully-managed-intune-app-19.png)   

16. この記事の「[スマート カードを設定する](enroll-android-device-disa-purebred.md#set-up-smart-card)」セクションに進み、デバイスの設定を完了します。  

### <a name="qr-code-enrollment"></a>QR コードでの登録  
このセクションでは、会社から提供された QR コードをスキャンします。  完了すると、デバイス登録手順に戻ります。     
  
1. **[ようこそ]** 画面で、画面を 5 回タップして QR コードのセットアップを起動します。  

   ![デバイス セットアップの [ようこそ] 画面の例の画像。画面タップ指示が強調表示されている。](./media/qr-code-intune-app-01.png)  

2. 画面の指示に従って Wi-Fi に接続します。  
3. お使いのデバイスに QR コード スキャナーがない場合、セットアップ画面にスキャナーのインストールの進行状況が表示されます。 インストールが完了するまで待ちます。  
4. メッセージが表示されたら、組織から提供されている登録プロファイル QR コードをスキャンします。  
5. ステップ 4 の「[デバイスを登録する](#enroll-device)」に戻り、セットアップを続けます。  

### <a name="token-enrollment"></a>トークンでの登録  
このセクションでは、会社から提供されたトークンを入力します。 完了すると、デバイス登録手順に戻ります。  

1. Google サインイン画面の **[メールまたは電話]** ボックスに、「**afw#setup**」と入力します。 **[次へ]** をタップします。 

   ![Google サインイン画面の例の画像。"afw#setup" がフィールドに入力されている。](./media/token-intune-app-01.png)   

2. **[Android Device Policy]\(Android デバイス ポリシー\)** アプリの **[インストール]** を選択します。 インストールを続けます。 お使いのデバイスによっては、追加の条件を確認して同意する必要があります。    

3. **[このデバイスの登録]** 画面で、 **[次へ]** を選択します。  

4. **[コードの入力]** を選択します。  

5. **[Scan or enter code]\(コードのスキャンまたは入力\)** 画面で、組織から提供されたコードを入力します。  **[次へ]** をクリックします。  

   ![[Scan or enter code]\(コードのスキャンまたは入力\) 画面の例の画像。強調表示された [次へ] ボタン。](./media/token-intune-app-04.png)  

6. ステップ 4 の「[デバイスを登録する](#enroll-device)」に戻り、セットアップを続けます。


## <a name="set-up-smart-card"></a>スマート カードを設定する  

> [!NOTE]
> これらの手順を完了するには、Purebred アプリが必要です。これは、登録後、デバイスに自動的にインストールされます。 しばらく待ってもアプリがまだ存在しない場合は、IT サポート担当者にお問い合わせください。  

1. 登録が完了すると、Intune アプリから、スマート カードを設定するよう通知されます。 通知をタップします。 通知が表示されない場合は、メールを確認してください。

   > [!div class="mx-imgBorder"]
   > ![デバイスのホーム画面上の Intune アプリのプッシュ通知のスクリーンショット。](./media/action-required-in-app-android.png)

2. **[Set up smart card] (スマート カードを設定する)** 画面で、次の操作を行います。

   1. 組織のセットアップ手順へのリンクをタップして、それらを確認します。 組織で追加の手順が提供されていない場合は、この記事が表示されます。

   2. **[開始]** をタップします。   

   > [!div class="mx-imgBorder"]
   > ![Intune アプリの [Set up smart card]\(スマート カードのセットアップ\) 画面のスクリーンショット。](./media/smart-card-open-disa-purebred-android.png)

3. **[証明書の取得]** 画面で、 **[LAUNCH PUREBRED]\(Purebred の起動\)** をタップして、Purebred アプリを開きます。 (このアプリはデバイスに自動的にインストールされているはずです。 存在しない場合は、サポート担当者にお問い合わせください。)  

   > [!div class="mx-imgBorder"]
   > ![DISA Purebred アプリを開くための Intune アプリのプロンプトのスクリーンショット。](./media/open-app-prompt-disa-purbred-android.png)  

4. 正常に実行するために、Purebred アプリに追加のアクセス許可が必要になる場合があります。 プロンプトが表示されたら、 **[許可]** または **[Allow all the time]\(常に許可\)** をタップします。 これらのアクセス許可が必要な理由の詳細については、サポート担当者または Purebred エージェントとお話しください。  

5. Purebred アプリを開いたら、組織の Purebred エージェントと協力して、職場または学校のリソースにアクセスするために必要な証明書をダウンロードしてインストールします。

    > [!IMPORTANT]
    > このプロセスの間にプロンプトが表示されたら、 **[OK]** または **[インストール]** をタップします。 インストールするように求められている証明機関 (CA) または証明書の名前は変更しないでください。    

6. インストールが完了すると、証明書の準備ができたことを示す通知を受け取ります。 その通知をタップして Intune アプリに戻ります。

    > [!div class="mx-imgBorder"]
    > ![[Allow access to certificates]\(証明書へのアクセスを許可\) 画面のスクリーンショット](./media/certificates-ready-prompt-disa-purbred-android.png)

7. **[Allow access to certificates]\(証明書へのアクセスを許可\)** 画面で、DISA Purebred から取得した派生資格情報にアクセスするためのアクセス許可を Intune アプリに付与します。 この手順により、保護されている職場や学校のリソースにアクセスするたびに、組織が本人確認を確実に行うことができます。  

    1. **[次へ]** をタップします。

       > [!div class="mx-imgBorder"]
       > !["証明書の準備完了" プロンプトのスクリーンショット](./media/certificates-access-disa-purbred-android.png)

    2. **証明書の選択**を求めるメッセージが表示されたら、選択内容を変更しないでください。 正しい証明書が既に選択されているので、 **[選択]** または **[OK]** のタップのみを行います。  

       > [!div class="mx-imgBorder"]
       > ![[Choose certificate]\(証明書の選択\) プロンプトのスクリーンショット](./media/choose-certificates-prompt-disa-purbred-android.png)

    3. 派生資格情報は複数の証明書で構成されているため、 **[Choose certificate]\(証明書の選択\)** プロンプトが複数回表示される場合があります。 プロンプトが表示されなくなるまで、前の手順を繰り返します。  

8. すべての証明書が処理されたら、Intune アプリでデバイスの設定が完了するまで待機します。 **[すべての設定が完了しました!]** 画面が表示されると、設定が完了したことがわかります。  

    > [!div class="mx-imgBorder"]
    > ![[すべての設定が完了しました] 画面のスクリーンショット](./media/all-set-android.png)

## <a name="next-steps"></a>次のステップ

登録が完了すると、メール、Wi-Fi、組織で使用できるようになっているアプリなど、職場のリソースにアクセスできるようになります。 Intune アプリでアプリを取得、検索、インストール、アンインストールする方法について詳しくは、以下をご覧ください。

* [デバイスで管理対象アプリを使用する](use-managed-apps-on-your-device-android.md)  
* [ポータル サイト Web サイトからアプリを管理する](manage-apps-cpweb.md)  


サポートが必要な場合は、 社内サポートに問い合わせてください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。
