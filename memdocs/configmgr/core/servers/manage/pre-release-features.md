---
title: プレリリース機能
titleSuffix: Configuration Manager
description: プレリリース機能は、運用環境での初期テスト用の Current Branch に含まれている機能です。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e341fab9f76ab6994f051dbd5e2333c3f521b4d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703540"
---
# <a name="pre-release-features-in-configuration-manager"></a>Configuration Manager のプレリリース機能

*適用対象:Configuration Manager (Current Branch)*

プレリリース機能は、運用環境での初期テスト用の Current Branch に含まれている機能です。 これらの機能は完全にサポートされていますが、現在開発中です。 プレリリース カテゴリから移動するまでは変更が行われる可能性があります。

## <a name="give-consent"></a>同意する  

プレリリース機能を使用する前に、プレリリース機能を使用することに同意します。 同意することは階層ごとに 1 回限りの操作であり、元に戻すことはできません。 同意するまでは、更新プログラムに含まれている新しいプレリリース機能を有効にすることはできません。 プレリリース機能を有効にした後で無効にすることはできません。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。  

2. リボンの **[階層設定]** をクリックします。  

3. [階層設定のプロパティ] の **[全般]** タブで、 **[プレリリース機能を使用することに同意する]** オプションを有効にします。 **[OK]** をクリックします。  

## <a name="enable-pre-release-features"></a>プレリリース機能を有効にする

プレリリース機能を含む更新プログラムをインストールすると、これらの機能は、更新プログラムに含まれる標準の機能と一緒に、[更新とサービス] ウィザードに表示されます。

### <a name="if-you-have-given-consent"></a>同意した場合

更新とサービス ウィザードで、プレリリース機能を有効にします。 他の機能の場合と同じように、プレリリース機能を選択します。

必要に応じて、後で **[管理]** ワークスペース内の **[更新とサービス]** の下にある **[機能]** ノードからプレリリース機能を有効にします。 機能を選択し、リボンの **[有効にする]** をクリックします。 同意するまで、このオプションは利用できません。

### <a name="if-you-havent-given-consent"></a>同意していない場合

更新とサービス ウィザードに、プレリリース機能は表示されますが、有効にすることはできません。 更新プログラムがインストールされた後、 **[機能]** ノードにこれらの機能が表示されます。 しかし、同意するまでそれらを有効することはできません。

> [!IMPORTANT]  
> 複数サイトの階層では、中央管理サイトからオプション機能またはプレリリース機能のみを有効にできます。 この動作によって、階層全体で競合が発生しないようにします。 <!--507197-->  
>
> スタンドアロン プライマリ サイトで同意し、新しい中央管理サイトをインストールして階層を拡張する場合、中央管理サイトでもう一度同意する必要があります。  

プレリリース機能を有効にすると、Configuration Manager の階層マネージャー (HMAN) は機能が利用可能になる前に変更を処理する必要があります。 多くの場合、変更の処理はすぐに行われます。 HMAN の処理サイクルによっては、完了までに最大 30 分かかることがあります。 変更が処理された後、その機能を使用するには、まずコンソールを再起動します。

## <a name="list-of-pre-release-features"></a><a name="bkmk_table"></a> プレリリース機能の一覧

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](pre-release-features.md).  

> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](pre-release-features.md). Beginning with version 1906, it's no longer a pre-release feature.  

-->

<!-- With each current branch release, to help purge this list a bit, remove any entries that were added as a full feature in a version that's no longer supported -->
| 機能          | プレリリース版として追加 | 完全機能として追加 |
|------------------|----------------------|-------------------------|
| [オーケストレーション グループ](../../../sum/deploy-use/orchestration-groups.md) <!--3098816--> | バージョン 2002 | ![未追加](media/red_x.png) |
| [タスク シーケンスの展開の種類](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt) <!--3555953--> | バージョン 2002 | ![未追加](media/red_x.png) |
| [中央管理サイトの削除](../deploy/install/remove-central-administration-site.md) <!-- 3607277 --> | バージョン 2002 | ![未追加](media/red_x.png) |
| [タスク シーケンス デバッガー](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71--> | バージョン 1906 | ![未追加](media/red_x.png) |
| [アプリケーション グループ](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D--> | バージョン 1906 | ![未追加](media/red_x.png) |
| [Azure Active Directory ユーザー グループの探索](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->| バージョン 1906 | バージョン 2002 |
| [コレクションのメンバーシップの結果の Azure Active Directory グループとの同期](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->| バージョン 1906| バージョン 2002 |
| [CMPivot スタンドアロン](cmpivot.md#bkmk_standalone) <!--3555890/4692885,no GUID--> | バージョン 1906 | バージョン 2002 |
| [SMS プロバイダーの管理サービス](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service) <!--1359052--> | バージョン 1810 | バージョン 1906 |
| [拡張 HTTP サイト システム](../../plan-design/hierarchy/enhanced-http.md) <!--1356889,1358228--> | バージョン 1806 | バージョン 1810 |
| [共同管理デバイス向けのクライアント アプリ](../../../comanage/workloads.md#client-apps) <br/> (以前の名称は "*共同管理デバイス向けのモバイル アプリ*" でした) <!--1357892/3600959,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C--> | バージョン 1806 | バージョン 2002 |
| [パッケージ変換マネージャー](../../../apps/pcm/package-conversion-manager.md) <!--1357861--> | バージョン 1806 | バージョン 1810 |
| [段階的展開](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) <!--1356837--> | バージョン 1802 | バージョン 1806 |
| [Windows Defender アプリケーション制御の管理](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) <!--3600958 (fka 1355092 & 1319346)--> | バージョン 1702 | バージョン 1906 |
| [クラスター対応のコレクションのサービス (サーバー グループ)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697--> | バージョン 1602 | ![未追加](media/red_x.png) |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!TIP]  
> 最初に有効にする必要があるプレリリース版以外の機能の詳細については、「[更新プログラムのオプション機能の有効化](install-in-console-updates.md#bkmk_options)」を参照してください。  
>
> Technical Preview Branch でのみ利用できる機能の詳細については、[Technical Preview](../../get-started/technical-preview.md) に関するページを参照してください。  
