---
title: クエリのセキュリティとプライバシー
titleSuffix: Configuration Manager
description: サイト データベースから情報のクエリを実行するときのセキュリティとプライバシーのベスト プラクティスを理解します。
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 882eedd1be029d5824fbd5d26a3f08d8f8f0021d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695700"
---
# <a name="security-and-privacy-for-queries-in-configuration-manager"></a>Configuration Manager のクエリのセキュリティとプライバシー

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager でクエリを使用すると、指定した条件に従ってサイト データベースの情報を取得できます。 Configuration Manager では、標準操作中にサイト データベース情報が収集されます。 たとえば、探索またはインベントリ中に収集された情報を使用して、特定の条件を満たすデバイスを特定するクエリを構成できます。  

 クエリの詳細については、[クエリの概要](../../../core/servers/manage/introduction-to-queries.md)に関するページを参照してください。 クエリを使用することで取得できるデータを収集する Configuration Manager の操作に関するセキュリティのベスト プラクティスとプライバシー情報について詳しくは、「[Configuration Manager のセキュリティとプライバシー](../../../core/plan-design/security/security-and-privacy.md)」をご覧ください。  

## <a name="security-best-practices-for-queries"></a>クエリについて推奨するセキュリティ運用方法

 クエリに対して、セキュリティに関する次のベスト プラクティスを使用してください。  

|セキュリティのベスト プラクティス|説明|  
|----------------------------|----------------------|  
|ネットワークの場所に保存されているクエリをエクスポートまたはインポートする場合は、その場所とネットワーク チャネルをセキュリティで保護します。|ネットワーク フォルダーにアクセスできるユーザーを制限します。<br /><br /> ネットワークの場所とサイト サーバー間でサーバー メッセージ ブロック (SMB) 署名またはインターネット プロトコル セキュリティ (IPsec) を使用し、インポートする前のクエリ データが攻撃者によって改ざんされるのを防止します。|  

## <a name="next-steps"></a>次のステップ
  
[Configuration Manager のセキュリティとプライバシー](../../../core/plan-design/security/security-and-privacy.md)
