---
title: Technical Preview 1701 の機能
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1701 で使用できる機能について説明します。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: f100d28b3fd4ce0d310ddb2f0b4e777c72f72881
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076205"
---
# <a name="capabilities-in-technical-preview-1701-for-configuration-manager"></a>Configuration Manager の Technical Preview 1701 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*



この記事では、Configuration Manager の Technical Preview バージョン 1701 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 このバージョンの Technical Preview をインストールする前に、説明のトピック「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。    


**このバージョンでお試しいただける新機能を次に示します。**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>ソフトウェア更新ポイントの境界グループの改善
このプレビュー以降、境界グループを使用して、クライアントをソフトウェアの更新ポイントに関連付けられるようになりました。 これは、追加のサイト システムの役割を管理するために境界グループの変更を展開する継続的な作業の一部です。  境界グループの変更は、Technical Preview 1609 および Current Branch (バージョン 1610) で初めて導入されました。  

このプレビューでは、新しい境界グループの動作を使用して、クライアントが使用できるソフトウェアの更新ポイントを管理することができます。これは、クライアントが使用できる配布ポイントの管理方法と似ています。  

- ソフトウェアの更新ポイントをホストする 1 つ以上のサーバーを関連付けるように境界グループを構成します。
- 新しいソフトウェアの更新ポイントをシークしているクライアントは、現在の境界グループに関連付けられているものの使用を試みます。
- クライアントが、現在のソフトウェアの更新ポイントに到達できず、現在の境界グループからの更新ポイントも見つけられない場合、フォールバック動作を使用して、使用可能なソフトウェアの更新ポイントのプールを拡張します。    

境界グループの詳細については、Current Branch のコンテンツの[境界グループ](../servers/deploy/configure/boundary-groups.md)に関する記述を参照してください。

ただし、このプレビューでは、ソフトウェアの更新ポイントの境界グループの一部のみが実装されています。 ソフトウェアの更新ポイントを追加して、ソフトウェアの更新ポイントを含む近隣の境界グループを構成することはできますが、ソフトウェアの更新ポイントのフォールバック時間がまだサポートされていないため、クライアントはフォールバックが開始されるまで 2 時間待機することになります。

以下に、このテクニカル プレビューでのソフトウェアの更新ポイントの動作について説明します。  

- **新しいクライアントでは境界グループを使用して、ソフトウェアの更新ポイントを選択します。** バージョン 1701 をインストールした後にインストールしたクライアントは、ソフトウェアの更新ポイントを、クライアントの境界グループに関連付けられているものの中から選択します。

  これは、クライアントが、クライアント フォレストを共有するソフトウェアの更新ポイントのリストからランダムに選択する以前の動作に置き換わるものです。   

- **以前にインストールされたクライアントは、フォールバックして新しいソフトウェアの更新ポイントを見つけるまで、引き続き、現在のものを使用します。**
  以前にインストールされ、既にソフトウェアの更新ポイントがあるクライアントは、フォールバックするまで引き続き、そのソフトウェアの更新ポイントを使用します。 これには、クライアントの現在の境界グループに関連付けられていないソフトウェアの更新ポイントが含まれます。 その場合、現在の境界グループからソフトウェアの更新ポイントをすぐに見つけて使用を試みることはありません。

  ソフトウェアの更新ポイントが既にあるクライアントがこの新しい境界グループの動作の使用を開始するのは、現在のソフトウェアの更新ポイントに到達できず、フォールバックを開始した場合のみです。
  この遅延は、新しい動作への切り替えの際に生じるもので意図的なものです。 これは、ソフトウェアの更新ポイントが変更されると、クライアントがデータと新しいソフトウェアの更新ポイントを同期する場合に、ネットワーク帯域幅が多く使用される可能性があるためです。 遷移の遅延は、すべてのクライアントが新しいソフトウェアの更新ポイントに同時に切り替える場合に、ネットワークの飽和を回避するのに役立ちます。

- **フォールバック時間の構成:** このテクニカル プレビューでは、新しいソフトウェアの更新ポイントを検索するためにクライアントがフォールバックを開始する時間の構成はサポートされていません。 これには、さまざまな境界グループの関係に対して構成する場合がある、 **[フォールバック時間 (分)]** と **[フォールバックしない]** の構成が含まれます。

  したがって、クライアントは、使用可能な新しいソフトウェアの更新ポイントを検索するために、フォールバックを開始するまで 2 時間、現在のソフトウェアの更新ポイントへの接続を試みる現在の動作を保持します。

  クライアントは、フォールバックを使用する場合、使用可能なソフトウェアの更新ポイントのプールを作成するためにフォールバックの境界グループ構成を使用します。 このプールには、クライアントの*現在の境界グループ*、*近隣の境界グループ*、およびクライアント *サイトの既定の境界グループ*からのソフトウェアの更新ポイントがすべて含まれます。

- **既定のサイトの境界グループを構成する:**  
  ソフトウェアの更新ポイントを *Default-Site-Boundary-Group&lt;sitecode>* に追加することを検討します。 これにより、別の境界グループのメンバーではないクライアントは確実に、フォールバックしてソフトウェアの更新ポイントを見つけられるようになります。


境界グループのソフトウェアの更新ポイントを管理する場合、[Current Branch ドキュメントの手順](../servers/deploy/configure/boundary-group-procedures.md)を使用できますが、構成する可能性のあるフォールバック時間はソフトウェアの更新ポイントではまだ使用されていないことを忘れないでください。


## <a name="hardware-inventory-collects-uefi-information"></a>ハードウェア インベントリでの UEFI 情報の収集
新しいハードウェア インベントリ クラス (**SMS_Firmware**) とプロパティ (**UEFI**) は、コンピューターが UEFI モードで起動しているかどうかを判別するのに役立ちます。 コンピューターが UEFI モードで起動している場合、**UEFI** プロパティは **TRUE** に設定されています。 これはハードウェア インベントリでは既定で有効になっています。 ハードウェア インベントリの詳細については、「[ハードウェア インベントリを構成する方法](../clients/manage/inventory/configure-hardware-inventory.md)」を参照してください。

## <a name="improvements-to-operating-system-deployment"></a>オペレーティング システムの展開に関する機能拡張
オペレーティング システムの展開について、次のように機能が拡張されました。その多くは、皆さまからのフィードバックに基づくものです。
- [**アプリケーションのインストール タスク シーケンス ステップでより多くのアプリケーションをサポート**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t):**アプリケーションのインストール** タスク シーケンス ステップでインストールできるアプリケーションの最大数が 99 に増えました。 以前のアプリケーションの最大数は 9 でした。
- [**アプリケーションのインストール タスク シーケンス ステップで複数のアプリを選択**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step):タスク シーケンス エディターでアプリケーションのインストール タスク シーケンス ステップにアプリケーションを追加する際に、 **[インストールするアプリケーションの選択]** ウィンドウから複数のアプリケーションを選択できるようになりました。
- [**スタンドアロン メディアの有効期限の設定**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media):スタンドアロン メディアを作成する場合に、メディアに対して、必要に応じて開始日と有効期限を設定するための新しいオプションが追加されました。 これらの設定は既定では無効になっています。 スタンドアロン メディアが実行される前に、この日付はコンピューター上のシステム時刻と比較されます。 システム時刻が開始時刻より前か、有効期限より後の場合、スタンドアロン メディアは開始されません。 これらのオプションは、New-CMStandaloneMedia PowerShell コマンドレットを使用して利用することもできます。
- [**スタンドアロン メディアでの追加コンテンツのサポート**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic):スタンドアロン メディアで追加のコンテンツがサポートされるようになりました。 追加のパッケージ、ドライバー パッケージ、およびアプリケーションを選択し、タスク シーケンスで参照される他のコンテンツと共にメディアにステージングすることができます。 以前は、タスク シーケンスで参照されるコンテンツのみがスタンドアロン メディアにステージングされていました。
- [ **[ドライバーの自動適用] タスク シーケンス ステップの構成可能なタイムアウト**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout):HTTP カタログの要求時に [ドライバーの自動適用] タスク シーケンス ステップでタイムアウト値を構成する場合に、新しいタスク シーケンス変数を使用できるようになりました。 次の変数と既定値 (秒) を使用できます。
   - SMSTSDriverRequestResolveTimeOut - 既定値:60
   - SMSTSDriverRequestConnectTimeOut - 既定値:60
   - SMSTSDriverRequestSendTimeOut - 既定値:60
   - SMSTSDriverRequestReceiveTimeOut - 既定値:480
- [**タスク シーケンス ステップでパッケージ ID が表示されるようになりました**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste):パッケージ、ドライバー パッケージ、オペレーティング システム イメージ、ブート イメージ、またはオペレーティング システム アップグレード パッケージを参照するすべてのタスク シーケンス ステップで、参照されるオブジェクトのパッケージ ID が表示されるようになりました。 タスク シーケンス ステップでは、アプリケーションの参照時にオブジェクト ID が表示されます。
- **ビルド バージョンによる Windows 10 ADK の追跡**:ビルド バージョンで Windows 10 ADK を追跡できるようになりました。これで、Windows 10 ブート イメージのカスタマイズ時により多くの操作がサポートされるようになります。 たとえば、サイトで Windows ADK for Windows 10 バージョン 1607 を使用する場合、コンソールでカスタマイズできるのはバージョン 10.0.14393 のブート イメージのみになります。 WinPE バージョンのカスタマイズの詳細については、「[ブート イメージのカスタマイズ](../../osd/get-started/customize-boot-images.md)」を参照してください。
- **既定のブート イメージのソース パスを変更できなくなりました**:既定のブート イメージは Configuration Manager で管理され、既定のブート イメージのソース パスは Configuration Manager コンソールや Configuration Manager SDK を使用して変更できなくなりました。 カスタム ブート イメージのカスタム ソース パスは引き続き構成可能です。

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>クラウドベースの配布ポイントでソフトウェアの更新をホストする
このプレビュー バージョン以降、クラウドベースの配布ポイントを使用して、ソフトウェアの更新パッケージをホストできるようになります。 ただし、Microsoft Update から直接ソフトウェアの更新をダウンロードするようにクライアントを構成できるため、ソフトウェアの更新パッケージをクラウドベースの配布ポイントに展開する際に発生する可能性のある追加コストを考慮してください。

クラウドベースの配布ポイントの使用については、Configuration Manager の Current Branch のコンテンツにある[クラウドベースの配布ポイントの使用](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)に関する記述を参照してください。

## <a name="validate-device-health-attestation-data-via-management-points"></a>管理ポイント経由でデバイス正常性構成証明データを検証する

このプレビュー バージョン以降、クラウドまたはオンプレミスの正常性構成証明サービスの正常性構成証明レポート データを検証するように管理ポイントを構成できるようになります。 **[管理ポイント コンポーネントのプロパティ]** ダイアログ ボックスの **[詳細オプション]** タブで、**オンプレミスのデバイス正常性構成証明サービスの URL** を**追加**、**編集**、または**削除**することができます。 クライアント エージェントの **[カスタム デバイス設定]** を **[オンプレミスの正常性構成証明サービスを使用]** に指定することもできます。  この設定値を **[はい]** にすると、クラウドベース サービスではなく、オンプレミス管理ポイントへのレポートが有効になります。

### <a name="try-it-out"></a>試してみましょう

- **管理ポイントでオンプレミスデバイス正常性構成証明を有効にする**<br>  Configuration Manager コンソールで、管理ポイントに移動し、 **[管理ポイント コンポーネントのプロパティ]** を開き、 **[詳細オプション]** タブをクリックします。 **[追加]** をクリックし、**オンプレミス デバイス正常性構成証明サービスの URL** として、オンプレミス URL (https://10.10.10.10) など) を指定します。
- **クライアント エージェントのオンプレミス管理ポイント正常性構成証明レポートを有効にする**<br>Configuration Manager コンソールで、 **[管理]**  >  **[クライアント設定]** の順に選択してダブルクリックするか、新しい**カスタム デバイス設定**を作成します。 **[コンピューター エージェント]** を選択し、 **[オンプレミスの正常性構成証明サービスを使用する]** を **[はい]** に設定します。 **[Enable communication with Device Health Attestation Service]** (デバイス正常性構成証明サービスとの通信を有効にする) が **[はい]** に設定されており、 **[Use on-premises Health Attestation]** (オンプレミスの正常性構成証明を使用する) が **[いいえ]** に設定されている場合、管理ポイントではクラウドベースのデバイス正常性構成証明サービスが使用されます。

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>Microsoft Azure Government クラウドで OMS コネクタを使用する
このテクニカル プレビューでは、Microsoft Operations Management Suite (OMS) コネクタを使用して、Microsoft Azure Government クラウド上にある OMS ワークスペースに接続できるようになりました。  

これを行うには、Government クラウドをポイントするように構成ファイルを変更し、OMS コネクタをインストールします。

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>Microsoft Azure Government クラウドに OMS コネクタをセットアップする
1. Configuration Manager コンソールがインストールされている任意のコンピューターで、Government クラウドをポイントするように、***&lt;CM install path>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config*** 構成ファイルを編集します。

   **編集内容:**

   設定名 *FairFaxArmResourceID* の値が、"<https://management.usgovcloudapi.net/"> と同一になるように変更します。

   - **元の値:** &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
     &lt;value>&lt;/value>   
     &lt;/setting>

   - **編集後の値:**      
     &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value><https://management.usgovcloudapi.net/&lt;/value>>  
     &lt;/setting>

   設定名 *FairFaxAuthorityResource* の値が、"<https://login.microsoftonline.com/>" と同一になるように変更します。

   - **元の値:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
     &lt;value>&lt;/value>

   - **編集後の値:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
     &lt;value><https://login.microsoftonline.com/&lt;/value>>

2. 2 つの変更を含むファイルを保存したら、同じコンピューター上で Configuration Manager コンソールを再起動し、そのコンソールを使用して OMS コネクタをインストールします。 コネクタをインストールするには、「[Microsoft Operations Management Suite に Configuration Manager からのデータを同期](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)」の情報を使用し、Microsoft Azure Government クラウド上にある **Operations Management Suite のワークスペース**を選択します。

3. OMS コネクタをインストールしたら、サイトに接続されているコンソールを使用する際に Government クラウドへの接続を使用できます。

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>ハイブリッド MDM の作成ウィザードで Android と iOS のバージョン指定が不要に

ハイブリッド モバイル デバイス管理 (MDM) のこのテクニカル プレビューから、Intune で管理されるデバイスの新しいポリシーとプロファイルを作成する場合に Android および iOS の特定のバージョンを指定する必要がなくなりました。 代わりに、次のデバイス タイプのいずれかを選択します。

- Android
- Samsung KNOX Standard 4.0 以降
- iPhone
- iPad

この変更は、次の項目を作成するウィザードに影響します。

- 構成項目
- コンプライアンス ポリシー
- 証明書プロファイル
- 電子メール プロファイル
- VPN プロファイル
- Wi-Fi プロファイル

この変更により、新しい Configuration Manager のリリースまたは拡張機能を必要とせずに、ハイブリッド展開で新しい Android および iOS のバージョンによりすばやくサポートを提供できます。 Intune スタンドアロンで新しいバージョンがサポートされると、ユーザーはモバイル デバイスをそのバージョンにアップグレードできるようになります。

以前のバージョンの Configuration Manager からアップグレードする場合の問題を防ぐため、モバイルのオペレーティング システムのバージョンが各項目の [プロパティ] ページに表示されています。 特定のバージョンを対象にする必要がある場合は、新しい項目を作成し、新しく作成された項目の [プロパティ] ページで、対象のバージョンを指定します。
