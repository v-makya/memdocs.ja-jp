---
title: 中国のネットワーク エンドポイントのデプロイ - Microsoft Intune
titleSuffix: ''
description: Intune の中国のエンドポイントを確認します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: fd52b34b70b71874a42486cbdc87cd3d7d2f9037
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994244"
---
# <a name="china-endpoints-for-microsoft-intune"></a>Microsoft Intune の中国のエンドポイント

このページには、Intune のデプロイでのプロキシ設定に必要な中国のエンドポイントが一覧表示されています。

ファイアウォールとプロキシ サーバーの背後にあるデバイスを管理するには、Intune に対する通信を有効にする必要があります。

- Intune クライアントは、**HTTP (80)** と **HTTPS (443)** を使用しているため、プロキシ サーバーは両方のプロトコルをサポートする必要があります
- Intune では、一部のタスク (ソフトウェア更新プログラムのダウンロードなど) で、manage.microsoft.com への認証されていないプロキシ サーバー アクセスが必要です

個々のクライアント コンピューターでプロキシ サーバーの設定を変更できます。 また、グループ ポリシーの設定を使用して、指定したプロキシ サーバーの背後にあるすべてのクライアント コンピューターの設定を変更することもできます。

マネージド デバイスは、 **[すべてのユーザー]** がファイアウォール経由でサービスにアクセスできるように構成する必要があります。

中国のお客様の Windows 10 自動登録とデバイス登録の詳細については、[Windows デバイスの登録の設定](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration)に関する記事をご覧ください。

次の表は、Intune クライアントがアクセスするポートとサービスの一覧です。

|**エンドポイント**|**IP アドレス**|
|---------------------|-----------|
|*.manage.microsoft.cn | 40.73.38.143<br>139.217.97.81<br>52.130.80.24<br>40.73.41.162<br>40.73.58.153<br>139.217.95.85 |


## <a name="intune-customer-designated-endpoints-in-china"></a>Intune のお客様向けに指定された中国のエンドポイント
- Azure portal: https:\//portal.azure.cn/
- Microsoft 365: https:\//portal.partner.microsoftonline.cn/
- Intune ポータル サイト: https:\//portal.manage.microsoftonline.cn/
- Microsoft Endpoint Manager admin center: https:\//endpoint.microsoftonline.cn/


## <a name="partner-service-endpoints"></a>パートナー サービス エンドポイント

21Vianet が運用している Intune は、次のパートナー サービス エンドポイントに依存しています。
- Azure AD Sync サービス: https:\//syncservice.partner.microsoftonline.cn/DirectoryService.svc
- Evo STS: https:\//login.chinacloudapi.cn/
- Azure AD Graph: https:\//graph.chinacloudapi.us
- MS Graph: https:\//microsoftgraph.chinacloudapi.cn
- ADRS: https:\//enterpriseregistration.microsoftonline.us

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>次のステップ
[中国の 21Vianet が運用している Intune に関する詳細](china.md)

