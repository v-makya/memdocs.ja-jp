---
title: 使用されるアカウント
titleSuffix: Configuration Manager
description: Configuration Manager で使用されている Windows のグループ、アカウント、SQL オブジェクトを識別し、管理します。
ms.date: 10/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c0cfc9ee0fe80aa39ba49b25c392334a01169a8a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703770"
---
# <a name="accounts-used-in-configuration-manager"></a>Configuration Manager で使用されるアカウント

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager で使用される Windows グループ、アカウント、SQL オブジェクト、それらの使用方法、要件を確認するには、以下の情報を参照してください。  

- [Configuration Manager で作成および使用される Windows グループ](#bkmk_groups)  
  - [ConfigMgr_CollectedFilesAccess](#configmgr_collectedfilesaccess)  
  - [ConfigMgr_DViewAccess](#configmgr_dviewaccess)  
  - [ConfigMgr リモート コントロール ユーザー](#configmgr-remote-control-users)  
  - [SMS Admins](#sms-admins)  
  - [SMS_SiteSystemToSiteServerConnection_MP_&lt;sitecode\>](#bkmk_remotemp)  
  - [SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitecode\>](#bkmk_remoteprov)  
  - [SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitecode\>](#bkmk_remotestat)  
  - [SMS_SiteToSiteConnection_&lt;sitecode\>](#bkmk_filerepl)  

- [Configuration Manager が使用するアカウント](#bkmk_accounts)
  - [Active Directory グループ探索アカウント](#active-directory-group-discovery-account)  
  - [Active Directory システム探索アカウント](#active-directory-system-discovery-account)  
  - [Active Directory ユーザー探索アカウント](#active-directory-user-discovery-account)  
  - [Active Directory フォレスト アカウント](#active-directory-forest-account)  
  - [証明書登録ポイント アカウント](#certificate-registration-point-account)  
  - [OS イメージのキャプチャ アカウント](#capture-os-image-account)  
  - [クライアント プッシュ インストール アカウント](#client-push-installation-account)  
  - [登録ポイントの接続アカウント](#enrollment-point-connection-account)  
  - [Exchange Server 接続アカウント](#exchange-server-connection-account)  
  - [管理ポイントの接続アカウント](#management-point-connection-account)  
  - [マルチキャスト接続アカウント](#multicast-connection-account)  
  - [ネットワーク アクセス アカウント](#network-access-account)  
  - [パッケージ アクセス アカウント](#package-access-account)  
  - [レポート サービス ポイントのアカウント](#reporting-services-point-account)  
  - [リモート ツールの許可されたビューアー アカウント](#remote-tools-permitted-viewer-accounts)  
  - [サイト インストール アカウント](#site-installation-account)
  - [サイト システムのインストール アカウント](#site-system-installation-account)  
  - [サイト システム プロキシ サーバー アカウント](#site-system-proxy-server-account)  
  - [SMTP サーバー接続アカウント](#smtp-server-connection-account)  
  - [ソフトウェア更新ポイントの接続アカウント](#software-update-point-connection-account)  
  - [ソース サイトのアカウント](#source-site-account)  
  - [ソース サイトのデータベース アカウント](#source-site-database-account)  
  - [タスク シーケンス ドメイン参加アカウント](#task-sequence-domain-join-account)  
  - [タスク シーケンス ネットワーク フォルダー接続アカウント](#task-sequence-network-folder-connection-account)  
  - [タスク シーケンス実行アカウント](#task-sequence-run-as-account)  

- [SQL で Configuration Manager によって使用されるユーザー オブジェクト](#bkmk_sqlusers)
  - [smsdbuser_ReadOnly](#smsdbuser_readonly)
  - [smsdbuser_ReadWrite](#smsdbuser_readwrite)
  - [smsdbuser_ReportSchema](#smsdbuser_reportschema)

- [SQL で Configuration Manager によって使用されるデータベース ロール](#bkmk_sqlroles)
  - [smsdbrole_AITool](#smsdbrole_aitool)
  - [smsdbrole_AIUS](#smsdbrole_aius)
  - [smsdbrole_AMTSP](#smsdbrole_amtsp)
  - [smsdbrole_CRP](#smsdbrole_crp)
  - [smsdbrole_CRPPfx](#smsdbrole_crppfx)
  - [smsdbrole_DMP](#smsdbrole_dmp)
  - [smsdbrole_DmpConnector](#smsdbrole_dmpconnector)
  - [smsdbrole_DViewAccess](#smsdbrole_dviewaccess)
  - [smsdbrole_DWSS](#smsdbrole_dwss)
  - [smsdbrole_EnrollSvr](#smsdbrole_enrollsvr)
  - [smsdbrole_extract](#smsdbrole_extract)
  - [smsdbrole_HMSUser](#smsdbrole_hmsuser)
  - [smsdbrole_MCS](#smsdbrole_mcs)
  - [smsdbrole_MP](#smsdbrole_mp)
  - [smsdbrole_MPMBAM](#smsdbrole_mpmbam)
  - [smsdbrole_MPUserSvc](#smsdbrole_mpusersvc)
  - [smsdbrole_siteprovider](#smsdbrole_siteprovider)
  - [smsdbrole_siteserver](#smsdbrole_siteserver)
  - [smsdbrole_SUP](#smsdbrole_sup)
  - [smsdbrole_WebPortal](#smsdbrole_webportal)
  - [smsschm_users](#smsschm_users)

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a><a name="bkmk_groups"></a> Configuration Manager で作成および使用される Windows グループ  

Configuration Manager は、次の Windows グループを自動的に作成し、多くの場合、自動的に保持します。  

> [!NOTE]  
> Configuration Manager でドメイン メンバーであるコンピューター上にグループが作成されるとき、グループはローカル セキュリティ グループになります。 コンピューターがドメイン コントローラーである場合、グループはローカル グループとして作成されます。 この種類のグループは、ドメイン内のすべてのドメイン コントローラー間で共有されます。  


### <a name="configmgr_collectedfilesaccess"></a><a name="configmgr_collectedfilesaccess"></a> ConfigMgr_CollectedFilesAccess

Configuration Manager は、このグループを使用して、ソフトウェア インベントリで収集されたファイルを表示するためのアクセスを許可します。  

詳しくは、「[ソフトウェア インベントリの概要](../../clients/manage/inventory/introduction-to-software-inventory.md)」をご覧ください。

#### <a name="type-and-location"></a>種類と場所
このグループは、プライマリ サイト サーバー上に作成されるローカル セキュリティ グループです。

サイトをアンインストールしても、このグループが自動的に削除されることはありません。 サイトをアンインストールした後、手動で削除します。

#### <a name="membership"></a>メンバーシップ
Configuration Manager は、グループ メンバーシップを自動的に管理します。 メンバーシップには、割り当てられたセキュリティ ロールからの保護可能な **[コレクション]** オブジェクトに対する **[収集ファイルの表示]** アクセス許可が付与されている管理ユーザーが含まれます。

#### <a name="permissions"></a>アクセス許可
既定では、このグループには、サイト サーバーの `C:\Program Files\Microsoft Configuration Manager\sinv.box\FileCol` フォルダーに対する**読み取り**アクセス許可が与えられます。  


### <a name="configmgr_dviewaccess"></a><a name="configmgr_dviewaccess"></a>ConfigMgr_DViewAccess  

このグループは、Configuration Manager がサイト データベース サーバー上または子プライマリ サイトのデータベース レプリカ サーバー上に作成するローカル セキュリティ グループです。 ユーザーが階層内のサイト間のデータベース レプリケーションに対する分散ビューを使用すると、サイトによって作成します。 中央管理サイトのサイト サーバー アカウントと SQL Server コンピューター アカウントが含まれています。

詳しくは、「[サイト間のデータ転送](data-transfers-between-sites.md)」をご覧ください。


### <a name="configmgr-remote-control-users"></a>ConfigMgr リモート コントロール ユーザー  

Configuration Manager リモート ツールは、このグループを使用して、ユーザーが**アクセス許可のあるユーザー**の一覧で設定するアカウントとグループを格納します。 サイトでは各クライアントにこの一覧が割り当てられます。  

詳細については、「[リモート コントロールの概要](../../clients/manage/remote-control/introduction-to-remote-control.md)」をご覧ください。

#### <a name="type-and-location"></a>種類と場所
このグループは、クライアントがリモート ツールを有効にするポリシーを受信すると Configuration Manager クライアントに作成されるローカル セキュリティ グループです。

クライアントのリモート ツールを無効にしても、このグループが自動的に削除されることはありません。 リモート ツールを無効にした後は、手動でそれを削除します。

#### <a name="membership"></a>メンバーシップ
既定では、このグループにメンバーシップはありません。 ユーザーを**アクセス許可のあるユーザー**の一覧に追加すると、このユーザーは自動的にこのグループに追加されます。

このグループにユーザーやグループを直接追加する代わりに、**アクセス許可のあるユーザー**の一覧を使用して、このグループのメンバーシップを管理します。

管理ユーザーは、アクセス許可のあるユーザーであるだけでなく、**コレクション** オブジェクトに対する**リモート制御**アクセス許可が割り当てられている必要があります。 このアクセス許可を割り当てるには、**リモート ツール オペレーター** セキュリティ ロールを使用します。  

#### <a name="permissions"></a>アクセス許可
既定では、このグループには、コンピューター上の任意の場所に対するアクセス許可は割り当てられていません。 それは、 **[アクセス許可のあるユーザー]** の一覧を保持するためだけに使用されます。  


### <a name="sms-admins"></a>SMS Admins  

このグループは、WMI 経由での SMS プロバイダーへのアクセスを許可するために、Configuration Manager によって使用されます。 SMS プロバイダーへのアクセスは、Configuration Manager コンソールでオブジェクトを表示および変更するために必要です。  

> [!NOTE]  
> 管理ユーザーの役割に基づいた管理構成によって、Configuration Manager コンソールを使用して管理ユーザーが表示および管理できるオブジェクトが決まります。  

詳細については、「[SMS プロバイダーの計画](plan-for-the-sms-provider.md)」を参照してください。

#### <a name="type-and-location"></a>種類と場所
このグループは、SMS プロバイダーのある各コンピューターに作成されるローカル セキュリティ グループです。 

サイトをアンインストールしても、このグループが自動的に削除されることはありません。 サイトをアンインストールした後、手動で削除します。

#### <a name="membership"></a>メンバーシップ
Configuration Manager は、グループ メンバーシップを自動的に管理します。 既定では、階層内の各管理ユーザーおよびサイト サーバーのコンピューター アカウントが、サイト内の各 SMS プロバイダー コンピューターの **SMS Admins** グループのメンバーとなります。

#### <a name="permissions"></a>アクセス許可
SMS Admins グループの権限とアクセス許可は、**WMI コントロール**という MMC スナップインで見ることができます。 既定では、このグループには `Root\SMS` WMI 名前空間に対する**アカウントの有効化**と**リモートの有効化**が付与されます。 認証されたユーザーは、**メソッドの実行**、**プロバイダーの書き込み**、および **アカウントの有効化**を実行できます。

リモートの Configuration Manager コンソールを使用するときは、サイト サーバー コンピューターと SMS プロバイダーの両方で、**リモートからのアクティブ化** DCOM アクセス許可を構成します。 これらの権限を、**SMS Admins** グループに付与します。 これらの権限をユーザーまたはグループに直接付与するのではなく、このようにすることで、管理が簡単になります。 詳細については、「[ リモート Configuration Manager コンソールに対する DCOM アクセス許可を構成する](../../servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole)」をご覧ください。 


### <a name="sms_sitesystemtositeserverconnection_mp_ltsitecode"></a><a name="bkmk_remotemp"></a> SMS_SiteSystemToSiteServerConnection_MP_&lt;sitecode\>  
 
サイト サーバーからリモートにある管理ポイントでは、サイト データベースに接続するためにこのグループが使用されます。 このグループは、サイトサーバーおよびサイト データベース上の受信トレイ フォルダーへの管理ポイント アクセスを提供します。  

#### <a name="type-and-location"></a>種類と場所
このグループは、SMS プロバイダーのある各コンピューターに作成されるローカル セキュリティ グループです。

サイトをアンインストールしても、このグループが自動的に削除されることはありません。 サイトをアンインストールした後、手動で削除します。

#### <a name="membership"></a>メンバーシップ
Configuration Manager は、グループ メンバーシップを自動的に管理します。 既定では、メンバーシップには、サイトの管理ポイントを持つリモート コンピューターのコンピューター アカウントが含まれます。

#### <a name="permissions"></a>アクセス許可
既定では、このグループには、サイト サーバーの `C:\Program Files\Microsoft Configuration Manager\inboxes` フォルダーに対する**読み取り**、**読み取りと実行**、**フォルダーの内容の一覧表示**のアクセス許可が付与されます。 このグループには、管理ポイントがクライアント データを書き込む **inboxes** の下のサブフォルダーへの追加の**書き込み**アクセス許可が付与されます。


### <a name="sms_sitesystemtositeserverconnection_smsprov_ltsitecode"></a><a name="bkmk_remoteprov"></a> SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitecode\>  
 
リモート SMS プロバイダー コンピューターでは、サイト サーバーに接続するためにこのグループが使用されます。  

#### <a name="type-and-location"></a>種類と場所
このグループは、サイト サーバー上に作成されるローカル セキュリティ グループです。

サイトをアンインストールしても、このグループが自動的に削除されることはありません。 サイトをアンインストールした後、手動で削除します。

#### <a name="membership"></a>メンバーシップ
Configuration Manager は、グループ メンバーシップを自動的に管理します。 既定では、メンバーシップにはコンピューター アカウントまたはドメイン ユーザー アカウントが含まれています。 このアカウントを使用して、各リモート SMS プロバイダーからサイト サーバーへの接続が行われます。

#### <a name="permissions"></a>アクセス許可
既定では、このグループには、サイト サーバーの `C:\Program Files\Microsoft Configuration Manager\inboxes` フォルダーに対する**読み取り**、**読み取りと実行**、**フォルダーの内容の一覧表示**のアクセス許可が付与されます。 このグループには、受信トレイの下のサブフォルダーに対する**書き込み**および**変更**の追加アクセス許可もあります。 SMS プロバイダーでは、これらのフォルダーへのアクセスが必要です。

このグループには、サイト サーバー上の `C:\Program Files\Microsoft Configuration Manager\OSD\Bin` 下のサブフォルダーへの**読み取り**アクセス許可もあります。 

また、`C:\Program Files\Microsoft Configuration Manager\OSD\boot` の下のサブフォルダーに対しても、次のアクセス許可を持っています。
- **読み取り**  
- **読み取りと実行**  
- **フォルダーの内容の一覧表示**  
- **書き込み**  
- **変更**   


### <a name="sms_sitesystemtositeserverconnection_stat_ltsitecode"></a><a name="bkmk_remotestat"></a> SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitecode\>  

Configuration Manager のリモート サイト システム コンピューターのファイル ディスパッチ マネージャー コンポーネントでは、サイト サーバーに接続するためにこのグループが使用されます。  

#### <a name="type-and-location"></a>種類と場所
このグループは、サイト サーバー上に作成されるローカル セキュリティ グループです。

サイトをアンインストールしても、このグループが自動的に削除されることはありません。 サイトをアンインストールした後、手動で削除します。

#### <a name="membership"></a>メンバーシップ
Configuration Manager は、グループ メンバーシップを自動的に管理します。 既定では、メンバーシップにはコンピューター アカウントまたはドメイン ユーザー アカウントが含まれています。 このアカウントは、ファイル ディスパッチ マネージャーを実行している各リモート サイト システムからサイト サーバーに接続するために使用されます。

#### <a name="permissions"></a>アクセス許可
既定では、このグループには、サイト サーバーの `C:\Program Files\Microsoft Configuration Manager\inboxes` フォルダーとそのサブフォルダーに対する**読み取り**、**読み取りと実行**、**フォルダーの内容の一覧表示**のアクセス許可が付与されます。 

このグループには、サイト サーバー上の `C:\Program Files\Microsoft Configuration Manager\inboxes\statmgr.box` フォルダーに対する**書き込み**と**変更**の追加アクセス許可もあります。


### <a name="sms_sitetositeconnection_ltsitecode"></a><a name="bkmk_filerepl"></a> SMS_SiteToSiteConnection_&lt;sitecode\>  
Configuration Manager は、このグループを使用して、階層内のサイト間でファイルベースのレプリケーションを有効にします。 このサイトにファイルを直接転送する各リモート サイトについて、このグループには **ファイル レプリケーション アカウント**として設定されたアカウントが含まれます。  

#### <a name="type-and-location"></a>種類と場所
このグループは、サイト サーバー上に作成されるローカル セキュリティ グループです。

#### <a name="membership"></a>メンバーシップ
新しいサイトを別のサイトの子としてインストールすると、Configuration Manager によって、新しいサイト サーバーのコンピューター アカウントが、親サイト サーバーのこのグループに、自動的に追加されます。 さらに、Configuration Manager は、親サイトのコンピューター アカウントを新しいサイト サーバーのグループに追加します。 ファイルベースの転送用に別のアカウントを指定する場合は、移行先のサイト サーバーのこのグループにアカウントを追加します。

サイトをアンインストールしても、このグループが自動的に削除されることはありません。 サイトをアンインストールした後、手動で削除します。

#### <a name="permissions"></a>アクセス許可
既定では、このグループには、`C:\Program Files\Microsoft Configuration Manager\inboxes\despoolr.box\receive` フォルダーに対する**フル コントロール**があります。



## <a name="accounts-that-configuration-manager-uses"></a><a name="bkmk_accounts"></a> Configuration Manager が使用するアカウント  

Configuration Manager に次のアカウントを設定できます。  


### <a name="active-directory-group-discovery-account"></a>Active Directory グループ探索アカウント  

サイトでは、ユーザーが指定した Active Directory Domain Services 内の場所から次のオブジェクトを探索するために、**Active Directory グループ探索アカウント**が使用されます。
- ローカル、グローバル、およびユニバーサル セキュリティ グループ
- これらのグループ内のメンバーシップ
- 配布グループ内のメンバーシップ
  - 配布グループは、グループ リソースとしては探索されません

このアカウントは、探索を実行するサイト サーバーのコンピューター アカウントでも、Windows ユーザー アカウントでも構いません。 このアカウントには、探索対象に指定された Active Directory の場所に対する**読み取り**アクセス許可が必要です。  

詳細については、「[Active Directory グループの探索](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutGroup)」をご覧ください。


### <a name="active-directory-system-discovery-account"></a>Active Directory システム探索アカウント  

サイトでは、ユーザーが指定した Active Directory Domain Services 内の場所からコンピューターを探索するために、**Active Directory システム探索アカウント**が使用されます。  

このアカウントは、探索を実行するサイト サーバーのコンピューター アカウントでも、Windows ユーザー アカウントでも構いません。 このアカウントには、探索対象に指定された Active Directory の場所に対する**読み取り**アクセス許可が必要です。  

詳細については、「[Active Directory システムの探索](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutSystem)」をご覧ください。


### <a name="active-directory-user-discovery-account"></a>Active Directory ユーザー探索アカウント  
 
サイトでは、ユーザーが指定した Active Directory Domain Services 内の場所からユーザー アカウントを探索するために、**Active Directory ユーザー探索アカウント**が使用されます。  

このアカウントは、探索を実行するサイト サーバーのコンピューター アカウントでも、Windows ユーザー アカウントでも構いません。 このアカウントには、探索対象に指定された Active Directory の場所に対する**読み取り**アクセス許可が必要です。  

詳細については、「[Active Directory ユーザー探索](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)」をご覧ください。 


### <a name="active-directory-forest-account"></a>Active Directory フォレスト アカウント  

サイトでは、Active Directory フォレストからネットワーク インフラストラクチャを探索するために、**Active Directory フォレスト アカウント**が使用されます。 中央管理サイトとプライマリ サイトも、フォレストの Active Directory Domain Services にサイト データを発行するためにそれを使用します。  

> [!NOTE]  
> セカンダリ サイトでは、Active Directory に発行するときに、必ず、セカンダリ サイト サーバーのコンピューター アカウントを使います。  

信頼されていないフォレストを探索して発行するには、Active Directory フォレスト アカウントはグローバル アカウントでなければなりません。 サイト サーバーのコンピューター アカウントを使用しない場合は、グローバル アカウントのみ選択できます。  

このアカウントは、ネットワーク インフラストラクチャを探索する各 Active Directory フォレストの **[読み取り]** アクセス許可を持っている必要があります。  

このアカウントは、サイト データを発行する各 Active Directory フォレスト内の **System Management** コンテナーおよびすべての子オブジェクトに対する**フル コントロール** アクセス許可を持っている必要があります。 詳細については、「[サイト発行のために Active Directory を準備する](../network/extend-the-active-directory-schema.md)」を参照してください。  

詳細については、「[Active Directory フォレストの探索](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest)」をご覧ください。


### <a name="certificate-registration-point-account"></a>証明書登録ポイント アカウント  

証明書登録ポイントでは、Configuration Manager データベースに接続するために、**証明書登録ポイント アカウント**が使用されます。 既定ではそのコンピューター アカウントが使用されますが、代わりに、ユーザー アカウントを構成することができます。 証明書登録ポイントがサイト サーバーの信頼されていないドメインにあるときは、ユーザー アカウントを指定する必要があります。 このアカウントには、サイト データベースに対する**読み取り**アクセス許可のみが必要です。理由は、書き込みタスクは、状態メッセージ システムが処理するためです。  

詳細については、「[証明書プロファイルの概要](../../../protect/deploy-use/introduction-to-certificate-profiles.md)」をご覧ください。


### <a name="capture-os-image-account"></a>OS イメージのキャプチャ アカウント  

OS イメージをキャプチャするとき、Configuration Manager では、キャプチャされたイメージを格納するフォルダーにアクセスするために、**OS イメージのキャプチャ アカウント**が使用されます。 タスク シーケンスに**OS イメージのキャプチャ** ステップを追加する場合は、このアカウントが必要です。  

そのアカウントには、キャプチャされたイメージが格納されるネットワーク共有に対する**読み取り**と**書き込み**のアクセス許可が必要です。  

Windows でアカウントのパスワードを変更する場合は、新しいパスワードでタスク シーケンスを更新します。 Configuration Manager クライアントは、クライアント ポリシーの次回ダウンロード時に、新しいパスワードを受け取ります。  

このアカウントを使用する必要がある場合は、ドメイン ユーザー アカウントを 1 つ作成します。 必要なネットワーク リソースにアクセスするための最小限のアクセス許可をそのアカウントに付与し、すべてのキャプチャ タスク シーケンスでそれを使用します。  

> [!IMPORTANT]  
> このアカウントに対話型サインインのアクセス許可を割り当てないでください。  
>   
> このアカウントにはネットワーク アクセス アカウントを使用しないでください。  

詳しくは、「[OS をキャプチャするタスク シーケンスの作成](../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)」をご覧ください。


### <a name="client-push-installation-account"></a>クライアント プッシュ インストール アカウント  

クライアント プッシュ インストール方法を使用してクライアントを展開する場合、サイトではコンピューターに接続して Configuration Manager クライアント ソフトウェアをインストールするために、**クライアント プッシュ インストール アカウント**が使用されます。 このアカウントを指定しないと、サイト サーバーはそのコンピューター アカウントの使用を試みます。  

このアカウントは、ターゲット クライアント コンピューター上のローカル **Administrators** グループのメンバーである必要があります。 このアカウントに、**ドメイン管理者**の権限は必要ありません。  

複数のクライアント プッシュ インストール アカウントを指定できます。 Configuration Manager は、成功するまで 1 つずつ順番に試みます。  

> [!TIP]  
> 大規模な Active Directory 環境があり、このアカウントを変更する必要がある場合は、以下の手順を使用すると、このアカウント更新をいっそう効率的に調整できます。 
> 1. 異なる名前を持つ新しいアカウントを作成します   
> 2. Configuration Manager でクライアント プッシュ インストール アカウントの一覧に新しいアカウントを追加します  
> 3. Active Directory Domain Services によって新しいアカウントがレプリケートされるのに十分な時間を置きます  
> 4. その後、Configuration Manager と Active Directory Domain Services から古いアカウントを削除します  

> [!IMPORTANT]  
> このアカウントには、ローカルにサインインする権限を与えないでください。  

詳しくは、「[クライアント プッシュ インストール](../../clients/deploy/plan/client-installation-methods.md#client-push-installation)」をご覧ください。


### <a name="enrollment-point-connection-account"></a>登録ポイントの接続アカウント  

登録ポイントでは、Configuration Manager サイトのデータベースに接続するために、**登録ポイントの接続アカウント**が使用されます。 既定ではそのコンピューター アカウントが使用されますが、代わりに、ユーザー アカウントを構成することができます。 登録ポイントがサイト サーバーから信頼されていないドメインにある場合は、ユーザー アカウントを指定する必要があります。 このアカウントには、サイト データベースに対する**読み取り**および**書き込み**アクセス権が必要です。  

詳細については、[オンプレミス MDM のサイト システムの役割のインストール](../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)に関するページをご覧ください。


### <a name="exchange-server-connection-account"></a>Exchange Server 接続アカウント  

サイト サーバーでは、指定された Exchange Server に接続するために、**Exchange Server 接続アカウント**が使用されます。 この接続を使用して、Exchange Server サーバーに接続するモバイル デバイスの検索と管理が行われます。 このアカウントには、Exchange Server コンピューターへの必要なアクセス許可を提供する Exchange PowerShell コマンドレットが必要です。 コマンドレットの詳細については、「[Exchange Connector をインストールして構成する](../../../mdm/deploy-use/install-configure-exchange-connector.md)」を参照してください。  


### <a name="management-point-connection-account"></a>管理ポイントの接続アカウント  

管理ポイントでは、Configuration Manager サイトのデータベースに接続するために、**管理ポイントの接続アカウント**が使用されます。 この接続は、クライアントの情報の送信と取得に使用されます。 既定ではそのコンピューター アカウントが使用されますが、代わりに、ユーザー アカウントを構成することができます。 管理ポイントがサイト サーバーから信頼されていないドメインにある場合は、ユーザー アカウントを指定する必要があります。  

このアカウントは、Microsoft SQL Server を実行しているコンピューター上の権限の低いローカル アカウントとして作成します。  

> [!IMPORTANT]  
> このアカウントに対話型サインイン権限を付与しないでください。  


### <a name="multicast-connection-account"></a>マルチキャスト接続アカウント  

マルチキャストが有効な配布ポイントでは、サイト データベースから情報を読み取るために、**マルチキャスト接続アカウント**が使用されます。 既定ではそのコンピューター アカウントが使用されますが、代わりに、ユーザー アカウントを構成することができます。 サイト データベースが信頼されていないフォレストにある場合は、ユーザー アカウントを指定する必要があります。 たとえば、データ センターでは、サイト サーバーとサイト データベースとは別にフォレストに境界ネットワークがある場合、このアカウントを使用してマルチキャスト情報をサイト データベースから読み込みます。  

このアカウントが必要な場合は、Microsoft SQL Server を実行しているコンピューター上の権限の低いローカル アカウントとして作成します。  

> [!IMPORTANT]  
> このアカウントに対話型サインイン権限を付与しないでください。  

詳細については、「[Use multicast to deploy Windows over the network](../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md)」(マルチキャストを使用した、ネットワーク経由での Windows の展開) を参照してください。


### <a name="network-access-account"></a>ネットワーク アクセス アカウント  

クライアント コンピューターでは、ローカル コンピューター アカウントで配布ポイント上のコンテンツにアクセスできない場合に、**ネットワーク アクセス アカウント**が使用されます。 主に、ワークグループ クライアントや信頼されていないドメインのコンピューターに適用されます。 このアカウントは、OS の展開中に、OS をインストールしているコンピューターにドメインでのコンピューター アカウントがまだない場合にも使用されます。  

> [!Important]  
> ネットワーク アクセス アカウントは、プログラムの実行、ソフトウェア更新プログラムのインストール、タスク シーケンスの実行のためのセキュリティ コンテキストとして使用されることはありません。 ネットワーク上のリソースへのアクセス専用に使用されます。  

Configuration Manager クライアントでは、最初に、そのコンピューター アカウントを使用してコンテンツのダウンロードが試みられます。 それが失敗すると、ネットワーク アクセス アカウントが自動的に試みられます。  

バージョン 1806 以降のワークグループまたは Azure AD 参加済みクライアントは、ネットワーク アクセス アカウントを必要とせずに、配布ポイントからコンテンツに安全にアクセスできます。 この動作には、タスク シーケンスがブート メディア、PXE、またはソフトウェア センターから実行されている OS 展開シナリオが含まれます。 詳細については、「[Enhanced HTTP](enhanced-http.md)」(拡張 HTTP) をご覧ください。<!--1358228,1358278-->

> [!Note]  
> ネットワーク アクセス アカウントが必要ないように**拡張 HTTP** を有効にする場合は、配布ポイントで Windows Server 2012 以降が実行されている必要があります。 <!--SCCMDocs-pr issue #2696-->
>  
> この機能を有効にする前に、クライアントを少なくともバージョン 1806 にアップグレードしてください。 **拡張 HTTP** 接続だけを有効にすると、古いクライアントはこの方法を使用して認証できないため、配布ポイントからクライアント アップグレード パッケージをダウンロードできません。 <!--vso2841213-->   

#### <a name="permissions"></a>アクセス許可

このアカウントには、ソフトウェアにアクセスするためにクライアントで必要となる、コンテンツに対する最低限の適切なアクセス許可を付与します。 このアカウントは、配布ポイントで **[ネットワーク経由でコンピューターへアクセス]** の権限を持っている必要があります。 サイトごとに最大 10 個のネットワーク アクセス アカウントを構成することができます。  

このアカウントは、リソースへの必要なアクセスを可能にする任意のドメインに作成します。 ネットワーク アクセス アカウントには、常にドメイン名が含まれている必要があります。 このアカウントでは、パススルー セキュリティはサポートされません。 複数のドメインに配布ポイントがある場合は、信頼される側のドメインにアカウントを作成します。  

> [!TIP]  
> アカウントのロックアウトを避けるため、既存のネットワーク アクセス アカウントのパスワードは変更しないでください。 代わりに、新しいアカウントを作成して、Configuration Manager でその新しいアカウントを設定します。 すべてのクライアントが新しいアカウントの詳細情報を受け取ったら、ネットワーク共有フォルダーから古いアカウントを削除して、古いアカウントを削除します。  

> [!IMPORTANT]  
> このアカウントに対話型サインイン権限を付与しないでください。  
>   
> コンピューターがドメインに参加する権限をこのアカウントに付与しないでください。 タスク シーケンスの間にコンピューターをドメインに参加させる必要がある場合は、[タスク シーケンス ドメイン参加アカウント](#task-sequence-domain-join-account)を使用します。  

#### <a name="configure-the-network-access-account"></a>ネットワーク アクセス アカウントを構成する  

1.  Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開して **[サイト]** ノードを選択します。 次にサイトを選択します。  

2.  リボンの **[設定]** グループで、 **[サイト コンポーネントの構成]** を選択して、 **[ソフトウェアの配布]** を選択します。  

3.  **[ネットワーク アクセス アカウント]** タブを選択します。1 つまたは複数のアカウントを設定して、 **[OK]** を選択します。  


### <a name="package-access-account"></a>［パッケージ アクセス アカウント］  

**パッケージ アクセス アカウント**を使用すると、NTFS アクセス許可を設定して、配布ポイント上にあるパッケージの内容にアクセスできるユーザーおよびユーザー グループを指定できます。 既定では、Configuration Manager は、汎用のアクセス アカウントである **User** と **Administrator** にのみアクセス権を付与します。 その他の Windows アカウントや Windows グループを使用してクライアント コンピューターのアクセスを制御できます。 モバイル デバイスは、常にパッケージのコンテンツを匿名で取得するため、パッケージ アクセス アカウントは使用しません。  

既定では、Configuration Manager がコンテンツ ファイルを配布ポイントにコピーするときに、ローカルの **Users** グループに**読み取り**アクセスを、ローカルの **Administrators** グループに**フル コントロール**を許可します。 実際の必要なアクセス許可はパッケージに応じて異なります。 クライアントがワークグループや信頼されていないフォレストに含まれている場合は、そのクライアントはネットワーク アクセス アカウントを使用してパッケージ コンテンツにアクセスします。 ネットワーク アクセス アカウントに、定義されたパッケージ アクセス アカウントを使用したパッケージへのアクセス許可があることを確認してください。  

配布ポイントにアクセスできるドメイン内のアカウントを使用します。 パッケージの作成後にアカウントを作成または変更する場合は、パッケージを再配布する必要があります。 パッケージを更新しても、パッケージに対する NTFS アクセス許可は変更されません。  

ネットワーク アクセス アカウントは、**Users** グループのメンバーシップによって自動的に追加されるため、パッケージ アクセス アカウントとして追加する必要はありません。 パッケージ アクセス アカウントをネットワーク アクセス アカウントのみに制限しても、クライアントによるパッケージへのアクセスを妨げることはありません。  

#### <a name="manage-package-access-accounts"></a>パッケージ アクセス アカウントを管理する  

1.  Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** を選択します。  

2.  **[ソフトウェア ライブラリ]** ワークスペースで、アクセス アカウントの管理対象となるコンテンツの種類を決定し、それぞれに用意されている手順に従います。  

    - **アプリケーション**: **[アプリケーション管理]** を展開し、 **[アプリケーション]** を選択してから、アクセス アカウントを管理するアプリケーションを選択します。  

    - **パッケージ**: **[アプリケーション管理]** を展開し、 **[パッケージ]** を選択して、アクセス アカウントを管理するパッケージを選択します。  

    - **ソフトウェア更新プログラムの展開パッケージ**: **[ソフトウェア更新プログラム]** を展開し、 **[展開パッケージ]** を選択して、アクセス アカウントを管理する展開パッケージを選択します。  

    - **ドライバー パッケージ**: **[オペレーティング システム]** を展開し、 **[ドライバー パッケージ]** を選択して、アクセス アカウントを管理するドライバー パッケージを選択します。  

    - **OS イメージ**: **[オペレーティング システム]** を展開し、 **[オペレーティング システム イメージ]** を選択して、アクセス アカウントを管理するオペレーティング システム イメージを選択します。  

    - **OS アップグレード パッケージ**: **[オペレーティング システム]** を展開し、 **[オペレーティング システム アップグレード パッケージ]** を選択して、アクセス アカウントを管理する OS アップグレード パッケージを選択します。  

    - **ブート イメージ**: **[オペレーティング システム]** を展開し、 **[ブート イメージ]** を選択して、アクセス アカウントを管理するブート イメージを選択します。  

3.  選択したオブジェクトを右クリックして、 **[アクセス アカウントの管理]** を選択します。  

4.  **[アカウントの追加]** ダイアログ ボックスで、コンテンツに対するアクセス許可が付与されるアカウントの種類を指定して、アカウントに関連付けられているアクセス権を指定します。  

    > [!NOTE]  
    > アカウントのユーザー名を追加したときに Configuration Manager が同じ名前のローカル ユーザー アカウントとドメイン ユーザー アカウントを検出した場合、Configuration Manager は、ローカル ユーザー アカウントのアクセス権を設定します。  


### <a name="reporting-services-point-account"></a>レポート サービス ポイントのアカウント  
 
SQL Server Reporting Services は、**レポート サービス ポイント アカウント** を使用して、サイト データベースから Configuration Manager レポート用のデータを取得します。 指定した Windows ユーザー アカウントとパスワードは暗号化されて、SQL Server Reporting Services データベースに保存されます。  

> [!NOTE]  
> 指定するアカウントは、SQL Reporting Services データベースをホストするコンピューターに**ローカル ログオン**のアクセス許可がある必要があります。

> [!NOTE]  
> ConfigMgr データベースの smsschm_users SQL Database ロールに追加されることによって、このアカウントには必要なすべての権限が自動的に付与されます。

詳細については、「[レポートの概要](../../servers/manage/introduction-to-reporting.md)」をご覧ください。


### <a name="remote-tools-permitted-viewer-accounts"></a>リモート ツールの許可されたビューアー アカウント  

リモート コントロール用に **[アクセス許可のあるユーザー]** として指定するアカウントとは、クライアントでのリモート ツール機能の使用を許可されたユーザーの一覧です。  

詳細については、「[リモート コントロールの概要](../../clients/manage/remote-control/introduction-to-remote-control.md)」をご覧ください。


### <a name="site-installation-account"></a>サイト インストール アカウント
<!--SCCMDocs issue #572-->
Configuration Manager のセットアップを実行して新しいサイトをインストールするサーバーにサインインするには、ドメイン ユーザー アカウントを使用します。

このアカウントには次の権限が必要です。  

- 次のサーバーでの**管理者**:
    - サイト サーバー  
    - サイト データベースをホストする各サーバー  
    - サイトに対する SMS プロバイダーの各インスタンス  

- サイト データベースをホストする SQL Server インスタンスの **Sysadmin**  

Configuration Manager のセットアップでは、[SMS Admins](#sms-admins) グループにこのアカウントが自動的に追加されます。

インストール後は、このアカウントが Configuration Manager コンソールに対する権限を持つ唯一のユーザーになります。 このアカウントを削除する必要がある場合は、最初にその権限を別のユーザーに追加してください。

中央管理サイトを含むようにスタンドアロン サイトを拡張するときは、このアカウントに、スタンドアロン プライマリ サイトでの**完全な権限を持つ管理者**または**インフラストラクチャ管理者**のロールベースの管理権限が必要です。


### <a name="site-system-installation-account"></a>サイト システムのインストール アカウント  

サイト サーバーは、**サイト システムのインストール アカウント** を使用して、サイト システムのインストール、再インストール、アンインストール、およびセットアップを行います。 このサイト システムへの接続の開始をサイト サーバーに要求するようにサイト システムを設定すると、Configuration Manager は、サイト システムおよび役割をインストールした後で、このアカウントを使用してサイト システムからデータを取得します。 各サイト システムでは異なるインストール アカウントを使用できますが、そのサイト システムのすべての役割を管理するように設定できるインストール アカウントは 1 つだけです。  

このアカウントには、ターゲット サイト システムに対するローカルの管理アクセス許可が必要です。 また、このアカウントには、ターゲット サイト システム上のセキュリティ ポリシーで **[ネットワーク経由でコンピューターへアクセス]** が設定されている必要があります。  

> [!TIP]  
> ドメイン コントローラーが多数あり、これらのアカウントをドメイン間で使用する場合は、サイト システムをセットアップする前に、Active Directory でこれらのアカウントがレプリケートされていることを確認します。  
>   
> 管理対象の各サイト システムにローカル アカウントを指定すると、ドメイン アカウントを使用するより、この構成の方が安全です。 アカウントが侵害されても、攻撃者の行動が制限されます。 ただし、ドメイン アカウントのほうが管理は簡単です。 セキュリティと効果的な管理間のトレードオフを検討してください。  


### <a name="site-system-proxy-server-account"></a>サイト システム プロキシ サーバー アカウント
<!--SCCMDocs issue #648-->
以下のサイト システムの役割では、認証されたアクセスが必要なプロキシ サーバーまたはファイアウォール経由でインターネットにアクセスするために、**サイト システム プロキシ サーバー アカウント**が使用されます。

- 資産インテリジェンス同期ポイント
- Exchange Server コネクタ
- [サービス接続ポイント]
- ソフトウェアの更新ポイント

> [!IMPORTANT]  
> 必要なプロキシ サーバーまたはファイアウォールに対するアクセス許可ができるだけ制限されたアカウントを指定します。  

詳細については、「[プロキシ サーバーのサポート](../network/proxy-server-support.md)」を参照してください。


### <a name="smtp-server-connection-account"></a>SMTP サーバー接続アカウント  

サイト サーバーでは、SMTP サーバーで認証されたアクセスが必要なときにメール アラートを送信するために、**SMTP サーバー接続アカウント**が使用されます。  

> [!IMPORTANT]  
> 電子メールを送信するための最低限のアクセス許可を持つアカウントを指定します。  

詳細については、「[アラートとステータス システムの使用](../../servers/manage/use-alerts-and-the-status-system.md)」を参照してください。


### <a name="software-update-point-connection-account"></a>ソフトウェアの更新ポイントの接続アカウント  

サイト サーバーでは、次の 2 つのソフトウェア更新サービスに対して、**ソフトウェアの更新ポイントの接続アカウント**が使用されます。  

- Windows Server Update Services (WSUS)。製品の定義、分類、上流設定などの設定を行います。  

- WSUS 同期マネージャー。上流の WSUS サーバーまたは Microsoft Update への同期を要求します。  

[サイト システムのインストール アカウント](#site-system-installation-account)はソフトウェアの更新のコンポーネントをインストールできますが、ソフトウェアの更新ポイントでソフトウェアの更新固有の機能を実行することはできません。 信頼されていないフォレストにソフトウェアの更新ポイントがあるため、この機能にサイト サーバーのコンピューター アカウントを使用できない場合、サイト システムのインストール アカウントに加えて、このアカウントを指定する必要があります。  

このアカウントは、WSUS をインストールするコンピューター上のローカル管理者である必要があります。 さらに、ローカルの **WSUS Administrators** グループに属している必要があります。  

詳細については、[ソフトウェア更新プログラムの計画](../../../sum/plan-design/plan-for-software-updates.md)に関するページを参照してください。


### <a name="source-site-account"></a>ソース サイトのアカウント  

移行プロセスでは、ソース サイトの SMS プロバイダーにアクセスするために、**ソース サイトのアカウント**が使用されます。 移行ジョブのデータを収集するため、このアカウントにはソース サイトのサイト オブジェクトに対する **[読み取り]** アクセス許可が必要です。  

Configuration Manager 2007 の配布ポイントまたは配布ポイントが併置されたセカンダリ サイトがある場合、それらを Configuration Manager (Current Branch) の配布ポイントにアップグレードするときは、このアカウントに **Site** クラスに対する**削除**アクセス許可も必要です。 このアクセス許可は、アップグレードの間に Configuration Manager 2007 サイトから配布ポイントを正常に削除するためのものです。  

> [!NOTE]  
> Configuration Manager コンソールの **[管理]** ワークスペースの **[アカウント]** ノードでは、ソース サイトのアカウントと[ソース サイトのデータベース アカウント](#source-site-database-account)の両方が **[移行マネージャー]** として識別されます。  

詳細については、[階層間でのデータの移行](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies)に関するページを参照してください。


### <a name="source-site-database-account"></a>ソース サイトのデータベース アカウント  

移行プロセスは、**ソース サイトのデータベース アカウント**を使用して、ソース サイトの SQL Server データベースにアクセスします。 ソース サイトの SQL Server データベースからデータを収集するには、ソース サイトのデータベース アカウントに、ソース サイトの SQL Server データベースに対する**読み取り**および **実行**のアクセス許可が必要です。  

Configuration Manager (Current Branch) のコンピューター アカウントを使用する場合、このアカウントに次のすべてが該当することを確認します。  
  
- Configuration Manager 2007 サイトと同じドメイン内の **Distributed COM Users** セキュリティ グループのメンバーである  
- **SMS Admins** セキュリティ グループのメンバーである  
- あらゆる Configuration Manager 2007 オブジェクトの**読み取り**アクセス許可がある  

> [!NOTE]  
> Configuration Manager コンソールの **[管理]** ワークスペースの **[アカウント]** ノードでは、ソース サイトのアカウントと[ソース サイトのデータベース アカウント](#source-site-database-account)の両方が **[移行マネージャー]** として識別されます。  

詳細については、[階層間でのデータの移行](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies)に関するページを参照してください。


### <a name="task-sequence-domain-join-account"></a>タスク シーケンス ドメイン参加アカウント 

Windows セットアップでは、新しくイメージングされたコンピューターをドメインに参加させるために、**タスク シーケンス ドメイン参加アカウント**が使用されます。 このアカウントは、**ドメインに参加**オプションが設定された[ドメインまたはワークグループへの参加](../../../osd/understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)タスク シーケンス ステップで必要です。 このアカウントは[ネットワーク設定の適用](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings)で設定することもできますが、必須ではありません。  

このアカウントには、ターゲット ドメインにおける**ドメイン参加**権限が必要です。  

> [!TIP]  
> ドメインに参加するための最小限のアクセス許可を持つドメイン ユーザー アカウントを 1 つ作成し、すべてのタスク シーケンスにそれを使用します。  

> [!IMPORTANT]  
> このアカウントに対話型サインインのアクセス許可を割り当てないでください。  
>   
> このアカウントにはネットワーク アクセス アカウントを使用しないでください。  


### <a name="task-sequence-network-folder-connection-account"></a>タスク シーケンス ネットワーク フォルダー接続アカウント  

タスク シーケンス エンジンでは、ネットワーク上の共有フォルダーに接続するために、**タスク シーケンス ネットワーク フォルダー接続アカウント**が使用されます。 このアカウントは、[ネットワーク フォルダーへの接続](../../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)タスク シーケンス ステップで必要です。  

このアカウントは、指定された共有フォルダへアクセスするためのアクセス許可が必要です。 ドメイン ユーザー アカウントである必要があります。  

> [!TIP]  
> 必要なネットワーク リソースにアクセスするために最小限必要なアクセス許可を持つドメイン ユーザー アカウントを 1 つ作成し、それをすべてのタスク シーケンスに使用します。  

> [!IMPORTANT]  
> このアカウントに対話型サインインのアクセス許可を割り当てないでください。  
>   
> このアカウントにはネットワーク アクセス アカウントを使用しないでください。  


### <a name="task-sequence-run-as-account"></a>タスク シーケンス実行アカウント  

タスク シーケンス エンジンでは、ローカル システム アカウント以外の資格情報を使ってコマンド ラインまたは PowerShell スクリプトを実行するために、**タスク シーケンス実行アカウント**が使われます。 このアカウントは、 **[次のアカウントでこのステップを実行する]** オプションが選択された[コマンド ラインの実行](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine)および [PowerShell スクリプトの実行](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript)タスク シーケンス ステップで必要です。  

このアカウントは、タスク シーケンスに指定されているコマンド ラインを実行するために必要な最低限のアクセス許可を持つように設定します。 このアカウントには、対話型サインイン権限が必要です。 通常は、ソフトウェアのインストールとネットワーク リソースへのアクセスができる必要があります。 PowerShell スクリプトの実行タスクは、このアカウントにローカル管理者のアクセス許可が必要です。 

> [!IMPORTANT]  
> このアカウントにはネットワーク アクセス アカウントを使用しないでください。  
>   
> このアカウントをドメイン管理者にしないでください。  
>   
> このアカウントにローミング プロファイルを設定しないでください。 タスク シーケンスを実行すると、アカウントのローミング プロファイルがダウンロードされます。 これは、プロファイルをローカル コンピューター上でのアクセスに対して脆弱な状態のままにします。  
>   
> アカウントのスコープを制限する たとえば、タスク シーケンスごとに異なるタスク シーケンス実行アカウントを作成します。 1 つのアカウントが侵害された場合、侵害されるのはそのアカウントがアクセスできるクライアント コンピューターだけです。  
>   
> コマンド ラインにコンピューターの管理アクセスが必要な場合は、該当するタスク シーケンスを実行するすべてのコンピューターに、このアカウント専用のローカル管理者アカウントを作成することを検討してください。 そのアカウントは、不要になったら削除します。  


## <a name="user-objects-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlusers"></a>SQL で Configuration Manager によって使用されるユーザー オブジェクト 
<!--SCCMDocs issue #1160-->
Configuration Manager によって、SQL の次のユーザー オブジェクトが自動的に作成され、維持されます。  これらのオブジェクトは Configuration Manager データベース内の [セキュリティ/ユーザー] にあります。  

> [!IMPORTANT]  
>  これらのオブジェクトを変更したり、削除したりすると、Configuration Manager 環境内で大きな問題が引き起こされる可能性があります。  これらのオブジェクトは変更しないことをお勧めします。


### <a name="smsdbuser_readonly"></a>smsdbuser_ReadOnly

このオブジェクトは、クエリを読み取りで実行する際に使用されます。  このオブジェクトは一部のストアド プロシージャで利用されます。


### <a name="smsdbuser_readwrite"></a>smsdbuser_ReadWrite

このオブジェクトは、動的 SQL ステートメントのアクセス許可を提供する目的で使用されます。


### <a name="smsdbuser_reportschema"></a>smsdbuser_ReportSchema

このオブジェクトは、SQL レポートを実行する目的で使用されます。  次のストアド プロシージャは spSRExecQuery という関数と共に使用されます。


## <a name="database-roles-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlroles"></a>SQL で Configuration Manager によって使用されるデータベース ロール
<!--SCCMDocs issue #1160-->
Configuration Manager によって、SQL の次のロール オブジェクトが自動的に作成され、維持されます。 これらのロールからは、データを取得するか、ConfigMgr データベースにデータを挿入したり、このデータベースからデータを挿入したりするため、各ロールで必要となるアクションを実行する目的で、特定のストアド プロシージャ、テーブル、ビュー、関数へのアクセスが与えられます。 これらのオブジェクトは Configuration Manager データベース内の [セキュリティ/ロール/データベース ロール] にあります。

> [!IMPORTANT]  
> これらのオブジェクトを変更したり、削除したりすると、Configuration Manager 環境内で大きな問題が引き起こされる可能性があります。  これらのオブジェクトは変更しないことをお勧めします。

### <a name="smsdbrole_aitool"></a>smsdbrole_AITool

資産インテリジェンス ボリューム ライセンスのインポート。 ConfigMgr からは、資産インテリジェンスで使用されるボリューム ライセンスをインポートできるように、RBA に基づいてユーザー アカウントにこのアクセス許可が与えられます。  このアカウントは、完全な管理者ロールまたは Asset Manager ロールによって追加されることもあります。

### <a name="smsdbrole_aius"></a>smsdbrole_AIUS

資産インテリジェンス更新同期 ConfigMgr からは、資産インテリジェンス同期ポイント アカウントをホストするコンピューター アカウントに、資産インテリジェンス プロキシ データを取得したり、アップロードが保留になっている AI データを表示したりするためのアクセスが与えられます。

### <a name="smsdbrole_amtsp"></a>smsdbrole_AMTSP

帯域外管理。 このロールは、Intel AMT をサポートするデバイス上でデータを取得する目的で、Configuration Manager AMT ロールによって使用されます。

> [!NOTE]  
> このロールは、ConfigMgr の新しいリリースで非推奨となります。

### <a name="smsdbrole_crp"></a>smsdbrole_CRP

証明書登録ポイント System Center Endpoint Protection (SCEP) サポート。 ConfigMgr からは、証明書の署名と更新のために、SCEP サポートの証明書登録ポイントをサポートするサイト システムのコンピューター アカウントにアクセス許可が与えられます。

### <a name="smsdbrole_crppfx"></a>smsdbrole_CRPPfx

証明書登録ポイント PFX サポート。 ConfigMgr からは、署名と更新のために PFX サポートに構成されている証明書登録ポイントをサポートするサイト システムのコンピューター アカウントにアクセス許可が与えられます。

### <a name="smsdbrole_dmp"></a>smsdbrole_DMP

デバイス管理ポイント。 ConfigMgr からは、MDM 登録デバイスのサポートを提供する [Allow mobile devices and Mac Computer to uses this management point]\(モバイル デバイスと Mac コンピューターにこの管理ポイントを使用することを許可する\) オプションがある管理ポイントのコンピューター アカウントにこのアクセス許可が与えられます。

### <a name="smsdbrole_dmpconnector"></a>smsdbrole_DmpConnector

サービス接続ポイント。 ConfigMgr からは、利用統計情報を取得し、提供し、クラウド サービスを管理し、サービス更新プログラムを取得する目的でサービス接続ポイントをホストするコンピューター アカウントにこのアクセス許可が与えられます。

### <a name="smsdbrole_dviewaccess"></a>smsdbrole_DViewAccess

分散ビュー。 Configuration Manager からは、SQL Server 分散ビュー オプションがレプリケーション リンク プロパティで選択されているとき、CAS のプライマリ サイト サービスのコンピューター アカウントにこのアクセス許可が与えられます。

### <a name="smsdbrole_dwss"></a>smsdbrole_DWSS

データ ウェアハウス。 ConfigMgr からは、データ ウェアハウス ロールをホストするコンピューター アカウントにこのアクセス許可が与えられます。

### <a name="smsdbrole_enrollsvr"></a>smsdbrole_EnrollSvr

 登録ポイント。 ConfigMgr からは、MDM 経由のデバイス登録を可能にする目的で、登録ポイントをホストするコンピューター アカウントにこのアクセス許可が与えられます。

### <a name="smsdbrole_extract"></a>smsdbrole_extract

すべての拡張スキーマ ビューへのアクセスが与えられます。

### <a name="smsdbrole_hmsuser"></a>smsdbrole_HMSUser

階層マネージャー サービス。 ConfigMgr からは、フェールオーバー状態メッセージと階層内サイト間の SQL Server Broker トランザクションを管理する目的で、このアカウントにアクセス許可が与えられます。

> [!NOTE]  
> smdbrole_WebPortal ロールは既定でこのロールのメンバーになります。

### <a name="smsdbrole_mcs"></a>smsdbrole_MCS

マルチキャスト サービス。 ConfigMgr からは、マルチキャストをサポートする配布ポイントのコンピューター アカウントにこのアクセス許可が与えられます。

### <a name="smsdbrole_mp"></a>smsdbrole_MP

管理ポイント。 ConfigMgr からは、ConfigMgr クライアントのサポートを与える目的で、管理ポイント ロールをホストするコンピューター アカウントにこのアクセス許可が与えられます。

### <a name="smsdbrole_mpmbam"></a>smsdbrole_MPMBAM

管理ポイント Microsoft BitLocker Administration and Monitoring。 ConfigMgr からは、登録のために MBAM を管理する管理ポイントをホストするコンピューター アカウントにこのアクセス許可が与えられます。

### <a name="smsdbrole_mpusersvc"></a>smsdbrole_MPUserSvc

管理ポイント アプリケーション要求。 ConfigMgr からは、ユーザーベース アプリケーション要求をサポートする目的で管理ポイントをホストするコンピューター アカウントにこのアクセス許可が与えられます。

### <a name="smsdbrole_siteprovider"></a>smsdbrole_siteprovider

SMS プロバイダー。 Configuration Manager からは、SMS プロバイダー ロールをホストするコンピューター アカウントにこのアクセス許可が与えられます。  

### <a name="smsdbrole_siteserver"></a>smsdbrole_siteserver

サイト サーバー。 ConfigMgr からは、プライマリまたは CAS サイトをホストするコンピューター アカウントにこのアクセス許可が与えられます。

### <a name="smsdbrole_sup"></a>smsdbrole_SUP

ソフトウェアの更新ポイント。 ConfigMgr からは、サードパーティ更新プログラムを使用するためにソフトウェア更新ポイントをホストするコンピューター アカウントにこのアクセス許可が与えられます。

### <a name="smsdbrole_webportal"></a>smsdbrole_WebPortal

アプリケーション カタログ Web サイト ポイント。 ConfigMgr からは、ユーザーベースでアプリケーションを展開する目的で、アプリケーション カタログ Web サイト ポイントをホストするコンピューター アカウントにアクセス許可が与えられます。

### <a name="smsschm_users"></a>smsschm_users

ユーザー レポート アクセス。 ConfigMgr からは、Configuration Manager レポート データを表示するために SMS レポート ビューへのアクセスを許可する目的で、レポート サービス ポイント アカウントに使用されるアカウントにアクセスが与えられます。  データは RBA の使用によりさらに制限されます。
