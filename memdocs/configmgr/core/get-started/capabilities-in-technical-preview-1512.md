---
title: Technical Preview 1512 の機能
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1512 で使用できる機能について説明します。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 03a6e7cd49bbb5a65a4364be398961c048d2a1b9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705680"
---
# <a name="capabilities-in-technical-preview-1512-for-configuration-manager"></a>Configuration Manager の Technical Preview 1512 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1512 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 このバージョンの Technical Preview をインストールする前に、説明のトピック「[Configuration Manager の Technical Preview](technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。  

 このバージョンでお試しいただける新機能を次に示します。  

##  <a name="device-health-attestation"></a><a name="bkmk_devicehealth"></a> デバイス正常性構成証明書  
 Technical Preview 1512 以降、管理者は Configuration Manager コンソールで Windows 10 デバイス正常性構成証明書の状態を確認できます。  この機能は、Configuration Manager および Configuration Manager と Microsoft Intune の併用で利用できます。 デバイス正常性構成証明書により、管理者はクライアント コンピューターの BIOS、TPM、ブート ソフトウェア構成が信頼のおけるものであることを確認できます。 デバイス正常性構成証明書をサポートするために、クライアント デバイスは、TPM 2 を有効にして Win10 を実行している必要があります。 デバイス正常性構成証明書には、次のそれぞれに対応しているデバイスの数が表示されます。  

-   起動時マルウェア対策  

-   BitLocker  

-   セキュア ブート  

-   コードの整合性  

コンソールには、最も不足している正常性構成証明書の設定もデバイスの数と共に表示されます。  

デバイス正常性構成証明書のプレビューを表示するには、Configuration Manager コンソールで **[監視]** ワークスペースに移動し、 **[セキュリティ]** ノードをクリックしてから **[正常性構成証明書]** をクリックします。  

##  <a name="in-console-monitoring-for-terms-and-conditions"></a><a name="bkmk_viewterms"></a> 使用条件のコンソール内での監視  
Technical Preview 1512 以降、Configuration Manager を Microsoft Intune と統合すると、Configuration Manager コンソールを使用して、IT 部門が構成した使用条件に同意したユーザーと同意していないユーザーを表示できます。  

**概要情報を表示するには:**  

-   Configuration Manager コンソールで **[監視]**  >  **[概要]**  >  **[展開]** の順に移動して、表示する使用条件の展開を選びます。  

**詳細情報を表示するには:**  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[概要]**  >  **[コンプライアンス設定]**  >  **[使用条件]** の順に移動して、表示する使用条件を選びます。  

2.  コンソールの下部にある **[展開]** タブを選び、展開を選んだら、 **[状態の表示]** をクリックします。  

##  <a name="improvements-to-endpoint-protection-policy-settings"></a><a name="bkmk_EPpolicy"></a> Endpoint Protection のポリシー設定の機能強化  
1512 Technical Preview では、Endpoint Protection マルウェア対策ポリシーに次の新しい設定が追加されました。  

-   リアルタイム保護: **ダウンロード時およびインストール前に、望ましくない可能性のあるアプリケーションをブロックする**  

    -   望ましくない可能性のあるアプリケーション (PUA) とは、評価および研究主導の識別に基づく脅威の分類の 1 つです。 ほとんどの場合、これらは望ましくないアプリケーションバンドラーか、そのバンドルされたアプリケーションです。  

    -   この保護ポリシーの設定は既定で有効になっています ([はい] に設定)。 この設定が有効な場合、PUA はダウンロード時とインストール時にブロックされます。 ただし、特定のファイルやフォルダーに環境内の特定のニーズを満たすを除外することができます。  

-   スキャンの設定: **フル スキャンの実行時に、マップされたネットワーク ドライブをスキャンする**  

    -   この設定により、管理者はより詳細な操作ができるようになり、スケジュールされたフル スキャン中にマップされたネットワーク ドライブが必ずスキャンされるリスクなしに、ネットワーク ファイルのオンデマンド スキャンができるようになります。  

    -   この設定を構成できるようにするには、設定 **ネットワーク ファイルをスキャンする** を最初に有効 (はい) にする必要があります。  

    -   既定で、この設定は [いいえ] になっており、マップされたネットワーク ドライブはフル スキャンでアクセスされません。  

-   自動サンプル ファイルの送信の設定:  

     マルウェア対策エンジンは、さらに詳しい分析のために Microsoft へのファイルのサンプルの送信を要求することがあります。 既定では、このようなサンプルを送信する前に必ず確認が求められます。 管理者は、この動作を構成する次の設定を管理できるようになりました。  

    -   詳細: **サンプル ファイルの自動送信を有効にすると、Microsoft は検出された特定の項目が危険であるかどうかを判断できます**。この設定を [はい] に設定して、サンプル ファイルの自動送信を有効にします。 既定では、この設定は [いいえ] で、サンプル ファイルの自動送信は無効であり、サンプルの送信前にユーザーに確認が求められます。   (この設定は、System Center 2012 R2 Configuration Manager SP1 で初めて導入されました)  

    -   詳細: **サンプル ファイルの自動送信の設定を変更することをユーザーに許可します**。この設定は、デバイス上のローカルの管理者権限を持つユーザーがクライアント インターフェイスでサンプル ファイルの自動送信の設定を変更できるかどうかを決定します。 既定では、この設定は [いいえ] です。つまり、設定は Configuration Manager コンソール内からのみ変更でき、デバイスのローカル管理者はこの構成を変更できません。  

         たとえば、管理者によって設定され、ユーザーが変更を許可されていない Windows 10 の Windows Defender の設定を次に示します。  

         ![TechRef&#95;WinDefender](../../core/get-started/media/TechRef_WinDefender.png "TechRef_WinDefender")  

    さらに、Endpoint Protection マルウェア対策ポリシーの [除外の設定] セクションの既存の **[ファイルとフォルダーを除外する]** 設定が改善され、デバイスを除外できるようになりました。 たとえば、 **\device\mvfs** を除外するよう指定できます (Multiversion File System の場合)。 ポリシーはデバイスのパスを検証しません。Endpoint Protection のポリシー設定は、デバイスの文字列を解釈できるクライアントのマルウェア対策エンジンに提供されます。  

**Endpoint Protection ポリシーを使用するための前提条件:**  

Endpoint Protection ポリシーを使用するには、Endpoint Protection クライアント設定を使用して、Endpoint Protection クライアントのインストールと管理をしておく必要があります。 これは、Windows 7、Windows 8、Windows 8.1 用の System Center Endpoint Protection クライアント、または Windows 10 用の管理されている Windows Defender を使用して行います。 「[Endpoint Protection](../../protect/deploy-use/endpoint-protection.md)」を参照してください。  
