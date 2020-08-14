---
title: BIOS を UEFI に変換する
titleSuffix: Configuration Manager
description: UEFI への移行用に FAT32 パーティションを準備するために、OS 展開のタスク シーケンスをカスタマイズする方法について説明します。
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 761270fe9419330e2d60d0483554ee6c932c1b26
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124887"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>BIOS からUEFI への変換を管理するためのタスク シーケンス手順

Windows 10 では、UEFI 対応デバイスを必要とする新しいセキュリティ機能が多数提供されます。 UEFI がサポートされている新しい Windows デバイスであっても、従来の BIOS が使用されている場合があります。 これまで、デバイスを UEFI に変換するには、各デバイスに移動し、ハード ディスクのパーティションを再分割して、ファームウェアを再構成する必要がありました。

Configuration Manager を使用すると、次の作業を自動的に行うことができます。

- BIOS から UEFI への変換のためにハード ドライブを準備する
- インプレース アップグレード プロセスの一部として BIOS から UEFI に変換する
- ハードウェア インベントリの一部として UEFI の情報を収集する

## <a name="hardware-inventory-collects-uefi-information"></a>ハードウェア インベントリでの UEFI 情報の収集

ハードウェア インベントリ クラス (**SMS_Firmware**) とプロパティ (**UEFI**) は、コンピューターが UEFI モードで起動しているかどうかを判別するのに役立ちます。 コンピューターが UEFI モードで起動している場合、**UEFI** プロパティは **TRUE** に設定されています。 ハードウェア インベントリでは、このクラスが既定で有効になります。 ハードウェア インベントリの詳細については、「[ハードウェア インベントリを構成する方法](../../core/clients/manage/inventory/configure-hardware-inventory.md)」を参照してください。

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive"></a>ハード ドライブを準備するためのカスタム タスク シーケンスを作成する

**TSUEFIDrive** 変数を使用して、OS 展開のタスク シーケンスをカスタマイズできます。 **コンピューターの再起動**ステップで、ハード ドライブの FAT32 パーティションを UEFI への移行用に準備します。 以下の手順では、このアクションを行うためのタスク シーケンスのステップを作成する方法の例を示します。

### <a name="prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>UEFI への変換用に FAT32 パーティションを準備する

OS をインストールする既存のタスク シーケンスに、BIOS から UEFI への変換を行うステップを含む新しいグループを追加します。

1. ファイルと設定をキャプチャするステップの後、OS をインストールする手順の前に、新しいタスク シーケンス グループを作成します。 たとえば、 **[キャプチャ ファイルと設定]** グループの後に、 **[BIOS-to-UEFI]** という名前のグループを作成します。

1. 新しいグループの **[オプション]** タブで、新しいタスク シーケンス変数を条件として追加します。 **_SMSTSBootUEFI not equals "true"** に設定します。 この条件により、タスク シーケンスではこれらのステップが BIOS デバイスに対してだけ実行されます。

    :::image type="content" source="media/bios-to-uefi-group.png" alt-text="BIOS から UEFI へのグループの条件":::

1. 新しいグループの下に、 **[コンピューターの再起動]** タスク シーケンスのステップを追加します。 **[再起動後に実行するものを指定してください]** で、 **[このタスク シーケンスに割り当てられているブート イメージ]** を選択します。 この操作により、Windows PE でコンピューターが再起動されます。

1. **[オプション]** タブで、タスク シーケンス変数を条件として追加します。 **_SMSTSInWinPE equals "false"** に設定します。 この条件により、タスク シーケンスでは、コンピューターが既に Windows PE にある場合、このステップは実行されません。

    :::image type="content" source="media/restart-in-windows-pe.png" alt-text="コンピューター再起動ステップでの条件":::

1. ファームウェアを BIOS から UEFI に変換する OEM ツールを起動するステップを追加します。 このステップは通常、OEM ツールを実行するコマンドを含む**コマンド ラインの実行**です。

1. **ディスクのフォーマットとパーティション作成** タスク シーケンス ステップを追加します。 このステップでは、次のオプションを構成します。

    1. OS をインストールする前に、UEFI に変換するための FAT32 パーティションを作成します。 **[ディスクの種類]** で **[GPT]** を選択します。

        :::image type="content" source="media/format-and-partition-disk.png" alt-text="ディスクのフォーマットとパーティション作成ステップの構成":::

    1. FAT32 パーティションのプロパティに移動します。 **[変数]** フィールドに「`TSUEFIDrive`」と入力します。 タスク シーケンスでこの変数が検出されると、コンピューターを再起動する前に、UEFI 移行のためのパーティションが準備されます。

        :::image type="content" source="media/partition-properties.png" alt-text="FAT32 パーティションのプロパティの構成":::

    1. タスク シーケンスでその状態の保存とログ ファイルの格納に使用される NTFS パーティションを作成します。

1. 別の**コンピューターの再起動**タスク シーケンスのステップを追加します。 **[再起動後に実行するものを指定してください]** で、 **[このタスク シーケンスに割り当てられているブート イメージ]** をオンにして、Windows PE でコンピューターを起動します。

    > [!TIP]
    > 既定では、EFI パーティションのサイズは 500 MB です。 環境によっては、ブート イメージが大きすぎてこのパーティションに格納できない場合があります。 この問題を回避するには、EFI パーティションのサイズを増やします。 たとえば、1 GB に設定します。<!-- SCCMDocs#1024 -->

## <a name="convert-from-bios-to-uefi-during-in-place-upgrade"></a><a name="bkmk_ipu"></a> インプレース アップグレードの間に BIOS から UEFI に変換する

Windows 10 には、簡単な変換ツール **MBR2GPT.EXE** が含まれています。 それを使用すると、UEFI 対応ハードウェア用のハード ディスクのパーティションを再分割するプロセスが自動化されます。 Windows 10 へのインプレース アップグレード プロセスに、変換ツールを統合することができます。 このツールと、アップグレード タスク シーケンス、およびファームウェアを BIOS から UEFI に変換する OEM ツールを組み合わせます。

### <a name="requirements"></a>要件

- サポートされているバージョンの Windows 10
- UEFI をサポートするコンピューター
- コンピューターのファームウェアを BIOS から UEFI に変換する OEM ツール

### <a name="process-to-convert-from-bios-to-uefi-during-an-in-place-upgrade-task-sequence"></a>インプレース アップグレード タスク シーケンスの間に BIOS から UEFI に変換するプロセス

1. [OS をアップグレードするタスク シーケンスの作成](create-a-task-sequence-to-upgrade-an-operating-system.md)

1. タスク シーケンスを編集します。 **後処理**グループで、次の変更を行います。

    1. **コマンド ラインの実行**ステップを追加します。 MBR2GPT ツールのコマンド ラインを指定します。 完全な OS で実行されている場合は、データを変更または削除することなく、ディスクを MBR から GPT に変換するように構成します。 **コマンド ライン**で次のコマンドを入力します: `MBR2GPT.exe /convert /disk:0 /AllowFullOS`

    > [!TIP]
    > 完全な OS ではなく、Windows PE で MBR2GPT.EXE ツールを実行することもできます。 MBR2GPT.EXE ツールを実行するステップの前に、コンピューターを Windows PE で再起動するステップを追加します。 次に、コマンド ラインから **/AllowFullOS** オプションを削除します。

    ツールと使用可能なオプションの詳細については、「[MBR2GPT.EXE](https://docs.microsoft.com/windows/deployment/mbr-to-gpt)」を参照してください。

    1. ファームウェアを BIOS から UEFI に変換する OEM ツールを実行するステップを追加します。 このステップは通常、OEM ツールを実行するコマンド ラインを含む**コマンド ラインの実行**です。

    1. **コンピューターの再起動**ステップを追加し、 **[現在インストールされている既定のオペレーティング システム]** を選択します。

1. タスク シーケンスを展開します。
