---
title: マルウェアからコンピューターを保護する
titleSuffix: Configuration Manager
description: Configuration Manager で Endpoint Protection を実装してマルウェアからコンピューターを保護する方法について説明します。
ms.date: 05/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
author: mestew
ms.author: mstewart
manager: doubeby
ms.openlocfilehash: 6e0e350fe490de50a053e93f2922feba5e0ea8c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706420"
---
# <a name="example-scenario-use-endpoint-protection-to-protect-computers-from-malware"></a>シナリオ例: マルウェアからコンピューターを保護するために Endpoint Protection を使用する

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager で Endpoint Protection を実装して、組織のコンピューターをマルウェアによる攻撃から保護する方法に関するサンプル シナリオを示します。  



## <a name="scenario-overview"></a>シナリオの概要

 ウッドグローブ銀行では、Configuration Manager がインストールされ、使用されています。 現在この銀行は System Center Endpoint Protection を使用して、マルウェアによる攻撃からコンピューターを保護しています。 また、Windows グループ ポリシーによって、社内のすべてのコンピューターで Windows ファイアウォールが有効になっていること、Windows ファイアウォールが新しいプログラムをブロックする場合にはユーザーに通知することが確認されています。  

Configuration Manager 管理者は、ウッドグローブ銀行のマルウェア対策ソフトウェアを System Center Endpoint Protection にアップグレードするよう依頼されています。これにより、この銀行は、最新のマルウェア対策機能の恩恵を受け、Configuration Manager コンソールからマルウェア対策ソリューションを一元管理できるようになります。 


## <a name="business-requirements"></a>業務要件

この実装を行うには、以下の要件があります。  

- Configuration Manager を使用して、現在グループ ポリシーによって管理されている Windows ファイアウォール設定を管理します。  

- Configuration Manager ソフトウェア更新プログラムを使用して、マルウェア定義をコンピューターにダウンロードします。 ソフトウェア更新プログラムが利用できない場合 (たとえば、コンピューターが企業ネットワークに接続されていない場合など)、コンピューターによって Microsoft Update から定義の更新プログラムのダウンロードが行われる必要があります。  

- ユーザーのコンピューターでは、毎日マルウェアのクイック スキャンを実行する必要があります。 ただしサーバーは、業務時間外の毎週土曜日午前 1 時に、フル スキャンを実行する必要があります。  

- 次のいずれかのイベントが発生するたびに電子メール アラートを送信します。  

  -   いずれかのコンピューターでマルウェアが検出される。  

  -   5% を超えるコンピューターで同じマルウェアの脅威が検出される  

  -   任意の 24 時間以内に同じマルウェアの脅威が 6 回以上検出される  

  -   任意の 24 時間以内に 4 つ以上の異なる種類のマルウェアが検出される  

  管理者は、Endpoint Protection を実装するために次の手順を行います。  



##  <a name="steps-to-implement-endpoint-protection"></a>Endpoint Protection を実装する手順を実行します。  

|プロセス|参照先|  
|-------------|---------------|  
|管理者は、Configuration Manager での Endpoint Protection の基本概念に関して、提供されている情報を確認します。|Endpoint Protection の詳細については、「[Endpoint Protection](endpoint-protection.md)」を参照してください。|  
|管理者は Endpoint Protection を使用するために必要な前提条件を確認して実装します。|Endpoint Protection の前提条件の詳細については、「[Endpoint Protection の導入計画](../plan-design/planning-for-endpoint-protection.md)」を参照してください。|  
|管理者は、ウッドグローブ銀行の最上位階層にある 1 つのサイト システム サーバーにのみ Endpoint Protection サイト システムの役割をインストールします。|Endpoint Protection サイト システムの役割をインストールする方法について詳しくは、「[Configure Endpoint Protection](endpoint-protection-configure.md)」(Endpoint Protection の構成) の「前提条件」を参照してください。|  
|管理者は、SMTP サーバーを使用して電子メール アラートを送信するように Configuration Manager を構成します。<br /><br /> **注:** SMTP サーバーを構成する必要があるのは、Endpoint Protection アラートが生成されるときに電子メールで通知する場合のみです。|詳細については、「[Endpoint Protection のアラートを構成する](endpoint-configure-alerts.md)」を参照してください。|  
|管理者は、Endpoint Protection クライアントをインストールするすべてのコンピューターとサーバーが含まれるデバイス コレクションを作成します。 管理者は、このコレクションに「**Endpoint Protection によって保護されるすべてのコンピューター**」という名前を付けます。<br /><br /> **ヒント**: ユーザーのコレクションに対してアラートを構成することはできません。|コレクションの作成方法については、[コレクションの作成方法](../../core/clients/manage/collections/create-collections.md)に関するページを参照してください。|  
|管理者は、コレクションに対して次のアラートを構成します。 <br /><br />1) **マルウェアが検出された場合**:管理者はアラートの重要度 **[重大]** を構成します。 <br /><br />2) **多数のコンピューターで同じ種類のマルウェアが検出された場合**:管理者はアラートの重要度 **[重大]** を構成し、5% を超えるコンピューターでマルウェアが検出された場合にこのアラートが生成されることを指定します。 <br /><br />3) **同種類のマルウェアが指定時間内に特定のコンピューター上で繰り返し検出される場合**:管理者はアラートの重要度 [重大] を構成し、マルウェアが 24 時間以内に 5 回を超えて検出された場合にこのアラートが生成されることを指定します。 <br /><br />4) **複数の種類のマルウェアが指定時間内に同じコンピューター上で検出される場合**:管理者はアラートの重要度 [重大] を構成し、3 種類を超えるマルウェアが 24 時間以内に検出された場合にこのアラートが生成されることを指定します。<br /><br /> **[アラートの重要度]** の値は、Configuration Manager コンソールに、および電子メール メッセージで受信するアラートに表示されるアラート レベルを示します。<br /><br /> さらに、Configuration Manager コンソールでアラートを監視できるように、オプション **[このコレクションを Endpoint Protection ダッシュボードに表示する]** を選択します。|「[Endpoint Protection の構成](endpoint-configure-alerts.md)」で "Configuration Manager でのアラートの構成方法" を参照してください。|  
|管理者は、Configuration Manager ソフトウェア更新プログラムを、自動展開ルールを使用して 1 日に 3 回、定義の更新プログラムをダウンロードして展開するように構成します。|詳細については、「[Use Configuration Manager software updates to deliver definition updates](endpoint-definitions-configmgr.md)」(Configuration Manager ソフトウェア更新プログラムを使用して定義の更新プログラムを配信する) の「Configuration Manager ソフトウェア更新プログラムにより定義の更新プログラムを配信する」を参照してください。|  
|管理者は、Microsoft によって推奨されているセキュリティ設定が含まれる、既定のマルウェア対策ポリシーの設定を調べます。 毎日のクイック スキャンを実行するコンピューターに関しては、次の設定を変更します。<br /><br /> 1) **クライアント コンピューターでクイック スキャンを毎日実行する**: **はい**。<br /><br /> 2) **日次クイック スキャンの実行予定時刻**: **午前 9:00**。<br /><br /> 管理者は、定義の更新のソースとして **[Microsoft Update から配信される更新プログラム]** が既定で選択されていることに注意します。 この選択項目は、Configuration Manager ソフトウェアの更新プログラムを受信できない場合に、コンピューターによる Microsoft Update からの定義のダウンロードする、というビジネス要件と合致します。|[Endpoint Protection 用にマルウェア対策ポリシーを作成し展開する方法](endpoint-antimalware-policies.md)に関する記事を参照してください。|  
|管理者は、「**Woodgrove Bank のサーバー**」という名前の Woodgrove Bank のサーバーのみが含まれるコレクションを作成します。|[コレクションの作成方法](../../core/clients/manage/collections/create-collections.md)に関するページを参照してください|  
|管理者は、「**Woodgrove Bank のサーバー ポリシー**」という名前のカスタム マルウェア対策ポリシーを作成します。 **[スケジュールされたスキャン]** の設定のみを追加し、次の変更を行います。<br /><br /> **スキャンの種類**: **完全**<br /><br /> **スキャンの実行日**: **土曜日**<br /><br /> **スキャン時刻**: **午前 1:00**<br /><br /> **クライアント コンピューターでクイック スキャンを毎日実行する**: **いいえ**。|[Endpoint Protection 用にマルウェア対策ポリシーを作成し展開する方法](endpoint-antimalware-policies.md)に関する記事を参照してください。|  
|管理者は、「**Woodgrove Bank のサーバー ポリシー**」カスタム マルウェア対策ポリシーを「**Woodgrove Bank のサーバー**」コレクションに展開します。|「[Endpoint Protection 用にマルウェア対策ポリシーを作成し展開する方法](endpoint-antimalware-policies.md)」の「マルウェア対策ポリシーをクライアント コンピューターに展開するには」を参照してください。|  
|管理者は Endpoint Protection の新しいカスタム クライアント デバイス設定セットを作成し、「**ウッドグローブ銀行の Endpoint Protection 設定**」という名前を付けます。<br /><br /> **注:** 階層内のすべてのクライアントにおいて Endpoint Protection をインストールして使用可能にする必要がない場合には、 **[クライアント コンピューターの Endpoint Protection クライアントを管理する]** と **[Endpoint Protection クライアントをクライアント コンピューターにインストールする]** のどちらも既定のクライアント設定として **[いいえ]** に構成されていることを確認してください。|詳しくは、の「[Endpoint Protection のカスタム クライアント設定を構成する](endpoint-protection-configure-client.md)」を参照してください。|  
|Endpoint Protection に関して以下の設定を構成します。<br /><br /> **[クライアント コンピューターの Endpoint Protection クライアントを管理する]** : **はい**<br /><br /> この設定と値を使用すると、インストールされている既存のすべての Endpoint Protection クライアントが Configuration Manager によって管理されます。<br /><br /> **[Endpoint Protection クライアントをクライアント コンピューターにインストールする]** : **はい**。</br></br>**注**: Configuration Manager 1802 以降では、Windows 10 デバイスに Endpoint Protection エージェントをインストールする必要がありません。 それが Windows 10 デバイスに既にインストールされている場合は、Configuration Manager によって削除されることはありません。 管理者は、少なくとも 1802 クライアント バージョンで実行されている Windows 10 デバイス上の Endpoint Protection エージェントを削除できます。|詳しくは、の「[Endpoint Protection のカスタム クライアント設定を構成する](endpoint-protection-configure-client.md)」を参照してください。|  
|管理者は、「**Woodgrove Bank の Endpoint Protection 設定**」クライアント設定を「**Endpoint Protection によって保護されたすべてのコンピューター**」コレクションに展開します。|「[Configuration Manager の Endpoint Protection の構成](endpoint-antimalware-policies.md)」の「Endpoint Protection のカスタム クライアント設定を構成する」を参照してください。|  
|管理者は、Windows ファイアウォール ポリシーの作成ウィザードを使用して、ドメイン プロファイル用の次の設定を構成してポリシーを作成します。<br /><br /> 1) **[Windows ファイアウォールを有効にする]** : **はい**<br /><br /> 2)<br />                    **[Windows ファイアウォールが新しいプログラムをブロックしたときにユーザーに通知する]** : **はい**|[Endpoint Protection 用 Windows ファイアウォール ポリシーの作成および展開方法](../../protect/deploy-use/create-windows-firewall-policies.md)に関するページを参照してください。|  
|管理者は新しいファイアウォール ポリシーを、先に作成した「**Endpoint Protection によって保護されたすべてのコンピューター**」コレクションに展開します。|「[Endpoint Protection 用 Windows ファイアウォール ポリシーを作成および展開する方法](create-windows-firewall-policies.md)」を参照してください。|  
|管理者は Endpoint Protection に関して利用可能な管理タスクを使用して、マルウェア対策および Windows ファイアウォールのポリシーの管理、必要に応じたオンデマンドのコンピューター スキャンの実行、コンピューターでの最新の定義の強制ダウンロード、マルウェアが検出されたときに追加実行する操作の指定を行います。|「[Endpoint Protection のためのマルウェア対策ポリシーとファイアウォール設定の管理方法](endpoint-antimalware-firewall.md)」を参照してください。|  
|管理者は次の方法を使って、Endpoint Protection の状態および Endpoint Protection によって実行されるアクションを監視します。<br /><br /> 1) **[監視]** ワークスペースの **[セキュリティ]** で **[Endpoint Protection のステータス]** ノードを使用する。<br /><br /> 2) **[資産とコンプライアンス]** ワークスペースの **[Endpoint Protection]** ノードを使用する。<br /><br /> 3) Configuration Manager の組み込みレポートを使用する。|「[Endpoint Protection を監視する方法](monitor-endpoint-protection.md)」を参照してください。|  

 管理者は、Endpoint Protection が正常に実装されたことを上司に報告し、Woodgrove Bank のコンピューターが、指示されたビジネス要件に従ってマルウェアから保護されていることを確認します。 

## <a name="next-steps"></a>次のステップ

詳細については、[Endpoint Protection の構成方法](endpoint-protection-configure.md)に関するページを参照してください。