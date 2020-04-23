---
title: Deployment Monitoring Tool
titleSuffix: Configuration Manager
description: Deployment Monitoring Tool を使用して、Configuration Manager クライアントで発生するソフトウェア展開の問題を解決します。
ms.date: 09/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9edc214f-f405-456d-80df-8adcc2a5428d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a27e96cf69ab01b58910ae02fc732940eda8a04
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707830"
---
# <a name="deployment-monitoring-tool"></a>Deployment Monitoring Tool

*適用対象:Configuration Manager (Current Branch)*

Deployment Monitoring Tool は、[Configuration Manager のツール](tools.md)の 1 つです。 Configuration Manager クライアント上のアプリケーション、ソフトウェア更新プログラム、および構成基準の展開のトラブルシューティングを支援するために設計されたグラフィカル ユーザー インターフェイスです。 このツールは、クライアントのいずれの状態も変更しないため、読み取り専用です。 一般的な展開シナリオの診断に安心して使用することができます。


## <a name="features"></a>機能

- ローカル クライアント上の展開の問題を解決するには、管理者として実行します。  

- リモート クライアント上の展開の問題を解決します。 管理者としてツールを起動してリモート コンピューターに接続します。  

- ツールで収集されたすべてのデータを XML 形式でエクスポートします。 その XML ファイルを他のユーザーと共有し、展開のトラブルシューティングについて話す共通のプラットフォームとして使用します。  

- 以前にエクスポートしたデータを別のコンピューターにインポートし、それを使用してオフライン モードでツールを実行します。   


## <a name="usage"></a>使用方法

Deployment Monitoring Tool は、グラフィカル ユーザー インターフェイスのみをサポートしています。 ツールを起動するには、**DeploymentMonitoringTool.exe** を管理者として実行します。 次の 3 つのビューがあります。  

- **クライアントのプロパティ**:デバイスと Configuration Manager クライアントに関する役に立つ属性の一覧が表示されます。 これが既定のビューです。   

- **展開**:現在ターゲットになっているすべての展開が表示されます。 結果ウィンドウの展開を選択すると、詳細ウィンドウに詳細情報が表示されます。  

- **すべての更新**:すべてのソフトウェア更新プログラムとその状態が表示されます。  

いずれのビューでも、データをコピーするには、セルを選択し、**Ctrl** + **C** キーを押します。


### <a name="actions-menu"></a>アクション メニュー

**[アクション]** メニューでは、次のアクションを使用できます。  

- **Connect to remote machine\(リモート コンピューターに接続\)** :接続先のコンピューターを選択します。 ユーザー名とパスワードを指定しない場合、現在の資格情報が使用されます。 **[保存]** をクリックしてリモート コンピューターに接続します。  

- **データのエクスポート**:データを書き込むファイルを選択し、 **[保存]** をクリックします。 エクスポートされた XML ファイルを使用して、別のコンピューターでリモート トラブルシューティングを行います。  

- **データのインポート**:ツールにインポートするファイルを選択します。  

- **ログの表示**:ビューに応じて、関連するログ ファイルを開きます。  
    - クライアントのプロパティ: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - 展開: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - すべての更新: `C:\Windows\WindowsUpdate.log`



## <a name="see-also"></a>関連項目

- [アプリケーションの展開](../../apps/deploy-use/deploy-applications.md)
- [ソフトウェア更新プログラムの展開](../../sum/deploy-use/deploy-software-updates.md)
- [構成基準を展開する](../../compliance/deploy-use/deploy-configuration-baselines.md)
