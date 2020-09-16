---
title: Windows 自動操縦顧客の同意
description: クラウドサービスプロバイダー (CSP) パートナーまたは OEM が、お客様の代理として Windows 自動操縦デバイスを登録するために顧客の承認を受ける方法について説明します。
keywords: MDM, セットアップ, Windows, Windows 10, OOBE, 管理, 展開, Autopilot, ZTD, ゼロタッチ, パートナー, MSFB, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
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
ms.openlocfilehash: db2dc86b4f7cb514f3ceca4d37bf387db31c13f4
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568553"
---
# <a name="windows-autopilot-customer-consent"></a>Windows 自動操縦顧客の同意

**適用先:Windows 10**

この記事では、クラウドサービスプロバイダー (CSP) パートナー (直接請求書、間接プロバイダー、または間接リセラー) または OEM が、お客様の代理として Windows 自動操縦デバイスを登録するための承認を受ける方法について説明します。

## <a name="csp-authorization"></a>CSP 認証

CSP パートナーは、次の制限事項に従って、お客様の代わりに Windows 自動操縦デバイスを登録するための顧客の承認を得ることができます。

<table>
<tr><td>直接 CSP<td>顧客からデバイスを登録するための直接承認を取得します。
<tr><td>間接 CSP プロバイダー<td>CSP リセラーパートナーと顧客との関係を通じてデバイスを登録するための暗黙的なアクセス許可を取得します。 間接 CSP プロバイダーは、Microsoft パートナーセンターからデバイスを登録します。
<tr><td>間接 CSP リセラー<td>顧客からデバイスを登録するための直接承認を取得します。 同時に、間接 CSP プロバイダーパートナーも承認を取得します。これは、間接プロバイダーまたは間接リセラーが顧客にデバイスを登録できることを意味します。 ただし、間接 CSP リセラーは、MPC UI (CSV ファイルを手動でアップロードする) を使用してデバイスを登録する必要があります。 間接 CSP プロバイダーは、MPC Api を使用してデバイスを登録できます。
</table>

### <a name="steps"></a>手順

CSP が顧客に対して Windows 自動操縦デバイスを登録するには、まず、次のプロセスを使用して、その CSP パートナーのアクセス許可を付与する必要があります。

1. CSP は、お客様に代わってデバイスを登録/管理するための承認/同意を求めるリンクを顧客に送信します。 そのためには次を行います。
    1. CSP は Microsoft パートナーセンターにログインします。
    2. 上部のメニューで [ **ダッシュボード** ] をクリックします。
    3. サイドメニューの [ **Customer** ] をクリックします。
    4. [ **再販業者関係の要求** ] リンクをクリックします。

        ![再販業者の関係を要求する](images/csp1.png)
 
    5. 代理管理者権限を委任するかどうかを示すチェックボックスをオンにします。
 
        ![委任された権限](images/csp2.png)

        > [!NOTE]
        > パートナーによっては、この同意を要求するときに、委任された管理者アクセス許可 (DAP) を要求する場合があります。 可能であれば、新しいバージョンの DAP を使用することをお勧めします (このドキュメントを参照)。 表示されていない場合は、Microsoft 管理センターまたは Microsoft 365 管理ポータルから簡単に DAP の状態を削除できます。 https://docs.microsoft.com/partner-center/customers_revoke_admin_privileges
    6. 上記のテンプレートを電子メールでお客様に送信します。

2. Microsoft 管理センターのグローバル管理者特権を持つお客様は、電子メールのリンクをクリックします。 リンクでは、次の Microsoft 365 管理センターページに移動します。

    ![同意するスクリーンショットと、パートナーページを承認するページ-代理管理者権限](images/csp3a.png)

    上の画像は、ユーザーが代理管理者権限 (DAP) を要求した場合に表示されるものです。 ページには、要求されている管理者ロールが表示されます。 お客様が代理管理者権限を要求しなかった場合は、次のページが表示されます。

    ![同意契約と承認パートナーページのスクリーンショット](images/csp3b.png) 

    > [!NOTE]
    > グローバル管理者特権を持たないユーザーがリンクをクリックすると、次のようなメッセージが表示されます。

    ![スクリーンショットのアクセス許可ページ](images/csp4.png)

3. **[はい]** チェックボックスをオンにし、[**同意**する] ボタンをクリックします。 承認は瞬時に行われます。
4. 承認要求が完了したことを確認するために、CSP は、MPC アカウントの **顧客** 一覧を確認できます。 顧客がリストに含まれている場合、要求は完了しています。 次に例を示します。

    ![顧客](images/csp5.png)

## <a name="oem-authorization"></a>OEM 承認

各 OEM には、それぞれの顧客に提供するための一意のリンクがあります。 OEM は、を通じて Microsoft から要求でき msoemops@microsoft.com ます。

1. 顧客への OEM メールリンク。
2. Microsoft Store for Business (MSfB) のグローバル管理者特権を持つお客様は、電子メールのリンクをクリックして、次の MSfB ページに直接移動します。

    ![スクリーンショットの同意パートナーへの招待のページ](images/csp6.png)

    > [!NOTE]
    > グローバル管理者特権を持たないユーザーがリンクをクリックすると、次のようなメッセージが表示されます。

    ![スクリーンショットの MSfB アクセス許可が必要ページ](images/csp7.png)

3. **[はい]** チェックボックスをオンにした後、[**同意**する] ボタンを選択すると、完了したことになります。 承認は瞬時に行われます。

    > [!NOTE]
    > このプロセスが完了したら、管理者が OEM を削除することはできません。 OEM を削除したり、アクセス許可を取り消したりするには、に要求を送信します。 msoemops@microsoft.com

4. OEM は、デバイス送信データの検証 API を使用して、同意が完了したことを確認できます。 この API については、最新バージョンの API に関するホワイトペーパー「p」で説明されています。 14ff [https://devicepartner.microsoft.com/assets/detail/windows-autopilot-integration-with-oem-api-design-whitepaper-docx](https://devicepartner.microsoft.com/assets/detail/windows-autopilot-integration-with-oem-api-design-whitepaper-docx) 。 **注**: このリンクには、Microsoft デバイスパートナーだけがアクセスできます。 この記事で説明されているように、OEM パートナーは、デバイスを登録する前に顧客の同意を受け取ったことを確認するために、API チェックを実行することをお勧めします。 このチェックは、登録プロセスのエラーを回避するのに役立ちます。

    > [!NOTE]
    > OEM 承認登録プロセス中に、OEM には代理管理者のアクセス許可は付与されません。

## <a name="summary"></a>まとめ

プロセスのこの段階では、Microsoft が不要になりました。同意交換は、OEM と顧客の間で直接行われます。 また、ボタンがクリックされるとすぐに、すべての処理が即座に行われます。
