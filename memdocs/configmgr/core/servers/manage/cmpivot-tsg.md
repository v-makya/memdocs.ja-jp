---
title: CMPivot のトラブルシューティング
titleSuffix: Configuration Manager
description: Configuration Manager で CMPivot のトラブルシューティングを行う方法について説明します。
ms.date: 10/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 36385bea-f05e-4300-947f-cb3927b3bac5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6bddf46df63eac70a536faaee04a2ac7243e534a
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128275"
---
# <a name="troubleshoot-cmpivot"></a>CMPivot のトラブルシューティング

CMPivot は、お使いの環境内でデバイスのリアルタイム状態へのアクセスを提供するツールです。 CMPivot により、対象となるコレクション内の現在接続されているすべてのデバイス上でクエリが実行され、結果が返されます。

場合によっては、CMPivot のトラブルシューティングが必要になることがあります。 たとえば、クライアントから CMPivot への状態メッセージが破損した場合、サイト サーバーではそのメッセージを処理できません。 この記事では、CMPivot での情報のフローを理解するのに役立ちます。

## <a name="troubleshoot-cmpivot-in-version-1902-and-later"></a><a name="bkmk_CMPivot-1902"></a> バージョン 1902 以降の CMPivot のトラブルシューティング

Configuration Manager バージョン 1902 以降では、階層内の中央管理サイト (CAS) から CMPivot を実行できます。 まだ、プライマリ サイトでクライアントへの通信が処理されます。

CAS から CMPivot を実行すると、プライマリ サイトとの通信のために高速メッセージ サブスクリプション チャネルが使われます。 CMPivot では、サイト間で標準の SQL レプリケーションは使われません。 お使いの SQL Server インスタンスまたは SQL プロバイダーがリモートである場合、または SQL Server Always On を使用する場合は、CMPivot の "ダブル ホップ シナリオ" が発生します。 "ダブル ホップ シナリオ" に対して制約付き委任を定義する方法の詳細については、「[バージョン 1902 以降の CMPivot](cmpivot-changes.md#bkmk_cmpivot1902)」をご覧ください。

>[!IMPORTANT]
> CMPivot のトラブルシューティングを行う場合は、管理ポイント (MP) およびサイト サーバーの SMS_MESSAGE_PROCESSING_ENGINE で詳細ログを有効にして、より詳しい情報を取得します。 また、クライアントの出力が 80 KB を超える場合は、MP とサイト サーバーの SMS_STATE_SYSTEM コンポーネントの詳細ログも有効にしてください。 詳細ログを有効にする方法について詳しくは、「[サイト サーバーのログ オプション](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site)」をご覧ください。

### <a name="get-information-from-the-site-server"></a>サイト サーバーから情報を取得する

既定では、サイト サーバーのログ ファイルは `C:\Program Files\Microsoft Configuration Manager\logs` にあります。 既定以外のインストール ディレクトリを指定した場合や、SMS プロバイダーのようなオフロード項目を別のサーバーに指定した場合は、この場所が異なる場合があります。 CAS から CMPivot を実行する場合、ログはプライマリ サイト サーバー上にあります。

`smsprov.log` で次の行を探します。

- Configuration Manager バージョン 1906:
  <pre><code lang="Log">Auditing: User &ltusername> initiated client operation 145 to collection &ltCollectionId>. </code></pre>

- Configuration Manager バージョン 1902:
  <pre><code lang="Log">Type parameter is 135.
  Auditing: User &ltusername> ran script 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 with hash dc6c2ad05f1bfda88d880c54121c8b5cea6a394282425a88dd4d8714547dc4a2 on collection &ltCollectionId>. </code></pre>

 `7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14` は、CMPivot のスクリプト GUID です。 この GUID は [CMPivot 監査ステータス メッセージ](cmpivot-changes.md#cmpivot-audit-status-messages)でも確認できます。

次に、CMPivot ウィンドウで ID を探します。 この ID は `ClientOperationID` です。

![ClientOperationID が強調表示されている CMPivot ウィンドウ](media/cmpivot-client-operationid-1902.png)

ClientAction テーブルから `TaskID` を検索します。 `TaskID` は ClientAction テーブルの `UniqueID` に対応しています。

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

`BgbServer.log` で、SQL から収集した `TaskID` を探し、`PushID` をメモします。 `TaskID` には `TaskGUID` というラベルが付けられます。 例:

<pre><code lang="Log">Starting to send push task (<b>PushID: 9</b> TaskID: 12 <b>TaskGUID: 9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b> TaskType: 15 TaskParam: PFNjcmlwdENvbnRlbnQgU2NyaXB0R3VpZD0nN0RDNkI2RjEtRTdGNi00M0MxL (truncated log entry)
Finished sending push task (<b>PushID: 9</b> TaskID: 12) to 2 clients
</code></pre>

### <a name="client-logs"></a>クライアント ログ

サイト サーバーからの情報を入手したら、クライアント ログを確認します。 既定では、クライアント ログは `C:\Windows\CCM\Logs` にあります。

`CcmNotificationAgent.log` で、次の行のようなログ エントリを探します。  

<pre><code lang="Log">Receive task from server with <b>pushid=9</b>, taskid=12, <b>taskguid=9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b>, tasktype=15 and taskParam=PFNjcmlwdEhhc2ggU2NyaXB0SGF (truncated log entry)
Send Task response message &ltBgbResponseMessage TimeStamp="2019-09-13T17:29:09Z"><b>&ltPushID>5</b>&lt/PushID>&ltTaskID>4&lt/TaskID>&ltReturnCode>1&lt/ReturnCode>&lt/BgbResponseMessage> successfuly.
 </code></pre>

`Scripts.log` の `TaskID` を確認します。 次の例では、`Task ID` `{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}` が表示されています。

<pre><code lang="Log">Sending script state message (fast): <b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Result are sent for ScriptGuid: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 and <b>TaskID: {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
</code></pre>

> [!NOTE]
> `Scripts.log` に "(fast)" が表示されない場合は、データが 80 KB を超えている可能性があります。 その場合、情報は状態メッセージとしてサイト サーバーに送信されます。 クライアントの `StateMessage.log` とサイト サーバーの `Statesys.log` を使用してください。

### <a name="review-messages-on-the-site-server"></a>サイト サーバーでメッセージを確認する

管理ポイントで[詳細ログ](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client)が有効になっている場合は、受信クライアント メッセージがどのように処理されるかを確認できます。 `MP_RelayMsgMgr.log` で、`TaskID` を探します。

`MP_RelayMsgMgr.log` の例では、クライアントの ID `(GUID:83F67728-2E6D-4E4F-8075-ED035C31B783)` と `Task ID {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}` を確認できます。 メッセージ ID は、クライアントの応答に割り当てられてからメッセージ処理エンジンに送信されます。

<pre><code lang="Log">MessageKey: GUID:83F67728-2E6D-4E4F-8075-ED035C31B783<b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Create message succeeded for <b>message id 22f00adf-181e-4bad-b35e-d18912f39f89</b>
Add message payload succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
Put message succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
CRelayMsgMgrHandler::HandleMessage(): ExecuteTask() succeeded
</code></pre>

`SMS_MESSAGE_PROCESSING_ENGINE.log` で[詳細ログ](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions)が有効になっている場合、クライアントの結果は処理されます。 `MP_RelayMsgMgr.log` で見つかったメッセージ ID を使用します。 ログ エントリの処理は次の例のようになります。

<pre><code lang="Log">Processing 2 messages with type Instant and IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]...
Processed 2 messages with type Instant. Failed to process 0 messages. All message IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]
</code></pre>

> [!TIP]
> 処理中に例外が発生した場合は、次の SQL クエリを実行して Exception 列を確認することで、その例外を確認できます。 処理された後のメッセージは、`MPE_RequestMessages_Instant` テーブルには含まれなくなります。
>
> ```SQL
> select * from MPE_RequestMessages_Instant where MessageID=<ID from SMS_MESSAGE_PROCESSING_ENGINE.log>
> ```

`BgbServer.log` で `PushID` を検索して、報告されたクライアントまたは失敗したクライアントの数を確認します。

<pre><code lang="Log">Generated BGB task status report c:\ConfigMgr\inboxes\bgb.box\Bgb5c1db.BTS at 09/16/2019 16:46:39. (<b>PushID: 9</b> ReportedClients: 2 FailedClients: 0)
</code></pre>

`TaskID` を使って、SQL から CMPivot に対する監視ビューを確認します。

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}'
```

[ ![バージョン 1902 でのトラブルシューティング用 CMPivot SQL クエリ](media/cmpivot-sql-queries-1902.png)](media/cmpivot-sql-queries-1902.png#lightbox)

## <a name="troubleshoot-cmpivot-in-1810-and-earlier"></a><a name="bkmk_CMPivot-1810"></a> 1810 以前の CMPivot のトラブルシューティング

Configuration Manager バージョン 1810 以前では、サイト サーバーによってクライアントとの通信が処理されます。

### <a name="get-information-from-the-site-server"></a>サイト サーバーから情報を取得する

既定では、サイト サーバーのログ ファイルは `C:\Program Files\Microsoft Configuration Manager\logs` にあります。 既定以外のインストール ディレクトリを指定した場合や、SMS プロバイダーのようなオフロード項目を別のサーバーに指定した場合は、この場所が異なる場合があります。

`smsprov.log` で次の行を探します。

<pre><code lang="Log">Auditing: User <username> initiated client operation 135 to collection &ltCollectionId>.
</code></pre>

CMPivot ウィンドウでこの ID を見つけます。 この ID は `ClientOperationID` です。

![ClientOperationID が強調表示されている CMPivot ウィンドウ](media/cmpivot-clientoperationid.png)

ClientAction テーブルから `TaskID` を検索します。 `TaskID` は ClientAction テーブルの `UniqueID` に対応しています。

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

`BgbServer.log` で、SQL から収集した `TaskID` を探します。 これには `TaskGUID` というラベルが付いています。 例:

<pre><code lang="Log">Starting to send push task (PushID: 260 TaskID: 258 TaskGUID: <b>F8C7C37F-B42B-4C0A-B050-2BB44DF1098A</b> TaskType: 15
TaskParam: PFNjcmlwdEhhc2ggU2NyaXB0SGF...truncated...to 5 clients with throttling (strategy: 1 param: 42)
Finished sending push task (PushID: 260 TaskID: 258) to 5 clients
</code></pre>

### <a name="client-logs"></a>クライアント ログ

サイト サーバーからの情報を入手したら、クライアント ログを確認します。 既定では、クライアント ログは `C:\Windows\CCM\Logs` にあります。

`CcmNotificationAgent.log` で、次のエントリのようなログを探します。  

<pre><code lang="Log"><b>Error! Bookmark not defined.</b>+PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT
g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp (truncated log entry)
</code></pre>

`Scripts.log` で `TaskID` を探します。 次の例では、`Task ID {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}` が表示されています。

<pre><code lang="Log">Sending script state message: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14
State message: Task Id <b>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</b>
</code></pre>

`StateMessage.log` を調べます。 次の例では、メッセージの下部近くの `<Param>` の横に `TaskID` があることがわかります。

``` XML
StateMessage body: <?xml version="1.0" encoding="UTF-16"?>
<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>

Successfully forwarded State Messages to the MP StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

### <a name="review-messages-on-the-site-server"></a>サイト サーバーでメッセージを確認する

`statesys.log` を開いて、メッセージが受信され、処理されたかどうかを確認します。 次の例では、メッセージの下部近くの `<Param>` の横に `TaskID` が表示されています。 これらのログ エントリを表示するには、SMS_STATE_SYSTEM コンポーネントの[詳細ログ](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions)を有効にします。

``` XML
CMessageProcessor - the cmdline to DB exec dbo.spProcessStateReport N'?<?xml version="1.0" encoding="UTF-
16"?>~~<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>~~'
```

メッセージが処理されていない場合は、状態メッセージの受信トレイを確認します。 既定の受信トレイの場所は `C:\Program Files\Microsoft Configuration Manager\inboxes\auth\statesys.box\` です。 次の場所にあるファイルを探します。

- 受信
- 破損
- プロセス

`TaskID` を使って、SQL から CMPivot に対する監視ビューを確認します。

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}'
```

>[!NOTE]
>バージョン 1810 以降を使用しているクライアントでは、出力が 80 KB を超える場合を除き、状態メッセージは使用されません。 そのような場合に CMPivot のトラブルシューティングを行うときは、MP とサイト サーバーの SMS_MESSAGE_PROCESSING_ENGINE の詳細ログを有効にすれば、さらに詳しい情報を得ることができます。 詳細ログを有効にする方法について詳しくは、「[サイト サーバーのログ オプション](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site)」をご覧ください。
>
> トラブルシューティングを行うには、次のログを参照してください。
>
> - `MP_Relay.log`
> - `SMS_MESSAGE_PROCESSING_ENGINE.log`

## <a name="next-steps"></a>次のステップ

- [CMPivot の使用](cmpivot.md)
- [PowerShell スクリプトの作成と実行](../../../apps/deploy-use/create-deploy-scripts.md)
