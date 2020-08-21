---
title: Windows 10 のサポート
titleSuffix: Configuration Manager
description: Configuration Manager でクライアントとして、または OSD 用にサポートされている Windows 10 のバージョンについて説明します
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6a30fc55fb4129b8ea3493b76fd6871a2a62f881
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126741"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Configuration Manager での Windows 10 のサポート  

*適用対象:Configuration Manager (Current Branch)*

次のような、Configuration Manager でサポートされる Windows 10 のバージョンについて説明します

- [Configuration Manager クライアントとしての Windows 10](#windows-10-as-a-client)
- [Windows 10 用のアセスメント & デプロイメント キット (ADK)](#windows-10-adk)

> [!TIP]
> クライアントとしての Windows Server のビルドは、関連する Windows 10 バージョンと同じものがサポートされています。 たとえば、Windows Server 2016 は Windows 10 LTSB 2016 と同じビルド バージョンで、Windows Server バージョン 1803 は Windows 10 バージョン 1803 と同じビルド バージョンです。
>
> サイト システムとしての Windows Server の詳細については、「[Configuration Manager サイト システム サーバーでサポートされるオペレーティング システム](supported-operating-systems-for-site-system-servers.md#bkmk_core)」を参照してください。

## <a name="windows-10-as-a-client"></a>クライアントとしての Windows 10

Configuration Manager は、Windows 10 の新しいバージョンが利用可能になると、できるだけ早くそのバージョンに対してクライアントとしてのサポートを提供しようとします。 製品には個別の開発およびリリースのスケジュールがあるため、Configuration Manager で提供するサポートは、各製品のリリース時期によって異なります。

Configuration Manager バージョンは、[そのバージョンのサポート](../../servers/manage/current-branch-versions-supported.md)の終了後に、マトリックスから除外されます。 同様に、Enterprise 2015 LTSB または 1511 などの Windows 10 バージョンのサポートは、サポートから削除されると、マトリックスから除外されます。

- Configuration Manager の現在のブランチの最新バージョンでは、セキュリティ更新プログラムと重要な更新プログラムの両方が受信されます。これらには、Windows 10 のバージョンに関する問題の修正プログラムが含まれる場合があります。 Microsoft で Configuration Manager の現在のブランチの新しいバージョンがリリースされた際、以前のバージョンでは、セキュリティ更新プログラムのみが受信されます。 詳細については、[Configuration Manager の Current Branch バージョンのサポート](../../servers/manage/current-branch-versions-supported.md)に関するページをご覧ください。  

    > [!NOTE]
    > Windows 10 を最新状態に保つ最良の方法は、Configuration Manager を最新状態に保つことです。 詳細については、「[Configuration Manager とサービスとしての Windows](../../understand/configuration-manager-and-windows-as-service.md)」を参照してください。  

- この情報は、「[クライアントとデバイスのサポートされるオペレーティング システム](supported-operating-systems-for-clients-and-devices.md)」の補足です。  

- Configuration Manager の Long-Term Servicing Branch を使用する場合は、「[Long-Term Servicing Branch でサポートされている構成](../../understand/supported-configurations-for-ltsb.md)」を参照してください。  

次の表は、さまざまなバージョンの Configuration Manager でクライアントとして使用できる Windows 10 のバージョン一覧です。

| Windows 10 バージョン | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 | ConfigMgr 2006 |
|---------------------|-----|-----|-----|-----|-----|-----|
| **1709**<br>(10.0.16299)   <!--10/13/2020-->   | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) | ![サポートされています](media/green_check.png) | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) |
| **1803**<br>(10.0.17134)   <!--11/10/2020-->   | ![サポート](media/green_check.png) | ![サポートされています](media/green_check.png) | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) |
| **1809**<br>(10.0.17763)   <!--05/11/2021-->   | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) |
| **1903**<br>(10.0.18362)   <!--12/08/2020-->   | ![サポートされていません](media/Red_X.png) | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) |
| **1909**<br>(10.0.18363)   <!--05/10/2022-->   | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) | ![サポートされています](media/green_check.png) | ![サポート](media/green_check.png) |
| **2004**<br>(10.0.19041)   <!--12/14/2021-->   | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) |

Configuration Manager Current Branch の現在サポートされているすべてのバージョンでは、次の Windows 10 LTSB/LTSC エディションがサポートされています。

- **Enterprise 2015 LTSB** <!--10/14/2025-->
- **Enterprise 2016 LTSB** <!--10/13/2026-->
- **Enterprise LTSC 2019** <!--01/09/2029-->

Windows ライフサイクルの詳細については、「[Windows ライフサイクルのファクト シート](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)」を参照してください。

| キー |
|--|
| ![サポートされています](media/green_check.png) = **サポートされています**  |
| ![サポートされていません](media/Red_X.png) = **サポートされていません** |

### <a name="windows-10-client-support-notes"></a><a name="bkmk_win10-notes"></a> Windows 10 クライアントのサポートに関するメモ

- 半期チャネル バージョンの Windows 10 のサポートには、エディション:Enterprise、Pro、Education、および Pro Education が含まれます。  

- バージョン 1906 以降では、Configuration Manager は Windows 10 Pro for Workstation をサポートします。

- Windows 10 バージョン 1909 では、OS 展開メディアでは 10.0.18362.418 としてバージョンが表示されます。

### <a name="windows-10-on-arm64"></a><a name="bkmk_arm64"></a> ARM64 上での Windows 10

Configuration Manager は、Windows 10 ARM64 デバイス上のクライアントをサポートします。 OS の展開はサポートされません。<!-- 1353704 -->

バージョン 2002 以降では、<!--5954175--> **すべての Windows 10 (ARM64)** プラットフォームが、要件の規則や適用性の一覧があるオブジェクトでサポートされている OS バージョンの一覧に示されます。

> [!NOTE]
> 以前にトップ レベルの **Windows 10** プラットフォームを選択した場合、このアクションは**すべての Windows 10 (64 ビット)** と**すべての Windows 10 (32 ビット)** の両方に自動的に選択されます。 この新しいプラットフォームは自動的には選択されません。 **すべての Windows 10 (ARM64)** を追加する場合は、一覧から手動で選択します。

### <a name="support-for-windows-insider"></a><a name="bkmk_WIfB-support"></a> Windows Insider のサポート

Configuration Manager バージョン 1906 以降では、[Windows Insider ビルドの更新とサービス](../../../sum/get-started/configure-classifications-and-products.md#bkmk_WIfB)を実行できます。 この機能は、お客様の便宜のために提供されています。 この機能は動作するはずですが、サポートはベスト エフォートで提供されます。 この機能が停止した場合、それに対して Configuration Manager により修正プログラムが発行されない可能性があります。  

Windows Insider に関するフィードバックをご提供いただける場合は、[フィードバック Hub](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback) をご利用ください。

## <a name="windows-10-adk"></a>Windows 10 ADK

Configuration Manager を使用してオペレーティング システムを展開する場合、Windows ADK は必須の外部依存コンポーネントです。 詳細については、以下の記事を参照してください。

- [OS の展開のインフラストラクチャ要件](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10)

- [Windows ADK for Windows 10 をダウンロードする](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

    > [!IMPORTANT]
    > Windows 10 バージョン 1809 以降、Windows PE は個別のインストーラーとなっています。 それ以外に機能の違いはありません。
    >
    > **Windows ADK for Windows 10** と、**ADK 用の Windows PE アドオン**の両方をダウンロードしてください。

次の表は、さまざまなバージョンの Configuration Manager で使用できる Windows 10 ADK のバージョン一覧です。

| Windows 10 ADK バージョン  | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 | ConfigMgr 2006 |
|--------------------|-----|-----|-----|-----|-----|-----|
| **1709**<br>(10.1.16299) | ![サポートされていません](media/Red_X.png)   | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![下位互換性あり](media/blue_compat.png) | ![下位互換性あり](media/blue_compat.png) | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) |
| **1809**<br>(10.1.17763) | ![サポート](media/green_check.png) | ![サポート](media/green_check.png) | ![下位互換性あり](media/blue_compat.png) | ![下位互換性あり](media/blue_compat.png) | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) |
| **1903**<br>(10.1.18362) | ![サポートされていません](media/Red_X.png) | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) | ![サポートされています](media/green_check.png) | ![サポート](media/green_check.png) | ![下位互換性あり](media/blue_compat.png) |
| **2004**<br>(10.1.19041) | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) | ![サポートされていません](media/Red_X.png) | ![サポートされています](media/green_check.png) | ![サポート](media/green_check.png) |

|キー|
|--|
| ![サポートされています](media/green_check.png) = **サポートされています** <br/> この表では、Configuration Manager のバージョンとの関連でのみ、Windows ADK のサポート仕様をまとめています。 Microsoft では、展開している Windows のバージョンに合う Windows ADK を使用することをお勧めします。 Windows 10 の最新バージョンを展開するときは、Windows ADK の最新バージョンを使用してください。 Windows ADK の最新バージョンでは、古いバージョンの OS (Windows 8.1 など) の展開がサポートされている場合があります。<!-- SCCMDocs issue 1229 --> Windows ADK コンポーネントのサポートについては、「[DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms)」(DISM でサポートされているプラットフォーム) および「[USMT requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1)」(USMT の要件) を参照してください。 |
| ![下位互換性あり](media/blue_compat.png)  = **下位互換性あり** <br/> この組み合わせはテストされていませんが、動作するはずです。 既知の問題や注意事項が記述されます。 |
| ![サポートされていません](media/Red_X.png) = **サポートされていません** |

### <a name="windows-10-adk-support-notes"></a><a name="bkmk_adk-notes"></a> Windows 10 ADK のサポートに関するメモ

- Configuration Manager は、Windows 10 ADK の x86 および amd64 コンポーネントのみをサポートします。 ARM または ARM64 コンポーネントは現在はサポートされていません。

- Windows Server のビルドには、関連付けられている Windows 10 バージョンと同じ Windows ADK が必要です。 たとえば、Windows Server 2016 は Windows 10 LTSB 2016 と同じビルド バージョンです。
