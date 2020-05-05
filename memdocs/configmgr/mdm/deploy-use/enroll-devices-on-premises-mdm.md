---
title: オンプレミス MDM のデバイスの登録
titleSuffix: Configuration Manager
description: Configuration Manager でオンプレミスモバイルデバイス管理 (MDM) のデバイスを登録する方法について説明します。
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ca7f792bb6b419dd1d20d495bdb53bc7c2be506
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724606"
---
# <a name="enroll-devices-for-on-premises-mdm-in-configuration-manager"></a>Configuration Manager でオンプレミス MDM のデバイスを登録する

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager オンプレミスモバイルデバイス管理 (MDM) を使用してデバイスを管理するには、まず登録する必要があります。 その後、Configuration Manager がデバイスと通信して管理タスクを実行できるようになります。 Configuration Manager には、デバイスを登録する2つの方法があります。

- **ユーザー登録**: ユーザーのデバイスで登録プロセスを開始します。 ユーザー登録を成功させるには、信頼されたルート証明書をデバイスにインストールし、クライアント設定で登録のためにユーザーをプロビジョニングします。 デバイスを登録するには、ユーザーが資格情報を入力するだけで済みます。

    詳細については、「[ユーザーがデバイスを登録する方法](user-enroll-devices-on-premises-mdm.md)」を参照してください。

- **一括登録**: デバイスのユーザーが登録を開始しません。 Configuration Manager で一括登録パッケージを作成します。 デバイスで開くと、デバイスを登録するために必要な情報がパッケージによって提供されます。

    詳細については、「[デバイスを一括登録する方法](bulk-enroll-devices-on-premises-mdm.md)」を参照してください。

オンプレミス MDM でデバイスを登録するために Configuration Manager がサポートしている OS バージョンの詳細については、「[サポートされ](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)ている構成」を参照してください。
