---
title: アプリケーション ダウンロードのテクニカル リファレンス
titleSuffix: Configuration Manager
description: Configuration Manager でのアプリケーション ダウンロードのトラブルシューティングに関するテクニカル リファレンスです。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 41c29a07-9bf6-4ec4-b3f2-1c05e001eff7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: effa8115a5023a8e0611f6bc4245a101b3a47e38
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688860"
---
# <a name="application-download-in-configuration-manager"></a>Configuration Manager でのアプリケーション ダウンロード

*適用対象:Configuration Manager (Current Branch)*

続行する前に、[アプリケーション展開クライアント コンポーネント](client-components-technical-reference.md)を参照して、DCM と CI エージェントのジョブの処理を理解してください。

## <a name="download-initiation"></a>ダウンロードの開始

アプリケーションのコンテンツのダウンロードは、**StateDownloadingContents** フェーズ中に、クライアントの CI エージェント コンポーネントによって開始されます。 このプロセスは、アプリケーションがデバイス コレクションに展開されるか、ユーザー コレクションに展開されるかに関係なく同じです。

- **使用可能**な展開の場合、ユーザーがソフトウェア センターからアプリケーションのインストールを開始すると、アプリケーションのコンテンツがダウンロードされます。
- **必須**の展開では、割り当てがアクティブになり、評価後にアプリケーションが適用可能であることが検出されたときにアプリケーションのコンテンツがダウンロードされます。 割り当てがアクティブになるタイミングを理解するには、[デバイス コレクションへのアプリケーションの展開についての記事](device-deployment-technical-reference.md)または[ユーザー コレクションへのアプリケーションの展開に関する記事](user-deployment-technical-reference.md)を参照してください。

CI エージェントがコンテンツのダウンロードを開始すると、CI タスク マネージャー コンポーネントによって処理されるタスクが作成されます。 次に、CI タスク マネージャーによってコンテンツのダウンロードが開始されます。 このアクティビティは、展開の種類の一意な ID を使用して **CITaskMgr.log** で追跡できます。

<pre><code class="lang-text"><b>Initiating task ContentDownload</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {53EA65C2-D596-4215-83E4-F7007B78E18C}
</code></pre>

## <a name="distribution-point-location"></a>配布ポイントの場所

すべてのダウンロード タスクは、クライアント キャッシュの管理を担当するコンテンツ アクセス コンポーネントによって処理されます。 ダウンロード タスクが作成されると、コンテンツ アクセス コンポーネントは、コンテンツがクライアント キャッシュで既に使用可能かどうかを確認します。 コンテンツが利用できない場合は、コンテンツを取得できる配布ポイントの一覧を取得する場所の要求を作成します。 このアクティビティは、コンテンツの一意な ID を使用して、クライアントの **CAS.log** と **LocationServices.log** で追跡できます。

```text
Requesting locations synchronously for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 with priority Foreground
ContentLocationRequest : <Request XML Body>
Reply Message Body : <Reply XML Body>
```

> [!IMPORTANT]
> ロケーション サービス コンポーネントは場所の要求を処理しますが、管理ポイントに直接場所を要求することはしません。 通常、管理ポイントへのすべての要求は CCM メッセージング コンポーネントを経由し、そこで **CcmMessaging.log** に記録されます。

ロケーション応答 XML には、クライアントの境界グループに基づく配布ポイントの一覧が含まれています。 この一覧は、[コンテンツ ソースの優先度](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#content-source-priority)に従って、クライアントの WMI で解析および永続化されます。 このアクティビティは、コンテンツの一意な ID を使用して `Persisted location` を検索すると、**ContentTransferManager.log** に表示されます。 

ロケーション応答 XML に配布ポイントが含まれていない場合、**ContentTransferManager.log** に `Received empty location update` が表示され、アプリケーションのダウンロード中にクライアントが 0% で停止する可能性があります。 この応答は、通常、境界グループの構成の問題が原因で発生します。 詳細については、「[ダウンロードの失敗](../deploy-use/troubleshoot-application-deployment.md#download-failures)」を参照してください。

## <a name="content-download"></a>コンテンツのダウンロード

配布ポイントの場所を取得すると、コンテンツ アクセス コンポーネントがコンテンツ転送ジョブを作成します。 このアクティビティは、コンテンツの一意な ID を使用して **CAS.log** で追跡できます。

<pre><code class="lang-text">Submitted CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> to download Content <b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b> under context System
</code></pre>

コンテンツ転送マネージャーは、コンテンツをダウンロードするためのデータ転送サービス ジョブを作成します。 このアクティビティは、コンテンツの一意な ID を使用して、クライアントの **ContentTransferManager.log** で追跡できます。

<pre><code class="lang-text">CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> (corresponding DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>) started download from '<Distribution Point URL>/<b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b>' for full content download.
</code></pre>

> [!NOTE]
> このログ エントリは、CTM と DTS のジョブ ID を識別するために使用できます。これを使用すると、それぞれ **ContentTransferManager.log** と **DataTransferService.log** のコンテンツ転送の進行状況を追跡できます。

データ転送サービスは、バックグラウンド インテリジェント転送サービス (BITS) ジョブを作成し、ダウンロードが完了するまで待機することによって、アプリケーション コンテンツのダウンロードを実行します。 このアクティビティは、**ContentTransferService.log** から取得した DTS ジョブ ID を使用して、クライアントの **DataTransferService.log** で追跡できます。

<pre><code class="lang-text">Starting BITS job '{40263E01-2EDD-462F-ABBA-A5E892CB9229}' for DTS job '<b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>' under user 'S-1-5-18'.
DTSJob <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> in state 'DownloadingData'.
DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> has completed
</code></pre>

ダウンロードが完了すると、コンテンツ アクセス コンポーネントに通知されます。 コンテンツ アクセス コンポーネントは、ダウンロードされたコンテンツを検証して、ダウンロード中にコンテンツが変更されていないことを確認します。 このアクティビティは、コンテンツの一意な ID を使用して **CAS.log** で追跡できます。

```text
Hash verification succeeded for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 downloaded under context System
```

最後に、コンテンツが検証された後、CI エージェントはタスク完了通知を受信し、CI エージェント ジョブは次のフェーズに移動します。

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateDownloadingContents</b>)
</code></pre>

## <a name="next-steps"></a>次のステップ

- [アプリケーションのインストール](deployment-install-technical-reference.md)
