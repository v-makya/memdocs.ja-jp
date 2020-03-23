---
title: Intune ポータル サイトで Android デバイスを登録する | Microsoft Docs
description: Intune ポータル サイトで Android デバイスを登録する方法について説明します
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
ms.assetid: 0ed3a002-7533-4001-ae24-e10b64b66620
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 0f6efa6d026879a3231c21662e799bf8ba7ada09
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79337747"
---
# <a name="enroll-your-device-with-company-portal"></a>Intune ポータル サイトでデバイスを登録する  
自分個人または会社所有の Android デバイスを登録して、会社のメール、アプリ、データにアクセスします。 Intune ポータル サイトでは、Android 4.4 以降が実行されている Samsung Knox などの Android デバイスがサポートされています。  
</br>
> [!VIDEO https://www.youtube.com/embed/k0Q_sGLSx6o?rel=0]

> [!NOTE]
> Samsung KNOX は、ネイティブ Android に用意されている以外の追加保護のために特定の Samsung 製のデバイスで使用されるセキュリティの一種です。 Samsung KNOX デバイスかどうかを確認するには、 **[設定]**  >  **[About device]\(デバイス情報\)** を選択します。 そこに **[KNOX version]\(KNOX バージョン\)** と表示されない場合は、ネイティブ Android デバイスです。

## <a name="enroll-device"></a>デバイスを登録する  
必ず、[無料の Intune ポータル サイト アプリを Google Play からインストール](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)します。 

登録中に、デバイスの使用方法に適したカテゴリを選ぶように求められる場合があります。 会社のサポートは、その回答を使用して、ユーザーがアクセスできるアプリを確認します。  

1. Intune ポータル サイト アプリを開き、職場または学校アカウントでサインインします。  

2. 組織の使用条件への同意を求められたら、 **[すべて受け入れる]** をタップします。  

   ![Intune ポータル サイトの使用条件画面で [すべて受け入れる] ボタンが強調して示されている画像の例。](./media/accept-terms-1911.png)  


3. 組織で行えることと行えないことを確認してください。 その後、 **[続行]** をタップします。


    ![ポータル サイトの [ユーザーのプライバシーに配慮しています。] 画面の画像例 ([続行] ボタンが強調表示されています)。](./media/android-privacy-screen-1911.png)  
4. 以降の手順の内容を確認します。 **[次へ]** をタップします。  

    ![Intune ポータル サイトの [次の手順] 画面で [次へ] ボタンが強調して示されている画像の例。](./media/android-whats-next-1911.png)  


5. Android のバージョンによっては、デバイスの特定の部分へのアクセスを許可するように求められる場合があります。 これらのプロンプトは Google によって要求されるものであり、Microsoft では管理されていません。  

    次のアクセス許可に対して **[Allow]\(許可\)** をタップします。  
    * **[Allow Company Portal to make and manage phone calls]\(電話での通話とその管理をポータル サイトに許可する\)** : このアクセス許可を有効にすると、デバイスで国際携帯電話局識別番号 (IMEI) を、組織のデバイス管理プロバイダーである Intune と共有できます。 このアクセス許可を有効にしても安全です。 Microsoft が電話をかけたり管理したりすることはありません。  
    * **[Allow Company Portal to access your contacts]\(ポータル サイトに連絡先へのアクセスを許可する\)** : このアクセス許可を有効にすると、Intune ポータル サイト アプリで職場アカウントを作成、使用、管理できます。  このアクセス許可を有効にしても安全です。 Microsoft が連絡先にアクセスすることはありません。 

    アクセス許可を無効にすると、次に Intune ポータル サイトにサインインするときに、再びメッセージが表示されます。 今後このメッセージが表示されないようにするには、 **[今後このメッセージを表示しない]** を選択します。 アプリのアクセス許可を管理するには、設定アプリで **[アプリ]**  >  **[ポータル サイト]**  >  **[アクセス許可]**  >  **[電話]** に移動します。  

6. デバイス管理アプリをアクティブ化します。 

    Intune ポータル サイトでは、デバイスを安全に管理するためにデバイス管理者のアクセス許可が必要です。 アプリをアクティブ化すると、デバイスのロック解除が繰り返し失敗した場合など、潜在的なセキュリティの問題を組織で特定し、適切に対応できるようになります。  

    ![デバイス管理者アクティブ化画面のアクティブ化ボタンが強調して示されている画像の例。](./media/activate-device-administrator-1911.png)  

> [!NOTE]
> Microsoft がこの画面のメッセージを制御することはありません。 Microsoft は、言い回しがやや極端であることを理解しています。 Intune ポータル サイトでは、組織に関連する制限とアクセス権を指定することはできません。 組織でのアプリの使用方法について不明な点がある場合は、IT サポート担当者にお問い合わせください。 組織の連絡先情報を検索するには、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)に移動してください。  


7. デバイスの登録が開始されます。 Samsung Knox デバイスを使用している場合は、最初に ELM エージェントのプライバシー ポリシーを確認して同意するように求められます。   

    ![登録時に表示される Samsung Knox プライバシー ポリシー画面の画像の例。](./media/and-enroll-7-knox-privacy-policy.png)  

8. **[会社アクセスのセットアップ]** 画面で、デバイスが登録されていることを確認します。 その後、 **[続行]** をタップします。  

    ![Intune ポータル サイトの [会社アクセスのセットアップ] 画面で [デバイスを管理対象にします] が完了している画像の例。](./media/update-settings-1911.png)  

9. 組織によって、デバイス設定を更新するように求められる場合があります。 設定を調整するには、 **[解決]** をタップします。 設定の更新が完了したら、 **[続行]** をタップします。  

   ![Intune ポータル サイトの [デバイス設定の更新] 画面の [解決] ボタンと [続行] ボタンが強調して示されている画像の例。](./media/resolve-settings-1911.png)  

10. セットアップが完了したら、 **[完了]** をタップします。    

    ![ポータル サイトの [会社アクセスのセットアップ] 画面の画像例 (完了したセットアップが表示され、[完了] ボタンが強調表示されています)。](./media/android-enrollment-done-1911.png) 

## <a name="next-steps"></a>次のステップ  

学校または職場のアプリをインストールする前に、 **[設定]**  >  **[セキュリティ]** に移動し、 **[Unknown sources]\(不明なソース\)** をオンにします。 このオプションをオンにしない場合、アプリをインストールしようとすると次のメッセージが表示されます: インストールがブロックされました。 セキュリティ上の理由から、デバイスは不明のソースから取得したアプリのインストールをブロックするように設定されています。 メッセージの **[設定]** をタップして、 **[Unknown sources]\(不明なソース\)** に直接移動できます。  

> [!Note]
> 組織で通信費管理ソフトウェアを使用している場合は、デバイスの登録を完了する前にいくつかの追加手順を実行します。 詳細については、[こちら](enroll-your-device-with-telecom-expense-management-android.md)を参照してください。

Intune にデバイスを登録している最中にエラーが表示された場合は、[会社のサポートにメールを送る](send-logs-to-your-it-admin-by-email-android.md)ことができます。  

サポートが必要な場合は、 社内サポートに問い合わせてください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。  