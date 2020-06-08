---
title: Microsoft Intune を使用して多数の OEMConfig プロファイルを Zebra デバイスに展開する - Azure |Microsoft Docs
description: Microsoft Intune を使用して、Android エンタープライズを実行している Zebra デバイスに複数の OEMConfig デバイス構成プロファイルを作成し、展開します。 Zebra のアクションおよびステップを使用して、プロファイルを並べ替えます。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2a38c445018200d9fe80db19142f123aba783b60
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311168"
---
# <a name="deploy-multiple-oemconfig-profiles-to-zebra-devices-in-microsoft-intune"></a>Microsoft Intune で複数の OEMConfig プロファイルを Zebra デバイスに展開する

Microsoft Intune では、OEMConfig を使用して Android エンタープライズ デバイスに対する OEM 固有の設定をカスタマイズします。 これらの設定はデバイスの製造元に固有であり、Intune の構成プロファイルを使用して展開されます。

Zebra デバイスでは、同じデバイスに複数のプロファイルを展開したり、割り当てたりすることができます。 既存の OEMConfig プロファイルでは、次回デバイスが Intune と同期されるときに、この機能を使用できます。

この機能は、以下に適用されます。

- Android エンタープライズを実行している Zebra デバイス

OEMConfig の機能や使用方法などの、OEMConfig の詳細については、[OEMConfig 構成プロファイル](android-oem-configuration-overview.md)に関するページを参照してください。

この記事では、Microsoft Intune で複数の OEMConfig プロファイルを Zebra デバイスに展開し、順序を記述し、レポート機能を使用する方法について説明します。

## <a name="prerequisites"></a>[前提条件]

[OEMConfig 構成プロファイル](android-oem-configuration-overview.md)を作成します。

## <a name="use-multiple-profiles"></a>複数のプロファイルを使用する

Zebra デバイスでは、各デバイスで同時に多数のプロファイルを持つことができます。 この機能を使用すると、Zebra OEMConfig 設定を小さなプロファイルに分割できます。 たとえば、すべてのデバイスに影響を与えるベースライン プロファイルを作成します。 次に、デバイスに固有の設定を構成する追加のプロファイルを作成します。

Zebra の OEMConfig スキーマでは、**アクション**も使用されます。 アクションとは、デバイスで実行される操作のことです。 これによって設定は構成されません。 これらのアクションを使用して、ファイルのダウンロードをトリガーする、クリップボードをクリアするなどが可能です。 サポートされているアクションの完全な一覧については、[Zebra のドキュメント](https://techdocs.zebra.com/oemconfig/10-0/about/)に関するページを参照してください (Zebra の Web サイトが開きます)。

たとえば、いくつかの設定をデバイスに適用する Zebra OEMConfig プロファイルを作成したとします。 もう 1 つの Zebra OEMConfig プロファイルには、クリップボードをクリアするアクションが含まれています。 最初のプロファイルを Zebra デバイス グループに割り当てました。 その後、これらのデバイスでクリップボードをクリアする必要が生じました。 最初のプロファイルを変更することなく、同じデバイス グループに 2 つ目のプロファイルを割り当てます。 最初のプロファイルで作成された構成設定を再送信したり、設定に影響を与えたりすることなく、デバイスのクリップボードをクリアすることができます。

別の例として、いくつかの Zebra デバイスの設定が構成された、OEMConfig プロファイルを割り当てたとします。 最近、ユーザーから特定のアプリケーションに関する問題が報告され、アプリのキャッシュを消去する必要が生じました。 "キャッシュの消去" アクションのみを含む、新しい OEMConfig プロファイルを作成します。 プロファイルを必要とするデバイスに、それを割り当てます。

## <a name="ordering"></a>順序

各デバイスに複数のプロファイルがある場合、プロファイルが展開される順序は保証されません。 この動作は Google Play の制限です。 操作を順番に実行するために、[Zebra のトランザクション ステップ機能](https://techdocs.zebra.com/oemconfig/10-0/mc/) (Zebra の Web サイトが開きます) を使用できます。 

つまり、順序が重要な場合は [Zebra のトランザクション ステップ機能](https://techdocs.zebra.com/oemconfig/10-0/mc/) (Zebra の Web サイトが開きます) を使用します。 順序が重要でない場合は、複数の Intune プロファイルを使用します。 

いくつか例を見てみましょう。

- これらのデバイスで他の設定を構成する前に、新しく登録されたすべての Zebra デバイスに対して Bluetooth を有効にする必要があります。 操作を順番に実行するには、Zebra のスキーマにある**ステップ**機能を使用します。

  2 つのトランザクション ステップを含む Intune プロファイルを 1 つ作成します。 最初のステップで Bluetooth の設定を行い、2 番目のステップでもう一方の設定を構成します。 Zebra の OEMConfig アプリがプロファイルを受け取ると、ステップを順番に実行します。

  詳細については、[Zebra のトランザクション ステップ](https://techdocs.zebra.com/oemconfig/10-0/mc/) (Zebra の Web サイトが開きます) に関するページを参照してください。

- すべての Zebra デバイスが 24 時間形式で時刻を表示するようにします。 これらのデバイスの一部で、カメラをオフにする必要があります。 時刻とカメラの設定は互いに依存していません。

  2 つの Intune プロファイルを作成します。

  - **プロファイル 1**:時刻を 24 時間形式で表示します。 月曜日に、このプロファイルは **[すべての Zebra AE デバイス]** グループに割り当てられます。
  - **プロファイル 2**:カメラをオフにします。 火曜日に、このプロファイルは **[Zebra AE factory devices]\(Zebra AE ファクトリ デバイス\)** グループに割り当てられます。

  水曜日に、10 台の新しい Zebra デバイスを Intune に登録します。 プロファイル 1 とプロファイル 2 が割り当てられます。 新しいデバイスは Intune と同期された後に、プロファイルを受け取ります。 デバイスは、プロファイル 1 の前にプロファイル 2 を受け取る可能性があります。

## <a name="enhanced-reporting"></a>強化されたレポート

プロファイルを展開すると、Zebra OEMConfig アプリによってデバイス上で実行されます。 Zebra OEMConfig アプリにより、プロファイルの状態が Intune に報告されます。 Endpoint Manager 管理センターでは、展開された OEMConfig プロファイルの状態と、エラーまたは警告を確認できます。

1. [Microsoft Endpoint Manager 管理センターを開きます](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 該当する Zebra OEMConfig プロファイル > **[モニター]**  >  **[デバイスの状態]** の順に選択します。 このオプションでは、OEMConfig プロファイルが割り当てられているデバイスが表示されます。
3. デバイス > **[デバイス構成]** の順に選択し、該当する Zebra OEMConfig プロファイルを選択します。 このオプションでは、成功または失敗したプロファイル設定が表示されます。

    失敗した行を選択します。 失敗した理由を詳しく説明する、詳細情報が表示されます。

## <a name="next-steps"></a>次のステップ

- [OEMConfig 構成プロファイル](android-oem-configuration-overview.md)について、さらに学習します。
- Android デバイス管理者で、[Mobility Extensions (MX)](android-zebra-mx-overview.md) を構成します。
- [プロファイルの状態を監視する](device-profile-monitor.md)。
