---
title: Package Conversion Manager
titleSuffix: Configuration Manager
description: Configuration Manager でパッケージをアプリケーションに変換する Package Conversion Manager について説明します。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f053fa73-c553-4522-a6b9-f885f23fe57c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 075dd860d20662679e5bdf58dae23d0220fa751e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689010"
---
# <a name="package-conversion-manager"></a>Package Conversion Manager

*適用対象:Configuration Manager (Current Branch)*

<!--1357861-->

バージョン 1806 以降の Package Conversion Manager では、Configuration Manager の従来のパッケージをアプリケーションに変換できます。 アプリケーションには、依存関係、要件の規則、検出方法、およびユーザーとデバイスのアフィニティなど、追加の利点があります。

> [!Tip]  
> この機能はバージョン 1806 で[プレリリース機能](../../core/servers/manage/pre-release-features.md)として初めて導入されました。 バージョン 1810 からは、この機能はプレリリース機能ではなくなりました。  


Configuration Manager アプリケーションには、クライアント デバイスに展開されるファイルやプログラムが含まれています。 しかし、従来のパッケージやプログラムとは異なり、アプリケーションはユーザーを中心に考えられた追加の機能を提供します。 たとえば、ソフトウェア パッケージや仮想アプリケーション パッケージの展開の種類、またはモバイル デバイス用アプリケーションのバージョンを含むアプリケーションもあります。

詳細については、以下の記事を参照してください。 
- [アプリケーション管理の概要](../understand/introduction-to-application-management.md)  
- [パッケージとプログラム](../deploy-use/packages-and-programs.md)  

> [!Important]  
> 古いバージョンの Package Conversion Manager を以前にインストールした場合は、まず、それをアンインストールしてからサイトをアップグレードします。 この統合されたバージョンをインストールする必要はありませんが、既存のバージョンと競合する可能性があります。  

この統合されたバージョンの Package Conversion Manager は、Configuration Manager の現在のブランチ サイト内にあるパッケージに対して機能します。 スタンドアロン ツールではありません。 古いバージョンの Configuration Manager 内にパッケージとプログラムがある場合、まず、現在のブランチ サイトにパッケージを移行します。 詳細については、[階層間でのデータの移行](../../core/migration/migrate-data-between-hierarchies.md)に関するページを参照してください。

<!-- SCCMDocs-pr issue #3357 -->
Configuration Manager バージョン 1902 には次の改善が含まれています。
- スケジュールされたパッケージの分析は、既定では 7 日ごとに実行されます
- パッケージを分析および変換するための PowerShell コマンドレット
- 一般的なバグ修正と改善



## <a name="planning"></a>計画

パッケージのアプリケーションへの変換を開始する前に、まず、計画を作成します。 次のプロセスは、計画の一例です。

- [詳細パッケージ変換計画の定義](#bkmk_define)  

- [変換するパッケージの選択と準備](#bkmk_prepare)  

- [テスト パッケージの選択](#bkmk_test)  

- [パッケージの分析、調査、および変換](#bkmk_analyze)  

- [アプリケーションのテストと展開](#bkmk_deploy)  


### <a name="define-a-detailed-package-conversion-plan"></a><a name="bkmk_define"></a> 詳細パッケージ変換計画の定義

このセクションでは、パッケージ変換計画の 2 つのサンプルについて説明します。  

- [リソース使用率が高いテスト環境](#bkmk_define-high):実稼働環境を完全にレプリケートするためのリソース、アクセス許可、アーキテクチャを備えたテスト環境があります。  

- [リソース使用率が制限されるテスト環境](#bkmk_define-limited):実稼働環境を完全にレプリケートするテスト環境がありません。  

お使いの環境に固有のその他の問題に対応するために、必要に応じてこれらのプランを調整します。

#### <a name="sample-plan-for-a-high-resource-test-environment"></a><a name="bkmk_define-high"></a> リソース使用率が高いテスト環境のサンプル計画

お使いのテスト環境がリソース、アクセス許可、および実稼働環境とほぼ同じアーキテクチャを備えています。 テスト環境を使用して、効率的にすべてのパッケージを分析および変換してから、すべての Configuration Manager アプリケーションをテストします。 この作業が完了した後は、アプリケーションを実稼働環境に転送します。 

パッケージ変換計画は、次と同様の手順になるでしょう。  

1.  変換するパッケージを選択します。  

2.  変換するパッケージをテスト環境に移行します。  

3.  パッケージの変換準備をします。  

4.  テスト パッケージを選択します。  

5.  テスト パッケージの分析、調査、および変換を行います。  

6.  変換されたアプリケーションをテストします。  

7.  残存する (テストしていない) パッケージの分析と変換を行います。  

8.  テスト環境からアプリケーションをエクスポートします。 それらのアプリケーションを実稼働環境にインポートします。  

#### <a name="sample-plan-for-a-limited-resource-test-environment"></a><a name="bkmk_define-limited"></a> リソースが限られているテスト環境のサンプル計画

お使いのテスト環境がリソース、アクセス許可、および実稼働環境とほぼ同じアーキテクチャを備えていません。 すべてのパッケージの分析、テスト、および変換を行うことはできません。 このシナリオでは、お使いのテスト パッケージの分析、調査、変換、およびテストのみを行います。 その後、残存するパッケージを実稼働環境に移行して、分析と変換を行います。 

パッケージ変換計画は、次と同様の手順になるでしょう。

1.  変換するパッケージを選択します。  

2.  テスト パッケージを選択します。  

3.  テスト パッケージをテスト環境に移行します。  

4.  テスト パッケージの変換準備をします。  

5.  テスト パッケージの分析、調査、および変換を行います。  

6.  変換されたアプリケーションをテストします。  

7.  テスト環境からテスト アプリケーションをエクスポートします。 その後、それらのアプリケーションを実稼働環境にインポートします。  

8.  残存するパッケージを実稼働環境に移行して、変換準備をします。  

9.  実稼働環境で、残存するパッケージの分析、調査、および変換を行います。  

10. 残存するアプリケーションを実稼働環境にリリースします。  


### <a name="select-and-prepare-packages-for-conversion"></a><a name="bkmk_prepare"></a> 変換するパッケージの選択と準備

#### <a name="select-the-packages-that-you-want-to-convert"></a><a name="bkmk_prepare-select"></a> 変換するパッケージの選択

すべてのパッケージが、アプリケーションへの変換に適しているわけではありません。 パッケージの変換を開始する前に、変換しない予定のパッケージを特定します。 

アプリケーションに変換するのに最適なパッケージの種類は、ユーザー インターフェイスを含むものです。たとえば、  

- Windows インストーラーのファイル (.msi および .msu)  

- Microsoft Application Virtualization (App-V) プログラム  

- Windows 実行可能ファイル (.exe)  

パッケージのままにするのが最適で、アプリケーションに変換しないパッケージの種類。

- システム メンテナンス ツール。 たとえば、スクリプトやバックアップ ユーティリティなど。  

- サポート外のソフトウェアに対するパッケージ。

> [!Tip]  
> アプリケーションへの変換が適切でないパッケージを特定したら、それらを Configuration Manager コンソールの別のフォルダーに移動します。 Configuration Manager コンソールにパッケージ フォルダーを作成するには、次の手順を実行します。  
> - **[パッケージ]** ノードを右クリックします。  
> - **[フォルダー]** を選択して、 **[フォルダーの作成]** を選択します。  
> - `Not Converted` などのフォルダー名を入力します。  
> - **[OK]** をクリックします。  

#### <a name="prepare-the-packages-for-conversion"></a>パッケージの変換準備

変換する各パッケージが、次の条件に合うか確認します。  

- ソース ファイルの場所が、完全な UNC パス (`\\Server\Share\File` など) である。  

- Windows インストーラーのファイルで、一意の製品コードのみを使用している。  


### <a name="select-test-packages"></a><a name="bkmk_test"></a> テスト パッケージの選択

可能であれば、テスト パッケージのグループには、次の条件を満たすパッケージを含める必要があります。  

- 少なくとも 1 つのテストパッケージの準備状態が **[自動]** である。  

- 少なくとも 1 つのテストパッケージの準備状態が **[手動]** である。  

テスト パッケージが、次の例のように、コア パッケージであることが理想です。  

- よく理解しているパッケージ。  

- 組織にとって最も重要なパッケージ。  

- 最もテストが容易なパッケージ。  

テストに適切なパッケージを特定します。 その後、Configuration Manager コンソールの別のフォルダーにそれらのパッケージを移動します。


### <a name="analyze-investigate-and-convert-packages"></a><a name="bkmk_analyze"></a> パッケージの分析、調査、および変換

#### <a name="analyze-packages"></a>パッケージの分析

個々のパッケージまたは小規模なグループを分析するには、Configuration Manager コンソールに統合されている Package Conversion Manager を使用します。 詳細については、[パッケージを分析および変換する方法](how-to-analyze-and-convert.md)に関するページを参照してください。  

> [!NOTE]  
> 次に、 **[監視]** ワークスペースの **[パッケージ変換のステータス]** ノードに移動します。 分析と変換プロセスの概要情報が表示されます。  

#### <a name="investigate-analysis-results"></a>分析結果の調査

テスト パッケージを分析した後、準備状態が **[手動]** または **[エラー]** となっているパッケージを調査します。 その状態の理由を判断します。 準備状態が **[手動]** または **[エラー]** となる一般的な原因には、たとえば以下があります。

- パッケージに、アプリケーションの展開の種類で検出方法の作成に必要な情報が含まれていない。  

- コレクションをグローバル条件と要件に変換するために必要な情報が、パッケージに含まれていない。  

- パッケージに複数のプログラムが含まれている。  

- パッケージが、アプリケーションに変換しなかった別のパッケージに依存している。  

詳細については、次のリソースを参照してください。  

- 「[Technical reference for Package Conversion Manager error messages](error-messages.md)」(Package Conversion Manager のエラー メッセージのテクニカル リファレンス) でエラーメッセージと修正について確認する  

- ログ ファイル **PCMTrace.log** を確認する  

- [Package Conversion Manager のトラブルシューティング](troubleshoot-pcm.md)  

#### <a name="convert-the-packages"></a>パッケージの変換

パッケージの変換方法の詳細については、[パッケージを分析および変換する方法](how-to-analyze-and-convert.md)に関するページを参照してください。

> [!NOTE]  
> 次に、 **[監視]** ワークスペースの **[パッケージ変換のステータス]** ノードに移動します。 分析と変換プロセスの概要情報が表示されます。  


### <a name="test-and-deploy-the-applications"></a><a name="bkmk_deploy"></a> アプリケーションのテストと展開

詳細パッケージ変換計画に従って、テスト環境または実作業環境で、アプリケーションをテストします。



## <a name="recommendations"></a>推奨事項

- **[監視]** ワークスペースの **[パッケージ変換のステータス]** ノードを使用します。 分析と変換プロセスの概要情報が表示されます。  

- パッケージのプログラム (ラッパーと呼ばれます) を調べます。 Package Conversion Manager のプラグインを使用して、同等の Configuration Manager の機能に関数を変換します。  

- 運用環境で展開する前に、変換したプリケーションのテストを十分に行います。  



## <a name="next-steps"></a>次のステップ

[パッケージの分析および変換方法](how-to-analyze-and-convert.md)
