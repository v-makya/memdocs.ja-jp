---
title: Intune ポータル サイトで Android の仕事用プロファイルを登録する | Microsoft Docs
description: 仕事用プロファイルを作成して Intune ポータル サイトにデバイスを登録する方法。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/08/2020
ms.togit pic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 33ffff16-0280-43bf-87b3-74ddf4439bfa
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: cbfdd10ce15a477fe574a486ee3d4a3779d18e90
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881662"
---
# <a name="enroll-device-with-android-work-profile"></a>Android の仕事用プロファイルでデバイスを登録する

自分の個人用の Android デバイスを登録して、職場または学校のメール、アプリ、その他のデータにアクセスできます。 登録中に、Android の仕事用プロファイルを設定します。 このプロファイルにより、デバイス上の個人データが作業データから分離されます。 仕事用プロファイルは組織によって管理されます。これは作業ファイルとデータで構成されます。 会社のサポートでは、デバイス上の個人情報は管理できません。  
</br>
> [!VIDEO https://www.youtube.com/embed/9Dl8HsGk4tI]

詳細については、「[仕事用プロファイルを作成するとどうなりますか](what-happens-when-you-create-a-work-profile-android.md)」を参照してください。

## <a name="create-work-profile-and-enroll-device"></a>仕事用プロファイルを作成してデバイスを登録する

1. Intune ポータル サイト アプリを開き、職場または学校アカウントでサインインします。 この無料アプリをインストールしていない場合は、[Google Play](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) からインストールしてください。  

2. **[会社アクセスのセットアップ]** 画面で、 **[開始]** をタップします。  

    ![[会社アクセスのセットアップ] 画面のスクリーンショット](./media/access-setup-work-profile-1911.png)  

3. 組織で行えることと行えないことを確認してください。 その後、 **[続行]** をタップします。 

    ![ポータル サイトの [ユーザーのプライバシーに配慮しています。] 画面の画像例 ([続行] ボタンが強調表示されています)。](./media/android-privacy-screen-1911.png)  

4. 仕事用プロファイルの作成に関する Google の契約条件を確認します。 次に、 **[ACCEPT & CONTINUE]\(同意して続行\)** をタップします。 この画面の外観は、使用するデバイスの Android バージョンによって異なります。 

    ![Google の仕事用プロファイルの契約条件のスクリーンショット](./media/android-wp-05-1908.png)  

5. 仕事用プロファイルが設定されている間待機します。  

    ![[Setting up work profile]\(仕事用プロファイルを設定しています\) 画面のスクリーンショット。](./media/android-wp-05a-1908.png)  

   Android のバージョンによっては、追加の画面が表示される場合があります。 そこでは、まだセットアップの途中であることが示されます。 この画面が表示された場合は、ポータル サイト アプリにリダイレクトされ、サインインが行われるまでしばらく待機します。  

    ![リダイレクト メッセージが表示された [まだ途中です] 画面のスクリーンショット。](./media/android-wp-05b-1908.png)  

6. **[会社アクセスのセットアップ]** 画面で、仕事用プロファイルが作成されていることを確認します。 その後、 **[続行]** をタップします。  

    ![仕事用プロファイルが作成されたことを示す [会社アクセスのセットアップ] のスクリーンショット。](./media/work-profile-complete-1911.png)  

7. 仕事用プロファイルがアクティブであることを確認します。 その後、 **[続行]** をタップします。 

    ![仕事用プロファイルがアクティブであることを示す [会社アクセスのセットアップ] のスクリーンショット。](./media/work-profile-active-1911.png)  

8. 組織によって、デバイス設定を更新するように求められる場合があります。 設定を調整するには、 **[解決]** をタップします。 設定の更新が完了したら、 **[続行]** をタップします。    

    ![ポータル サイトの [デバイス設定の更新] 画面の画像例 ([解決] ボタンと [続行] ボタンが強調表示されています)。](./media/resolve-settings-1911.png) 


9. セットアップが完了したら、 **[完了]** をタップします。  

    ![ポータル サイトの [会社アクセスのセットアップ] 画面の画像例 (完了したセットアップが表示され、[完了] ボタンが強調表示されています)。](./media/work-profile-done-1911.png)  

10. Google Play で組織のおすすめのアプリを表示するように求めるメッセージが表示されたら、 **[開く]** を選択します。 

    ![Google Play のバッジ付きバージョンを開くように求めるポータル サイトのプロンプトの画像の例。](./media/get-apps-banner-android-2005.png) 

    アプリをインストールする準備ができていない場合は、Google Play のバッジ付きバージョンに直接移動することで、いつでも後からアクセスできます。 また、ポータル サイトのメニューから **[アプリの取得]** を選択することもできます。  

    ![[アプリの取得] リンクが強調表示されたポータル サイトのメニューの画像の例。](./media/updated-drawer-android-2005.png) 



## <a name="next-steps"></a>次のステップ  

これでデバイスが登録されたので、デバイスに学校または仕事用のアプリをインストールできます。 managed Google Play ストアにアクセスし、これらのアプリを検索してインストールしてください。 

サポートが必要な場合は、 社内サポートに問い合わせてください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。
