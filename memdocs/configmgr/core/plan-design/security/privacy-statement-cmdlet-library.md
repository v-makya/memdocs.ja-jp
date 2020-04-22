---
title: コマンドレットのプライバシーに関する声明
titleSuffix: Configuration Manager
description: Configuration Manager コマンドレットに関連するデータを Microsoft が収集して使用する方法について説明します
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 551a8086894f877d07c57fbe2848c2befacfc5b5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695750"
---
# <a name="configuration-manager-cmdlet-library-privacy-statement"></a>Configuration Manager コマンドレット ライブラリのプライバシーに関する声明

*適用対象:Configuration Manager (Current Branch)*

このプライバシーに関する声明は、Configuration Manager Cmdlet Library の機能に適用されます。  

## <a name="usage-data"></a>使用状況データ  

#### <a name="what-this-feature-does"></a>この機能の実行内容

Configuration Manager コマンドレット ライブラリを利用すると、Windows PowerShell のコマンドレットおよびスクリプトを使用して Configuration Manager 階層を管理できます。 コマンドレット ライブラリは、傾向および使用パターンを識別することを目的に、ライブラリのコマンドレットのお客様による使用方法に関する情報を収集します。 また、コマンドレット ライブラリでは、コマンドレットの使用時に発生するエラーの種類と数も収集されます。  

#### <a name="information-collected-processed-or-transmitted"></a>収集、処理、または送信される情報
   
収集される使用状況データには、コマンドレットの開始、停止、終了、非推奨のコマンドレットの実行、コマンドレットに関する SMS プロバイダーの操作のアクティビティ メトリックスが含まれます。 この情報は個人を特定するものではありません。 収集されるエラー情報には、コマンドレットから返されるエラーのほか、例外エラーの詳細が含まれます。 エラーの詳細レポートには、お客様のコンピューターに接続されているデバイスのシリアル番号など、個人を特定できる情報が意図せず含まれる場合があります。 コマンドレット ライブラリは、エラー レポートに含まれる情報のフィルター処理および匿名化を行い個人の特定が可能な情報を削除してから、当該レポートをマイクロソフトに送信します。  

#### <a name="use-of-information"></a>情報の使用
   
Microsoft ではこの情報を Microsoft が提供する製品およびサービスの品質、セキュリティ、整合性の改善のために使用します。  

#### <a name="choicecontrol"></a>選択および制御   

この使用状況データ機能は既定で有効になっています。 Configuration Manager コマンドレット ライブラリには、この機能を制御する 2 つのレジストリ キーがあります。  

 完全に停止するには、これら 2 つのレジストリ キーの値を設定します。 これらは、各 Event Tracing for Windows (ETW) プロバイダー用です。  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (ドライブ プロバイダーの使用状況データの停止)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (コマンドレットの使用状況データの停止)  

  使用状況データ設定を変更する際は、コンピューターに応じて固有の変更を行います。  


## <a name="next-steps"></a>次のステップ

[Configuration Manager のコマンドレット ライブラリ ドキュメント](https://docs.microsoft.com/powershell/sccm/configurationmanager/)。   
