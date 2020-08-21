---
title: LTSB の概要
titleSuffix: Configuration Manager
description: Configuration Manager の Long-Term Servicing Branch について説明します。
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1370c1bf80283ff30ad54378ad58ecd9a5d24d47
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699366"
---
# <a name="introduction-to-the-long-term-servicing-branch-of-configuration-manager"></a>Configuration Manager の Long-Term Servicing Branch の概要

*適用対象: System Center Configuration Manager (Long-Term Servicing Branch)*

Configuration Manager の Long-Term Servicing Branch (LTSB) は、ブランチの 1 つで、すべてのユーザーが使用できるインストール オプションとして設計されています。 ただし、Configuration Manager のソフトウェア アシュアランス (SA) または同等のサブスクリプションの権利が期限切れになったユーザーにとっては、これが唯一の選択肢になります。

Configuration Manager バージョン 1606 では、Configuration Manager の Current Branch と比較すると、LTSB の機能が制限されています。

> [!TIP]   
> Configuration Manager LTSB は、System Center スイートの長期サービス チャネル (LTSC) に関連していません。 詳しくは、「[System Center リリース オプションの概要](/system-center/ltsc-and-sac-overview)」をご覧ください。

## <a name="features-that-arent-available"></a>利用できない機能

Configuration Manager の Current Branch では、LTSB を使用する場合には使用できない次の機能がサポートされています。

- 新しい機能を追加したり機能を改善したりする、コンソール内の更新プログラム。
- サイト サーバーとクライアントとして使用する新しくリリースされたオペレーティング システムのサポート。
- オンプレミス MDM
- 最近の Windows 10 バージョンのサポートなど、Windows 10 サービス ダッシュボードとサービス プラン。  
- Windows Server と Windows 10 LTSB の今後のリリースのサポート
- 資産インテリジェンス
- クラウドベースの配布ポイント
- Exchange Online と Exchange Connector    

これらの機能のサポートは LTSB では使用できません。一部の機能は Configuration Manager コンソールに表示されますが、選択したり使用したりすることはできません。

クラウド統合と、Configuration Manager Current Branch バージョン 1610 以降に含まれる機能は、LTSB では使用できません。 これらの機能には以下が含まれますが、これらに限定されません。<!--SCCMDocs#1823-->

- 共同管理
- Desktop Analytics
- クラウド管理ゲートウェイ
- Azure Active Directory の統合
- ビジネス向け Microsoft Store からのアプリ

## <a name="find-ltsb-documentation"></a>LTSB のドキュメントを検索する

LTSB は、Current Branch バージョン 1606 に基づいています。 LTSB 固有の注意事項と制限事項が記載された [Current Branch の ドキュメント](../../index.yml)を使用してください。 以下に関する記事で、これらの注意事項と制限事項を確認できます。

- [LTSB のインストール](install-the-ltsb.md)
- [LTSB の Current Branch へのアップグレード](convert-to-current-branch.md)
- [LTSB のサポートされている構成](supported-configurations-for-ltsb.md)
- [Configuration Manager の LTSB の管理](manage-the-ltsb.md)

LTSB について Current Branch ドキュメントを参照する場合、バージョン 1606 以前についての説明は LTSB にも当てはまります。 バージョン 1610 以降で導入された機能や説明は LTSB ではサポートされません。

## <a name="licensing-overview-for-the-ltsb"></a>LTSB のライセンスの概要   

2016 年 10 月 1 日の時点で Configuration Manager ライセンスに対してソフトウェア アシュアランス (SA) が有効になっているお客様または同等のサブスクリプション権限を持っているお客様には、2016 年 10 月リリースのバージョン 1606 の Configuration Manager を使用する権限があります。 2016 年 10 月 1 日以降、Configuration Manager に対する権限を持つお客様には、インストール時に Current Branch および Long-Term Servicing Branch (LTSB) の 2 つのライセンス オプションが表示されます。

System Center Configuration Manager に対して永続的な権利を持つお客様または、10 月 1 日の後に SA またはサブスクリプションが期限切れになったお客様は、該当する時点で最新のバージョンである System Center Configuration Manager LTSB をインストールできます。

これらのライセンスについて詳しくは、[Microsoft ボリューム ライセンス プログラムを通じて購入する製品の使用条件](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1)に関するページをご覧ください。

Configuration Manager ブランチのライセンスについて詳しくは、[Configuration Manager のライセンスとブランチ](learn-more-editions.md)に関するページをご覧ください。

## <a name="next-steps"></a>次のステップ

お使いの環境に適したブランチは Configuration Manager LTSB だと思われた場合は、新しい階層の一部として[新しい LTSB サイトをインストールする](install-the-ltsb.md#install-a-new-site)か、[System Center 2012 Configuration Manager サイトと階層をアップグレード](install-the-ltsb.md#upgrade-from-system-center-2012-configuration-manager)してください。