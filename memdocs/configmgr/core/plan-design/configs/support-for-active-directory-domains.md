---
title: Active Directory ドメインのサポート
titleSuffix: Configuration Manager
description: Active Directory ドメインで Configuration Manager サイト システムの要件について説明します。
ms.date: 10/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ab317597633eb432c73d2999590c1859124ddcfd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688580"
---
# <a name="support-for-active-directory-domains-in-configuration-manager"></a>Configuration Manager の Active Directory ドメインのサポート

*適用対象:Configuration Manager (Current Branch)*

すべての Configuration Manager サイト システムは、サポートされている Active Directory ドメインのメンバーであることが必要です。 Configuration Manager クライアント コンピューターは、ドメインのメンバー、またはワークグループのメンバーになれます。  

## <a name="requirements-and-limitations"></a>要件と制限事項

- ドメイン メンバーシップは、境界ネットワークでインターネット ベースのクライアント管理をサポートするサイト システムにも適用されます。 (このようなネットワークは、DMZ、非武装地帯、スクリーン サブネットと呼ばれることもあります)  

- サイト システムの役割をホストするコンピューターでは、次の構成は変更できません。  

  - ドメイン メンバーシップ (ドメインのサイト システムを削除して、同じドメインに再度参加することを含みます)

  - ドメイン名  

  - コンピューター名  

  これらの変更を行う前に、サイト システム ロールをアンインストールしてください。 サイト サーバーにこれらの変更を加えるには、まずサイトをアンインストールします。 また、サイト サーバー上でこの変更を管理するために、[パッシブ モードでサイト サーバー](../../servers/deploy/configure/site-server-high-availability.md)を作成することも検討してください。

- Configuration Manager では、Windows Server 2008 R2 以降のドメインおよびフォレストの機能レベルがサポートされています。<!-- SCCMDocs#1853 -->

## <a name="disjoint-namespace"></a><a name="bkmk_Disjoint"></a> 不整合のある名前空間

*名前空間に不整合*があるドメイン内で Configuration Manager のサイト システムとクライアントをインストールできます。  

不整合のある名前空間では、あるコンピューターのプライマリ DNS のサフィックスが、そのコンピューターの Active Directory DNS ドメイン名と一致しません。 それとは別の不正後のある名前空間のシナリオは、ドメイン コントローラーの NetBIOS ドメイン名が Active Directory DNS ドメイン名と一致しない場合に発生します。  

### <a name="disjoint-scenarios"></a>不整合のシナリオ

次のセクションに、不整合のある名前空間についてサポートされるシナリオを記載します。  

#### <a name="scenario-1"></a>例 1

ドメイン コントローラーのプライマリ DNS サフィックスが、Active Directory DNS ドメイン名と異なっています。 ドメインのメンバーであるコンピューターは、不整合になることも、不整合にならないこともあります。

このシナリオのドメイン コントローラーは不整合になります。 サイト サーバーやコンピューターなど、ドメインに属するコンピューターには、次のいずれかに一致するプライマリ DNS サフィックスを与えることができます。

- ドメイン コントローラーのプライマリ DNS サフィックス
- Active Directory DNS ドメイン名

#### <a name="scenario-2"></a>シナリオ 2

Active Directory ドメイン内のメンバー コンピューターには不整合があるにもかかわらず、ドメイン コントローラーには不整合がありません。

このシナリオでは、サイト システムのプライマリ DNS サフィックスが、Active Directory DNS ドメイン名と異なっています。 ドメイン コントローラーのプライマリ DNS サフィックスが、Active Directory DNS ドメイン名と同じです。 Configuration Manager クライアントであるメンバー コンピューターには、次のいずれかに一致するプライマリ DNS サフィックスを与えることができます。

- 不整合のあるサイト システム サーバーのプライマリ DNS サフィックス
- Active Directory DNS ドメイン名

### <a name="configure-disjoint-namespace"></a>不整合のある名前空間の構成

不整合のあるドメイン コントローラーにコンピューターがアクセスできるようにするには、ドメイン オブジェクト コンテナーの **msDS-AllowedDNSSuffixes** Active Directory 属性を変更します。 この属性に両方の DNS サフィックスを追加します。  

組織内のすべての DNS 名前空間が *DNS サフィックス検索一覧*に含まれていることを確認するには、不整合があるドメイン内のコンピューターごとに検索一覧を構成します。 名前空間の一覧に次のサフィックスを含めます。

- ドメイン コントローラーのプライマリ DNS サフィックス
- DNS ドメイン名
- Configuration Manager と通信することがある他のサーバーの追加の名前空間

グループ ポリシーを使用すると、**ドメイン ネーム システム (DNS) サフィックス検索**一覧を構成できます。  

> [!IMPORTANT]  
> Configuration Manager でコンピューターを参照する場合は、プライマリ DNS サフィックスを使用してコンピューターを入力します。 このサフィックスは、**dnsHostName** 属性として Active Directory ドメインに登録した完全修飾ドメイン名と一致し、およびシステムに関連付けられたサービス プリンシパル名と一致する必要があります。  

## <a name="single-label-domains"></a><a name="bkmk_SLD"></a> 単一ラベルのドメイン

Configuration Manager は、次に示す条件が満たされたときには、単一ラベルのドメイン内のサイト システムとクライアントをサポートします。  

- Active Directory Domain Services の単一ラベルのドメインは、有効な最上位ドメインを持つ不整合がある DNS 名前空間で構成します。  

  **例:** Contoso の単一ラベルのドメインは、contoso.com の DNS に不整合のある名前空間が含まれるように構成します。 Configuration Manager で Contoso ドメイン内のコンピューターに DNS サフィックスを指定するときには、"Contoso" ではなく "Contoso.com" を指定します。  

- システム コンテキストでのサイト サーバー間の分散コンポーネント オブジェクト モデル (DCOM) 接続は、Kerberos 認証を使用して正常に実行できる必要があります。  
