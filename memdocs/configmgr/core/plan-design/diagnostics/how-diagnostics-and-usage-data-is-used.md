---
title: 診断データの使用
titleSuffix: Configuration Manager
description: Configuration Manager により収集された診断と使用状況データを Microsoft が使用する方法について説明します。
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6a014d60c49b0ff7e10cd74c101294dd002266d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697130"
---
# <a name="how-microsoft-uses-configuration-manager-diagnostics-and-usage-data"></a>Microsoft による Configuration Manager の診断結果と使用状況データの使用方法

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager で収集される診断結果と使用状況データは、製品がどのように動作しているかに関するフィードバックを Microsoft にただちに示しており、今後の更新プログラムの調整に使用されます。 また、運用環境で使用される構成を設計およびテストするために役立つ構成データを Microsoft が確認することもできます。 次に例を示します。

- サイト サーバーで使用されている Windows サーバーのバージョン

- インストール済みの言語パック

- 製品の既定値に対する SQL スキーマのデルタ

このデータによってエンジニアリング チームは、最も一般的な構成を使用した最適なエクスペリエンスを確保できるように今後のテストを計画できます。 このデータは、頻繁なリリース サイクルに対応した迅速な調整と適応を行ううえで非常に重要です。

診断結果と使用状況データがどのように使用されないかということも、同様に重要です。 Microsoft では、このデータを以下のためには使用しません。

- 使用許諾契約に対する顧客の使用状況の比較などのライセンスの監査

- サポート外の製品の監査

- 機能の使用状況や地理的位置情報 (タイム ゾーン) などの利用可能なデータに基づいた広告

Microsoft では、製品を向上させるために、使用可能なデータを使用します。 次に例を示します。

- Configuration Manager の現在のブランチで提供される初期サポートでは、Windows Server 2008 R2 のサポート タイムラインが制限されていました。 Microsoft では、Configuration Manager Current Branch にアップグレードしたお客様からの使用状況データを調査しました。 それにより、この OS をまだ使用しているお客様をサポートするために、このタイムラインを変更して延長する必要があることが確認されました。

- Microsoft では、更新プログラムをインストールするための前提条件の確認を強化しました。 それらが古いルールを削除し、追加のケースを考慮して、いくつかの問題を自動的に修復するようにしました。  

> [!div class="nextstepaction"]
> [Configuration Manager でのデータの収集方法](how-diagnostics-and-usage-data-is-collected.md)
