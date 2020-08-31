---
title: Windows の自動操縦更新
ms.reviewer: ''
manager: laurawi
description: Windows の自動操縦更新
keywords: 自動操縦、更新、Windows 10
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: a677dec0d722f0ef17a8c16248a41dea1b0be947
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068122"
---
# <a name="windows-autopilot-update"></a>Windows の自動操縦更新

**適用対象**

- Windows 10 バージョン 1903

Windows 自動操縦更新プログラムによって、組織の自動操縦用デバイスに最新の自動操縦機能と修正プログラムがインストールされます。 デバイスは、最新の Windows OS バージョンには移動されません。 自動操縦更新を使用すると、デバイスの現在の OS バージョンを維持しながら、新しい自動操縦機能やバグ修正の恩恵を受けることができます。

Windows 自動操縦更新プロセスは、重要な [Windows ゼロデイパッチ (ZDP) の更新](/windows-hardware/customize/desktop/windows-updates-during-oobe) チェック後に行われます。 更新プロセス中、デバイスは新しい自動操縦更新プログラムの Windows Update を確認します。 自動操縦更新プログラムが利用可能な場合、デバイスは更新プログラムをダウンロードしてインストールし、自動的に再起動します。 次の例を参照してください。

 ![自動操縦更新プログラム1](images/update1.png)<br>
 ![自動操縦更新2](images/update2.png)<br>
 ![自動操縦用更新プログラム3](images/update3.png)

次の図は、windows 自動操縦更新ノードを使用した、既定のエクスペリエンス (OOBE) 中の一般的な Windows 自動操縦展開オーケストレーションを示しています。

 ![自動操縦更新フロー](images/update-flow.png)

## <a name="release-cadence"></a>リリース サイクル

- 自動操縦更新プログラムが利用可能な場合、通常は、その月の第4火曜日にリリースされます。 例外が発生した場合は、別の週に更新プログラムがリリースされる可能性があります。
- サポート技術情報 (KB) の記事も公開され、更新プログラムに含まれている変更を文書化することができます。

リリース済みの更新プログラムの一覧については、「 [自動操縦の更新履歴](windows-autopilot-whats-new.md#windows-autopilot-update-history)」を参照してください。

## <a name="see-also"></a>関連項目

[OOBE 中の Windows Update](/windows-hardware/customize/desktop/windows-updates-during-oobe)<br>
[Windows 自動操縦の新機能](windows-autopilot-whats-new.md)<br>