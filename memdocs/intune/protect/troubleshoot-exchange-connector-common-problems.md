---
title: Intune Exchange コネクタに関する一般的な問題のトラブルシューティング
titleSuffix: Microsoft Intune
description: オンプレミスの Microsoft Intune Exchange コネクタに関する一般的な問題をトラブルシューティングして解決します。
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55f51f94cf26aa2486ef390d5fbb668eaf013e10
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "79350630"
---
# <a name="resolve-common-problems-with-the-intune-exchange-connector"></a>Intune Exchange コネクタに関する一般的な問題を解決する
 
この記事は、Intune 管理者が Intune Exchange コネクタの操作に関する一般的な問題を解決するのに役立ちます。

トラブルシューティングを始める前に、コネクタに関する基本的な情報について、[Intune のオンプレミス Exchange Connector のトラブルシューティング](troubleshoot-exchange-connector.md)に関するページを確認してください。 コネクタの構成の一般的な問題についても確認してください。

## <a name="an-exchange-activesync-device-isnt-discovered-from-exchange"></a>Exchange ActiveSync デバイスが Exchange から検出されない

Exchange ActiveSync デバイスが Exchange から検出されないときは、[Exchange Connector のアクティビティを監視](exchange-connector-install.md#on-premises-intune-exchange-connector-high-availability-support)して、Exchange Connector が Exchange Server と同期しているかどうかを調べます。 デバイスが参加してから同期が行われていない場合は、同期ログを収集し、サポート リクエストに添付してください。 デバイスが参加してから完全同期またはクイック同期が正常に完了している場合は、次の問題を確認します。

- ユーザーに Intune のライセンスがあることを確認します。 ない場合、Exchange Connector ではデバイスが検出されません。

- ユーザーのプライマリ SMTP アドレスが Azure Active Directory (Azure AD) のユーザー プリンシパル名 (UPN) と異なる場合、Exchange Connector は、そのユーザーのデバイスを検出しません。 この問題を解決するのには、プライマリ SMTP アドレスを修正します。

- 環境内に Exchange 2010 メールボックス サーバーと Exchange 2013 メールボックス サーバーが両方ともある場合は、Exchange Connector を Exchange 2013 クライアント アクセス サーバー (CAS) にポイントすることをお勧めします。 Exchange Connector が Exchange 2010 CAS と通信するように設定されていると、Exchange Connector は Exchange 2013 のユーザー デバイスを検出しません。

- Exchange Online Dedicated 環境の場合、初期セットアップ中に Exchange Connector を専用環境内の (Exchange 2010 CAS ではなく) Exchange 2013 CAS にポイントする必要があります。 Connector は、PowerShell コマンドレットを実行するときに、Exchange 2013 CAS のみと通信します。

## <a name="problems-with-the-notification-email-message"></a>通知メール メッセージに関する問題

Android Knox が実行されていないデバイス上のオンプレミス メールボックスに対する条件付きアクセスをサポートするには、Intune Exchange コネクタによって送信される "今すぐ開始" メール メッセージから Intune の登録が開始することを確認します。 メッセージから登録を開始すると、デバイスはすべてのプラットフォーム (Exchange、Azure AD、Intune) で一意の Activescid を確実に受信できるようになります。

次の理由により、ユーザーが通知メール メッセージを受信できない可能性があります。

- 通知アカウントが正しく設定されていません。
- 通知アカウントの自動検出が失敗しました。
- メール メッセージを送信するための Exchange Web サービス (EWS) 要求が失敗しました。

メール通知の問題のトラブルシューティングを行うには、次のセクションを確認してください。

### <a name="check-the-notification-account-that-retrieves-autodiscover-settings"></a>自動検出の設定を取得する通知アカウントを確認する

1. 自動検出サービスと EWS が Exchange クライアント アクセス サービスで構成されていることを確認します。 詳しくは、「[クライアント アクセス サービス](https://docs.microsoft.com/Exchange/architecture/client-access/client-access)」および「[Exchange Server の自動検出サービス](https://docs.microsoft.com/Exchange/architecture/client-access/autodiscover?view=exchserver-2019)」をご覧ください。

2. 通知アカウントが次の要件を満たしていることを確認します。

   - アカウントに、Exchange On-Premises サーバーによってホストされているアクティブなメールボックスがあります。

   - アカウントの UPN が SMTP アドレスと一致します。

3. 自動検出には、Exchange クライアント アクセス サーバーを指す **Autodiscover.SMTPdomain.com** (たとえば、Autodiscover.contoso.com) の DNS レコードを持つ DNS サーバーが必要です。 レコードを確認するには、*Autodiscover.SMTPdomain.com* の代わりに FQDN を指定して、次の手順のようにします。

   1. コマンド プロンプトで、「*NSLOOKUP*」と入力します。

   2. 「*Autodiscover.SMTPdomain.com*」と入力します。 出力は次の図のようになります。![Nslookup 結果](./media/troubleshoot-exchange-connector-common-problems/nslookup-results.png
      )

   また、 https://testconnectivity.microsoft.com でインターネットから自動検出サービスをテストすることもできます。 または、Microsoft 接続アナライザー ツールを使用して、ローカル ドメインからテストします。 詳細については、「[Microsoft 接続アナライザー ツール](https://docs.microsoft.com/previous-versions/office/exchange-remote-connectivity/jj851141(v=exchg.80))」を参照してください。


### <a name="check-autodiscovery"></a>自動検出を確認する

自動検出が失敗する場合は、次の手順を試してください。

1. [有効な自動検出 DNS レコードを構成します](https://docs.microsoft.com/previous-versions/exchange-server/exchange-150/mt473798(v=exchg.150))。

2. Intune Exchange Connector 構成ファイルに、EWS の URL をハードコーディングします。

   1. EWS の URL を調べます。 Exchange の既定の EWS URL は `https://<mailServerFQDN>/ews/exchange.asmx` ですが、URL が異なる場合があります。 お使いの環境の正しい URL を確認するには、Exchange 管理者に問い合わせてください。

   2. *OnPremisesExchangeConnectorServiceConfiguration.xml*ファイルを編集します。 既定では、ファイルは、Exchange コネクタが実行されているコンピューターの *%ProgramData%\Microsoft\Windows Intune Exchange Connector* にあります。 ファイルをテキストエディターで開き、環境の EWS URL を反映するように次の行を変更します。 `<ExchangeWebServiceURL>https://<YourExchangeHOST>/EWS/Exchange.asmx</ExchangeWebServiceURL>`

3. ファイルを保存し、コンピューターを再起動するか、Microsoft Intune Exchange コネクタ サービスを再起動します。

>[!NOTE]
> この構成では、Intune Exchange コネクタは自動検出の使用を停止し、代わりに EWS の URL に直接接続します。

## <a name="next-steps"></a>次のステップ

特定のエラーに関するヘルプについては、「[Intune Exchange コネクタでのよくあるエラーを解決する](troubleshoot-exchange-connector-common-errors.md)」を試してください。

サポートを受けるか、Intune コミュニティから支援を受けるには:

- Intune コンソールを使用して問題のトラブルシューティングを行う方法、または Microsoft のサポート ケースを開く方法については、[サポートの利用](../fundamentals/get-support.md)に関するページを参照してください。
- [Microsoft Intune フォーラム](https://social.technet.microsoft.com/Forums/home?forum=microsoftintuneprod)に問題を投稿してください。