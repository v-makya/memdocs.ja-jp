---
title: Exchange Connector に関するトラブルシューティング
titleSuffix: Microsoft Intune
description: Intune のオンプレミス Exchange Connector に関連する問題のトラブルシューティングを行います。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: a7e3c742-295b-40bb-9afa-17f243062500
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: af44b09f5e539306a24ae0e0294b3ad674f7cb74
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "79338553"
---
# <a name="troubleshoot-the-intune-exchange-connector"></a>Intune Exchange Connector に関するトラブルシューティング

この記事では、Intune Exchange Connector に関連するイシューのトラブルシューティングを行う方法について説明します。

## <a name="before-you-start"></a>開始する前に

Intune での Exchange コネクタの問題のトラブルシューティングを始める前に、しっかりした足場で作業できるように、基本的な情報をいくつか収集します。 これにより、問題の性質をより深く理解し、より迅速に解決できます。

- プロセスがインストール要件を満たしていることを確認します。 「[オンプレミスの Intune Exchange Connector を設定する](exchange-connector-install.md)」をご覧ください。
- アカウントに Exchange と Intune 両方の管理者権限があることを確認します。
- 完全で正確なエラー メッセージのテキスト、詳細、およびメッセージが表示される場所に注意します。
- 問題がいつ始まったかを確認します。 
  - コネクタを初めて設定していますか? 
  - 正常に動作していたコネクタで問題が起きるようになりましたか?
  - 動作していた場合、Intune 環境、Exchange 環境、またはコネクタのソフトウェアが実行されていたコンピューターで、どのような変更が発生しましたか?
- MDM 機関は何ですか?
- どのバージョンの Exchange を使用していますか?

### <a name="use-powershell-to-get-more-data-on-exchange-connector-issues"></a>PowerShell を使用して Exchange Connector のイシューに関するより多くのデータを取得する

- メールボックスに対するすべてのモバイル デバイスの一覧を取得するには、`Get-ActiveSyncDeviceStatistics -mailbox mbx` を使用します
- メールボックスに対する SMTP アドレスの一覧を取得するには、`Get-Mailbox -Identity user | select emailaddresses | fl` を使用します
- デバイスのアクセス状態に関する詳細情報を取得するには、`Get-CASMailbox <upn> | fl` を使用します

## <a name="review-the-connector-configuration"></a>コネクタの構成を確認する

[オンプレミスの Exchange Connector の要件](exchange-connector-install.md#intune-exchange-connector-requirements)を再確認して、環境とコネクタが正しく構成されていることを確認します。 

### <a name="general-considerations-for-the-connector"></a>コネクタに関する一般的な考慮事項

- ファイアウォールとプロキシ サーバーで、Intune Exchange コネクタがホストされているサーバーと Intune サービスの間の通信が許可されていることを確認します。

- Intune Exchange コネクタがホストされているコンピューターと Exchange クライアント アクセス サーバー (CAS) は、ドメインに参加し、同じ LAN 上に存在している必要があります。 Intune Exchange コネクタによって使用されるアカウントに、必要なアクセス許可が追加されていることを確認します。

- "*自動検出*" の設定を取得するには、通知アカウントが使用されます。 Exchange での自動検出について詳しくは、「[Exchange Server の自動検出サービス](https://docs.microsoft.com/exchange/architecture/client-access/autodiscover?view=exchserver-2016)」をご覧ください。

- Intune Exchange Connector では、通知メール メッセージと "*使用開始*" リンクを送信するために (Intune に登録する場合)、通知アカウントの資格情報を使用して EWS URL に要求が送信されます。 Android の非 Knox デバイスでは、"*使用開始*" リンクを使用して登録する必要があります。 そうしないと、これらのデバイスは条件付きアクセスによってブロックされます。

### <a name="common-issues-for-connector-configurations"></a>コネクタの構成に関する一般的な問題

- **アカウントのアクセス許可**:[Microsoft Intune Exchange Connector] ダイアログ ボックスで、[必須の Windows PowerShell Exchange コマンドレット](exchange-connector-install.md#exchange-cmdlet-requirements)を実行するための適切なアクセス許可を持つユーザー アカウントが指定されていることを確認します。
- **通知メール メッセージ**: 通知を有効にし、通知アカウントを指定します。
- **クライアント アクセス サーバーの同期**: Exchange Connector を構成するときに、Exchange Connector がホストされているサーバーに対して最低のネットワーク待機時間が可能な CAS を指定します。 特に Exchange Online Dedicated を使用している場合は、CAS と Exchange Connector 間の通信の遅延によってデバイスの検出が遅くなる可能性があります。
- **同期スケジュール**:新しく登録されたデバイスを持つユーザーは、Exchange Connector が Exchange CAS と同期するまで、アクセスに遅延が生じる可能性があります。 完全同期は 1 日に 1 回実行され、差分 (クイック) 同期は 1 日に数回実行されます。 遅延を最小限に抑えるために、[クイック同期または完全同期を手動で適用](exchange-connector-install.md#manually-force-a-quick-sync-or-full-sync)することができます。

## <a name="next-steps"></a>次のステップ
次の記事は、一般的な問題と特定のエラーを解決するのに役立ちます。

- [Intune Exchange コネクタでの一般的な問題を解決する](troubleshoot-exchange-connector-common-problems.md)。
- [Intune Exchange コネクタでのよくあるエラーを解決する](troubleshoot-exchange-connector-common-errors.md)。

サポートまたは Intune コミュニティから支援を受けます。

- Intune コンソールを使用して問題のトラブルシューティングを行う方法、または Microsoft のサポート ケースを開く方法については、[サポートの利用](../fundamentals/get-support.md)に関するページを参照してください。 
- [Microsoft Intune フォーラム](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod)に問題を投稿してください。  
