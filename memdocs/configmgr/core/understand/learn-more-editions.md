---
title: ライセンスとブランチ
titleSuffix: Configuration Manager
description: Configuration Manager で使用可能なインストール オプションに関するライセンス要件について説明します
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed335c65369840085fe44ba2f1b81d7806a0e3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906047"
---
# <a name="licensing-and-branches-for-configuration-manager"></a>Configuration Manager のライセンスとブランチ

*適用対象:Configuration Manager (Current Branch) と System Center Configuration Manager (Long-Term Servicing Branch)*

この記事を利用して、Configuration Manager で使用可能なインストール オプションに関するライセンス要件についてご確認ください。 そのようなインストール オプションには、次のブランチが含まれています。

- Current Branch
- Long-Term Servicing Branch (LTSB)
- Current Branch の評価版インストール
- Technical Preview Branch

## <a name="licensing-overview"></a>ライセンスの概要

2016 年 10 月 1 日の時点で Configuration Manager ライセンスに対してソフトウェア アシュアランス (SA) が有効になっているお客様または同等のサブスクリプション権限を持っているお客様には、2016 年 10 月リリースのバージョン 1606 の Configuration Manager を使用する権限があります。 2016 年 10 月 1 日以降、Configuration Manager に対する権限を持つお客様には、インストール時に Current Branch および Long-Term Servicing Branch (LTSB) の 2 つのライセンス オプションが表示されます。

Microsoft ボリューム ライセンス プログラムを通してご購入いただいた製品の使用条件については、「[Licensing Terms and Documentation (ライセンス条項とドキュメント)](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1)」をご覧ください。


## <a name="licensed-branches"></a>ライセンスされたブランチ

この記事では、ソフトウェア アシュアランス契約または同等のサブスクリプション権限が参照されます。 この Microsoft ライセンス契約によって、Configuration Manager をインストールして使用するための権限が付与されます。

### <a name="current-branch"></a>Current Branch

Current Branch をご使用いただくには、Configuration Manager に対するソフトウェア アシュアランス契約または同等の権限が必要です。 詳細については、「[ソフトウェア アシュアランスと Current Branch](#software-assurance-and-the-current-branch)」をご覧ください。

このブランチは、品質と機能に関する更新プログラムを Microsoft から定期的に受信する必要がある運用環境での使用に対応しています。 これにより、すべての機能と機能強化を使用するためのアクセス権が提供されます。

1710 リリース以降では、更新プログラムの各バージョンは一般公開リリース日から 18 か月間サポートされます。 詳細については、[Configuration Manager の Current Branch バージョンのサポート](../servers/manage/current-branch-versions-supported.md)に関するページをご覧ください。

### <a name="long-term-servicing-branch-ltsb"></a>Long-Term Servicing Branch (LTSB)

LTSB をご使用いただくには、2016 年 10 月 1 日以降の、Microsoft との間で現在有効になっているソフトウェア アシュアランス契約が必要です。 詳細については、「[ソフトウェア アシュアランスと LTSB](#software-assurance-and-the-ltsb)」をご覧ください。

このブランチは、運用環境での使用に対応しています。 これは、2016 年 10 月 1 日以降に Configuration Manager に対するソフトウェア アシュアランス (SA) または同等のサブスクリプション権限が期限切れになったお客様にご使用いただくためのものです。 Current Branch と比較して、このブランチには制限があります。

このブランチでは、Configuration Manager に対するセキュリティ上重要な更新プログラムは利用できますが、新機能については利用できません。

### <a name="evaluation-installation-of-the-current-branch"></a>Current Branch の評価版インストール

評価版は、Microsoft とのソフトウェア アシュアランス契約がなくてもご使用いただけます。 [評価版インストール](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection)は必ず Current Branch となり、180 日間ご使用いただけます。

評価版インストールは、Current Branch の完全インストールにアップグレード可能です。 評価版インストールを Long-Term Servicing Branch にアップグレードすることはできません。

### <a name="technical-preview-branch"></a>Technical Preview Branch

[Technical Preview Branch](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) もご利用いただけます。 このブランチは Configuration Manager の制限付きビルドであり、これを使って新機能をお試しいただけます。 Technical Preview は、ライセンス版とは異なるメディアを使用してインストールします。 詳細については、[Technical Preview](../get-started/technical-preview.md) に関するページをご覧ください。


## <a name="software-assurance-agreements"></a>ソフトウェア アシュアランス契約

2016 年 10 月 1 日以降の Configuration Manager のライセンスまたは同等のサブスクリプション権限の状態に応じて、インストールおよび使用できるブランチが決定されます。

### <a name="software-assurance-and-the-current-branch"></a>ソフトウェア アシュアランスと Current Branch

Configuration Manager の Current Branch をご使用いただく権限は、次の方法で取得できます。

- **System Center:** System Center Standard または Datacenter のライセンスに対して SA が有効になっているお客様は、Configuration Manager の Current Branch オプションをインストールしてご使用いただけます。

- **System Center Configuration Manager:** Configuration Manager のライセンスまたは同等のサブスクリプション権限に対して SA が有効になっている客様は、Configuration Manager の Current Branch オプションをインストールしてご使用いただけます。

2016 年 10 月 1 日以降、Configuration Manager のライセンスまたは同等のサブスクリプション権限に対して SA が有効になっているお客様の場合:

- Current Branch をインストールしてご使用いただけます。
- SA またはサブスクリプションが期限切れになった場合は、Current Branch を再インストールしていただく必要があります。

### <a name="software-assurance-and-the-ltsb"></a>ソフトウェア アシュアランスと LTSB

2016 年 10 月 1 日以降、Configuration Manager のライセンスまたは同等のサブスクリプション権限に対して SA が有効になっているお客様の場合:

- LTSB をインストールしてを使用することができます。 Configuration Manager に対して永続的な権利をお持ちのお客様、または SA またはサブスクリプションが期限切れになったお客様は、期限切れになった時点で最新のバージョンである Configuration Manager LTSB をインストールできます。

LTSB は、Current Branch バージョン 1606 をベースにしており、次の制限があります。

- Current Branch から LTSB への変換はサポートされていません。 現在 Current Branch サイトをお持ちの場合も、新しいサイトとして LTSB をインストールしていただく必要があります。  

- LTSB では、Current Branch のすべての機能がサポートされているわけではありません。 詳細については、[Long-Term Servicing Branch の概要](introduction-to-the-ltsb.md)に関するページをご覧ください。 制限事項の例としては、機能セットの制限、アップグレード オプションの制限、製品サポート ライフサイクルの分離などがあります。  

### <a name="software-assurance-expiration-date"></a>ソフトウェア アシュアランスの有効期限

2016 年 10 月リリースのバージョン 1606 基準メディア以降、Configuration Manager に対してソフトウェア アシュアランス契約の有効期限の日付を指定することができます。 **ソフトウェア アシュアランスの有効期限**は、便利なリマインダーとしてご利用いただける省略可能な値です。 Configuration Manager セットアップの実行時に、または後ほど Configuration Manager コンソール内から、これを追加できます。

> [!NOTE]
> お客様が指定した有効期限の日付が Microsoft によって検証されることはありません。また、ライセンスの検証にこの日付が使用されることもありません。 これは、お客様の有効期限のリマインダーとしてご使用ください。 Configuration Manager によってオンラインで提供される新しいソフトウェア更新プログラムが定期的にチェックされる場合、この値は便利です。 このような追加の更新プログラムを使用する資格を得るには、お客様のソフトウェア アシュアランス ライセンスが最新の状態になっている必要があります。

#### <a name="to-specify-the-software-assurance-expiration-date"></a>ソフトウェア アシュアランスの有効期限を指定するには

- Configuration Manager メディアからセットアップを実行する場合は、セットアップ ウィザードの **[プロダクト キー]** ページでその値を指定します。

- Configuration Manager コンソールの **[階層設定]** で、 **[ライセンス]** タブ上の値を指定します。


## <a name="licensing-resources"></a>ライセンスに関するリソース

製品のライセンスについてさらに詳しく学習する場合は、次のリソースをご利用ください。

### <a name="microsoft-volume-licensing-service-center-vlsc"></a>Microsoft ボリューム ライセンス サービス センター (VLSC)

- [VLSC の概要](https://www.microsoft.com/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Microsoft ボリューム ライセンスでの製品の使用条件](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1)

- ボリューム ライセンスをお持ちのお客様は、ライセンスの概要を[ボリューム ライセンス サービス センター](https://www.microsoft.com/Licensing/servicecenter/default.aspx)で確認できます。 **[ライセンス]** メニューに移動して、 **[ライセンスの概要]** を選択します。

### <a name="vlsc-videos"></a>VLSC ビデオ

- VLSC のしくみに関するトレーニング用ビデオをご覧いただく場合は、「[マイクロソフト ボリューム ライセンス サービス センター (VLSC) に関するトレーニングとリソース](https://www.microsoft.com/licensing/existing-customer/vlsc-training-and-resources)」に移動して **[VLSC デモビデオ]** を選択してください。

- [有効なソフトウェア アシュアランス契約を検索する場所について](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0) (43 秒から)  

- [VLSC のアクセス許可を取得する方法](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4) VLSC の読み取りおよび書き込みのアクセス許可は、組織内の他のユーザーに委任することができます。
