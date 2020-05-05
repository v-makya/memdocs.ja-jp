---
title: オンプレミス MDM のアプリを管理する
titleSuffix: Configuration Manager
description: Configuration Manager で、オンプレミスモバイルデバイス管理 (MDM) 用のアプリケーションを管理します。
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 693f661f2a2db59335ec8e463842a0ad03c977f3
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724786"
---
# <a name="manage-apps-for-on-premises-mdm-in-configuration-manager"></a>Configuration Manager でオンプレミス MDM のアプリを管理する

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager オンプレミスモバイルデバイス管理 (MDM) を使用してデバイスを管理する場合、次の種類のアプリケーションを管理できます。

- Windows Phone アプリケーション パッケージ (*.xap ファイル)
- Windows Phone アプリケーション パッケージ (Windows Phone ストア内)
- MDM を介した Windows インストーラー
- Web アプリケーション

Configuration Manager アプリケーションと展開の種類の管理に関する一般的な情報については、「 [Configuration Manager アプリケーションの管理タスク](../../apps/deploy-use/management-tasks-applications.md)」を参照してください。

## <a name="create-windows-phone-application"></a><a name="bkmk_winphone"></a>Windows Phone アプリケーションの作成

Configuration Manager アプリケーションには、1 つ以上の展開の種類があります。 展開の種類には、インストール ファイルとデバイスにソフトウェアを展開するために必要な情報が含まれています。 また、展開の種類には、ソフトウェアを展開するタイミングと方法を指定する規則があります。

アプリと展開の種類を作成する一般的な手順については、「[アプリケーションの作成](../../apps/deploy-use/create-applications.md#bkmk_create)」を参照してください。

Configuration Manager は、Windows mobile デバイスで次の種類のアプリファイルをサポートしています。

|デバイスの種類|サポートされるファイルの種類|
|-----------------|---------------------|
|Windows Phone 8|xap|
|Windows Phone 8.1|xap、appx、appxbundle|
|Windows 10 Mobile|xap、appx、appxbundle|

Windows Phone アプリを**利用可能**または**必須**として展開します。 アプリのアンインストールにも展開を使用します。

## <a name="deploy-and-monitor-apps"></a>アプリの展開と監視

デスクトップやサーバーなどの他のデバイスと同じように Configuration Manager でモバイルデバイスのアプリケーションを展開および監視します。 詳細については、次の記事を参照してください。

- [アプリケーションの展開](../../apps/deploy-use/deploy-applications.md)
- [アプリケーションの監視](../../apps/deploy-use/monitor-applications-from-the-console.md)

モバイルデバイスに固有の次の制限事項を確認します。

- MDM 登録デバイスは、シミュレートされた展開、ユーザー エクスペリエンス、またはスケジュール設定をサポートしていません。

- 1つのアプリに100を超えるロケールを追加しないでください。 この操作は、アプリがデバイスにインストールされないようにします。

## <a name="next-step"></a>次のステップ

デプロイされたアプリケーションを新しいアプリケーションに変更、アンインストール、または置き換えるには、Configuration Manager 内の任意のアプリと同じように管理します。 詳細については、「[アプリケーションの更新とインベントリからの削除](../../apps/deploy-use/update-and-retire-applications.md)」を参照してください。
