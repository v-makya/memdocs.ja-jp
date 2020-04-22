---
title: コレクションのセキュリティとプライバシー
titleSuffix: Configuration Manager
description: Configuration Manager のコレクションのセキュリティとプライバシーのベスト プラクティスを入手します。
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 42345ee91baaad7dcc82eab537fbeb697d6cd7ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695530"
---
# <a name="security-and-privacy-for-collections-in-configuration-manager"></a>Configuration Manager のコレクションのセキュリティとプライバシー

*適用対象:Configuration Manager (Current Branch)*

このトピックには、Configuration Manager のコレクションに対するセキュリティのベスト プラクティスとプライバシー情報が含まれています。  

 Configuration Manager のコレクションには特別なプライバシー情報はありません。 コレクションは、ユーザーやデバイスなどのリソースのコンテナーです。 コレクション メンバーシップは、標準操作中に Configuration Manager が収集する情報によって変わることがあります。 たとえば、探索またはインベントリで収集されたリソース情報を使用して、コレクションが特定の条件に合うデバイスを含むように構成されることがあります。 コレクションが、ソフトウェアの展開や対応確認など、クライアント管理操作のための現在のステータス情報をベースにする可能性もあるのです。 クエリ ベースのコレクションに加えて、管理ユーザーはリソースをコレクションに追加することもできます。  

 コレクションの詳細については、[コレクションの概要](../../../../core/clients/manage/collections/introduction-to-collections.md)に関するページを参照してください。 コレクション メンバーシップの構成に使用することができる Configuration Manager 操作に関するセキュリティのベスト プラクティスとプライバシー情報の詳細については、[Configuration Manager のセキュリティのベスト プラクティスとプライバシー情報](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md)に関するページを参照してください。  

## <a name="security-best-practices-for-collections"></a>コレクションについて推奨するセキュリティ運用方法  
 次の表に、コレクションについて推奨する運用方法をまとめます。  

|セキュリティのベスト プラクティス|説明|  
|----------------------------|----------------------|  
|ネットワークの場所に保存されているマネージド オブジェクト フォーマット (MOF) ファイルを使用してエクスポートまたはインポートするときには、ネットワークの場所とネットワーク チャネルをセキュリティで保護します。|ネットワーク フォルダーにアクセスできるユーザーを制限します。<br /><br /> ネットワークの場所とサイト サーバーの間で、サーバー メッセージ ブロック (SMB) 署名またはインターネット プロトコル セキュリティ (IPsec) を使用して、攻撃者からエクスポートされたコレクション データの改ざんを防止します。 情報開示を防ぐため、IPsec を使用してネットワーク上のデータを暗号化します。|  

### <a name="security-issues-for-collections"></a>コレクションについてのセキュリティの問題  
 コレクションには次のようなセキュリティの問題が伴います。  

-   コレクション変数を使用すると、ローカル管理者が機密情報を読めてしまう可能性があります。  

     コレクション変数は、オペレーティング システムを展開する際に使用することができます。  
