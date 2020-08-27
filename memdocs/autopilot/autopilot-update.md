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
ms.openlocfilehash: 723d81655e0d0c3101cf199057e1c4dbba8e2925
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908418"
---
# <a name="windows-autopilot-update"></a>Windows の自動操縦更新

**適用対象**

-   Windows 10 バージョン 1903

Windows 自動操縦の更新プログラムを使用すると、最新の自動操縦機能と重大な問題の修正を取得できます。最新の Windows OS バージョンに移行する必要はありません。 自動操縦の更新により、組織は現在の OS バージョンを維持しながら、新しい自動操縦機能やバグ修正の恩恵を受けることができます。
 
自動操縦の展開プロセス中に、Windows の自動操縦更新プログラムは、重要な [Windows ゼロデイ修正プログラム (ZDP) の更新](/windows-hardware/customize/desktop/windows-updates-during-oobe) チェック後に新しいノードとして追加されました。 更新プロセス中に、Windows の自動操縦デバイスは Windows Update に接続して、新しい自動操縦更新プログラムがあるかどうかを確認します。  自動操縦更新プログラムが利用可能な場合、デバイスは更新プログラムをダウンロードしてインストールし、自動的に再起動します。 次の例を参照してください。

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