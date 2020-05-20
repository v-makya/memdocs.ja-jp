---
title: Windows 10 更新プログラムの配信の最適化
titleSuffix: Configuration Manager
description: Configuration Manager を使用して、Windows 10 を最新の状態に保つための更新プログラムのコンテンツを管理する方法について説明します。
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 835dcd0c86244c1731cb6c6e040d577160759614
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83267792"
---
# <a name="optimize-windows-10-update-delivery-with-configuration-manager"></a>Configuration Manager による Windows 10 更新プログラムの配信の最適化

*適用対象:Configuration Manager (Current Branch)*

多くのお客様は、Configuration Manager を使用した適切なコンテンツ配布戦略によって Windows 10 の月次更新プログラムを入手し、Windows 10 を最新の状態に保つことができます。 大規模な組織にとって、毎月の品質更新プログラムのサイズは懸念の原因となり得ます。 帯域幅とネットワークの負荷を削減して更新プログラムの配信を最適化するために役立ついくつかのテクノロジが存在します。 この記事では、そのようなテクノロジについて説明および比較し、使用するテクノロジの決定に役立つ推奨事項を提供します。  
 
Windows 10 は複数の種類の更新プログラムを提供します。 詳しくは、「[Windows Update for Business を使った更新プログラムの展開](/windows/deployment/update/waas-manage-updates-wufb#types-of-updates-managed-by-windows-update-for-business)」をご覧ください。 この記事では、Windows 10 *品質*更新プログラムと Configuration Manager を中心に説明しています。 


## <a name="express-update-delivery"></a>高速更新プログラムの配信

Windows 10 品質更新プログラムのダウンロード サイズは非常に大きくなる可能性があります。 一貫性を確保し、更新をシンプルに行えるようにするために、各パッケージには以前にリリースされた修正プログラムがすべて含まれています。 Microsoft では、高速と呼ばれる機能によって、各クライアントがダウンロードする Windows 10 更新プログラムのコンテンツのサイズを削減しました。 高速は、Windows Update サービスから更新プログラムを直接プルする何百万ものデバイスで使用されており、ダウンロード サイズを大幅に削減します。 クライアントが Windows Update サービスから直接ダウンロードしない環境でもこのメリットは有効です。 

Configuration Manager バージョン 1702 では、Windows 10 品質更新プログラムの[高速インストール ファイル](manage-express-installation-files-for-windows-10-updates.md)のサポートが追加されました。 ただし、操作性向上のため、Configuration Manager バージョン 1802 以降を使用することをお勧めします。 ダウンロード速度の最適なパフォーマンスを確保するには、Windows 10 バージョン 1703 以降を使用することもお勧めします。 

> [!NOTE]  
> 高速バージョンのコンテンツは、フルファイル バージョンよりも大幅にサイズが大きくなります。 高速インストール ファイルには、更新対象となる各ファイルのバリエーションがすべて含まれます。 そのため、Configuration Manager で高速サポートを有効にすると、更新パッケージ ソースの更新プログラムおよび配布ポイントで必要なディスク領域が増加します。 配布ポイントにおけるディスク領域の要件が増えたとしても、クライアントがその配布ポイントからダウンロードするコンテンツ サイズは削減されます。 クライアントがダウンロードするコンテンツは少量 (差分) であり、すべての更新プログラムではありません。


## <a name="peer-to-peer-content-distribution"></a>ピアツーピアのコンテンツ配布

クライアントがダウンロードするのが必要とされるコンテンツの一部だけであるとしても、ピアツーピアのコンテンツ配布を利用すれば、環境における Windows の更新を迅速に行うことができます。 品質更新プログラムのダウンロード ソースとしてピアを活用することは、ローカルの配布ポイントがリモート オフィスに存在しない環境で有効です。 これにより、すべてのクライアントが低速な WAN リンク経由でリモートの配布ポイントからコンテンツをダウンロードする必要がなくなります。 ピアの使用は、クライアントが Windows Update サービスにフォールバックする際にも役立ちます。 1 つのピアでクラウドから更新プログラムのコンテンツをダウンロードすれば、それらを他のデバイスで使用できるようになります。

Configuration Manager では、次のような多くのピアツーピア テクノロジがサポートされています。
- Windows 配信の最適化
- Configuration Manager のピア キャッシュ
- Windows BranchCache  

以降のセクションでは、これらのテクノロジについて詳しく説明します。

### <a name="windows-delivery-optimization"></a>Windows 配信の最適化

[配信の最適化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization)は Windows 10 に組み込まれている主要なダウンロード テクノロジであり、ピアツーピアの配布方法です。 Windows 10 クライアントは、同じ更新プログラムをダウンロードするローカル ネットワーク上の他のデバイスからコンテンツを取得できます。 [配信の最適化で使用可能な Windows のオプション](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#delivery-optimization-options)を使用すると、クライアントをグループとして構成できます。 このグループ化によって、ピアツーピア要求を満たすために最適な候補であるデバイスを組織で特定できます。 配信の最適化では、デバイスを最新の状態に保つために使用される帯域幅を大幅に削減して、ダウンロード時間を短縮します。

> [!NOTE]  
> 配信の最適化は、クラウド管理ソリューションです。 ピアツーピア機能を利用するには、配信の最適化クラウド サービスへのインターネット アクセスが必要です。 必要なインターネット エンドポイントの詳細については、[配信の最適化に関してよく寄せられる質問](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)に関するページをご覧ください。 

最良の結果を得るには、配信の最適化の[ダウンロード モード](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#download-mode)を**グループ (2)** に設定して、*グループ ID* を定義する必要があります。 グループ モードでは、同じグループに属するデバイス (リモート オフィスにあるデバイスを含む) 間の内部サブネットをピアリングによって通過できます。 ドメインおよび AD DS サイトに関係なく独自のカスタム グループを作成するには、[グループ ID オプション](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#select-the-source-of-group-ids)を使用します。 配信の最適化による帯域幅の最適化を目標とするほとんどの組織には、グループ ダウンロード モードが推奨されます。

クライアントがさまざまなネットワークをローミングする場合、これらのグループ ID を手動で構成することは困難です。 Configuration Manager バージョン 1802 では、[境界グループと配信の最適化を統合](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)することにより、このプロセスの管理を簡略化する新機能が追加されました。 起動したクライアントは、その管理ポイントと通信してポリシーを取得し、ネットワークと境界グループの情報を提供します。 Configuration Manager は、各境界グループに対して一意の ID を作成します。 サイトでは、クライアントの位置情報を使用して、Configuration Manager の境界 ID に基づくクライアントの配信の最適化グループ ID を自動的に構成します。 別の境界グループにローミングしたクライアントは、その管理ポイントと通信し、新しい境界グループ ID が自動的に再構成されます。 この統合により、配信の最適化では、Configuration Manager の境界グループ情報を利用して更新プログラムのダウンロード元となるピアを検出できます。

### <a name="delivery-optimization-starting-in-version-1910"></a><a name="bkmk_DO-1910"></a> バージョン 1910 以降の配信最適化
<!--4699118-->
Configuration Manager バージョン 1910 以降では、Windows 10 バージョン 1709 以降を稼働しているクライアントに向けたすべての Windows Update コンテンツの配布に対して、高速インストール ファイルだけでなく、配信の最適化を使用できるようになりました。

Windows Update のすべてのインストール ファイルに配信の最適化を使用するには、次の[ソフトウェア更新プログラムのクライアント設定](../../core/clients/deploy/about-client-settings.md#software-updates)を有効にします。

- **[使用可能な場合、クライアントが差分コンテンツをダウンロードできるようにする]** を **[はい]** に設定します。
- **[クライアントが差分コンテンツの要求を受信するために使用するポート]** を 8005 (既定) またはカスタム ポート番号に設定します。

> [!IMPORTANT]
> - 配信の最適化は有効にする必要があり (既定)、バイパスすることはできません。 詳細については、[Windows 配信の最適化のリファレンス](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference)に関する記事をご覧ください。
> - 差分コンテンツに対する[ソフトウェア更新プログラムのクライアント設定](../../core/clients/deploy/about-client-settings.md#software-updates)を変更する場合は、[配信の最適化のクライアント設定](../../core/clients/deploy/about-client-settings.md#delivery-optimization)を確認してください。
> - Office COM を有効にしている場合、Office 365 クライアントの更新プログラムに対して配信の最適化を使用することはできません。 Office COM は、Office 365 クライアントの更新プログラムを管理するために Configuration Manager によって使用されます。 Office COM の登録を解除すれば、Office 365 の更新プログラムに対して配信の最適化を使用できるようになります。 Office COM を無効にすると、Office 365 のソフトウェア更新プログラムは、Office 自動更新 2.0 の既定のスケジュールされたタスクによって管理されます。 これは、Office 365 の更新プログラムのインストール プロセスが Configuration Manager によって指示または監視されないことを意味します。 Configuration Manager では、コンソール内の Office 365 クライアント管理ダッシュボードを設定するために、引き続きハードウェア インベントリから情報が収集されます。 Office COM の登録を解除する方法の詳細については、「[Office 365 クライアントを有効にして、Configuration Manager ではなく Office CDN から更新を受信できるようにする](https://docs.microsoft.com/deployoffice/manage-office-365-proplus-updates-with-configuration-manager#enable-office-365-clients-to-receive-updates-from-the-office-cdn-instead-of-configuration-manager)」を参照してください。
> - コンテンツの保存に CMG を使用する場合、[クライアント設定](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available)の **[Download delta content when available]\(デルタ コンテンツが使用可能な場合はダウンロードする\)** が有効になっていると、サードパーティの更新プログラムのコンテンツはクライアントにダウンロードされません。 <!--6598587-->


### <a name="configuration-manager-peer-cache"></a>Configuration Manager のピア キャッシュ

[ピア キャッシュ](../../core/plan-design/hierarchy/client-peer-cache.md)は Configuration Manager の機能です。これにより、クライアントはローカルの Configuration Manager キャッシュのコンテンツを他のクライアントと直接共有できます。 ピア キャッシュは、Windows BranchCache などの他のピア キャッシュ ソリューションに代わるものではありません。 それらのソリューションと連携し、配布ポイントなどの従来のコンテンツ展開ソリューションを拡張するオプションを提供します。 ピア キャッシュは BranchCache に依存しません。 BranchCache を有効にしていない場合または使用していない場合でも、ピア キャッシュは正常に動作します。

> [!NOTE]  
> クライアントは、現在の境界グループ内にあるピア キャッシュ クライアントのコンテンツのみをダウンロードできます。  


### <a name="windows-branchcache"></a>Windows BranchCache
[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) は Windows における帯域幅最適化テクノロジです。 各クライアントにはキャッシュがあります。また、各クライアントはコンテンツの代替ソースとして機能します。 同じネットワーク上のデバイスがこのコンテンツを要求できます。 常に配布ポイントへのアクセスが必要な方法とは異なり、[Configuration Manager で BranchCache を使用](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache)すると、ピアが互いにコンテンツをソーシングできます。 BranchCache を使用すると、ファイルが個々のクライアントにキャッシュされ、他のクライアントは必要に応じてファイルを取得できます。 この方法では、単一の取得ポイントを使用するのではなく、キャッシュが分散されます。 これにより、帯域幅が大幅に削減され、クライアントが要求したコンテンツを受け取る時間も短縮されます。



## <a name="selecting-the-right-peer-caching-technology"></a>適切なピア キャッシュ テクノロジの選択

高速インストール ファイルに適したピア キャッシュ テクノロジの選択は、環境や要件によって異なります。 Configuration Manager が前述のピアツーピア テクノロジをすべてサポートする場合でも、環境に最も有用なテクノロジを使用する必要があります。 ほとんどのお客様は、配信の最適化のインターネット要件をクライアントが満たしていることを前提としており、Windows 10 に組み込みのピア キャッシュと配信の最適化で十分です。 クライアントがこれらのインターネット要件を満たしていない場合は、Configuration Manager のピア キャッシュ機能の使用を検討してください。 現在 Configuration Manager で BranchCache を使用しておらず、要件がすべて BranchCache で満たされる場合は、高速ファイルと BranchCache の使用が最適なオプションです。 

### <a name="peer-cache-comparison-chart"></a>ピア キャッシュの比較表


| 機能  | 配信の最適化  | ピア キャッシュ  | BranchCache  |
|---------|---------|---------|---------|
| サブネット間でサポート | はい | はい | いいえ |
| 帯域幅調整 | ○ (ネイティブ) | ○ (BITS を使用) | ○ (BITS を使用) |
| 一部のコンテンツをサポート | はい (この列の次の行に記載されている、サポートされているすべてのコンテンツの種類に対して)。 | Office 365 および高速更新の場合のみ | はい (この列の次の行に記載されている、サポートされているすべてのコンテンツの種類に対して)。 |
| サポートされているコンテンツの種類 | **ConfigMgr 経由:** </br> - 高速更新 </br> - すべての Windows 更新プログラム (バージョン 1910 以降)。 これには Office 更新プログラムは含まれません。</br> </br> **Microsoft クラウド経由:**</br> - Windows 更新プログラムとセキュリティ更新プログラム</br> - ドライバー</br> - Windows ストア アプリ</br> - ビジネス向け Windows ストアのアプリ | Configuration Manager のすべてのコンテンツの種類 ([Windows PE](../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) でダウンロードされるイメージを含む) | Configuration Manager のすべてのコンテンツの種類 (イメージを除く) |
| ディスク制御におけるキャッシュ サイズ | はい | はい | はい |
| ピア ソースの検出 | 自動 | 手動 (クライアント エージェント設定) | 自動 |
| ピア検出 | 配信の最適化クラウド サービスを使用 (インターネット アクセスが必要) | 管理ポイントを使用 (クライアントの境界グループに基づく) | マルチキャスト |
| レポート | はい (Desktop Analytics を使用) | Configuration Manager クライアント データ ソース ダッシュボード | Configuration Manager クライアント データ ソース ダッシュボード |
| WAN の使用の制御 | ○ (ネイティブ、グループ ポリシー設定による制御が可能) | 境界グループ | サブネットのサポートのみ |
| Configuration Manager による管理 | 一部 (クライアント エージェント設定) | ○ (クライアント エージェント設定) | ○ (クライアント エージェント設定) |



## <a name="conclusion"></a>結論

Microsoft では、必要に応じて Configuration Manager と高速インストール ファイルおよびピア キャッシュ テクノロジを使用して Windows 10 品質更新プログラムの配信を最適化することをお勧めします。 この方法では、品質更新プログラムをインストールするためにサイズの大きいコンテンツをダウンロードする Windows 10 デバイスに関連する課題が軽減されます。 毎月の品質更新プログラムを展開して Windows 10 デバイスを最新の状態に保つことも推奨されます。 このプラクティスにより、デバイスに必要な毎月の品質更新プログラムのコンテンツの差分が削減されます。 このコンテンツの差分の削減により、配布ポイントまたはピア ソースからダウンロードするコンテンツのサイズが小さくなります。 

高速インストール ファイルの性質上、コンテンツ サイズは従来の自己完結型ファイルよりも大幅に大きくなります。 このサイズが原因で、Windows Update サービスから Configuration Manager サイト サーバーへの更新プログラムのダウンロードに時間がかかります。 サイト サーバーと配布ポイントの両方に必要なディスク領域も増加します。 品質更新プログラムのダウンロードと配布に必要な合計時間も長くなる可能性があります。 ただし、Windows 10 デバイスによる品質更新プログラムのダウンロードとインストール時におけるデバイス側のメリットは顕著です。 詳細については、「[高速インストール ファイルの使用](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc708456(v=ws.10)?#using-express-installation-files)」をご覧ください。

更新プログラムのサイズが大きくなるというサーバー側のトレードオフが高速サポートの採用を妨げる要因であるとしても、デバイス側のメリットの方がお客様のビジネスおよび環境にとって重要である場合、Microsoft では [Windows Update for Business](integrate-windows-update-for-business-windows-10.md) と Configuration Manager の使用をお勧めします。 Windows Update for Business は、高速のメリットをすべて提供します。環境全体で高速インストール ファイルをダウンロード、格納、および配布する必要はありません。 クライアントは Windows Update サービスから直接コンテンツをダウンロードするため、配信の最適化を引き続き利用できます。



## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a> よく寄せられる質問

#### <a name="how-do-windows-express-downloads-work-with-configuration-manager"></a>Windows の高速ダウンロードは Configuration Manager と連携しますか?

Windows Update エージェント (WUA) は最初に高速コンテンツを要求します。 高速更新プログラムをインストールできない場合は、フルファイル更新にフォールバックできます。  

1. Configuration Manager クライアントは、更新プログラムのコンテンツをダウンロードするように WUA に指示します。 WUA は高速ダウンロードを開始すると、高速パッケージの一部であるスタブ (たとえば、`Windows10.0-KB1234567-<platform>-express.cab`) を最初にダウンロードします。  

2. WUA はこのスタブをコンポーネント ベース サービシング (CBS) である Windows Update インストーラーに渡します。 CBS では、スタブを使用してローカル インベントリを処理 (デバイス上のファイルの差分を、提供されている最新バージョンのファイルに到達するために必要な項目と比較) します。  

3. 続いて、CBS は 1 つ以上の高速 .psf ファイルから必要な範囲のファイルをダウンロードするよう WUA に求めます。  

4. 配信の最適化が有効になっていて、必要な範囲のピアが検出された場合、クライアントは、ConfigMgr クライアントとは無関係にピアからダウンロードします。 配信の最適化が無効になっている場合、または必要な範囲のピアがない場合、ConfigMgr クライアントによってこれらの範囲がローカルの配布ポイント (またはピア、または Microsoft Update) からダウンロードされます。 この範囲は Windows Update エージェントに渡されます。これにより、範囲を適用するために CBS で使用できるようになります。


#### <a name="why-are-the-express-files-psf-so-large-when-stored-on-configuration-manager-peer-sources-in-the-ccmcache-folder"></a>Configuration Manager のピア ソースで ccmcache フォルダーに格納される際に高速ファイル (.psf) のサイズが大きくなるのはなぜですか?

高速ファイル (.psf) はスパース ファイルです。 ファイルが使用するディスク上の実際の領域を特定するには、ファイルの **[ディスク上のサイズ]** プロパティを確認します。 [ディスク上のサイズ] プロパティは、[サイズ] の値よりも大幅に小さくなるはずです。  


#### <a name="does-configuration-manager-support-express-installation-files-with-windows-10-feature-updates"></a>Configuration Manager は Windows 10 機能更新プログラムを含む高速インストール ファイルをサポートしますか?

いいえ。現時点で Configuration Manager がサポートするのは、Windows 10 品質更新プログラムを含む高速インストール ファイルのみです。  


#### <a name="how-much-disk-space-is-needed-per-quality-update-on-the-site-server-and-distribution-points"></a>サイト サーバーおよび配布ポイントにおいて、それぞれの品質更新プログラムに必要なディスク領域はどのくらいですか?

状況により異なります。 それぞれの品質更新プログラムでは、フルファイル バージョンと高速バージョンの両方の更新プログラムがサーバーに格納されます。 Windows 10 品質更新プログラムは累積的なものであるため、これらのファイルのサイズは月ごとに増加します。 各言語の更新プログラムにつき、最低でも 5 GB を予定しておいてください。 


#### <a name="do-configuration-manager-clients-still-benefit-from-express-installation-files-when-falling-back-to-the-windows-update-service"></a>Configuration Manager クライアントでも、Windows Update サービスへのフォールバックの際に高速インストール ファイルのメリットがありますか?

はい。 次に示すソフトウェア更新プログラムの展開オプションを使用すれば、クラウド サービスへのフォールバックの際も、クライアントは引き続き高速更新と配信の最適化を使用できます。  

**現在、近隣、またはサイトの境界グループ内の配布ポイントでソフトウェア更新プログラムを利用できない場合は、Microsoft 更新プログラムからコンテンツをダウンロードします**


#### <a name="why-is-express-file-content-not-downloaded-for-existing-updates-after-i-enable-express-file-support"></a>高速ファイルのサポートを有効にした後で、既存の更新プログラムに対する高速ファイルのコンテンツがダウンロードされないのはなぜですか? 

変更が有効になるのは、サポートを有効化した後に同期および展開された新しい更新プログラムに対してのみです。


#### <a name="is-there-any-way-to-see-how-much-content-is-downloaded-from-peers-using-delivery-optimization"></a>配信の最適化を使用してピアからダウンロードしたコンテンツの量を確認する方法はありますか?
Windows 10 バージョン 1703 (およびそれ以降) には、2 つの新しい PowerShell コマンドレット (**Get-DeliveryOptimizationPerfSnap** と **Get-DeliveryOptimizationStatus**) が含まれています。 これらのコマンドレットは、配信の最適化とキャッシュの使用状況に関する分析情報を提供します。 詳しくは、[Windows 10 更新プログラムの配信の最適化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#the-cloud-service-doesnt-see-other-peers-on-the-network)に関するページをご覧ください


#### <a name="how-do-clients-communicate-with-delivery-optimization-over-the-network"></a>クライアントはネットワーク経由で配信の最適化とどのように通信しますか?
ネットワーク ポート、プロキシの要件、およびファイアウォールのホスト名について詳しくは、[配信の最適化についてよく寄せられる質問](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)をご覧ください。

## <a name="log-files"></a>ログ ファイル

差分ダウンロードを監視するには、次のログ ファイルを使用します。

- WUAHandler.log
- DeltaDownload.log

## <a name="next-steps"></a>次のステップ

- [ソフトウェア更新プログラムの展開](deploy-software-updates.md)
- [ソフトウェア更新プログラムの自動展開](automatically-deploy-software-updates.md)
