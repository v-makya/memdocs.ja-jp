---
title: Send Schedule Tool
titleSuffix: Configuration Manager
description: Send Schedule Tool を使用して、Configuration Manager クライアントのスケジュールをトリガーします。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d5ce547d-3b3b-47d3-bcd7-6ff94692c046
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78e154c5361063224d9e8c99bc87ba117958edf4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707470"
---
# <a name="send-schedule-tool"></a>Send Schedule Tool

*適用対象:Configuration Manager (Current Branch)*

Send Schedule Tool は、[Configuration Manager のツール](tools.md)の 1 つです。 クライアントのスケジュールをトリガーする場合や、指定した構成基準の評価をトリガーする場合にこのツールを使用します。 ローカル コンピューターの場合やリモート クライアントを対象とする場合に役立ちます。  

たとえば、このツールを使用してインベントリ スケジュールまたはコンプライアンス評価をトリガーします。 複数の Configuration Manager クライアントがインベントリまたはコンプライアンス ステータスについて最近報告していない場合は、ツールを実行して各クライアントで必要なスケジュールを開始します。



## <a name="usage"></a>使用方法

管理者として **SendSchedule.exe** を実行します。 

`SendSchedule /L [Computer Name]`
`SendSchedule "<Message GUID | DCM UID>" [Computer Name]` 

メッセージ (GUID) をトリガーした後に、**SMSClientMethodProvider.log** を確認します。 使用可能なメッセージ GUID の詳細については、「[メッセージ ID](#bkmk_sendschedule-guids)」を参照してください。

構成基準 (DCM UID) の評価をトリガーした後に、**DCMAgent.log** を確認します。



## <a name="command-line-options"></a>コマンド ライン オプション


### <a name="option-l"></a>オプション: `/L` 
送信に使用できるすべてのメッセージ GUID または DCM UID を一覧表示します。 データ テーブルに、各メッセージのわかりやすいメッセージ名が表示されます。 コンピューター名が存在しない場合は、ローカル コンピューターが使用されます。 コンピューター名なしでメッセージを指定した場合、メッセージはローカル コンピューターに送信されます。 



## <a name="examples"></a>例

#### <a name="list-the-available-messages-on-the-local-machine"></a>ローカル コンピューターで使用できるメッセージを一覧表示する 
`SendSchedule /L` 

#### <a name="list-the-available-messages-on-the-client-mypc"></a>クライアント MyPC で使用できるメッセージを一覧表示する: 
`SendSchedule /L MyPC`

#### <a name="trigger-hardware-inventory-on-the-local-machine"></a>ローカル コンピューターでハードウェア インベントリをトリガーする
`SendSchedule {00000000-0000-0000-0000-000000000001}`

#### <a name="trigger-hardware-inventory-on-mypc"></a>MyPC のハードウェア インベントリを有効にする: 
`SendSchedule {00000000-0000-0000-0000-000000000001} MyPC` 

#### <a name="trigger-the-evaluation-of-a-specific-configuration-baseline-on-mypc"></a>MyPC の特定の構成基準の評価をトリガーする: 
`SendSchedule ScopeId_611E8382-C064-4B62-B0DE-EFFB52AE8994/Baseline_36722778-69dd-4423-9632-b61148b2b67e MyPC` 



## <a name="message-ids"></a><a name="bkmk_sendschedule-guids"></a> メッセージ ID

|［メッセージ ID］  |表示名  |
|---------|---------|
|{00000000-0000-0000-0000-000000000001}|ハードウェア インベントリ|
|{00000000-0000-0000-0000-000000000002}|ソフトウェア インベントリ|
|{00000000-0000-0000-0000-000000000003}|Discovery Inventory|
|{00000000-0000-0000-0000-000000000010}|ファイル コレクション|
|{00000000-0000-0000-0000-000000000011}|IDMIF Collection|
|{00000000-0000-0000-0000-000000000021}|Request Machine Assignments|
|{00000000-0000-0000-0000-000000000022}|Evaluate Machine Policies|
|{00000000-0000-0000-0000-000000000023}|Refresh Default MP Task|
|{00000000-0000-0000-0000-000000000024}|LS (Location Service) Refresh Locations Task|
|{00000000-0000-0000-0000-000000000025}|LS Timeout Refresh Task|
|{00000000-0000-0000-0000-000000000026}|Policy Agent Request Assignment (User)|
|{00000000-0000-0000-0000-000000000027}|Policy Agent Evaluate Assignment (User)|
|{00000000-0000-0000-0000-000000000031}|Software Metering Generating Usage Report|
|{00000000-0000-0000-0000-000000000032}|Source Update Message|
|{00000000-0000-0000-0000-000000000037}|Clearing proxy settings cache|
|{00000000-0000-0000-0000-000000000040}|Machine Policy Agent Cleanup|
|{00000000-0000-0000-0000-000000000041}|User Policy Agent Cleanup|
|{00000000-0000-0000-0000-000000000042}|Policy Agent Validate Machine Policy / Assignment|
|{00000000-0000-0000-0000-000000000043}|Policy Agent Validate User Policy / Assignment|
|{00000000-0000-0000-0000-000000000051}|Retrying/Refreshing certificates in AD on MP|
|{00000000-0000-0000-0000-000000000061}|Peer DP Status reporting|
|{00000000-0000-0000-0000-000000000062}|Peer DP Pending package check schedule|
|{00000000-0000-0000-0000-000000000063}|SUM Updates install schedule|
|{00000000-0000-0000-0000-000000000101}|Hardware Inventory Collection Cycle|
|{00000000-0000-0000-0000-000000000102}|Software Inventory Collection Cycle|
|{00000000-0000-0000-0000-000000000103}|Discovery Data Collection Cycle|
|{00000000-0000-0000-0000-000000000104}|File Collection Cycle|
|{00000000-0000-0000-0000-000000000105}|IDMIF Collection Cycle|
|{00000000-0000-0000-0000-000000000106}|Software Metering Usage Report Cycle|
|{00000000-0000-0000-0000-000000000107}|Windows Installer Source List Update Cycle|
|{00000000-0000-0000-0000-000000000108}|Software Updates Policy Action Software Updates Assignments Evaluation Cycle|
|{00000000-0000-0000-0000-000000000109}|PDP Maintenance Policy Branch Distribution Point Maintenance Task|
|{00000000-0000-0000-0000-000000000110}|DCM policy|
|{00000000-0000-0000-0000-000000000111}|Send Unsent State Message|
|{00000000-0000-0000-0000-000000000112}|State System policy cache cleanout|
|{00000000-0000-0000-0000-000000000113}|Update source policy|
|{00000000-0000-0000-0000-000000000114}|Update Store Policy|
|{00000000-0000-0000-0000-000000000115}|State system policy bulk send high|
|{00000000-0000-0000-0000-000000000116}|State system policy bulk send low|
|{00000000-0000-0000-0000-000000000121}|Application manager policy action|
|{00000000-0000-0000-0000-000000000122}|Application manager user policy action|
|{00000000-0000-0000-0000-000000000123}|Application manager global evaluation action|
|{00000000-0000-0000-0000-000000000131}|Power management start summarizer|
|{00000000-0000-0000-0000-000000000221}|Endpoint deployment reevaluate|
|{00000000-0000-0000-0000-000000000222}|Endpoint AM policy reevaluate|
|{00000000-0000-0000-0000-000000000223}|External event detection|



