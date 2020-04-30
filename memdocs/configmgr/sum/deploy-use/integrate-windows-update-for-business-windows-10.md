---
title: Windows Update for Business の統合
titleSuffix: Configuration Manager
description: Windows Update for Business (WUfB) を使用すると、Windows Update サービスに接続されているデバイスの Windows 10 を最新の状態に保つことができます。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/07/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: 8bfd535c93cb9f1dcfc42705f3cce61874dfe226
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709320"
---
# <a name="integrate-with-windows-update-for-business"></a>Windows Update for Business との統合

*適用対象:Configuration Manager (Current Branch)*

Windows Update for Business (WUfB) を使用すると、組織内の Windows 10 ベースのデバイスが Windows Update (WU) サービスに直接接続しているときに、最新のセキュリティ防御と Windows の機能によってこれらのデバイスが常に最新に保たれるようにすることができます。 Configuration Manager では、WUfB を使用してソフトウェア更新プログラムを取得する Windows 10 コンピューターと、WSUS を使用して取得する Windows 10 コンピューターを区別することができます。  

> [!WARNING]
> ご利用のデバイスに共同管理を使用していて、[Windows Update ポリシー](../../comanage/workloads.md#windows-update-policies)を Intune に移行している場合は、デバイスの [Windows Update for Business ポリシーは Intune から](https://docs.microsoft.com/intune/windows-update-for-business-configure)提供されます。
> - Configuration Manager クライアントが共同管理されたデバイスにまだインストールされている場合は、累積的更新プログラムと機能更新プログラムの設定は Intune によって管理されます。 ただし、サード パーティ製の修正プログラムは、Configuration Manager で引き続き管理されます ([**クライアント設定**](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates)で有効にした場合)。  

 WUfB または Windows Insider などの WU から更新プログラムを受信するように Configuration Manager クライアントが設定されている場合に、以下に示す Configuration Manager の一部の機能が使用できなくなりました。  

- Windows Update の適用状況レポート:  
  - Configuration Manager では WU に発行された更新プログラムは認識されません。 WU から更新プログラムを受信するように構成された Configuration Manager クライアントでは、これらの更新プログラムは Configuration Manager コンソールで **[不明]** と表示されます。  

  - 全体のコンプライアンス対応状態のトラブルシューティングが困難になっています。これは、以前は **[不明]** ステータスが WSUS からのスキャン状態を報告していないクライアントに対してのみ使用されていたためです。 今後はこれに、WU から更新プログラムを受信する Configuration Manager クライアントも含まれることになります。  

  - 定義の更新のコンプライアンスは全体的な更新プログラムのコンプライアンス レポートの一部であるため、これも期待どおりに機能しません。

- 更新プログラムのコンプライアンス状態に基づく Defender の全体的な Endpoint Protection のレポートでは、スキャン データの不足により正確な結果が返されません。  

- Configuration Manager では、Office、IE、および Visual Studio などの Microsoft 更新プログラムを、WUfB に接続して更新プログラムを受信するクライアントに展開できません。  

- Configuration Manager では、WSUS に発行され、かつ Configuration Manager を介して管理されるサード パーティの更新プログラムを、WUfB に接続して更新プログラムを受信するクライアントに引き続き展開できます。 WUfB に接続しているクライアントにサード パーティ製の更新プログラムをインストールしない場合は、[[クライアントのソフトウェア更新プログラムを有効にする]](../../core/clients/deploy/about-client-settings.md#software-updates) というクライアント設定を無効にします。

- ソフトウェア更新プログラムのインフラストラクチャを使用する Configuration Manager の完全なクライアント展開は、WUfB に接続して更新プログラムを受信するクライアントに対しては機能しません。  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>WUfB を使用して Windows 10 の更新プログラムを取得するクライアントを識別する

次の手順を使用して、Windows 10 の更新プログラムとアップグレードの取得に WUfB を使用するクライアントを特定します。 次に、WSUS を使用して更新プログラムを取得することをやめるようこれらのクライアントを構成し、これらのクライアントのソフトウェア更新ワークフローを無効にするクライアント エージェント設定を展開します。  

### <a name="prerequisites-for-wufb"></a>WUfB の前提条件

- Windows 10 Desktop Pro または Windows 10 Enterprise Edition バージョン 1511 以降を実行するクライアント

- [Windows Update for Business](https://docs.microsoft.com/windows/deployment/update/waas-manage-updates-wufb) が展開され、クライアントが WUfB を使用して Windows 10 の更新プログラムとアップグレードを取得している。  

### <a name="to-identify-clients-that-use-wufb"></a>WUfB を使用するクライアントを識別するには  

1. Windows Update エージェントが既に有効になっている場合は、WSUS に対してスキャンを実行していないことを確認します。 コンピューターが WSUS または Windows Update に対してスキャンを実行しているかどうかを示すために、次のレジストリ キーを使用できます。 レジストリ キーが存在しない場合は、WSUS に対してスキャンされません。
    - **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**
1. Configuration Manager リソース エクスプローラーの **Windows Update** ノードの下に、新しい属性 **UseWUServer** があります。
1. 更新プログラムとアップグレードのために WUfB を介して接続されているすべてのコンピューターを対象とした **UseWUServer** 属性に基づいて、コレクションを作成します。 次のようなクエリに基づいて、コレクションを作成できます。  

    ```wql
    Select sr.* from SMS_R_System as sr join SMS_G_System_WINDOWSUPDATE as su on sr.ResourceID=su.ResourceID where su.UseWUServer is null
    ```

1. ソフトウェア更新ワークフローを無効にするクライアント エージェント設定を作成します。 WUfB に直接接続されているコンピューターのコレクションに設定を展開します。
1. WUfB を介して管理されているコンピューターの対応ステータスには **[不明]** と表示され、全体のコンプライアンス対応率をカウントする際に、これらのコンピューターは除外されます。  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Windows Update for Business 遅延ポリシーの構成
<!-- 1290890 -->
Configuration Manager バージョン 1706 以降、Windows Update for Business によって直接管理されている Windows 10 デバイスの Windows 10 機能更新プログラムまたは品質更新プログラムに対し、遅延ポリシーを構成できるようになりました。 遅延ポリシーの管理は、 **[ソフトウェア ライブラリ]**  >  **[Windows 10 のサービス]** の下の新しい **[Windows Update for Business ポリシー]** ノードでできます。

> [!NOTE]
> Configuration Manager バージョン 1802 以降では、Windows Insider の遅延ポリシーを設定できます。 <!--507201-->  
Windows Insider プログラムの詳細については、[Windows Insider Program for Business の概要](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business)に関するページを参照してください。

### <a name="prerequisites-for-deferral-policies"></a>遅延ポリシーの前提条件

- Windows 10 バージョン 1703 以降
- Windows Update for Business で管理されている Windows 10 デバイスには、インターネット接続が必要です

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Windows Update for Business 遅延ポリシーを作成するには

1. **[ソフトウェア ライブラリ]**  >  **[Windows 10 のサービス]**  >  **[Windows Update for Business ポリシー]** に移動します。
1. **[ホーム]** タブの **[作成]** グループで、 **[Windows Update for Business ポリシーを作成する]** を選択し、Windows Update for Business ポリシーの作成ウィザードを開きます。
1. **[全般]** ページで、ポリシーの名前と説明を入力します。
1. **[遅延ポリシー]** ページで、機能更新プログラムを遅延または一時停止するかどうかを設定します。 機能更新プログラムは通常、Windows の新機能です。 **[ブランチ準備レベル]** を設定すると、機能更新プログラムが Microsoft からリリースされた場合に、受け取りを遅延させるかどうか、およびその期間を定義できます。
    - **ブランチ準備レベル**:デバイスが Windows 更新プログラムを受信するブランチを設定します。 半期チャネル (対象指定)、半期チャネル、または Windows Insider ビルドを選択します。

        > [!NOTE]
        > **[半期チャネル (対象指定)]** のポリシーを Windows 10、*バージョン 1903 以降* に展開します。 **[半期チャネル]** のポリシーを Windows 10、*バージョン 1809 以前*に展開します。
        >
        > **[半期チャネル]** のポリシーを Windows 10 バージョン 1903 以降に展開した場合、展開はエラー **0x8004100c** で失敗します。<!-- 5593139 -->

    - **遅延期間 (日数)** :機能更新プログラムを遅延させる日数を指定します。 これらの機能更新プログラムの受け取りは、そのリリースから最大 365 日間遅延させることができます。
    - **機能更新プログラムの一時停止の開始**:更新プログラムを一時停止した時点から最大 35 日間、デバイスでの機能更新プログラムの受け取りを一時停止するかどうかを選択します。 最大日数が経過すると、一時停止機能は自動的に期限切れとなり、デバイスは適用可能な更新を確認するために Windows Update をスキャンします。 このスキャンが終ったら、もう一度更新を一時停止することができます。 機能更新プログラムの一時停止を解除するには、チェック ボックスをオフにします。
1. 品質更新プログラムを遅延または一時停止するかどうかを選択します。 品質更新プログラムは通常、既存の Windows 機能の修正と機能強化で、通常は毎月第 1 火曜日に公開されますが、Microsoft が任意のタイミングでリリースすることもあります。 品質更新プログラムが利用可能になった場合に受け取りを遅延させるかどうか、およびその期間を定義できます。
    - **遅延期間 (日数)** :品質更新プログラムを遅延させる日数を指定します。 これらの品質更新プログラムの受け取りは、そのリリースから最大 30 日間遅延させることができます。
    - **品質更新プログラムの一時停止の開始**:更新プログラムを一時停止した時点から最大 35 日間、デバイスでの品質更新プログラムの受け取りを一時停止するかどうかを選択します。 最大日数が経過すると、一時停止機能は自動的に期限切れとなり、デバイスは適用可能な更新を確認するために Windows Update をスキャンします。 このスキャンが終ったら、もう一度更新を一時停止することができます。 品質更新プログラムの一時停止を解除するには、チェック ボックスをオフにします。
1. **[他の Microsoft 製品の更新プログラムのインストール]** を選択して、遅延の設定を Microsoft Update と Windows Update に適用可能にするグループ ポリシー設定を有効にします。
1. **[Include drivers with Windows Update]\(ドライバーと Windows Update を含める\)** を選択して、Windows Update から自動的にドライバーを更新します。 この設定をオフにすると、Windows Update からドライバーの更新プログラムがダウンロードされません。
1. ウィザードを完了して新しいコレクションを作成します。

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Windows Update for Business 遅延ポリシーを展開するには

1. **[ソフトウェア ライブラリ]**  >  **[Windows 10 のサービス]**  >  **[Windows Update for Business ポリシー]** に移動します。
1. **[ホーム]** タブの **[展開]** グループで、 **[Windows Update for Business ポリシーを展開する]** を選択します。
1. 次の設定を構成します。
    - **展開する構成ポリシー**:展開する Windows Update for Business ポリシーを選択します。
    - **コレクション**: **[参照]** をクリックして、ポリシーを展開するコレクションを選択します。
    - **メンテナンス期間以外の修復を許可する**:ポリシーの展開先のコレクションにメンテナンス期間が設定されている場合、このオプションを有効にすると、ポリシー設定によって、メンテナンス期間外に値を修復できます。 メンテナンス期間について詳しくは、「[メンテナンス期間を使用する方法](../../core/clients/manage/collections/use-maintenance-windows.md)」を参照してください。
    - **スケジュール**:展開されたポリシーをクライアント コンピューター上で評価するコンプライアンス評価スケジュールを指定します。 単純なスケジュールとカスタム スケジュールの 2種類あります。
1. ウィザードを完了してポリシーを展開します。
