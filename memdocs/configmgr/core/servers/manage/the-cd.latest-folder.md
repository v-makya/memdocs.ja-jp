---
title: CD.Latest フォルダー
titleSuffix: Configuration Manager
description: Configuration Manager コンソール内から製品の更新プログラムを提供するプロセスについて説明します。
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 577bfd865ad3872c386384c3bba95cb009ef83ec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704050"
---
# <a name="the-cdlatest-folder-for-configuration-manager"></a>Configuration Manager の CD.Latest フォルダー

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager には、Configuration Manager コンソール内から製品の更新プログラムを提供するプロセスがあります。 Configuration Manager を更新するこの新しいメソッドをサポートするために、**CD.Latest** という名前の新しいフォルダーが作成されます。 このフォルダーには、サイトの更新されたバージョン用の Configuration Manager インストール ファイルのコピーが含まれます。  

CD.Latest フォルダーには **Redist** という名前のフォルダーが含まれます。セットアップ時にダウンロードして使用される再頒布可能ファイルがここに入ります。 これらのファイルは、その CD.Latest フォルダーにある Configuration Manager ファイルのバージョンに一致します。 CD.Latest フォルダーからセットアップを実行する場合、そのセットアップのバージョンに一致するファイルを使用する必要があります。 新しい現行のファイルを Microsoft からダウンロードするようにセットアップに指示するか、CD.Latest フォルダーに含まれている Redist フォルダーのファイルを使用するようにセットアップに指示できます。

構成基準メディアに **Redist** フォルダーは含まれません。 コンソール内の更新プログラムをインストールするまで、サイトに Redist フォルダーは作成されません。 それまでは、構成基準メディアからサイトをインストールするときに使った Redist フォルダーを使ってください。  

> [!TIP]  
> 使用する再頒布可能ファイルが現行のものであることを確認してください。 再頒布可能ファイルを最近ダウンロードしていない場合は、Microsoft からダウンロードするようセットアップを計画します。   

次は、中央管理サイトまたはプライマリ サイト サーバー上の CD.Latest フォルダーを作成または更新するシナリオです。  

- Configuration Manager コンソール内から、更新プログラムまたは修正プログラムをインストールすると、Configuration Manager インストール フォルダー内でフォルダーの作成または更新が行われます。  

- 組み込み Configuration Manager バックアップ タスクを実行すると、指定されたバックアップ フォルダーの場所でフォルダーの作成または更新が行われます。  

- 構成基準メディアを使用して新しいサイトをインストールすると、CD.Latest フォルダーが作成されます。


## <a name="supported-scenarios"></a>サポートされるシナリオ

CD.Latest フォルダーのソース ファイルは、次のシナリオでサポートされています。  

### <a name="backup-and-recovery"></a>バックアップと回復
サイトを回復するには、サイトと一致する CD.Latest フォルダーのソース ファイルを使用します。 組み込みのサイト バックアップ タスクを使用してサイトのバックアップを実行すると、CD.Latest フォルダーがバックアップの一部として含まれます。

- サイト回復の一部としてサイトを再インストールする場合は、バックアップに含まれている CD.Latest フォルダーからサイトをインストールします。 この操作で、サイトのバックアップおよびサイト データベースに一致するファイルのバージョンを使用してサイトがインストールされます。  

    - 適切な CD.Latest フォルダーのバージョンにアクセスできない場合は、ラボ環境でサイトをインストールして適切なファイル バージョンの CD.Latest フォルダーを取得します。 次に、回復するバージョンと一致するようにそのサイトを更新します。  

    - 適切な CD.Latest フォルダーとそこから取得できる内容がない場合は、サイトを回復できません。 この場合は、サイトを再インストールする必要があります。  

- CD.Latest フォルダーがないが、稼働中の子プライマリ サイトまたは中央管理サイトがある場合は、そのサイトを参照サイトとして使用してサイトを回復できます。  

### <a name="install-a-child-primary-site"></a>子プライマリ サイトをインストールする
1 つまたは複数のコンソール内の更新プログラムがインストールされている中央管理サイトの下に新しい子プライマリ サイトをインストールするときに、中央管理サイトの CD.Latest フォルダーからセットアップとソース ファイルを使用します。 このプロセスでは、中央管理サイトのバージョンと一致するインストール ソース ファイルを使用します。 詳細については、「[セットアップ ウィザードを使用してサイトをインストールする](../deploy/install/use-the-setup-wizard-to-install-sites.md)」を参照してください。  

### <a name="expand-a-stand-alone-primary-site"></a>スタンドアロン プライマリ サイトを拡張する
新しい中央管理サイトをインストールしてスタンドアロン プライマリ サイトを拡張するときには、プライマリ サイトの CD.Latest フォルダーからセットアップとソース ファイルを使用します。 このプロセスでは、プライマリ サイトのバージョンと一致するインストール ソース ファイルを使用します。 詳細については、「[スタンドアロン プライマリ サイトを拡張する](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)」を参照してください。

### <a name="install-a-secondary-site"></a>セカンダリ サイトをインストールする
<!-- SCCMDocs-pr issue #3164 -->
1 つまたは複数のコンソール内の更新プログラムがインストールされているプライマリ サイトの下に新しいセカンダリ サイトをインストールするときに、プライマリ サイトの CD.Latest フォルダーからソース ファイルを使用します。 

詳細については、「[セカンダリ サイトをインストールする](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary)」を参照してください。 


## <a name="unsupported-scenarios"></a>サポートされていないシナリオ

更新された CD.Latest のソース ファイルは、次に対してサポートされていません。  

- 新しい階層の新しいサイトのインストール  
- Microsoft System Center 2012 Configuration Manager サイトから Configuration Manager Current Branch へのアップグレード
- Configuration Manager クライアントのインストール
- Configuration Manager コンソールのインストール
