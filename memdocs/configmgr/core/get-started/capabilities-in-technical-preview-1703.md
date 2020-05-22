---
title: Technical Preview 1703 の機能
titleSuffix: Configuration Manager
description: Configuration Manager の Technical Preview バージョン 1703 で使用できる機能について説明します。
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: fb13844dd05049b9186909884aa0c457a8cfacd9
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428409"
---
# <a name="capabilities-in-technical-preview-1703-for-configuration-manager"></a>Configuration Manager の Technical Preview 1703 の機能

*適用対象:Configuration Manager (Technical Preview Branch)*

この記事では、Configuration Manager の Technical Preview バージョン 1703 で利用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 このバージョンの Technical Preview をインストールする前に、説明のトピック「[Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、Technical Preview の機能に関するフィードバックを提供する方法について理解してください。    


**このバージョンでお試しいただける新機能を次に示します。**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>ボリューム購入 iOS アプリをデバイス コレクションに展開する

ライセンスされたアプリをユーザーだけでなくデバイスにも展開できるようになりました。 デバイス ライセンスをサポートするアプリ機能に応じて、次のように、展開時に適切なライセンスが要求されます。

|||||
|-|-|-|-|
|Configuration Manager バージョン|アプリでのデバイス ライセンスのサポート|展開コレクションの種類|要求されるライセンス|
|1702 より前|はい|ユーザー|ユーザー ライセンス|
|1702 より前|いいえ|ユーザー|ユーザー ライセンス|
|1702 より前|はい|デバイス|ユーザー ライセンス|
|1702 より前|いいえ|デバイス|ユーザー ライセンス|
|1702 以降|はい|ユーザー|ユーザー ライセンス|
|1702 以降|いいえ|ユーザー|ユーザー ライセンス|
|1702 以降|はい|デバイス|デバイス ライセンス|
|1702 以降|いいえ|デバイス|ユーザー ライセンス|


## <a name="direct-links-to-applications-in-software-center"></a>ソフトウェア センターでのアプリケーションへの直接リンク

ソフトウェア センターでアプリケーションへの直接リンクをエンド ユーザーに提供できるようになりました。 つまり、エンド ユーザーは、アプリケーションをインストールするために、ソフトウェア センターを開いてアプリケーションを検索する必要がなくなりました。 この機能は、Configuration Manager アプリケーションについてのみ使用でき、パッケージやプログラム、タスク シーケンスについては使用できません。

### <a name="try-it-out"></a>試してみましょう                 

ソフトウェア センターを開いて特定のアプリケーションに移動するには、次の URL 形式を使用します。

**Softwarecenter:SoftwareId=_アプリケーション識別子_**

### <a name="how-to-get-the-application-identifier-of-an-application"></a>アプリケーションのアプリケーションの識別子を取得する方法

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** をクリックします。
2. [ソフトウェア ライブラリ] ワークスペースで **[アプリケーション管理]** を展開し、 **[アプリケーション]** をクリックします。
3. **[アプリケーション]** ビューで、列ヘッダーのいずれかを右クリックし、一覧から **[CI の固有 ID]** を選択します。 各アプリケーションの一意の ID が一覧に表示されます。
4. リンク先のアプリケーションの **[CI の固有 ID]** (**ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2** など) をメモしておきます。
5. 次に、アプリケーション GUID の後に続くテキスト (この例では **/2**) をすべて削除します。 これにより、アプリケーション識別子が得られます。
6. 最後に、リンクの作成を完了するために、アプリケーション識別子の前に **Softwarecenter:SoftwareID=** を付けます。 上記の例を使用して、次の最終的なリンクが表示されます。**Softwarecenter:SoftwareId= ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**。

このリンクを使用することにより、エンド ユーザーは、ソフトウェア センターで指定したアプリケーションを直接開くことができます。


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>Configuration Manager の Windows クライアント コンピューター用の PFX 証明書

Windows 10 を実行する Configuration Manager クライアント コンピューターにインポートした PFX 証明書プロファイルを展開できるようになりました。

### <a name="try-it-out"></a>試してみましょう

「[PFX 証明書プロファイルを作成する方法](../../mdm/deploy-use/create-pfx-certificate-profiles.md)」の指示に従って PFX プロファイルをインポートし、プロファイルを展開した後、対象のユーザーの証明書がインストールされたかどうかを確認します。



## <a name="configure-azure-services-wizard"></a>Azure サービスの構成ウィザード
Technical Preview 1703 では、**Azure サービスの構成**ウィザードが導入されました。 このウィザードは、Configuration Manager で使用するクラウド サービスを設定するための個々のワークフローに代わる、共通の構成エクスペリエンスを提供します。 このエクスペリエンスは、これまで、新しい Configuration Manager のコンポーネントや Azure のサービスを設定するたびに入力していたサブスクリプションや構成の詳細を提供する **Azure Web アプリ**によって実現されます。

Technical Preview 1703 では、ビジネス向け Windows ストア (WSfB) のみがこのウィザードを使用して構成されます。  他のクラウド サービスは、個別のワークフローを使用して構成されます。

- このプレビュー トピックの情報を使用して、Current Branch のトピック「[Configuration Manager によるビジネス向け Windows ストアからのアプリの管理](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)」の「[ビジネス向け Windows ストアの同期の設定](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_setup)」セクションに記載されている構成手順を置き換えます。

- Web アプリの詳細については、「[Azure App Service での認証および承認](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview)」と「[Web Apps の概要](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)」を参照してください。

### <a name="prerequisites-and-planning"></a>前提条件と計画
Configuration Manager とビジネス向け Windows ストアの間の接続を設定するとき、ストアから同期されたアプリ コンテンツが保存するフォルダーを指定する必要があります。 このフォルダーが安全であり、そのコンテンツをデバイスに展開できるようにするには、次のアクセス許可を配置します。
- サービス接続ポイント サイト システム ロール (階層の最上位サイト) をインストールするコンピューターで、**Computer$** アカウントを利用して指定したフォルダーの読み書き権限を用意する必要があります。  

- アプリの作成者に、指定したフォルダーの読み取り権限を与える必要があります。  

- SMS プロバイダーのインスタンスをホストする各コンピューターの **Computer$** アカウントで、指定したフォルダーを使用できる必要があります。

Azure Active Directory で、Configuration Manager を Web アプリケーションまたは Web API の管理ツールとして登録します。 これにより、後で必要なクライアント ID が作成されます。

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>ウィザードを使用した WSfB クラウド サービスの構成

1. コンソールで、 **[管理]**  >  **[概要]**  >  **[クラウド サービスの管理]**  >  **[Azure]**  >  **[Azure サービス]** に移動し、 **[Azure サービスの構成]** を選択して、**Azure サービス ウィザード**を開始します。

2. **[Azure サービス]** ページで、構成するサービスを選択し、 **[次へ]** をクリックします。 このプレビューでは、WSfB のみを構成できます。

3. **[全般]** ページで、 **[Azure サービス名]** のフレンドリ名とオプションの説明を入力し、 **[次へ]** をクリックします。

4. **[アプリ]** ページで、Azure 環境を指定し、 **[参照]** をクリックして[サーバー アプリ] ウィンドウを開きます。

5. **[サーバー アプリ]** ウィンドウで、使用するサーバー アプリを選択し、 **[OK]** をクリックします。
   サーバー アプリとは、Azure アカウントの構成 (クライアントのテナント ID、クライアント ID、シークレット キーなど) を格納する Azure Web アプリです。 利用可能なサーバー アプリがない場合は、次のいずれかを使用します。
   - **作成**: 新しいサーバー アプリを作成するには、 **[作成]** をクリックします。 アプリとテナントのフレンドリ名を指定します。 次に、Azure にサインインすると、Configuration Manager によって、Azure で Web アプリと、Web アプリで使用するクライアント ID やシークレット キーが作成されます。 その後、Azure Portal からこれらを表示できます。
   - **インポート**: ご利用の Azure サブスクリプションに既に存在する Web アプリを使用するには、 **[インポート]** をクリックします。 アプリとテナントのフレンドリ名を指定し、Configuration Manager で使用する Azure Web アプリのテナント ID、クライアント ID、シークレット キーを指定します。 情報を**確認**した後、 **[OK]** をクリックして続行します。  </br></br>

6. **[情報]** ページを確認し、指示に従って、追加の手順と構成を完了します。 これらの構成は、Configuration Manager でサービスを使用するために必要です。
   たとえば、WSfB を構成するには次を実行します。

   1. Azure で、Configuration Manager を Web アプリケーションまたは Web API 管理ツールとして登録し、クライアント ID を記録します。 また、管理ツール (Configuration Manager) で使用するためのクライアント キーを指定します。

   2.    WSfB コンソールで、ストアの管理ツールとして Configuration Manager を構成し、オフラインのライセンスされたアプリのサポートを有効にするには、少なくとも 1 つのアプリを購入する必要があります。   </br>

   操作を続行する準備ができたら **[次へ]** をクリックします。

7. **[アプリケーションの構成]** ページで、このサービスのアプリケーション カタログと言語の構成を完了し、 **[次へ]** をクリックします。
8. ウィザードが完了したのち、Configuration Manager コンソールに**ビジネス向け Windows ストア**を**クラウド サービスの種類**として構成したことが示されます。

WSfB のアプリの管理に関する [Current Branch のコンテンツ](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)に従って、ビジネス向け Windows ストアのアプリの同期、作成と展開、監視を行うことができるようになりました。

### <a name="modify-a-cloud-service-configuration"></a>クラウド サービスの構成の変更
クラウド サービスのプロパティを表示して編集し、構成を変更できます。

コンソールで、 **[管理]**  >  **[概要]**  >  **[クラウド サービスの管理]**  >  **[Azure]**  >  **[Azure サービス]** に移動し、 **[Azure サービスの構成]** を選択します。次に、クラウド サービスを選択し、 **[プロパティ]** を選択します。

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>インプレース アップグレード時に BIOS から UEFI に変換する
Windows 10 Creators Update では、EFI 対応ハードウェアのハード ディスクのパーティションを再分割するプロセスを自動化する簡単な変換ツールが導入され、変換ツールは Windows 7 から Windows 10 へのインプレース アップグレード プロセスに統合されます。 このツールをオペレーティング システムのアップグレード タスク シーケンスと、ファームウェアを BIOS から UEFI に変換する OEM ツールと組み合わせて使用する場合、Windows 10 Creators Update へのインプレース アップグレード時にコンピューターを BIOS から UEFI に変換することができます。 詳細については、「[Task sequence steps to manage BIOS to UEFI conversion](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu)」(BIOS からUEFI への変換を管理するためのタスク シーケンス手順) を参照してください。

## <a name="collapsible-task-sequence-groups"></a>折りたたみ可能なタスク シーケンス グループ
このバージョンでは、タスク シーケンス グループを展開および折りたたむ機能が導入されています。 個々のグループを展開または折りたたんだり、すべてのグループを一度に展開または折りたたんだりすることができます。


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>Windows Analytics for Upgrade Readiness を構成するためのクライアント設定
このバージョン以降では、デバイス クライアントの設定を使用して、Windows 診断データの構成を簡略化できます。これは、Configuration Manager で Upgrade Readiness のような Windows Analytics ソリューションを使用するために必要です。 Configuration Manager では、Windows Analytics からデータを取得し、クライアント コンピューターから報告される Windows 診断データに基づいて、お使いの環境の現在の状態に関する価値ある分析情報を提供することができます。 Windows 診断データは、クライアント コンピューターによって Windows 診断サービスに報告されます。その後、組織の OMS ワークスペースのいずれかでホストされている Windows Analytics ソリューションに、関連データが転送されます。 Upgrade Readiness は Windows Analytics ソリューションの 1 つで、マネージド デバイスでの Windows アップグレードに関する決定の優先順位を付ける際に役立ちます。

### <a name="prerequisites"></a>[前提条件]
- Upgrade Readiness クラウド サービスを使用するにはサイトを構成しておく必要があります。

### <a name="configure-windows-analytics-client-settings"></a>Windows Analytics クライアント設定の構成
Windows Analytics を構成するには、Configuration Manager コンソールで、 **[管理]**  >  **[クライアント設定]** に移動し、 **[Create Custom Device Client Settings] \(カスタム デバイス クライアント設定の作成)** をダブルクリックして、 **[Windows Analytics]** を選択します。  

次に、 **[Windows Analytics]** 設定タブに移動した後に、以下を構成します。
- **商用 ID**  
商用 ID キーは、管理するデバイスから組織の Windows Analytics データをホストする OMS ワークスペースに情報をマップします。 使用する商用 ID キーを Upgrade Readiness で既に構成している場合は、その ID を使用します。 まだ商用 ID キーがない場合は、商用 ID キーを生成します。

- **Windows 10 デバイスの診断データ レベル**を設定する

- **Windows 7、8、8.1 デバイスでの商用データ収集のオプトイン**を選択する   

- **Internet Explore のデータ収集の構成** Windows 8.1 以前のバージョンが動作しているデバイスでは、Internet Explorer で収集されるデータによって、Upgrade Readiness が Web アプリの非互換性を検出できるため、Windows 10 へのスムーズなアップグレードが妨げられる可能性が排除されます。 Internet Explorer のデータ収集は、インターネット ゾーンごとに有効にできます。
