---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 06/29/2020
ms.openlocfilehash: 26bfbe7b7cabef8c8dee56077b924b69c4c5886a
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590536"
---
### <a name="azure-ad-authentication-doesnt-work"></a><a name="ki_auth"></a> Azure AD 認証が機能しない
<!--7569264-->
Configuration Manager による Azure Active Directory (Azure AD Security Token Service) の使用が機能しません。 管理ポイントの **CCM_STS.log** には、次のエラーのようなエントリが含まれています:`ProcessRequest - Exception: System.IO.FileLoadException: Could not load file or assembly 'System.IdentityModel.Tokens.JWT.` また、HRESULT 0x80131040 も含まれています。

もう 1 つの症状は、クラウド管理ゲートウェイ (CMG) に関する問題です。 CMG 接続アナライザーを実行すると、管理ポイントの CMG チャネルのテストが失敗し、次のエラーが表示されます: `Failed to get ConfigMgr token with Azure AD token. Status code is '500' and status description is 'CMGConnector_InternalServerError'.`

この問題は、サポート ライブラリとのバージョンの不一致が原因で発生します。

この問題を回避するには、サイト サーバー上のインストール ディレクトリの \bin\X64 フォルダーから、管理ポイントの SMS_CCM\CCM_STS\bin フォルダーに **System.IdentityModel.Tokens.JWT.dll** をコピーします。
