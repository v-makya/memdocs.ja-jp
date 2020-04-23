---
title: Microsoft Endpoint Configuration Manager の FAQ
titleSuffix: Configuration Manager
description: Microsoft Endpoint Configuration Manager についてよく寄せられる質問
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: be276b34-e283-4386-8b45-5629e431c50d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05aeca86071ea823d3ebc3cf493bea4d418bad27
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706850"
---
# <a name="microsoft-endpoint-configuration-manager-faq"></a>Microsoft Endpoint Configuration Manager の FAQ

*適用対象:Configuration Manager (Current Branch、Technical Preview Branch)*

バージョン 1910 以降、Configuration Manager は Microsoft Endpoint Manager の一部になりました。 この記事では、よく寄せられる質問への回答を記載しています。

## <a name="summary"></a>[概要]

まずは、Microsoft 365 担当の Microsoft コーポレート バイス プレジデントである Brad Anderson による次の 2 分間のビデオをご覧ください。

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="faqs"></a>よく寄せられる質問

### <a name="what-is-microsoft-endpoint-manager"></a>Microsoft Endpoint Manager とは何ですか。

Microsoft Endpoint Manager は、すべてのデバイスを管理するための統合ソリューションです。 Microsoft は、ライセンスを簡素化して、Configuration Manager と Intune を統合しました。 既存の Configuration Manager の投資を引き続き活用しながら、Microsoft クラウドの機能をご自分のペースで利用できます。

次の Microsoft 管理ソリューションは、すべて **Microsoft Endpoint Manager** ブランドの一部になりました。

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Desktop Analytics](../../desktop-analytics/overview.md)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- [デバイス管理の管理コンソール](https://go.microsoft.com/fwlink/?linkid=2109094)に含まれるその他の機能

詳細については、Microsoft 365 担当の Microsoft コーポレート バイス プレジデントである Brad Anderson による次の投稿を参照してください。

- [お知らせのブログ投稿](https://aka.ms/cmannounce)
- [ビジョン ペーパー](https://aka.ms/MEMVisionPaper)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Microsoft Endpoint Manager での Configuration Manager の変更点は何ですか。

バージョン 1910 では、名前の変更を除けば、Configuration Manager は引き続き同じように機能します。

注目点としては、[スタート] メニューのフォルダー名が、[Configuration Manager コンソール](../servers/manage/admin-console.md#bkmk_open)や[ソフトウェアセンター](software-center.md#bkmk_open)などの共通コンポーネントについて変更されました。

### <a name="how-do-we-refer-to-the-product-now"></a>製品を参照する場合はどうすればよいですか。

- すべてのコンポーネントを含むソリューション全体を参照する場合: **Microsoft Endpoint Manager**

- オンプレミスのコンポーネントを参照する場合:
  - 初回参照時は、完全なブランド名を使用: **Microsoft Endpoint Configuration Manager**
  - 一般的な使用: **Configuration Manager**
  - スペースに制約がある場合の使用: **ConfigMgr** (一般的な使用名では不都合がある場合のみ)

### <a name="are-there-any-licensing-changes"></a>ライセンスの変更はありますか。

はい、ご利用いただけます。 Microsoft Ignite 2019 で発表されたように、Configuration Manager のライセンスをお持ちの場合は、Windows PC の[共同管理](../../comanage/overview.md)ができるように Intune のライセンスが付与されました。 詳細については、「[Configuration Manager のブランチとライセンスに関してよく寄せられる質問](product-and-licensing-faq.md#bkmk_mem)」を参照してください。

### <a name="why-do-i-still-see-system-center-configuration-manager-some-places"></a>まだ "System Center Configuration Manager" と表示されているところがあるのはなぜですか。

すべての製品、サービス、ドキュメントなどのサポート資料に対して変更を加えるには時間がかかります。

また、変更されない可能性のある基本コンポーネントもいくつかあります。 サイト サーバーのメインの Windows サービスは、**SMS_Executive** のままです。 このドキュメントをサポートしている GitHub リポジトリは、引き続き **SCCMDocs** になります。

## <a name="next-steps"></a>次のステップ

[Configuration Manager の増分バージョンの新機能](../plan-design/changes/whats-new-incremental-versions.md)について説明します。
