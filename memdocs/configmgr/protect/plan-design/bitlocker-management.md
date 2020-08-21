---
title: BitLocker 管理の計画
titleSuffix: Configuration Manager
description: Configuration Manager を使用して BitLocker ドライブ暗号化を管理する計画を立てます
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a4d8cda2-bc9b-4fb4-aa0d-23c31b4fc60b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8370c3352778fa6bb7c6229beb1c7610c419a86d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129299"
---
# <a name="plan-for-bitlocker-management"></a>BitLocker 管理の計画

*適用対象:Configuration Manager (Current Branch)*

<!-- 3601034 -->

バージョン 1910 以降は、Configuration Manager を使用して、Active Directory に参加しているオンプレミスの Windows クライアント用の BitLocker ドライブ暗号化 (BDE) を管理します。 Azure Active Directory に参加している、またはワークグループのクライアントはサポートされていません。 Configuration Manager には、Microsoft BitLocker Administration and Monitoring (MBAM) の代わりに使用できる完全な BitLocker ライフサイクル管理機能が用意されています。

> [!NOTE]
> Configuration Manager では、このオプション機能は既定で無効です。 この機能は、使用する前に有効にする必要があります。 詳細については、「[Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options)」 (更新プログラムのオプション機能の有効化) を参照してください。  

詳細については、「[BitLocker の概要](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview)」を参照してください。

> [!TIP]
> Microsoft Endpoint Manager クラウド サービスを使用して共同管理されている Windows 10 デバイスの暗号化を管理するには、[**Endpoint Protection** ワークロード](../../comanage/workloads.md#endpoint-protection)を Intune に切り替えます。 Intune の使用方法の詳細については、「[Windows 暗号化](/intune/protect/endpoint-protection-windows-10#windows-encryption)」を参照してください。

## <a name="features"></a>機能

Configuration Manager には、BitLocker ドライブ暗号化用の次の管理機能が用意されています。

### <a name="client-deployment"></a>クライアント展開

Windows 10 または Windows 8.1 が動作しているマネージド Windows デバイスに BitLocker クライアントを展開します

### <a name="manage-encryption-policies"></a>暗号化ポリシーの管理

- 例: ドライブの暗号化と暗号強度を選択し、ユーザーの除外ポリシー、固定データ ドライブの暗号化の設定を構成します。

- デバイスの暗号化に使用するアルゴリズムと、暗号化対象のディスクを決定します。

- デバイスを使用する前に、新しいセキュリティ ポリシーに準拠するようユーザーに強く依頼します。

- デバイスごとに組織のセキュリティ プロファイルをカスタマイズします。

- ユーザーが OS ドライブのロックを解除するときに、OS ドライブのみをロック解除するか、接続されているすべてのドライブをロック解除するかを指定します。

### <a name="compliance-reports"></a>コンプライアンス レポート

次の項目に関する組み込みレポート:

- ボリュームごとまたはデバイスごとの暗号化の状態
- デバイスのプライマリ ユーザー
- 準拠状態
- 非準拠の理由

### <a name="administration-and-monitoring-website"></a>管理と Web サイトの監視

キーのローテーションやその他の BitLocker 関連のサポートなど、キーの回復を支援することを Configuration Manager コンソール以外の組織内の他のペルソナに許可します。 たとえば、ヘルプ デスク管理者は、ユーザーがキーを回復するのを支援できます。

### <a name="user-self-service-portal"></a>ユーザー セルフサービス ポータル

ユーザーは、BitLocker で暗号化されたデバイスのロックを解除するための使い捨てのキーを使用できます。 このキーを使用すると、デバイス用に新しいキーが生成されます。

## <a name="prerequisites"></a>[前提条件]

- BitLocker 管理ポリシーを作成するには、Configuration Manager での**完全な権限を持つ管理者**ロールが必要です。

- BitLocker 回復サービスでは、Configuration Manager クライアントから管理ポイントへのネットワーク全体で回復キーを暗号化するために HTTPS が必要です。 次の 2 つのオプションがあります。

  - 回復サービスをホストする管理ポイント上の IIS Web サイトを HTTPS 対応にします。 このオプションは、Configuration Manager バージョン 2002 にのみ適用されます。<!-- 5925660 -->

  - HTTPS 用の管理ポイントを構成します。 このオプションは、Configuration Manager バージョン 1910 または 2002 に適用されます。

  詳細については、「[回復データの暗号化](../deploy-use/bitlocker/encrypt-recovery-data.md)」をご覧ください。

- BitLocker 回復サービスはデータベース レプリカを使用する管理ポイントにインストールされますが、クライアントは回復キーをエスクローできません。 そのため、BitLocker によってドライブが暗号化されません。 回復サービスを使用するには、レプリカ構成に含まれていない管理ポイントが少なくとも 1 つ必要です。 データベース レプリカを使用する管理ポイント上で、BitLocker 回復サービスを無効にしてください。<!-- 7813149 -->

- BitLocker 管理レポートを使用するには、レポート サービス ポイントのサイト システムの役割をインストールします。 詳しくは、[レポートの構成](../../core/servers/manage/configuring-reporting.md)に関するページをご覧ください。

    > [!NOTE]
    > 管理と監視用 Web サイトから**回復の監査レポート**を機能させる場合は、レポート サービス ポイントをプライマリ サイトでのみ使用してください。

- セルフサービス ポータルまたは管理と監視用 Web サイトを使用するには、Windows サーバーで IIS が実行されている必要があります。 Configuration Manager サイト システムを再利用することも、サイト データベース サーバーに接続されているスタンドアロンの Web サーバーを使用することもできます。 [サイト システム サーバーでサポートされている OS バージョン](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)を使用してください。

    > [!NOTE]
    > プライマリ サイト データベースを含むセルフサービス ポータルおよび管理と監視用 Web サイトのみをインストールしてください。 階層内で、各プライマリ サイトにこれらの Web サイトをインストールします。

- インストール プロセスを開始する前に、セルフサービス ポータルをホストする Web サーバーに [Microsoft ASP.NET MVC 4.0](https://docs.microsoft.com/aspnet/mvc/mvc4) と .NET Framework 3.5 機能をインストールします。 その他の必要な Windows サーバーの役割と機能は、ポータルのインストール プロセス中に自動的にインストールされます。

- ポータルのインストーラー スクリプトを実行するユーザー アカウントには、サイト データベース サーバーに対する SQL **sysadmin** 権限が必要です。 セットアップ プロセス中に、スクリプトによって Web サーバー マシン アカウントのログイン、ユーザー、および SQL の役割の権限が設定されます。 セルフサービス ポータルおよび管理と監視用 Web サイトのセットアップが完了したら、このユーザー アカウントを sysadmin 役割から削除できます。

- BitLocker 管理は仮想マシン (VM) またはサーバー OS ではサポートされていません。 このため、仮想マシンまたは サーバー OS では一部の機能が期待どおりに動作しないことがあります。 たとえば、仮想マシンでは、BitLocker 管理では仮想マシンの固定ドライブの暗号化は開始されません。 仮想マシンの追加の固定ドライブは、暗号化されていない場合でも、準拠として表示されることがあります。

> [!TIP]
> 既定では、**BitLocker の有効化**タスク シーケンス ステップはドライブ上の*使用済み領域*のみを暗号化します。 BitLocker 管理では、*ディスク全体*の暗号化を使用します。 **ディスク全体の暗号化を使用する**オプションを有効にするように、このタスク シーケンス ステップを構成してください。 詳しくは、「[タスク シーケンスのステップ - BitLocker の有効化](../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker)」をご覧ください。

## <a name="next-steps"></a>次のステップ

[回復データ の暗号化](../deploy-use/bitlocker/encrypt-recovery-data.md) (ポリシーを初めて展開する前のオプションの前提条件)

[BitLocker 管理クライアントの展開](../deploy-use/bitlocker/deploy-management-agent.md)
