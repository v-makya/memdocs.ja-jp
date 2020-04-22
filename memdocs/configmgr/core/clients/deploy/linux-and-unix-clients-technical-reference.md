---
title: UNIX/Linux クライアントのコンポーネント サービスとコマンド
titleSuffix: Configuration Manager
description: Configuration Manager での Linux クライアントおよび UNIX クライアントに対するコンポーネント サービスとコマンドについて説明します。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de564595ce51a336b5f11d4050928fa812269601
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693890"
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-configuration-manager"></a>Configuration Manager 用の Linux クライアントおよび UNIX クライアントのコンポーネント サービスとコマンド

*適用対象:Configuration Manager (Current Branch)*

> [!Important]  
> バージョン 1902 以降の Configuration Manager では、Linux または UNIX クライアントはサポートされていません。 
> 
> Linux サーバーを管理するには、Microsoft Azure の管理を検討してください。 Azure ソリューションには広範囲な Linux サポートが含まれており、ほとんどの場合、Linux のエンドツーエンド パッチ管理など、Configuration Manager 以上の機能を備えています。


 Linux および UNIX 用 Configuration Manager クライアントのクライアント コンポーネント サービスを次の表に示します。  

|［ファイル名］|説明|  
|---------------|----------------------|  
|ccmexec.bin|このサービスは、Windows ベースのクライアントの ccmexc サービスに似ています。 Configuration Manager サイト システムの役割とのすべての通信を担当します。また、ローカル コンピューターからハードウェア インベントリを収集するために omiserver.bin サービスとも通信します。<br /><br /> サポートされているコマンド ライン引数を確認するには、`ccmexec -h` を実行してください|  
|omiserver.bin|このサービスは、CIM サーバーです。 CIM サーバーでは、プロバイダーと呼ばれるプラグ可能なソフトウェア モジュールのフレームワークを提供します。 プロバイダーは、Linux および UNIX コンピューターのリソースと対話し、ハードウェア インベントリ データを収集します。 たとえば、 **プロセス プロバイダー** Linux のコンピューターは Linux オペレーティング システムのプロセスに関連付けられているデータを収集します。|  

 開始するには、使用できる次のテーブル一覧のコマンドでは、停止、または、Linux または UNIX のバージョンごとに、クライアント サービス (ccmexec.bin および omiserver.bin) を再起動します。 ccmexec サービスを開始または停止すると、omiserver サービスも開始または停止します。  

|オペレーティング システム|コマンド|  
|----------------------|--------------|  
|Universal Agent<br /><br /> RHEL 4 および SLES 9|開始: `/etc/init d/ccmexecd start`<br /><br /> 停止: `/etc/init d/ccmexecd stop`<br /><br /> 再起動: `/etc/init d/ccmexecd restart`|  
|Solaris 9|開始: `/etc/init d/ccmexecd start`<br /><br /> 停止: `/etc/init d/ccmexecd stop`<br /><br /> 再起動: `/etc/init d/ccmexecd restart`|  
|Solaris 10|開始:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> 停止:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|Solaris 11|開始:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> 停止:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|AIX|開始:<br /><br /> `startsrc -s omiserver`<br /><br /> `startsrc -s ccmexec`<br /><br /> 停止:<br /><br /> `stopsrc -s ccmexec`<br /><br /> `stopsrc -s omiserver`|  
|HP-UX|開始: `/sbin/init.d/ccmexecd start`<br /><br /> 停止: `/sbin/init.d/ccmexecd stop`<br /><br /> 再起動: `/sbin/init.d/ccmexecd restart`|  
