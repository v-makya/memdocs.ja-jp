---
title: Windows 自動操縦顧客の同意
description: クラウドサービスプロバイダー (CSP) パートナーまたは OEM が、お客様の代理として Windows 自動操縦デバイスを登録するために顧客の承認を受ける方法について説明します。
keywords: MDM, セットアップ, Windows, Windows 10, OOBE, 管理, 展開, Autopilot, ZTD, ゼロタッチ, パートナー, MSFB, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: e6e85b50fb96e5b6049cdadd5a2ae265896c2e93
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757122"
---
# <a name="windows-autopilot-customer-consent"></a>Windows 自動操縦顧客の同意

**適用対象: Windows 10**

この記事では、クラウドサービスプロバイダー (CSP) パートナー (直接請求書、間接プロバイダー、または間接リセラー) または OEM が、お客様の代理として Windows 自動操縦デバイスを登録するための承認を受ける方法について説明します。

## <a name="csp-authorization"></a>CSP 認証

CSP パートナーは、次の制限事項に従って、お客様の代わりに Windows 自動操縦デバイスを登録するための顧客の承認を得ることができます。

<table>
<tr><td>直接 CSP<td>顧客からデバイスを登録するための直接承認を取得します。
<tr><td>間接 CSP プロバイダー<td>CSP リセラーパートナーと顧客との関係を通じてデバイスを登録するための暗黙的なアクセス許可を取得します。  間接 CSP プロバイダーは、Microsoft パートナーセンターからデバイスを登録します。
<tr><td>間接 CSP リセラー<td>顧客からデバイスを登録するための直接承認を取得します。  同時に、間接 CSP プロバイダーパートナーも承認を取得します。これは、間接プロバイダーまたは間接リセラーが顧客にデバイスを登録できることを意味します。  ただし、間接 CSP リセラーは、MPC UI (CSV ファイルを手動でアップロードする) を使用してデバイスを登録する必要があります。一方、間接 CSP プロバイダーには、MPC Api を使用してデバイスを登録するオプションがあります。
</table>

### <a name="steps"></a>手順

CSP が顧客の代わりに Windows 自動操縦デバイスを登録するには、まず、次のプロセスを使用して、その CSP パートナーのアクセス許可を付与する必要があります。

1. CSP は、お客様に代わってデバイスを登録/管理するための承認/同意を求めるリンクを顧客に送信します。  そのためには、次の操作を実行します。
    - Microsoft パートナーセンターに CSP ログを記録する
    - 上部のメニューの [**ダッシュボード**] をクリックします。
    - サイドメニューの [ **Customer** ] をクリックします。
    - [**リセラーの関係を要求する**] ![ リンクをクリックします。](images/csp1.png)
    - 代理管理者権限を委任するかどうかを示すチェックボックスをオンにします。委任された ![ 権限](images/csp2.png)
    - 注: パートナーによっては、この同意を要求するときに、委任された管理者アクセス許可 (DAP) を要求する場合があります。  可能であれば、新しいバージョンの DAP を使用するように依頼する必要があります (このドキュメントを参照してください)。 それ以外の場合は、Microsoft 管理センターまたは Office 365 管理ポータルから、DAP の状態を簡単に削除できます。https://docs.microsoft.com/partner-center/customers_revoke_admin_privileges
    - 上記のテンプレートを電子メールでお客様に送信します。
2. Microsoft 管理センターのグローバル管理者特権を持つユーザーは、CSP から受信した電子メールの本文内のリンクをクリックし、次の Microsoft 365 管理センターページに直接移動します。

    ![グローバル管理者](images/csp3a.png)

    上の画像は、ユーザーが代理管理者権限 (DAP) を要求した場合に表示されるものです。 ページには、要求されている管理者ロールが表示されます。  顧客が代理管理者権限を要求しなかった場合は、次のページが表示されます。

    ![グローバル管理者](images/csp3b.png)   

    > [!NOTE]
    > グローバル管理者特権を持たないユーザーがリンクをクリックすると、次のようなメッセージが表示されます。

    ![グローバル管理者ではありません](images/csp4.png)

3. **[はい]** チェックボックスをオンにし、[**同意**する] ボタンをクリックします。 承認は瞬時に行われます。
4. CSP は、この同意/承認要求が完了したことを認識します。これは、顧客が CSP の MPC アカウントに**顧客**リストに表示されるためです。たとえば、次のようになります。

![顧客](images/csp5.png)

## <a name="oem-authorization"></a>OEM 承認

各 OEM には、それぞれの顧客に提供するための一意のリンクがあります。 OEM は、を通じて Microsoft から要求でき msoemops@microsoft.com ます。

1. 顧客への OEM メールリンク。
2. Microsoft Store for Business (MSfB) のグローバル管理者特権を持つユーザーは、OEM から受け取ったリンクをクリックすると、次の MSfB ページに直接移動します。

    ![グローバル管理者](images/csp6.png)

    > [!NOTE]
    > グローバル管理者特権を持たないユーザーがリンクをクリックすると、次のようなメッセージが表示されます。

    ![グローバル管理者ではありません](images/csp7.png)
3. **[はい]** チェックボックスをオンにした後、[**同意**する] ボタンを選択すると、完了したことになります。  承認は瞬時に行われます。

    > [!NOTE]
    > このプロセスが完了したら、管理者が OEM を削除することはできません。 OEM を削除したり、アクセス許可を取り消したりするには、に要求を送信します。msoemops@microsoft.com

4. OEM は、デバイス送信データの検証 API を使用して、同意が完了したことを確認できます。  この API については、最新バージョンの API に関するホワイトペーパー「p」で説明されています。 14ff [https://devicepartner.microsoft.com/assets/detail/windows-autopilot-integration-with-oem-api-design-whitepaper-docx](https://devicepartner.microsoft.com/assets/detail/windows-autopilot-integration-with-oem-api-design-whitepaper-docx) 。 **注**: このリンクには、Microsoft デバイスパートナーだけがアクセスできます。 このホワイトペーパーで説明されているように、OEM パートナーは、デバイスを登録する前に顧客の同意を受け取ったことを確認するために API チェックを実行することをお勧めします。これにより、登録プロセスでのエラーを回避できます。

    > [!NOTE]
    > OEM 承認登録プロセス中に、OEM には代理管理者のアクセス許可は付与されません。

## <a name="summary"></a>まとめ

プロセスのこの段階では、Microsoft が不要になりました。同意交換は、OEM と顧客の間で直接行われます。  また、ボタンがクリックされるとすぐに、すべての処理が即座に行われます。
