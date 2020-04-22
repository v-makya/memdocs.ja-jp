---
title: コレクションのベスト プラクティス
titleSuffix: Configuration Manager
description: Configuration Manager のコレクションのベスト プラクティスを示します。
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7e3e7b108ef48b218ee9d6a31064606b40a68fea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695240"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Configuration Manager のコレクションのベスト プラクティス

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager のコレクションに関する以下のベスト プラクティスを使用してください。  

## <a name="dont-use-incremental-updates-with-many-collections"></a><a name="bkmk_incremental"></a> 多数のコレクションに対して増分更新を使用しない

**[このコレクションで増分更新を使用する]** オプションを多数のコレクションに対して有効にすると、この構成が評価の遅延を引き起こす可能性があります。 しきい値は、階層内では約 200 コレクションです。 正確な数は、次の要因によります。  

- コレクションの総数  

- 階層内で、リソースが新しく追加または変更される頻度  

- 階層内のクライアント数  

- 階層内のコレクション メンバーシップ規則の複雑さ  

## <a name="maintenance-window-size-for-software-updates"></a>ソフトウェア更新プログラムのメンテナンス期間の長さ

デバイス コレクションのメンテナンス期間を構成して、Configuration Manager がソフトウェアをそれらのデバイスにインストールできる時間を制限することができます。 メンテナンス期間の構成で十分な時間が確保されていない場合、クライアントは重要なソフトウェア更新プログラムをインストールできない可能性があり、その結果、ソフトウェア更新プログラムによって緩和される攻撃に対してクライアントが脆弱なままになります。

> [!Tip]
> メンテナンス期間を計画するときに注意する必要がある重要な考慮事項は次のとおりです。
>
> - 既定のソフトウェア更新プログラムの最長実行時間は 60 分です。
> - 更新プログラムをインストールできるかどうかが Configuration Manager によって計算される場合、再起動のために、最大実行時間に 5 分が加えられます。
> - メンテナンス期間の残りの期間は、ソフトウェア更新プログラムの最長実行時間に 5 分を加えた時間よりも長くする必要があります。
