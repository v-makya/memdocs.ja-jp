---
title: Unicode および ASCII のサポート
titleSuffix: Configuration Manager
description: Configuration Manager オブジェクトでの Unicode および ASCII 文字のサポートについて説明します。
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bd3dad5f0ef24074ac8c8e6d2edf01d5641b541
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699900"
---
# <a name="unicode-and-ascii-support-in-configuration-manager"></a>Configuration Manager での Unicode および ASCII のサポート

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager では、ほとんどのオブジェクトを Unicode 文字を使用して作成します。 ただし、オブジェクトによっては ASCII 文字のみをサポートするものや、その他の制限が適用されるものもあります。  

## <a name="objects-that-use-ascii-characters"></a><a name="BKMK_ASCIIchar"></a> ASCII 文字を使用するオブジェクト

次のオブジェクトを作成する場合、Configuration Manager では ASCII 文字セットのみがサポートされます。  

- サイト コード  

- すべてのサイト システム サーバーのコンピューター名  

- 次の Configuration Manager アカウント:  

    > [!NOTE]  
    > 次のアカウントでは、ASCII 文字がサポートされます。ロシア語で実行されるサイトでは、RUS 文字もサポートされます。  

    - クライアント プッシュ インストール アカウント  

    - 管理ポイント データベース接続アカウント  

    - ネットワーク アクセス アカウント  

    - ［パッケージ アクセス アカウント］  

    - 標準センダー アカウント  

    - サイト システムのインストール アカウント  

    - ソフトウェアの更新ポイントの接続アカウント  

    - ソフトウェアの更新ポイントのプロキシ サーバー アカウント  

    > [!NOTE]  
    > 役割に基づいた管理権限を持つアカウントは Unicode をサポートします。  
    >
    > レポート サービス ポイント アカウントでは、RUS 文字以外の Unicode がサポートされます。  

- サイト サーバーとサイト システムの完全修飾ドメイン名 (FQDN)  

- Configuration Manager のインストール パス  

- SQL Server インスタンス名  

- 次のサイト システムの役割のパス:  

    - 登録ポイント  

    - 登録プロキシ ポイント  

    - レポート サービス ポイント  

    - 状態移行ポイント  

- 次のフォルダーのパス:  

    - クライアントの状態移行データを保管するフォルダー  

    - Configuration Manager のレポートを格納するフォルダー  

    - Configuration Manager のバックアップを保管するフォルダー  

    - サイトのセットアップのインストール ソース ファイルを保管するフォルダー  

    - セットアップが使用する前提条件のダウンロードを保管するフォルダー  

- 次のオブジェクトのパス:  

    - IIS の Web サイト  

    - 仮想アプリケーションのインストール パス  

    - 仮想アプリケーション名  

- ブート メディアの .ISO ファイル名  


## <a name="additional-limitations"></a><a name="BKMK_OtherCharLimitations"></a> その他の制限事項

サポートされる文字セットと言語バージョンに関するその他の制限事項は以下のとおりです。  

- Configuration Manager では、サイト サーバー コンピューターのロケールの変更はサポートされません。  

- エンタープライズ証明機関 (CA) では、2 バイト文字セット (DBCS) を使用するクライアント コンピューター名はサポートされません。 使用可能なクライアント コンピューター名は、PKI の IA5 文字の制限を受けます。 Configuration Manager では、DBCS を使用する CA 名またはサブネット名の値はサポートされません。  


## <a name="objects-that-arent-localized"></a><a name="BKMK_LangNonLocalize"></a> ローカライズされないオブジェクト

Configuration Manager データベースでは、格納されるほとんどのオブジェクトに対して Unicode がサポートされます。 可能であれば、コンピューターのロケールと一致する OS の言語でこの情報が表示されます。 クライアント インターフェイスまたは Configuration Manager コンソールで情報をコンピューターの OS 言語で表示するためには、コンピューターのロケールが、サイトにインストールされているクライアントの言語またはサーバーの言語と一致している必要があります。  

いくつかの Configuration Manager オブジェクトでは Unicode はサポートされていません。 それらは ASCII を使用してデータベースに格納されるか、追加の言語の制限が適用されます。 この情報は、常に ASCII 文字セットを使用して表示されるか、オブジェクトの作成時に使用された言語で表示されます。  
