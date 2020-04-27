---
title: BIOS からUEFI への変換を管理するためのタスク シーケンス手順
titleSuffix: Configuration Manager
description: UEFI への移行用に FAT32 パーティションを準備するために、オペレーティング システム展開タスク シーケンスをカスタマイズする方法について説明します。
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9183efd622cb425027500d3fe51ed7b86d3a94e4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079367"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>BIOS からUEFI への変換を管理するためのタスク シーケンス手順
Windows 10 では、UEFI 対応デバイスを必要とする新しいセキュリティ機能が多数提供されます。 最新の Windows PC では、UEFI がサポートされていても、従来の BIOS が使用されている場合があります。 デバイスを UEFI に変換する場合、各 PC に移動して、ハード ディスクのパーティションを再分割し、ファームウェアを再構成する必要がありました。 Configuration Manager でタスク シーケンスを使用すれば、BIOS から UEFI への変換のためにハード ドライブを準備し、インプレース アップグレード プロセスの一環として BIOS から UEFI への変換を行い、ハードウェア インベントリの一部として UEFI 情報を収集することができます。

## <a name="hardware-inventory-collects-uefi-information"></a>ハードウェア インベントリでの UEFI 情報の収集
バージョン 1702 以降では、新しいハードウェア インベントリ クラス (**SMS_Firmware**) とプロパティ (**UEFI**) を使用することができ、コンピューターが UEFI モードで起動しているかどうかを判別するのに役立ちます。 コンピューターが UEFI モードで起動している場合、**UEFI** プロパティは **TRUE** に設定されています。 これはハードウェア インベントリでは既定で有効になっています。 ハードウェア インベントリの詳細については、「[ハードウェア インベントリを構成する方法](../../core/clients/manage/inventory/configure-hardware-inventory.md)」を参照してください。

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive-for-bios-to-uefi-conversion"></a>カスタム タスク シーケンスを作成して BIOS から UEFI への変換のためにハード ドライブを準備する
Configuration Manager バージョン 1610 以降では、**コンピューターの再起動**の手順で、UEFI への移行に備えてハード ドライブに FAT32 パーティションを準備するため、新しい変数 TSUEFIDrive を使って、オペレーティング システムの展開タスク シーケンスをカスタマイズできるようになりました。 次の手順では、タスク シーケンスのステップを作成して BIOS からUEFI への変換のためにハード ドライブを準備する方法の例を示します。

### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>UEFI への変換のために FAT32 パーティションを準備するには:
オペレーティング システムをインストールする既存のタスク シーケンスでは、BIOS からUEFI への変換を実行する手順を含む新しいグループを追加します。

1. ファイルと設定をキャプチャする手順を完了したら、新しいタスク シーケンス グループを作成してから、オペレーティング システムをインストールするステップを実行します。 たとえば、 **[キャプチャ ファイルと設定]** グループの後に、 **[BIOS-to-UEFI]** という名前のグループを作成します。
2. 新しいグループの **[オプション]** タブで、新しいタスク シーケンス変数を条件 **_SMSTSBootUEFI** is **not equal** to **true** (_SMSTSBootUEFI は true と等しくない) として追加します。 これにより、コンピューターが既に UEFI モードになっている場合に、グループのステップが実行されないようにします。

   ![BIOS-to-UEFI グループ](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. 新しいグループの下に、 **[コンピューターの再起動]** タスク シーケンスのステップを追加します。 **[再起動後に実行するものを指定してください]** で、 **[このタスク シーケンスに割り当てられているブート イメージ]** をオンにして、Windows PE でコンピューターを起動します。  
4. **[オプション]** タブで、タスク シーケンス変数を条件 ( **_SMSTSInWinPE equals false**) として追加します。 これにより、コンピューターが既に Windows PE にある場合に、このステップが実行されないようにします。

   ![コンピューターの再起動のステップ](../../core/get-started/media/restart-in-windows-pe.png)
5. ファームウェアを BIOS から UEFI に変換する OEM ツールを起動するステップを追加します。 これは一般に、OEM ツールを起動するコマンド ラインを含む**コマンドラインの実行**タスク シーケンスのステップになります。
6. ハード ドライブをパーティションに分割してフォーマットするディスクのフォーマットとパーティション作成タスク シーケンスのステップを追加します。 このステップでは、次の操作を行います。
   1. オペレーティング システムをインストールする前に、UEFI に変換される FAT32 パーティションを作成します。 **[ディスクの種類]** で **[GPT]** を選びます。
    ![ディスクのフォーマットとパーティション作成のステップ](../media/format-and-partition-disk.png)
   2. FAT32 パーティションのプロパティに移動します。 **[変数]** フィールドに「**TSUEFIDrive**」を入力します。 タスク シーケンスでこの変数を検出すると、コンピューターを再起動する前に UEFI 移行のための準備をします。
    ![パーティションのプロパティ](../../core/get-started/media/partition-properties.png)
   3. タスク シーケンス エンジンがその状態を保存し、ログ ファイルを保存するために使用する NTFS パーティションを作成します。
7. **コンピューターの再起動**タスク シーケンスのステップを追加します。 **[再起動後に実行するものを指定してください]** で、 **[このタスク シーケンスに割り当てられているブート イメージ]** をオンにして、Windows PE でコンピューターを起動します。  

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>インプレース アップグレード時に BIOS から UEFI に変換する
Windows 10 Creators Update では、EFI 対応ハードウェアのハード ディスクのパーティションを再分割するプロセスを自動化する簡単な変換ツールが導入され、変換ツールは Windows 7 から Windows 10 へのインプレース アップグレード プロセスに統合されます。 このツールをオペレーティング システムのアップグレード タスク シーケンスと、ファームウェアを BIOS から UEFI に変換する OEM ツールと組み合わせて使用する場合、Windows 10 Creators Update へのインプレース アップグレード時にコンピューターを BIOS から UEFI に変換することができます。

**要件**:
- Windows 10 Creators Update
- UEFI をサポートするコンピューター
- コンピューターのファームウェアを BIOS から UEFI に変換する OEM ツール

### <a name="to-convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>インプレース アップグレード時に BIOS から UEFI に変換するには
1. Windows 10 Creators Update へのインプレース アップグレードを実行するオペレーティング システムのアップグレード タスク シーケンスを作成します。
2. タスク シーケンスを編集します。 **後処理グループ**で、次のタスク シーケンス ステップを追加します。
   1. [全般] から、**コマンド ラインを実行**ステップを追加します。 ディスクのデータを変更または削除せずに、ディスクを MBR から GPT に変換する MBR2GPT ツールのコマンド ラインを追加します。 コマンドラインで、次を入力します。**MBR2GPT /convert /disk:0 /AllowFullOS**. フル オペレーティング システムではなく、Windows PE で MBR2GPT.EXE ツールを実行することもできます。 その場合、MBR2GPT.EXE ツールを実行するステップの前にコンピューターを再起動するステップを WinPE に追加し、コマンド ラインから /AllowFullOS オプションを削除します。 ツールと使用可能なオプションの詳細については、「[MBR2GPT.EXE](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt)」を参照してください。
   2. ファームウェアを BIOS から UEFI に変換する OEM ツールを起動するステップを追加します。 これは一般に、OEM ツールを起動するコマンド ラインを含むコマンドラインの実行タスク シーケンスのステップになります。
   3. [全般] から、**コンピューターの再起動**ステップを追加します。 [再起動後に実行するものを指定してください] では、 **[現在インストールされている既定のオペレーティング システム]** を選択します。
3. タスク シーケンスを展開します。
