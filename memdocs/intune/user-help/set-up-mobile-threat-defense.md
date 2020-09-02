---
title: モバイル デバイスに Mobile Threat Defense をインストールする
description: モバイル脅威防御アプリの概要と、そのセットアップ方法について説明します。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/20/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser, contperfq1
ms.collection: ''
ms.openlocfilehash: 37b7006ef912d87276c11e09cb6db0c0f14059c4
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193914"
---
# <a name="install-mobile-threat-defense-app"></a>Mobile Threat Defense アプリのインストール  

> [!TIP]
> 市場にはさまざまな MTD アプリがあります。 どれを使用するかは、組織から指定されているはずです。 MTD アプリのインストールを求めるメッセージが表示されても、すぐにアプリのセットアップまたはインストールにリダイレクトされない場合は、IT サポート担当者に問い合わせてください。  

組織のセキュリティ要件の一部として、モバイル脅威防御 (MTD) ベンダー アプリのインストールが必要になる場合があります。 この種類のアプリでは、疑わしいアプリ、ネットワーク、OS の脆弱性など、デバイス上の脅威が検出され、アラートが生成されます。  

必要な MTD アプリがない場合は、職場または学校アカウントを使用して保護されたマネージド アプリ (Microsoft Excel や OneDrive など) にサインインできなくなります。 この記事では、[MTD アプリをセットアップ](set-up-mobile-threat-defense.md#set-up-mtd-app)して、再びアクセスできるようにする方法について説明します。    

## <a name="mtd-apps-for-ios"></a>iOS 用 MTD アプリ
iOS デバイスでは、次の MTD アプリがよく使用されます。 アプリを選択すると、App Store での一覧が表示されます。   

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139367)
* [Symantec Endpoint Protection (SEP) Mobile](https://go.microsoft.com/fwlink/?linkid=2139141)
* [Sandblast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139231)
* [Zimperium zIPS](https://go.microsoft.com/fwlink/?linkid=2139232)


## <a name="mtd-apps-for-android"></a>Android 用 MTD アプリ 
Android デバイスでは、次の MTD アプリがよく使用されます。 アプリを選択すると、Google Play ストアでの一覧が表示されます。  

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139453)
* [Symantec Endpoint Protection (SEP) Mobile](https://go.microsoft.com/fwlink/?linkid=2139454)
* [Sandblast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139455)
* [Zimperium mobile IPS (zIPS)](https://go.microsoft.com/fwlink/?linkid=2139142)  


## <a name="information-your-organization-can-see"></a>組織が参照できる情報   

組織では、個人のアプリ内のテキスト、電子メール、画像などのデータは表示できません。 MTD アプリでは、名前やバージョンなど、アプリに関する情報が組織に報告されます。 報告される実際の情報は、会社で使用している MTD ベンダーによって異なります。 組織には以下が表示されます。   

* アプリ名  
* アプリ ID:Google Play でアプリを示す一意名。  
* アプリのバージョンと短いバージョン番号:アプリの特定のリリース番号。  
* アプリのバンドルと動的なサイズ:デバイスでのアプリの使用領域。 


## <a name="set-up-mtd-app"></a>MTD アプリをセットアップする 
保護されたアプリにサインインすると、MTD アプリのインストールを求められます。 画面の手順に従ってインストールを完了し、保護されたアプリにアクセスできるようにします。 

その他のコンテキストについては、このセクションの [iOS](set-up-mobile-threat-defense.md#ios-setup) または [Android](set-up-mobile-threat-defense.md#android-setup) に関する手順を参照してください。 これらの手順は補足であり、画面に表示される指示の代わりになるものではありません。 

MTD アプリのインストールを求められても、どれをインストールすればよいかわからない場合は、IT サポート担当者に問い合わせてください。  

### <a name="device-registration"></a>デバイス登録  
デバイスの登録は、ID を確認し、学校または職場アカウントをデバイスに接続するために必要です。 デバイスが登録されていない場合は、MTD アプリをインストールする前に、その手順が画面上で自動的に案内されます。   

デバイス登録の詳細については、「[個人デバイスを組織のネットワークに登録する](/azure/active-directory/user-help/user-help-register-device-on-network)」を参照してください。  

### <a name="ios-setup"></a>iOS のセットアップ  
これらの手順は、保護されたアプリにサインインした後で表示される **[アクセスの取得]** 画面で始まります。  

1. **[アクセスの取得]** 画面の指示に従って、組織から要求された MTD アプリをインストールします。   
2. **[アクセスの取得]** 画面に戻り、 **[開く]** を選択します。  
3. MTD アプリによって、Microsoft Authenticator を開くためのアクセス許可が要求されます。 **[開く]** を選択します。 
4. サインインする職場アカウントを選択します。 
5. MTD アプリがデバイスでセキュリティ上の脅威をスキャンしている間、待ちます。 
6. 最初にアクセスしようとしていた学校または職場のアプリに戻ります。 この時点で、PIN の作成など、アプリのその他のセキュリティ要件を構成するように組織から求められる場合があります。   
7. これでアプリにアクセスできるようになります。 まだブロックされている場合:  
    * **[アクセスの取得]** 画面で、 **[再確認]** を選択します。  
    * MTD アプリにアクセスして、既存の脅威を確認します。 脅威を解決してアクセスを回復するために推奨される手順を実行します。    

### <a name="android-setup"></a>Android のセットアップ 
これらの手順は、保護されたアプリにサインインした後で表示される **[アクセスの取得]** 画面で始まります。  

1. **[アクセスの取得]** 画面の指示に従って、組織から要求された MTD アプリをインストールします。  
2. **[アクセスの取得]** 画面に戻り、 **[開く]** を選択します。  
3. MTD アプリによって、デバイスの特定の領域にアクセスするために必要なアクセス許可を要求されます。 このアプリが正常に動作するためには、連絡先へのアクセスを**許可**する必要があります。 要求されるアクセス許可は、MTD ベンダーによって異なります。  
4. サインインする職場アカウントを選択します。  
5. MTD アプリがデバイスでセキュリティ上の脅威をスキャンしている間、待ちます。  
6. 最初にアクセスしようとしていた学校または職場のアプリに戻ります。 この時点で、PIN の作成など、アプリのその他のセキュリティ要件を構成するように組織から求められる場合があります。  
7. これでアプリにアクセスできるようになります。 まだブロックされている場合:  
    * **[アクセスの取得]** 画面で、 **[再確認]** を選択します。  
    * MTD アプリにアクセスして、既存の脅威を確認します。 脅威を解決してアクセスを回復するために推奨される手順を実行します。  


## <a name="resolving-a-threat"></a>脅威の解決
脅威が検出され、組織で定義されている脅威レベルを超えた場合、組織では次のいずれかのことが行われます。  
   
* アクセスをブロックする:職場または学校アカウントにサインインしているときに、組織の保護されたアプリの使用をブロックします。  
* データをワイプする:組織の 1 つ以上の保護されたアプリから、職場または学校のデータを削除します。  

脅威を解決し、保護されたアプリへのアクセスを回復するには:  

1. デバイスで MTD アプリを開きます。     
2. アプリで脅威についての詳細を読みます。脅威を未解決のまま放置した場合のデバイスへの影響と、その解決方法について説明されています。 
3. デバイスで必要な変更を行った後、MTD アプリに戻り、新しいスキャンを開始します。 すべての脅威が解決されるまで、この手順を繰り返します。 変更が組織と同期されるまでに、数分かかることがあります。 それらの変更が同期されると、保護されたアプリに再びアクセスできるようになります。 

## <a name="get-support"></a>サポートを受ける
組織の連絡先情報を検索するには、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)に移動してください。 次のことについて問い合わせます。

* 使用している MTD アプリの確認  
* インストール  
* 失敗したインストール  
* 脅威の検出と解決  
* MTD アプリのアンインストール   
 

### <a name="share-app-logs-with-it-support"></a>アプリのログを IT サポートと共有する  
アプリのログを IT サポート担当者に送信し、失敗したインストールについてより多くのコンテキストを提供することもできます。  
* Android ユーザー:ポータル サイトから[ログをアップロードして電子メールで送信](./send-logs-to-your-it-admin-by-email-android.md)します。   

* iOS デバイス ユーザー:Microsoft Edge for iOS から[ログを取得して送信](/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs)します。  


## <a name="next-steps"></a>次のステップ  

マネージド アプリの動作方法、その入手方法、およびそれを使用していることを認識する方法についての詳細は、次の記事を参照してください。  

* [Android デバイスで管理対象アプリを使用する](use-managed-apps-on-your-device-android.md)
* [iOS デバイスで管理対象アプリを使用する](use-managed-apps-on-your-device-ios.md)  

サポートが必要な場合は、 社内サポートに問い合わせてください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。