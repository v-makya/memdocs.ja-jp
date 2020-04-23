---
title: OS 展開のユーザー エクスペリエンス
titleSuffix: Configuration Manager
description: Configuration Manager でのオペレーティング システム展開のタスク シーケンスの進行状況やメディア ウィザードなどのユーザー エクスペリエンスについて説明します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58849e40-30d5-4153-84b3-ca4af3a4f09d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5f92e76047a70f6d86406b1a364603163d902e62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703220"
---
# <a name="user-experiences-for-os-deployment"></a>OS 展開のユーザー エクスペリエンス

*適用対象:Configuration Manager (Current Branch)*

[タスク シーケンスを展開](../deploy-use/deploy-a-task-sequence.md)した後、シナリオによっては、ユーザーが展開と対話するためのさまざまな方法があります。 この記事では、OS の展開に関する主なユーザー エクスペリエンスと、それらを構成する方法について説明します。

- 影響の大きい展開に対するソフトウェア センターのユーザー通知
- PXE ブート エクスペリエンスの例
- メディアからのタスク シーケンス ウィザード
- タスク シーケンスの実行時の進行状況ウィンドウ
- タスク シーケンスが失敗したときのエラー ウィンドウ

## <a name="software-center"></a>ソフトウェア センター

影響の大きい展開の場合は、ソフトウェア センターに表示されるメッセージをカスタマイズできます。 ユーザーがソフトウェア センターで OS の展開を開くと、次のウィンドウのようなメッセージが表示されます。

![ソフトウェア センターからのエンドユーザーに対するカスタマイズされたタスク シーケンス通知](../media/user-notification-enduser.png)

このウィンドウのメッセージをカスタマイズする方法の詳細については、「[危険度の高い展開のカスタム通知を作成する](../deploy-use/manage-task-sequences-to-automate-tasks.md#create-a-custom-notification-for-high-risk-deployments)」を参照してください。

ウィンドウの上部にある組織名をカスタマイズすることもできます。 (上記の例では、既定値である `IT Organization` が示されています)。 **[コンピューター エージェント]** グループで **[組織名]** クライアント設定を変更します。 詳細については、「[クライアント設定について](../../core/clients/deploy/about-client-settings.md#computer-agent)」を参照してください。

<!--
optional vs required
**Allow user to interact** on required deployment?
-->

詳細については、[ソフトウェア センターを使用したネットワーク経由での Windows の展開](../deploy-use/use-software-center-to-deploy-windows-over-the-network.md)に関する記事を参照してください。

## <a name="pxe"></a>PXE

PXE のエクスペリエンスは、ハードウェア モデルによって異なります。 ネットワークに対して起動するために、UEFI ベースのデバイスでは通常 `Enter` キーが使用され、BIOS ベースのデバイスでは `F12` キーが使用されます。

次の例は、Hyper-V Gen1 (BIOS) PXE のエクスペリエンスを示しています。

![Hyper-V 仮想マシンからの BIOS PXE 画面の例](media/hyperv-pxe.png)

デバイスは、PXE を使用して正常に起動された後、起動可能なメディアと同様に動作します。 詳細については、「[タスク シーケンス ウィザード](#task-sequence-wizard)」の次のセクションを参照してください。

詳細については、「[PXE を使用したネットワーク経由での Windows の展開](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)」を参照してください。

> [!WARNING]
> PXE 展開を使用し、最初のブート デバイスとしてネットワーク アダプターを使用するデバイス ハードウェアを構成すると、これらのデバイスでは、ユーザーの操作なしで OS 展開のタスク シーケンスを自動的に開始できます。 展開の検証では、この構成は管理されません。 この構成により、プロセスが簡略化され、ユーザーの操作が減少する可能性がありますが、デバイスが誤って再イメージ化されるリスクが高くなります。

## <a name="task-sequence-wizard"></a>タスク シーケンス ウィザード

[タスク シーケンス メディア](../deploy-use/create-task-sequence-media.md)を使用する場合は、タスク シーケンス ウィザードが実行され、プロセスが示されます。

### <a name="welcome-to-the-task-sequence-wizard"></a>タスク シーケンス ウィザードへようこそ

![タスク シーケンス ウィザードのメイン ページのスクリーンショット](media/welcome-task-sequence-wizard.png)

- メディアをパスワードで保護している場合、ユーザーはこのようこそページにパスワードを入力する必要があります。

- 静的 IP アドレスまたはその他のカスタム ネットワーク設定を指定するには、 **[ネットワーク設定の構成]** を選択します。 それ以外の場合、デバイスは既定で DHCP を使用します。

- ネットワークにプロキシが必要な場合は **[プロキシ設定の構成]** を選択します。

### <a name="select-a-task-sequence-to-run"></a>実行するタスク シーケンスの選択

複数のタスク シーケンスをデバイスに展開すると、このページが表示され、タスク シーケンスを選択できます。 タスク シーケンスの名前と説明は、必ずユーザーが理解できるようにしてください。

![タスク シーケンス ウィザードのタスク シーケンス選択ページのスクリーンショット](media/task-sequence-wizard-select.png)

### <a name="edit-task-sequence-variables"></a>タスク シーケンス変数の編集

タスク シーケンス変数に空の値が含まれている場合は、ウィザードに変数の値を編集するためのページが表示されます。

![タスク シーケンス ウィザードのタスク シーケンス変数の編集ページのスクリーンショット](media/task-sequence-wizard-variables.png)

## <a name="prestart-commands"></a>起動前コマンド

タスク シーケンス メディアまたはブート イメージをカスタマイズして、起動前コマンドを実行できます。 起動前コマンドは、タスク シーケンスが開始される前に実行されます。 一般的なアクションには次のようなものがあります。

- コンピューター名などの動的な値の入力をユーザーに求める
- ネットワーク構成を指定する
- ユーザーとデバイスのアフィニティを設定する

起動前コマンドは、スクリプトまたはプログラムを使用して指定するコマンド ラインです。 ユーザー エクスペリエンスは、そのスクリプトまたはプログラムに固有のものです。

詳細については、以下の記事を参照してください。

- [タスク シーケンス メディアの起動前コマンド](prestart-commands-for-task-sequence-media.md)
- [ブート イメージの管理](../get-started/manage-boot-images.md#customization)
- [タスク シーケンス メディア](../deploy-use/create-task-sequence-media.md)

## <a name="task-sequence-progress"></a>タスク シーケンスの進行状況

タスク シーケンスが実行されると、 **[インストールの進行状況]** ウィンドウが表示されます。

![タスク シーケンスの進行状況ウィンドウの例](media/task-sequence-progress.png)

- このウィンドウは常に手前に表示されます。移動することはできますが、閉じたり最小化したりすることはできません。

- ウィンドウの上部にある組織名はカスタマイズすることができます。 (上記の例では、既定値である `IT Organization` が示されています)。 **[コンピューター エージェント]** グループで **[組織名]** クライアント設定を変更します。 詳細については、「[クライアント設定について](../../core/clients/deploy/about-client-settings.md#computer-agent)」を参照してください。

    > [!TIP]
    > タスク シーケンスでは、この値が読み取り専用の変数 [_SMSTSOrgName](task-sequence-variables.md#SMSTSOrgName) に格納されます。

- 小見出しはカスタマイズできます。 (上記の例では、既定値である `Running: <task sequence name>` が示されています)。タスク シーケンスのプロパティで、進行状況の通知テキストに**カスタム テキストを使用する**オプションを選択します。 最大 255 文字を使用できます。

- **実行中の処理**:最初の行には、現在のタスク シーケンス ステップの名前が表示されます。 その下の進行状況バーには、タスク シーケンスの全体的な完了状況が表示されます。

- 2 行目は、より詳細な進行状況を提供する一部のステップについてのみ表示されます。

- タスク シーケンス変数 [TSDisableProgressUI](task-sequence-variables.md#TSDisableProgressUI) を使用して、タスク シーケンスで進行状況を表示するタイミングを制御します。

    進行状況ウィンドウを完全に無効にするには、タスク シーケンス展開の **ユーザー エクスペリエンス** ページの **タスク シーケンスの進行状況の表示** オプションを無効にします。

バージョン 2002 以降では、タスク シーケンスの進行状況ウィンドウには次の改善が取り込まれています。<!--5932692-->

- 現在のステップ番号、ステップの合計数、完了率を表示します

- 組織名を 1 行により適切に表示するためのより広いスペースを確保できるようにウィンドウの幅を大きくしました

![タスク シーケンスの進行状況ウィンドウの例](media/2356386-task-sequence-progress.png)

既定では、タスク シーケンスの進行状況ウィンドウでは、既存のテキストが使用されます。 変更を行わない場合、動作はバージョン 1910 以前と同じです。 新しい進行状況の情報を表示するには、タスク シーケンス変数 [TSProgressInfoLevel](task-sequence-variables.md#TSProgressInfoLevel) を指定します。

カウントと完了率は、一般的なガイダンスのみを目的として使用されます。 これらの値は、タスク シーケンスのステップの合計数に基づいています。 タスク シーケンス ロジックに基づいて条件付きで実行されるステップを含むより複雑なタスク シーケンスの場合、進行状況は非線形となる可能性があります。

合計ステップ数に、タスク シーケンスの次の項目は含まれません。

- グループ。 この項目は他のステップのコンテナーであり、ステップ自体ではありません。

- **[タスク シーケンスの実行]** ステップのインスタンス。 このステップは他のステップのコンテナーです。

- 明示的に無効にしたステップ。 無効にされたステップはタスク シーケンス中に実行されません。

    > [!NOTE]
    > 無効なグループ内の有効なステップは、引き続き合計数に含まれます。

## <a name="task-sequence-error"></a>タスク シーケンス エラー

タスク シーケンスが失敗すると、 **[タスク シーケンス エラー]** ウィンドウが表示されます。

![[タスク シーケンス エラー] ウィンドウの例](media/task-sequence-error.png)

- タスク シーケンスの進行状況ウィンドウと同様に、見出しの情報をカスタマイズできます。

- ここには、タスク シーケンスの名前、エラー コード、およびユーザー向けの一般的なメッセージが表示されます。 例: `Task sequence: Upgrade to Windows 10 Enterprise has failed with the error code (0x80004005). For more information, contact your system administrator or helpdesk operator.`

- タイムアウト期間が経過すると、ウィンドウは自動的に閉じます。 既定では、タイムアウトは 15 分です。 この値は、タスク シーケンス変数 [SMSTSErrorDialogTimeout](task-sequence-variables.md#SMSTSErrorDialogTimeout) でカスタマイズできます。
