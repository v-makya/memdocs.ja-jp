---
title: Desktop Analytics の資産
titleSuffix: Configuration Manager
description: Desktop Analytics のデバイス、ドライバー、およびアプリについて説明します。
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe1338781cbb16a8485de050a294e34e487a2ecc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706650"
---
# <a name="assets-in-desktop-analytics"></a>Desktop Analytics の資産

デバイスから Desktop Analytics にデータが報告された後、次の資産のインベントリが提供されます。

- デバイス
- インストール済みのアプリ  

サービス ポータルで、Desktop Analytics メニューの **[資産]** を選択します。

## <a name="devices"></a>デバイス

**[デバイス]** タブには、Desktop Analytics に登録する組織内のすべてのデバイスに関する重要な情報が表示されます。 任意の列を基準にして並べ替えたり、特定の値をフィルター処理することができます。

> [!NOTE]  
> お使いの環境について表示されるはずのデバイス数がダッシュボードで報告されない場合は、[Desktop Analytics のトラブルシューティング](troubleshooting.md)に関する記事を参照してください。  

展開計画には、デバイスの詳細情報が表示されます。 詳細については、「[資産の計画](about-deployment-plans.md#plan-assets)」を参照してください。

## <a name="apps"></a>アプリ

**[アプリ]** タブには、サービスによって Windows デバイス上で検出されたすべてのインストール済みアプリが表示されます。

**[注目]** アプリは、2% を超える登録済みアプリにインストールされています。

次のカテゴリのいずれかを設定して、アプリの **[重要度]** を構成します。

- 重要
- 重要
- 無視
- 未レビュー
- 重要でない<!-- 3587232 -->

一覧からアプリを選択し、 **[編集]** を選択します。 この操作を行うと、アプリの詳細が表示されます。 **[重要度]** ドロップダウン メニューを選択し、値を設定します。 **[所有者]** を割り当てることもできます。 変更する場合は、 **[保存]** を選択します。

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp" /> システム アプリとストア アプリの自動アップグレード判定

<!-- 3587232 -->
Desktop Analytics ワークフローのすべての注目アプリについて、 **[重要度]** と **[アップグレード判定]** を特定することは重要です。 これらのアプリに注釈を付ける手間を減らすために、特定の種類のアプリには、自動的に "*重要でない*" とマークされます。 こうしたアプリの展開計画のアップグレード判定にも "*準備完了*" とマークされます。 次のアプリは互換性があり、Windows のアップグレード後も引き続き機能します。

- Microsoft から発行されるシステム アプリとコンポーネント

- Microsoft Store から管理および更新されるアプリ

> [!TIP]
> グローバル レベルまたは展開計画に従って、アプリの入力を管理します。
>
> 1. Desktop Analytics ポータルの **[管理]** メニューで、 **[資産]** を選択します。 次に **[アプリ]** を選択します。
>
> 2. **[種類]** 列と **[カテゴリ]** 列を使用して、これらのアプリのカテゴリを管理します。
>
>    - ストア アプリの場合は、 **[種類]** を **[モダン]** に絞り込みます。
>    - システム アプリの場合は、 **[カテゴリ]** を **[バックグラウンド プロセス]** または **[Windows コンポーネント]** に絞り込みます。

展開計画では、 **[アップグレード判定]** を設定することもできます。 詳細については、「[資産の計画](about-deployment-plans.md#plan-assets)」を参照してください。

### <a name="usage"></a>使用方法

<!-- 5533890 -->

- **合計インストール数**: この値は、Desktop Analytics に登録されたすべてのデバイスに対する選択されたアプリのインストール数です。

- **インストール率**: この値は、Desktop Analytics に登録されたデバイスの合計に対する、選択されたアプリのインストールの割合です。

- **過去 30 日間にこのアプリを起動したデバイス**: この値は、ユーザーが選択されたアプリを起動したデバイスの数です。 これには、過去 30 日間に使用状況が報告されたデバイスのみが含まれます。 この数は、Windows 10 の任意のバージョンで実行されている Desktop Analytics に登録されたお客様のすべてのデバイスが対象になります。 この数は、展開プランによって異なる可能性があります。

## <a name="next-steps"></a>次のステップ

- [Desktop Analytics の展開計画について学習する](about-deployment-plans.md)  

- [セキュリティと機能の更新について学習する](about-updates.md)  

- [Desktop Analytics での互換性評価](compat-assessment.md)  
