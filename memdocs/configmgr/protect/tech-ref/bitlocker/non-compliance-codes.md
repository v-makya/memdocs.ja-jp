---
title: 非コンプライアンス コード
titleSuffix: Configuration Manager
description: BitLocker ポリシーに準拠していない Configuration Manager クライアントからの使用可能なコードのテクニカル リファレンス
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6c28fa29-fc97-49ef-9fc3-cb062bdba908
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e8ee130929605f8087eb7fbef55e8a27618c3aed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705960"
---
# <a name="non-compliance-codes"></a>非コンプライアンス コード

*適用対象:Configuration Manager (Current Branch)*

<!--3601034-->

クライアントの WMI は、次の準拠していないコードを提供します。 また、特定のデバイスが準拠していないとして報告する理由についても説明します。

WMI を表示するには、さまざまな方法があります。 たとえば、次の PowerShell コマンドを使用します。

``` PowerShell
(Get-WmiObject -Class mbam_Volume -Namespace root\microsoft\mbam).ReasonsForNoncompliance
```

> [!TIP]
> デバイスが準拠している場合、このコマンドは何も返しません。
>
> また、このクラスの `Compliant` 属性を確認することもできます。これは、デバイスが準拠している場合は `1` です。

|非コンプライアンス コード|コンプライアンス違反の理由|
|--- |--- |
|0|AES 256 ではない暗号強度。|
|1|BitLocker ポリシーによって、このボリュームを暗号化するように求められていますが、暗号化されていません。|
|2|BitLocker ポリシーによって、このボリュームを暗号化*しない*ように求められていますが、暗号化されています。|
|3|BitLocker ポリシーによって、このボリュームで TPM 保護機能を使用するように求められていますが、使用されていません。|
|4|BitLocker ポリシーによって、このボリュームで TPM + PIN 保護機能を使用するように求められていますが、使用されていません。|
|5|BitLocker ポリシーでは、TPM 以外のマシンを準拠として報告することは許可されていません。|
|6|ボリュームには TPM 保護機能がありますが、TPM が表示されていません。|
|7|BitLocker ポリシーによって、このボリュームでパスワード保護機能を使用するように求められていますが、それがありません。|
|8|BitLocker ポリシーによって、このボリュームでパスワード保護機能を使用*しない*ように求められていますが、使用されています。|
|9|BitLocker ポリシーによって、このボリュームで自動ロック解除保護機能を使用するように求められていますが、それがありません。|
|10|BitLocker ポリシーによって、このボリュームで自動ロック解除保護機能を使用*しない*ように求められていますが、使用されています。|
|11|BitLocker がポリシーの競合を検出したため、このボリュームを準拠として報告できません。|
|12|OS ボリュームを暗号化するためにシステム ボリュームが必要ですが、存在しません。|
|13|ボリュームの保護が一時停止されています。|
|14|OS ボリュームが暗号化されていない限り、自動ロック解除保護機能は安全ではありません。|
|15|ポリシーによって、暗号の最小強度が XTS-AES-128 ビットであることが求められていますが、実際の暗号強度はそれよりも弱いものになっています。|
|16|ポリシーによって、暗号の最小強度が XTS-AES-256 ビットであることが求められていますが、実際の暗号強度はそれよりも弱いものになっています。|
