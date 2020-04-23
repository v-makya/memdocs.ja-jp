---
title: 電源管理の推奨事項
titleSuffix: Configuration Manager
description: Configuration Manager の電源管理の Microsoft 推奨事項をご確認ください。
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 02cfb32f9187ca5a0ae0ad70ffcb4b85db8afb1b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696630"
---
# <a name="recommendations-for-power-management-in-configuration-manager"></a>Configuration Manager の電源管理の推奨事項

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の電源管理については、次の推奨事項をご利用ください。  

## <a name="monitor-at-a-representative-time"></a>典型的な時間で監視する

電源管理の監視段階からは、組織のコンピューターに関する次の情報が与えられます。

- 電力消費
- アクティビティ
- 電源管理機能
- 環境影響量

デバイスを監視する典型的時間を選択します。 たとえば、休日に監視しても、コンピューターの電力使用状況について現実的なレポートが与えられません。

## <a name="create-a-control-collection"></a>コントロール コレクションを作成する

2 つのコンピューター コレクションを作成して、電源プランをコンピューターに適用した場合の影響を監視します。 最初のコレクションには、電源設定を適用するコンピューターの大部分を含めてください。 *コントロール コレクション*には、残りのコンピューターを含めてください。 最初のコレクションに、必要な電源管理プランを適用します。 次に、レポートを実行し、2 つのコレクション間の影響を比較します。  

## <a name="run-reports-before-you-apply-a-plan"></a>プランを適用する前にレポートを実行する

電源管理プランをコンピューターのコレクションに適用する前に、**電源設定**レポートを実行します。 このレポートを使用すると、コレクションのコンピューターで既に構成されている電源管理設定の理解に役立ちます。 既存の設定について調査を行わずに新しい電源管理設定を適用すると、電力消費量が増えることがあります。  

## <a name="exclude-servers"></a>サービスを除外する

Windows Server を実行しているコンピューターの電源管理はサポートされていません。 サーバーをコレクションに追加し、コレクションを電源管理から除外します。  

> [!NOTE]
> Configuration Manager では Windows Server の電源管理がサポートされていませんが、分析と報告のために電源使用状況データが収集されます。

## <a name="exclude-other-computers"></a>他のコンピューターを除外する

電源管理を希望しないコンピューターがある場合、そのようなコンピューターを除外コレクションに追加します。  

次の種類のコンピューターは電源管理から除外することが推奨されます。

- 電源を常にオンにしておく必要のあるコンピューター  

- ユーザーがリモートで接続する必要があるコンピューター。  

- 電源管理機能を使用できないコンピューター。  

- 配布ポイント サイト システムの役割を持つコンピューター  

- キオスク コンピューター、情報ディスプレイ、監視コンソールなど、コンピューターとモニターを常にオンにしておく必要がある公共のコンピューター。  

詳細については、「[電力管理の構成](configuring-power-management.md)」を参照してください。  

## <a name="apply-power-plans-to-a-test-collection"></a>電源プランをテスト コレクションに適用する

電源管理プランを多数のコンピューターが含まれるコレクションに適用する前に、テスト用のコレクションに適用して、電源プランの効果をテストします。  

電源管理からコンピューターを除外すると、すべての電源設定が元の値に戻ります。 個々の電源設定を元の値に戻すことはできません。  

## <a name="apply-power-plan-settings-individually"></a>電源プラン設定はそれぞれ個別に適用する

1 つの電源設定の適用効果を監視してから次の電源設定を適用します。 この過程により、それぞれの設定で求められる結果が得られることが確認されます。 詳細については、「[使用できる電源管理プランの設定](create-and-apply-power-plans.md#BKMK_Plans)」を参照してください。  

## <a name="regularly-monitor-computers-for-multiple-power-plans"></a>複数の電源プランについてコンピューターを定期的に監視する

電源管理には、複数の電源プランが適用されているコンピューターを表示するレポートも含まれます。**電源プランが複数あるコンピューター**。

あるコンピューターが複数のコレクションに属し、それぞれで異なる電源プランが適用されるとき、次の動作が適用されます。  

- **電源プラン**:1 台のコンピューターに複数の電源設定値が適用されている場合、最も制限の緩い値が使用されます。  

- **ウェイクアップ時間**:1 台のデスクトップ コンピューターに複数のウェイクアップ時間が適用されている場合、深夜に最も近い時間が使用されます。  

詳細については、「[電源プランが複数あるコンピューター](monitor-and-plan-for-power-management.md#BKMK_Multiple)」を参照してください。  

## <a name="save-or-export-power-management-information"></a>電源管理情報の保存またはエクスポート

監視段階とコンプライアンス段階でレポートを実行するとき、結果を保存またはエクスポートします。 Configuration Manager で後にデータを削除する場合、後で比較するためにデータを保存します。  

Configuration Manager では、次の電源管理情報がサイト データベースに保存されます。

- 日次レポートで使用される電源管理情報:31 日間

- 月次レポートで使用される電源管理情報:13 か月
