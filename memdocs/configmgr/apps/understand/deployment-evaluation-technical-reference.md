---
title: アプリケーション評価のテクニカル リファレンス
titleSuffix: Configuration Manager
description: Configuration Manager でのアプリケーション評価のトラブルシューティングに関するテクニカル リファレンスです。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a7035223-d7bd-47b4-896f-08de3416a4eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fdeec54489adfc0d2a5cceb99c7e7587ce1a41ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688840"
---
# <a name="application-deployment-evaluation"></a>アプリケーション デプロイの評価

*適用対象:Configuration Manager (Current Branch)*

続行する前に、[アプリケーション展開クライアント コンポーネント](client-components-technical-reference.md)を参照して、DCM と CI エージェントのジョブの処理を理解してください。

アプリケーションの評価は、展開がアクティブ化されるときに、DCM エージェント コンポーネントおよび CI エージェント コンポーネントによって実行されます。 割り当てがアクティブになるタイミングを理解するには、[デバイス コレクションへのアプリケーションの展開についての記事](device-deployment-technical-reference.md)または[ユーザー コレクションへのアプリケーションの展開に関する記事](user-deployment-technical-reference.md)を参照してください。

## <a name="application-detection-and-evaluation"></a>アプリケーションの検出と評価

アプリケーションの評価は、CI エージェント ジョブの **InvokingSdmMethod** フェーズで実行されます。 このフェーズでは、クライアントがアプリケーションに対して定義されている検出方法を評価し、アプリケーションがデバイスにインストールされているかどうかを判断します。 このアクティビティは、展開の種類の一意な ID または展開の種類の名前を使用して、**AppDiscovery.log** で追跡できます。

```text
Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ Did not detect app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
```

> [!NOTE]
> 上記の例では、MSI 製品コードがデバイスにインストールされているかどうかを確認することによって検出が実行される MSI アプリケーションの検出を示しています。 別の検出方法を使用するアプリケーションでは、適切な検出方法を使用して、アプリケーションがインストールされているかどうかを確認します。

次に、クライアントは、展開の目的に基づいて、アプリケーションの目的の状態を評価します。 この手順では、アプリケーションに適用される依存関係または置き換え規則がアプリケーションにあるかどうかも検出します。 このアクティビティは、アプリケーションと展開の種類の一意な ID を使用して **AppIntentEval.log** で追跡できます。

<pre><code class="lang-text"># Available Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Available</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Required Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Installed</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Requirement Rules Not Met

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = NotApplicable, ResolvedState = None</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]
</code></pre>

上のログ エントリで、**Current State** はアプリケーションが現在デバイスにインストールされているかどうかを示します。 **Applicability** は、定義された要件規則に基づいてアプリケーションが適用可能かどうかを示します。 **ResolvedState** は、展開の目的に基づいたアプリケーションの目的の状態を示します。

> [!TIP]
> [Deployment Monitoring Tool](../../core/support/deployment-monitoring-tool.md) を使用すると、アプリケーションの状態、適用性の状態、要件の違反を表示できます。

## <a name="next-steps"></a>次のステップ

- [アプリケーションのダウンロード](deployment-download-technical-reference.md)
