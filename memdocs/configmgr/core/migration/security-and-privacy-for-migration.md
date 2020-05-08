---
title: 移行のセキュリティとプライバシー
titleSuffix: Configuration Manager
description: Configuration Manager Current Branch 環境に移行するためのセキュリティのベスト プラクティスとプライバシー情報を確認します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ad92e4906c45b5c720ab35efc055449a27cc0850
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906214"
---
# <a name="security-and-privacy-for-migration-to-configuration-manager-current-branch"></a>Configuration Manager Current Branch への移行のセキュリティとプライバシー

*適用対象:Configuration Manager (Current Branch)*

このトピックでは、Configuration Manager Current Branch 環境に移行するためのセキュリティのベスト プラクティスとプライバシー情報を説明しています。  

## <a name="security-best-practices-for-migration"></a>移行のセキュリティのベスト プラクティス  
 次の表に、セキュリティのベスト プラクティスをまとめます。  

|セキュリティのベスト プラクティス|説明|  
|----------------------------|----------------------|  
|ソース サイトの SMS プロバイダー アカウントとソース サイトの SQL Server アカウントに、ユーザー アカウントではなく、コンピューター アカウントを使用します。|移行でユーザー アカウントを使用する必要がある場合は、移行完了後にアカウントの詳細を削除してください。|  
|ソース サイトの配布ポイントから移行先サイトの配布ポイントにコンテンツを移行する際には、IPsec を使用します。|不正な改ざんを検知するため移行対象のコンテンツはハッシュされますが、転送中にデータが変更された場合は移行に失敗します。|  
|移行ジョブを作成できる管理ユーザーを制限し、監視します。|移行先階層のデータベースの整合性は、管理ユーザーがソース階層からインポートすることを決めたデータの整合性によって左右されます。 また、管理ユーザーはソースのソース階層の全データを読むことができます。|  

### <a name="security-issues-for-migration"></a>移行に関するセキュリティの問題  
移行には以下のようなセキュリティの問題が伴います。  

-   クライアントがソース サイトからブロックされている場合、そのクライアント レコードが移行される前に、移行先階層に正常に割り当てられる場合があります。  

     Configuration Manager では、移行するクライアントのブロック状態が維持されますが、クライアント レコードの移行が完了する前にクライアントの割り当てが行われた場合には、クライアントが移行先階層に正常に割り当てられることがあります。  

-   監査メッセージは移行されません。  

ソース サイトから移行先サイトにデータが移行されると、ソース階層のすべての監査情報が失われます。  

## <a name="privacy-information-for-migration"></a>移行に関するプライバシー情報  
 移行処理では、ソース インフラストラクチャで指定したサイト データベースの情報が探索され、そのデータは移行先階層のデータベースに保管されます。 Configuration Manager がソース サイトまたはソース階層から探索できる情報は、ソース環境で有効にしていた機能や、ソース環境で実行していた管理操作に応じて変わります。  

 セキュリティとプライバシー情報の詳細については、次のトピックのいずれかを参照してください。  

-   Configuration Manager 2007 のプライバシー情報の詳細については、Configuration Manager 2007 ドキュメント ライブラリの「[Configuration Manager 2007 のセキュリティとプライバシー](https://docs.microsoft.com/previous-versions/system-center/configuration-manager-2007/bb680768(v=technet.10))」を参照してください。  

-   System Center 2012 Configuration Manager のプライバシー情報の詳細については、System Center 2012 Configuration Manager ドキュメント ライブラリの「[System Center 2012 Configuration Manager のセキュリティとプライバシー](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/gg682033(v=technet.10))」を参照してください。  

-   System Center Configuration Manager のプライバシー情報の詳細については、「[System Center Configuration Manager のセキュリティとプライバシー](../../core/plan-design/security/security-and-privacy.md)」を参照してください。  

サポートされるデータ全体またはその一部を、ソース サイトから移行先階層に移行できます。  

移行は既定では有効化されず、いくつかの構成手順を実行しなければなりません。 移行情報はマイクロソフトに送信されません。  

ソース階層からデータを移行する前に、プライバシーの要件を考慮してください。  
