---
title: 証明書プロファイルの前提条件
titleSuffix: Configuration Manager
description: Configuration Manager の証明書プロファイル、およびそれらの外部依存関係と製品内依存関係について説明します。
ms.date: 12/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0317fd02-3721-4634-b18b-7c976a4e92bf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: eed68d976235dbd915c46bbd2d410d7953441bd3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906861"
---
# <a name="prerequisites-for-certificate-profiles-in-configuration-manager"></a>Configuration Manager の証明書プロファイルの前提条件

*適用対象:Configuration Manager (Current Branch)*


Configuration Manager の証明書プロファイルには、外部依存関係と製品内依存関係があります。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係  

|依存関係|説明|  
|----------------|----------------------|  
|Active Directory 証明書サービス (AD CS) を実行するエンタープライズ証明機関 (CA)<br /><br /> 証明書を失効させるには、階層の最上位のサイト サーバーのコンピューター アカウントに *証明書の発行と管理* の権限が、証明書管理者の証明書プロファイルが使用する各証明書テンプレートに対して必要となります。 または、証明書管理者に、その証明書管理者が使用するすべての証明書テンプレートに対するアクセス許可を付与します。<br /><br /> 証明書要求のCA マネージャーによる承認が必要になるように設定することもできます。 ただし、証明書の発行に使用する証明書テンプレートで、証明書のサブジェクトを **[要求に含まれる]** に設定して、Configuration Manager によってサブジェクトの値が自動的に含まれるようにする必要があります。|Active Directory 証明書サービスの詳細については、「[Active Directory 証明書サービスの概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831740(v=ws.11))」を参照してください。|  
|PowerShell スクリプトを使用して検証し、必要に応じて、ネットワーク デバイス登録サービス (NDES) のロール サービスと Configuration Manager 証明書登録ポイントの前提条件をインストールします。 <br /><br />|指示ファイルの readme_crp.txt は、ConfigMgrInstallDir\cd.latest\SMSSETUP\POLICYMODULE\X64 にあります。<br /><br />PowerShell スクリプトの Test-NDES-CRP-Prereqs.ps1 は、指示と同じディレクトリにあります。 <br /><br /> PowerShell スクリプトは、NDES サーバーでローカルに実行する必要があります。|
|Windows Server 2012 R2 で実行される、Active Directory 証明書サービス用のネットワーク デバイス登録サービス (NDES) の役割サービス。<br /><br /> さらに<br /><br /> クライアントとネットワーク デバイス登録サービス間の通信で、TCP 443 (HTTPS 用) と TCP 80 (HTTP 用) 以外のポート番号を使用することはできません。<br /><br /> ネットワーク デバイス登録サービスを実行するサーバーは、発行元 CA とは別のサーバーに配置する必要があります。|Configuration Manager は、Windows Server 2012 R2 のネットワーク デバイス登録サービスと通信して、Simple Certificate Enrollment Protocol (SCEP) 要求を生成および検証します。<br /><br /> インターネットから接続するユーザーやデバイス (Microsoft Intune で管理されているモバイル デバイスなど) に証明書を発行する場合は、これらのデバイスが、ネットワーク デバイス登録サービスを実行しているサーバーにインターネットからアクセスできる必要があります。 たとえば、このサーバーを境界ネットワーク (DMZ、非武装地帯、スクリーン サブネットともいいます) に設置します。<br /><br /> ネットワーク デバイス登録サービスを実行するサーバーと発行元 CA の間にファイアウォールがある場合は、この 2 つのサービス間の通信トラフィック (DCOM) を許可するようにファイアウォールを構成する必要があります。 Configuration Manager サイト サーバーを実行するサーバーと発行元 CA 間の通信も同様に設定して、Configuration Manager が証明書を失効できるようにします。<br /><br /> SSL を必要とするようにネットワーク デバイス登録サービスが構成されている場合は、セキュリティのベスト プラクティスに従って、接続するデバイスがサーバー証明書を検証するために証明書失効リスト (CRL) にアクセスできるようにしてください。<br /><br /> ネットワーク デバイス登録サービスの詳細については、「[ポリシー モジュールとネットワーク デバイス登録サービスの使用](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn473016(v=ws.11))」を参照してください。|  
|PKI クライアント認証証明書およびエクスポートされたルート CA 証明書|この証明書は、ネットワーク デバイス登録サービスを実行しているサーバーが Configuration Manager から認証を受けるための証明書です。<br /><br /> 詳細については、「[Configuration Manager での PKI 証明書の要件](../../core/plan-design/network/pki-certificate-requirements.md)」をご覧ください。|  
|サポートされるデバイス オペレーティング システム|Windows 8.1、Windows RT 8.1、および Windows 10 を実行しているデバイスに証明書プロファイルを展開できます。|  

## <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係  

|依存関係|説明|  
|----------------|----------------------|  
|証明書登録ポイントのサイト システムの役割|証明書プロファイルを使用する前に、証明書登録ポイントのサイト システムの役割をインストールする必要があります。 この役割で Configuration Manager データベース、Configuration Manager サイト サーバー、および Configuration Manager ポリシー モジュールと通信します。<br /><br /> このサイト システムの役割のシステム要件とこの役割をインストールする階層内の場所の詳細については、「[Configuration Manager のサポートされている構成](../../core/plan-design/configs/supported-configurations.md)」記事の「**サイト システムの要件**」セクションを参照してください。<br /><br /> 証明書登録ポイントは、ネットワーク デバイス登録サービスを実行するサーバーと同じサーバーにインストールしないでください。|  
|Configuration Manager ポリシー モジュールが、Active Directory 証明書サービス用のネットワーク デバイス登録サービスの役割サービスを実行するサーバーにインストールされていること|証明書プロファイルを展開するには、Configuration Manager ポリシー モジュールをインストールする必要があります。 このポリシー モジュールは、Configuration Manager インストール メディアに収録されています。|  
|探索データ|証明書のサブジェクトとサブジェクトの別名の値は Configuration Manager によって供給され、検出によって収集された情報から取得されます。<br /><br /> ユーザー証明書:Active Directory ユーザー検出<br /><br /> コンピューター証明書:Active Directory システム探索とネットワーク探索|  
|証明書プロファイルを管理するためのセキュリティのアクセス許可|証明書プロファイルや Wi-Fi プロファイル、VPN プロファイルなどの会社のリソースのアクセス設定を管理するには、次のセキュリティのアクセス許可が必要です。<br /><br /> 証明書プロファイルのアラートとレポートを表示して管理する: **[アラート]** オブジェクトの **[作成]** 、 **[削除]** 、 **[変更]** 、 **[レポートの変更]** 、 **[読み取り]** 、 **[レポートの実行]** 。<br /><br /> 証明書プロファイルを作成して管理する: **[証明書プロファイル]** オブジェクトの **[作成者ポリシー]** 、 **[レポートの変更]** 、 **[読み取り]** 、 **[レポートの実行]** 。<br /><br /> Wi-Fi プロファイル、証明書プロファイル、VPN プロファイルの展開を管理する: **[コレクション]** オブジェクトの **[構成ポリシーの展開]** 、 **[クライアント ステータス アラートの変更]** 、 **[読み取り]** 、 **[リソースの読み取り]** 。<br /><br /> すべての構成ポリシーを管理する: **[構成のポリシー]** オブジェクトの **[作成]** 、 **[削除]** 、 **[変更]** 、 **[読み取り]** 、 **[セキュリティ スコープの設定]** 。<br /><br /> 証明書プロファイルに関連するクエリを実行する: **[クエリ]** オブジェクトの **[読み取り]** アクセス許可。<br /><br /> Configuration Manager コンソールで証明書プロファイルの情報を表示する: **[サイト]** オブジェクトの **[読み取り]** アクセス許可。<br /><br /> 証明書プロファイルのステータス メッセージを表示する: **[ステータス メッセージ]** オブジェクトの **[読み取り]** アクセス許可。<br /><br /> 信頼された証明機関証明書プロファイルを作成および変更する: **[信頼された証明機関証明書プロファイル]** オブジェクトの **[作成者ポリシー]** 、 **[レポートの変更]** 、 **[読み取り]** 、 **[レポートの実行]** 。<br /><br /> VPN プロファイルを作成して管理する: **[VPN プロファイル]** オブジェクトの **[作成者ポリシー]** 、 **[レポートの変更]** 、 **[読み取り]** 、 **[レポートの実行]** 。<br /><br /> Wi-Fi プロファイルを作成して管理する: **[Wi-Fi プロファイル]** オブジェクトの **[作成者ポリシー]** 、 **[レポートの変更]** 、 **[読み取り]** 、 **[レポートの実行]** 。<br /><br /> **[会社リソース アクセス マネージャー]** セキュリティ ロールには、Configuration Manager で証明書プロファイルを管理するのに必要な上記のアクセス許可が付与されています。 詳細については、「[セキュリティの構成](../../core/plan-design/security/configure-security.md)」記事の「**ロールベースの管理の構成**」セクションを参照してください。|  
