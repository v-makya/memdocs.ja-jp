---
title: コンテンツ管理のセキュリティとプライバシー
titleSuffix: Configuration Manager
description: Configuration Manager でのコンテンツ管理のセキュリティとプライバシーを最適化します。
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 067922149ef268aeb6cd562816aaa4971e184fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704480"
---
# <a name="security-and-privacy-for-content-management-in-configuration-manager"></a>Configuration Manager でのコンテンツ管理のセキュリティとプライバシー

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager でのコンテンツ管理のセキュリティとプライバシーについて説明します。 



##  <a name="security-best-practices-for-content-management"></a><a name="BKMK_Security_ContentManagement"></a> コンテンツ管理に関するセキュリティのベスト プラクティス  


#### <a name="advantages-and-disadvantages-of-https-or-http-for-intranet-distribution-points"></a>イントラネット配布ポイントに対する HTTPS または HTTP の長所と短所
イントラネット上の配布ポイントの場合は、HTTPS および HTTP を使用することの長所と短所を検討します。 ほとんどのシナリオでは、HTTP とパッケージ アクセス アカウントを承認に使用するほうが、暗号化はするが承認はしない HTTP を使用するよりもセキュリティが高くなります。 ただし、転送中に暗号化する機密データがコンテンツにあれば、HTTPS を使用します。  

-   **HTTPS を配布ポイントに使用すると**、Configuration Manager はコンテンツへのアクセスを承認するためにパッケージ アクセス アカウントを使用しませんが、コンテンツがネットワーク上を転送されるときに暗号化されます。  

-   **HTTP を配布ポイントに使用すると**、パッケージ アクセス アカウントを使用して承認できますが、コンテンツがネットワーク上を転送されるときに暗号化はされません。  

バージョン 1806 以降では、サイトで**拡張 HTTP** を有効にすることを検討してください。 この機能により、クライアントは Azure Active Directory 認証を使用して、HTTP の配布ポイントと安全に通信できます。 詳細については、「[Enhanced HTTP](enhanced-http.md)」(拡張 HTTP) をご覧ください。

#### <a name="protect-the-client-authentication-certificate-file"></a>クライアント認証証明書ファイルを保護する
配送ポイントに、自己署名入り証明書ではなく PKI クライアント認証証明書を使用する場合は、強力なパスワードで証明書ファイル (.pfx) を保護する。 ファイルをネットワーク上に保存する場合は、そのファイルを Configuration Manager にインポートするときにネットワーク チャネルをセキュリティで保護します。

管理ポイントとの通信のために配布ポイントで使用されるクライアント認証証明書をインポートするためにパスワードが必要な場合、この構成は攻撃者から証明書を保護するのに役立ちます。 ネットワークの場所とサイト サーバーの間でサーバー メッセージ ブロック (SMB) 署名または IPsec を使用して、攻撃者が証明書ファイルを改ざんするのを防ぎます。  

#### <a name="remove-the-distribution-point-role-from-the-site-server"></a>サイト サーバーから配布ポイントの役割を削除する
既定では、Configuration Manager のセットアップはサイト サーバーに配布ポイントをインストールします。 クライアントは、サイト サーバーと直接通信する必要はありません。 攻撃を回避するには、配布ポイントの役割を他のサイト システムに割り当てて、サイト サーバーから削除します。  

#### <a name="secure-content-at-the-package-access-level"></a>パッケージ アクセス レベルでコンテンツを保護する
配布ポイントを共有すると、すべてのユーザーに読み取りアクセス権が許可されます。 ユーザーがアクセス可能なコンテンツを制限するために、配布ポイントが HTTP に構成される場合はパッケージ アクセス アカウントを使用します。 この構成は、パッケージ アクセス アカウントがサポートされないクラウド配布ポイントには適用されません。 詳細については、「[パッケージ アクセス アカウント](accounts.md#package-access-account)」をご覧ください。

#### <a name="configure-iis-on-the-distribution-point-role"></a>配布ポイントの役割に IIS を構成する
配布ポイント サイト システムの役割を追加するときに Configuration Manager によって IIS がインストールされる場合は、配布ポイントのインストールが完了したら、HTTP リダイレクトまたは IIS 管理スクリプトとツールを削除します。 配布ポイントには、HTTP リダイレクトまたは IIS 管理スクリプトとツールは必要ありません。 攻撃を回避するには、Web サーバーの役割に対するこれらの役割サービスを削除します。  配布ポイントの Web サーバーの役割に対する役割サービスの詳細については、「[サイトとサイト システムの前提条件](../configs/site-and-site-system-prerequisites.md)」をご覧ください。  

#### <a name="set-package-access-permissions-when-you-create-the-package"></a>パッケージを作成するときにパッケージ アクセス許可を設定します。
パッケージ ファイルのアクセス アカウントの変更は、パッケージを再配布したときのみ有効になるため、最初にパッケージを作成するときに、パッケージ アクセス許可を設定します。 パッケージが大きい場合、パッケージが多数の配布ポイントに配布される場合、コンテンツを配布するためのネットワーク帯域幅容量が限られている場合は、この構成が重要です。  

#### <a name="implement-access-controls-to-protect-media-that-contains-prestaged-content"></a>事前設定されたコンテンツを含むメディアを保護するためにアクセス制御を実装する
事前設定されたコンテンツは圧縮されていますが暗号化されていません。 攻撃者がファイルを読み取って変更し、デバイスにダウンロードする可能性があります。 Configuration Manager クライアントが改ざんされているコンテンツを拒否しても、それでもダウンロードされます。  

#### <a name="import-prestaged-content-with-extractcontent"></a>ExtractContent で事前設定されたコンテンツをインポートする
ExtractContent.exe コマンド ライン ツールを使用して、事前設定されたコンテンツのみをインポートします。 改ざんと権限の昇格を避けるには、Configuration Manager に付属する承認済みのコマンド ライン ツールのみを使用します。  

#### <a name="secure-the-communication-channel-between-the-site-server-and-the-package-source-location"></a>サイト サーバーとパッケージ ソースの場所との間の通信チャネルをセキュリティで保護する
アプリケーションおよびパッケージを作成するときは、サイト サーバーとパッケージ ソースの場所との間で IPsec または SMB 署名を使用します。 この構成は、攻撃者がソース ファイルを改ざんするのを防ぐのに役立ちます。  

#### <a name="remove-default-virtual-directories-for-custom-website-with-the-distribution-point-role"></a>配布ポイントの役割が割り当てられるカスタム Web サイトに対する既定の仮想ディレクトリを削除する
配布ポイントの役割のインストール後に、既定の Web サイトではなくカスタム Web サイトを使うようにサイトの構成オプションを変更する場合は、既定の仮想ディレクトリを削除します。 既定の Web サイトからカスタム Web サイトに切り替えるとき、Configuration Manager によって古い仮想ディレクトリが削除されることはありません。 もともと Configuration Manager によって既定の Web サイトの下に作成された以下の仮想ディレクトリを削除します。  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  


#### <a name="for-cloud-distribution-points-protect-your-azure-subscription-details-and-certificates"></a>クラウド配布ポイントについては、Azure サブスクリプションの詳細と証明書を保護する
クラウド配布ポイントを使用する場合、次の重要度が高い項目を保護します。
- Azure サブスクリプションのユーザー名とパスワード
- Azure 管理証明書 
- クラウド配布ポイントのサービス証明書

証明書を安全に保存します。 また、クラウド配布ポイントを構成するときにネットワーク経由で証明書を参照する場合は、サイト システム サーバーとソースの場所の間で IPsec または SMB 署名を使用します。  

#### <a name="for-service-continuity-monitor-the-expiry-date-of-the-cloud-distribution-point-certificates"></a>サービスの継続性については、クラウド配布ポイント証明書の有効期限を監視する
Configuration Manager では、クラウド配布ポイント用にインポートされた証明書の期限切れが近づいても、警告されません。 Configuration Manager とは別に有効期限を監視します。 期限が切れる前に、証明書を更新して、新しい証明書をインポートするようにします。 サーバー認証証明書を外部のパブリック プロバイダーから取得する場合、更新された証明書を受け取るまでに余分に時間がかかる可能性があるため、このような対応が重要です。  

 いずれかの証明書の期限が切れると、Cloud Services Manager はステータス メッセージ ID **9425** を生成します。 CloudMgr.log ファイルには、証明書が**期限切れ状態である**ことを示すエントリが含まれ、有効期限日も UTC で記録されています。  



## <a name="security-considerations-for-content-management"></a>コンテンツ管理についてのセキュリティの考慮事項  

コンテンツ管理を計画するときは、次の点を考慮してください。  

-   クライアントは、ダウンロードが終わるまでコンテンツを検証しません。  

     Configuration Manager クライアントは、コンテンツがクライアント キャッシュにダウロードされた後でのみ、コンテンツのハッシュを検証します。 攻撃者によって、ダウンロードされるファイルのリスト、あるいはコンテンツ自体が改ざんされると、ダウンロード プロセスにおいて、クライアントのみのかなり広いネットワーク帯域幅が消費されてから、無効なハッシュが発生してコンテンツが破棄される可能性があります。  

-   クラウド配布ポイントを使用する場合、コンテンツへのアクセスは社内に自動的に制限されます。 選択したユーザーまたはグループに制限を広げることはできません。  

-   クラウド配布ポイントを使用する場合、クライアントは管理ポイントから認証され、Configuration Manager トークンを使用して、クラウド配布ポイントにアクセスします。 トークンの有効期間は 8 時間です。 この動作は、信頼しなくなったクライアントをブロックしても、そのトークンの有効期間が切れるまで、クラウド配布ポイントからコンテンツを継続してダウンロードできることを意味します。 この時点で、クライアントはブロックされているため、管理ポイントはクライアント用に追加のトークンを発行しません。  

     この 8 時間内にブロックされたクライアントがコンテンツをダウンロードしないようにするには、クラウド サービスを停止します。 Configuration Manager コンソールで **[管理]** ワークスペースに進み、 **[クラウド サービス]** を展開して **[クラウド配布ポイント]** ノードを選択します。  



##  <a name="privacy-information-for-content-management"></a><a name="BKMK_Privacy_ContentManagement"></a> コンテンツ管理のプライバシー情報  

 管理ユーザーがこの操作を選択することがありますが、Configuration Manager はコンテンツ ファイルのユーザー データを含みません。  



## <a name="see-also"></a>関連項目

- [コンテンツ管理の基本的な概念](fundamental-concepts-for-content-management.md)  

- [アプリケーション管理に関するセキュリティとプライバシー](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

- [ソフトウェア更新プログラムのセキュリティとプライバシー](../../../sum/plan-design/security-and-privacy-for-software-updates.md)  

- [OS の展開のセキュリティとプライバシー](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  
