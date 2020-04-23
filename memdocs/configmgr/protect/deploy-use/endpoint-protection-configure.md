---
title: Endpoint Protection の構成
titleSuffix: Configuration Manager
description: Configuration Manager を設定して Windows Defender のマルウェア定義を更新および配布する方法について説明します。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e48f20dd56f445a10faa485b8bb7e86dbb05f75a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704520"
---
# <a name="configure-endpoint-protection"></a>Endpoint Protection の構成

*適用対象:Configuration Manager (Current Branch)*

Endpoint Protection を使用して構成マネージャー クライアント コンピューターのセキュリティとマルウェアを管理するには、事前にこの記事の構成手順を実行する必要があります。  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Configuration Manager の Endpoint Protection の構成方法  
 Configuration Manager の Endpoint Protection には、外部依存関係と製品内部の依存関係があります。  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Configuration Manager で Endpoint Protection を構成する手順  
 次の表に、Endpoint Protection の構成に関する手順、説明、および参照情報を示します。  

> [!IMPORTANT]  
>  Windows 10 コンピューターの Endpoint Protection を管理する場合、Windows Defender のマルウェア定義ファイルを更新し、配布するように Configuration Manager を構成する必要があります。 Windows Defender は Windows 10 に含まれていますが、SCEPInstall をインストールする必要があります。また、Endpoint Protection のカスタム クライアント設定が必要です (以下の**手順 5**)。 </br> </br>
> Configuration Manager 1802 以降、Windows 10 デバイスには、Endpoint Protection エージェント (SCEPInstall) をインストールする必要がありません。 Windows 10 デバイスに既にインストールされている場合、Configuration Manager は削除されません。 管理者は、少なくとも 1802 クライアント バージョンで実行されている Windows 10 デバイス上の Endpoint Protection エージェントを削除できます。 SCEPInstall.exe は、一部のコンピューターの C:\Windows\ccmsetup 上に引き続き存在する可能性がありますが、新しいクライアントのインストールにはダウンロードされない必要があります。 この場合も Endpoint Protection のカスタム クライアント設定 (**手順 5**) は必要です。 <!--503654-->

|手順|詳細|  
|-----------|-------------|  
|**手順 1:** [Endpoint Protection ポイント サイト システムの役割を作成する](endpoint-protection-site-role.md)|Endpoint Protection を使用するには、事前に Endpoint Protection ポイント サイト システムの役割をインストールしておく必要があります。 これは、1 つのサイト システム サーバーのみにインストールします。また、中央管理サイトまたはスタンドアロンのプライマリ サイトの階層の最上位にインストールしなければなりません。 |  
|**手順 2:** [Endpoint Protection のアラートを構成する](endpoint-configure-alerts.md)|マルウェア感染などの特定のイベントが発生すると、管理者にアラートが通知されます。 アラートは、 **[監視]** ワークスペースの **[アラート]** ノードに表示されます。必要に応じて、指定のユーザーに電子メールで送信することもできます。 |  
|**手順 3:** [Endpoint Protection クライアントの定義ファイルの更新ソースを構成する](endpoint-definition-updates.md)|Endpoint Protection は、さまざまなソースを使用して定義ファイルの更新をダウンロードするように構成できます。 |  
|**手順 4:** [既定のマルウェア対策ポリシーを構成してカスタムのマルウェア対策ポリシーを作成する](endpoint-antimalware-policies.md)|既定のマルウェア対策ポリシーは、Endpoint Protection クライアントがインストールされると適用されます。 展開されているカスタムのポリシーは、クライアント展開の 60 分以内に既定で適用されます。 Endpoint Protection クライアントを展開する前に、マルウェア対策ポリシーを構成していることを確認します。 |  
|**手順 5:** [Endpoint Protection のカスタム クライアント設定を構成する](endpoint-protection-configure-client.md)|カスタム クライアント設定を使用して、階層内のコンピューターのコレクションに Endpoint Protection 設定を構成します。<br /><br /> 注:階層内のすべてのコンピューターに適用する場合を除き、既定の Endpoint Protection クライアント設定は構成しないでください。 |  
