---
title: 拡張相互運用性クライアント
titleSuffix: Configuration Manager
description: Current Branch サイトでの静的な Configuration Manager クライアントの長期的サポートに対する拡張相互運用性クライアントの使用について説明します。
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 61296321251be45cfa0449a3e4f21ba79a024753
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706980"
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>将来のバージョンの Current Branch サイトとの拡張相互運用性のために構成マネージャー クライアント ソフトウェアを使用する

*適用対象:Configuration Manager (Current Branch)*  

ビジネス要件によっては、一部のデバイスで構成マネージャー クライアントを定期的に更新することができないことがあります。 たとえば、変更管理ポリシーに従う必要がある場合や、デバイスがミッション クリティカルな場合です。 これらのニーズには、拡張相互運用性クライアント (EIC) と呼ばれる長期使用のための新しいクライアントをインストールすることによって対応します。 EIC は、キオスク デバイスや販売時点管理デバイスのように、頻繁に更新できない特定のデバイスにのみ使用します。 ほとんどのクライアントについては、[自動クライアント アップグレード](../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)を引き続き使用します。

## <a name="how-it-works"></a>しくみ

通常、Configuration Manager の新しい[コンソール内更新プログラム](../servers/manage/install-in-console-updates.md)をインストールすると、その新機能を使用できるように、クライアント ソフトウェアが自動的に更新されます。 このシナリオでは、新しい機能と更新プログラムを受け取る Current Branch にやはり更新します。 ほとんどのデバイスは、ユーザーがインストールする各バージョンの更新プログラムで Configuration Manager クライアント ソフトウェアを更新します。 ただし、クライアント ソフトウェアの更新プログラムを受信させたくない重要なシステムのサブセットには、拡張相互運用性クライアントをインストールします。 拡張相互運用性クライアントの場合、新しいバージョンのクライアント ソフトウェアを明示的に展開するまで、新しいクライアント ソフトウェアはインストールされません。

## <a name="supported-versions"></a>サポートされるバージョン

次の表では、このシナリオでサポートされている Configuration Manager クライアントのバージョンを示します。

| バージョン | 公開日 | サポート終了日 |
|---------|---------|---------|
| 1902<br/>5.00.8790 | 2019 年 3 月 27 日 | 2021 年 3 月 27 日以降 |
| 1802<br/>5.00.8634 | 2018 年 5 月 1 日 | 2020 年 5 月 1 日以降 |
| 1606<br/>5.00.8412 | 2016 年 11 月 18 日 | 2019 年 5 月 1 日 |

> [!TIP]  
> EIC は、リリース日から 2 年以上サポートされます。 リリース日の詳細については、「[Configuration Manager の Current Branch バージョンのサポート](../servers/manage/current-branch-versions-supported.md)」をご覧ください。  

クライアントのサポートが期限切れになる前に、Current Branch で管理するデバイスの拡張相互運用性クライアントを更新するように計画を立ててください。 更新するには、新しいバージョンのクライアントを Microsoft からダウンロードし、現在の拡張相互運用性クライアントを使用しているデバイスにその新しいクライアント ソフトウェアを展開します。

## <a name="how-to-use-the-eic"></a>EIC の使用方法

1. これらのデバイスをコレクションに追加し、そのコレクションを自動クライアント アップグレードから除外します。 詳しくは、[クライアントをアップグレードから除外する方法](../clients/manage/upgrade/exclude-clients-windows.md)に関する記事をご覧ください。  

1. Configuration Manager 更新プログラムのインストール メディアの `\SMSSETUP\Client` フォルダーから、サポートされているバージョンから EIC を入手します。 フォルダーの内容をすべてコピーするようにします。  

    > [!TIP]  
    > [ボリューム ライセンス サービス センター](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC) で Configuration Manager のメディアを見つけるには、 **[Downloads and Keys]\(ダウンロードとキー\)** タブに移動し、`System Center Config` を検索して、 **[System Center Config Mgr (current branch)]\(System Center Configuration Manager (Current Branch)\)** を選択します。

1. デバイスに EIC を手動でインストールします。 詳細については、「[クライアントの手動インストール方法](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)」をご覧ください。  

    > [!Important]  
    > バージョン 1606 のクライアントをバージョン 1802 にアップグレードするときは、CCMSETUP のオプション **/AlwaysExcludeUpgrade:True** を使用します。 そうしないと、クライアントは除外ポリシーの前に自動的にアップグレードするためのポリシーを管理ポイントから受信する可能性があります。  

## <a name="limitations"></a>制限事項

- 拡張相互運用性クライアント ソフトウェアの更新プログラムは、コンソール内更新プログラムを使用して入手できません。 EIC の更新方法について詳しくは、「[除外したクライアントをアップグレードする方法](../clients/manage/upgrade/exclude-clients-windows.md#bkmk_override)」をご覧ください。  

- EIC は次の機能のみをサポートします。  

  - ソフトウェア更新プログラム  
  - ハードウェアとソフトウェアのインベントリ
  - パッケージとプログラム

## <a name="next-steps"></a>次のステップ

[クライアントをアップグレードから除外する方法](../clients/manage/upgrade/exclude-clients-windows.md)

クライアントがデバイスに適切にインストールされていることを確認するには、「[クライアントを監視する方法](../clients/manage/monitor-clients.md)」をご覧ください。
