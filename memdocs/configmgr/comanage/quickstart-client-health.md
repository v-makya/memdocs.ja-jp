---
title: 共同管理でのクライアントの正常性
titleSuffix: Configuration Manager
description: Azure portal 上の Intune から Configuration Manager クライアントの正常性を把握する
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11fbeaf76737a832afca7351e8587e0d9c4bacac
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690830"
---
# <a name="client-health-with-co-management"></a>共同管理でのクライアントの正常性

ネットワークの正常性は、デバイスの移行時の正常性に直接関連します。 Intune は、ネットワーク上に存在しない場合でも異常なクライアントと通信することができます。 共同管理を使用して、この機能を Configuration Manager の機能と組み合わせて、98% の既知の正常なクライアントについて報告します。 その後、リアルタイムですべてのクライアントでの可視性を検出、評価、および提供できます。 Intune では、接続されたすべてのクライアントでのコンプライアンスのアップグレードに必要なサポートも追加されます。

次のビデオでは、シニア プログラム マネージャーの Rob York とプロダクト マーケティング マネージャーの Locky Ainley が共同管理でのクライアントの正常性について説明し、デモを行っています。

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>利点

クライアントの正常性の評価は最優先事項です。 System Center 2012 Configuration Manager では **CCMeval** が追加されました。 このユーティリティは、Configuration Manager クライアントの外部にあります。 クライアントの正常性の監視と自動修復が提供されます。 しかし、このレポートは、内部ネットワーク上に物理的または仮想的に存在するデバイスに依存します。 共同管理はこの問題に対処するのに役立ちます。

共同管理では、Intune でクライアントの正常性状態をレポートできます。 データの有効性に関するタイムスタンプ情報が提供されます。 この情報により、デバイスが正常であるか、接続可能であるか、アプリをインストールできるか、あるいは必要な OS ビルドに更新できるかどうかがわかります。 

この機能の詳細については、Ignite 2018 での [Configuration Manager の新機能](https://myignite.techcommunity.microsoft.com/sessions/64591)に関するセッションのこのビデオをご覧ください。

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


Configuration Manager で、クライアントがインストールされているというデバイス状態が提供されたが、そうではない場合、Intune で詳細情報を提供することができます。その場合、クライアントに接続する必要はありません。 Intune のデバイスの正常性情報は簡単に理解できます。 状態が**正常性**以外の場合、トラブルシューティングを行って修正するための推奨事項と次の手順が示されます。

> [!Note]  
> 今後のバージョンでは、次の利点が得られることが予想されます。
> - Configuration Manager で CCMeval に追加の機能が含まれます  
> - Configuration Manager と Intune の両方で異常である可能性のあるマシンをより簡単に識別できるようになります  
> - Intune でクライアントの正常性データをグループ化することができます  



## <a name="value-proposition"></a>価値提案

この機能では、現在、Intune で外部データ ソースを使用できます。 広範なクライアントの問題のトラブルシューティング時に、次の手順を決定することができます。 これで、追加のレポートを作成したり、他のツールを使ってクライアント データを引き出す必要はなくなります。

正常なクライアントがある場合は、修正プログラムのコンプライアンスはすぐに更新されます。 より適切な修正プログラムのコンプライアンスは、より適切なセキュリティを意味します。



## <a name="configure"></a>構成

この機能で作業を開始するには、次の手順を使用します。

- デバイスを Windows 10、バージョン 1709 以降に更新する  

- [共同管理を有効にする](how-to-enable.md)  
    - すべてのワークロードを Intune に切り替える必要はありません  

- Configuration Manager のサイトとクライアントを*バージョン 1806* 以降に更新する  


### <a name="review-configuration-manager-client-health-in-intune"></a>Intune で Configuration Manager クライアントの正常性を確認する

1. [Azure ポータル](https://portal.azure.com/)することができます。  

2. **[すべてのサービス]**  >  **[Intune]** の順に選択します。 Intune は **[監視 + 管理]** セクションにあります。  

3. **[Microsoft Intune]** ウィンドウを開いたら、 **[ヘルプとサポート]** の下にあるメニューから、 **[トラブルシューティング]** ページに移動します。  

4. **[ユーザーの選択]** オプションを使用して、 **[デバイス]** リストで特定のデバイスを見つけ、それを選択してデバイス ページを開きます。  

5. 共同管理の情報は、デバイス ページの下部に表示されます。 この情報には、クライアントの正常性の次のフィールドが含まれます。  
    - **Configuration Manager エージェントの状態**  
    - **Configuration Manager エージェントの最終チェックイン時刻**  

> [!Tip]  
> Intune に登録されたデバイスは、1 日 3 回、約 8 時間ごとにクラウド サービスに接続されます。 
