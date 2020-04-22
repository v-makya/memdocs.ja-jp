---
title: クライアント展開のベスト プラクティス
titleSuffix: Configuration Manager
description: Configuration Manager でのクライアント展開のベスト プラクティスを入手します。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28f8bfb2ef012fcd4f19835190b7c042d38fd9e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693880"
---
# <a name="best-practices-for-client-deployment-in-configuration-manager"></a>Configuration Manager でのクライアント展開のベスト プラクティス

*適用対象:Configuration Manager (Current Branch)*


## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Active Directory コンピューターには、ソフトウェア更新プログラムを使ったクライアントのインストールを行う  
 このクライアント展開方法は、既存の Windows テクノロジを使用し、Active Directory インフラストラクチャと統合し、Configuration Manager で最低限の構成しか必要とせず、ファイアウォール用の構成が最も容易で、最も安全です。 グループ ポリシーの構成にセキュリティ グループと WMI フィルターを使用するので、どのコンピューターに Configuration Manager クライアントをインストールするかについても、柔軟に制御できます。  

 詳細については、「 [ソフトウェアの更新に基づいたインストールを使用した Configuration Manager クライアントのインストール方法](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP)」をご覧ください。  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Active Directory スキーマを拡張してサイトを公開し、コマンドライン オプションなしでCCMSetup が実行できるようにする  
 Active Directory スキーマを Configuration Manager 用に拡張して、サイトが Active Directory Domain Services に公開されるとき、多くのクライアント インストール プロパティが Active Directory Domain Services に公開されます。 コンピューターでこれらのクライアント インストール プロパティを見つけることができる場合は、Configuration Manager クライアントの展開時にそれらを使用できます。 この情報は自動的に生成されるため、インストール プロパティを手動で入力するために発生する人的ミスのリスクが排除されます。  

 詳細については、「[Active Directory Domain Services に発行されたクライアント インストールのプロパティについて](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)」をご覧ください。  

## <a name="use-a-phased-rollout-to-manage-cpu-usage"></a>段階的なロールアウトを使用して CPU 使用率を管理する  
 クライアントの段階的なロールアウトを使用して、CPU 処理の要件によるサイト サーバーへの影響を最小化します。 業務時間外にクライアントを展開すると、日中他のビジネス サービスに使用できる帯域幅が増え、ユーザーのコンピューターの反応が遅くなったり、再起動を要求して、ユーザーに支障をきたしたりすることがありません。  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>主要なクライアント展開が終わったら、自動アップグレードを有効化する  
 [自動クライアント アップグレード](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)は、おそらくオフラインだったために主要なクライアント インストール方法に含まれなかった少数のクライアント コンピューターをアップグレードする場合に役立ちます。 

> [!NOTE]  
>  Configuration Manager のパフォーマンスが改善され、プライマリ クライアントのアップグレード方法として自動アップグレードを使用できるようになりました。 ただし、パフォーマンスは、クライアント数など、階層のインフラストラクチャに左右されます。  


## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>client.msi プロパティを使ってクライアントをインストールするときは、SMSMP と FSP を使用する  
 SMSMP プロパティはクライアントが通信する最初の管理ポイントを指定し、Active Directory ドメイン サービス、DNS、WINS などの、サービスの場所のソリューションへの依存を排除します。  

 FSP プロパティを使ってフォールバック ステータス ポイントをインストールすると、クライアントのインストールや割り当てを監視し、通信上の問題点を特定できます。  

 これらのオプションの詳細については、[クライアント インストールのプロパティについて](../../../../core/clients/deploy/about-client-installation-properties.md)に関するページを参照してください。  

## <a name="install-client-language-packs-before-you-install-the-clients"></a>クライアントをインストールする前に、クライアント言語パックをインストールする  
クライアントを展開する前に、クライアント言語パックをインストールすることをお勧めします。 クライアントをインストールしてから、(追加の言語を有効化するために) サイトに[クライアントの言語パック](../../../../core/servers/deploy/install/language-packs.md)をインストールする場合、追加の言語を使用するには、クライアントを再インストールする必要があります。 モバイル デバイス クライアントの場合、モバイル デバイスをワイプして再登録する必要があります。  

## <a name="prepare-required-pki-certificates-in-advance"></a>必要な PKI 証明書を事前に準備する  
 インターネット上のデバイス、登録済みモバイル デバイス、および Mac コンピューターを管理するには、サイト システム (管理ポイントと配布ポイント) とクライアント デバイスに PKI 証明書が必要です。 運用ネットワークでは、状況に応じて、管理者が新しい証明書を使用するために管理承認を変更したり、サイト システム サーバーを再起動する必要があります。また、ユーザーは新しいグループ メンバーシップのためにログオフおよびログオンが必要になる場合があります。 さらに、セキュリティ アクセス許可のレプリケーションと新しい証明書テンプレートのために、十分な時間を見込む必要があります。  

 必要な PKI 証明書の詳細については、「[Configuration Manager での PKI 証明書の要件](../../../../core/plan-design/network/pki-certificate-requirements.md)」を参照してください。  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>クライアントをインストールする前に必要なクライアント設定とメンテナンス期間を構成する  
 [クライアント設定](../../../../core/clients/deploy/configure-client-settings.md)とメンテナンス期間は、クライアントをインストールする前または後に構成できますが、クライアントをインストールしてすぐにこれらの設定を使用できるように、クライアントをインストールする前に必要な設定を構成することをお勧めします。 

 サーバーや Windows Embedded デバイスといった重要なデバイスでは、業務の継続性を確保するために、メンテナンス期間を構成します。 必要なソフトウェア更新プログラムとマルウェア対策ソフトウェアによってコンピューターが営業時間内に再起動しないように、メンテナンス期間を設定することができます。  

> [!IMPORTANT]  
>  Unified Write Filter (UWF) で保護する予定の Windows 10 コンピューターでは、クライアントをインストールする前に UWF のデバイスを構成する必要があります。 これにより、メンテナンス モード中に権限の低いユーザーをロックアウトしてデバイスにログインできなくするカスタム資格情報プロバイダーを使用して、Configuration Manager がクライアントをインストールできるようになります。  

## <a name="plan-your-user-enrollment-experience-for-mac-computers-and-mobile-devices"></a>Mac コンピューターとモバイル デバイスのユーザー登録エクスペリエンスを計画する   
 ユーザーが Configuration Manager を使用して自分の Mac コンピューターとモバイル デバイスを登録する場合、ユーザー エクスペリエンスを計画します。 たとえば、Web ページを使用してインストールおよび登録プロセスをスクリプト化し、ユーザーが入力する情報を必要最小限に抑えたり、手順とリンクを電子メールで送信したりすることができます。  

## <a name="use-file-based-write-filters-for-windows-embedded-devices"></a>Windows Embedded デバイスにファイル ベースの書き込みフィルターを使用する 
 Enhanced Write Filter (EWF) を使用する組み込みデバイスでは、状態メッセージの再同期が発生しやすくなります。 Enhanced Write Filter を使用する組み込みデバイスが少数の場合は、この問題に気がつかない可能性があります。 ただし、差分のインベントリではなく完全なインベントリを送信する場合など、情報を再同期する組み込みデバイスが多数ある場合、ネットワーク パケットが大幅に増え、サイト サーバーの CPU 処理量が多くなる可能性があります。  

 有効にする書き込みフィルターの種類を選択できる場合は、Configuration Manager クライアント上のネットワークと CPU の効率のために、ファイル ベースの書き込みフィルターを選択し、デバイスの再起動から次の再起動までクライアントの状態とインベントリ データを維持する例外を構成します。 書き込みフィルターの詳細については、[Windows Embedded デバイスへのクライアント展開の計画](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)に関するページを参照してください。  

 プライマリ サイトでサポートできる Windows Embedded クライアントの最大数の詳細については、「 [クライアントとデバイスでサポートされるオペレーティング システム](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)」を参照してください。  
