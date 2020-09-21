---
title: Intune でのデータ収集
titleSuffix: Microsoft Intune
description: Intune で個人データがどのように収集されるかを学習します。
keywords: プライバシー, 個人データ
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d1171740-936d-46a5-af37-f418bd6fa63e
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bcd7ff1ae51314bc57be2bed39c7fe8ca7114d82
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076109"
---
# <a name="data-collection-in-intune"></a>Intune でのデータ収集

Intune を使用して会社または個人のデバイスを登録すると、ビジネス操作のサポート、顧客との取引、およびサービスのサポートのため、Intune により一部の個人データが収集、処理、および共有されます。 Intune では、次のソースから個人データが収集されます。

- Microsoft Endpoint Manager admin center での管理者による Intune の使用。
- エンド ユーザーのデバイス (デバイスの Intune 管理用の登録時と使用中)。
- (管理者の指示による) サード パーティ サービスでの顧客アカウント。
- 診断、パフォーマンス、使用状況の情報。

Intune では、これらのソースから、[必須](#required-data)、[オプション](#optional-data)の 2 つのカテゴリに分類される情報が収集されます。 各カテゴリのデータは、顧客データ、個人データ、診断データ、およびサービス生成されたデータにさらに分類されます。 

> [!NOTE]
> Microsoft では、いかなる理由でも、Microsoft のサービスによって収集されたデータを第三者に販売することはありません。

## <a name="required-data"></a>必要なデータ

必須カテゴリのデータは、お客様がサービスを想定どおりに動作させるために必要なデータで構成されます。 Intune によって収集されるデータのほとんどは、必須データです。 このデータは、ユーザー、デバイス、またはアプリケーションに関連付けられていて、管理の性質上、必要不可欠です。 収集されるデータには、個人データと個人情報以外のデータの両方が含まれます。 個人データには、特定可能なデータ (エンド ユーザーが直接識別される場合がある)、システムによって生成された一意の識別子を使用した匿名化済みデータ (エンタープライズ サービスをユーザーに提供するために使用される)、サポート データ、およびアカウント データが含まれます。 個人情報以外のデータには、サービス生成されたシステム メタデータや組織/テナント情報が含まれます。 また、Intune ではアクセス制御データを収集して、[ロールベースのアクセス制御](../fundamentals/role-based-access-control.md)のような機能を通じて、管理者ロールや機能へのアクセスが管理されます。

Intune によって収集される必須データには、次のようなものが含まれます。 

- ユーザー情報
  - 所有者名またはユーザーの表示名 (AzureUserID で識別される Azure に登録されているユーザーの名前)
  - ユーザー プリンシパル名または電子メール アドレス
  - 電話番号
  - サード パーティのユーザー識別子 (AppleID など)
- ハードウェア インベントリ情報
  - デバイス名
  - 製造元
  - オペレーティング システム
  - シリアル番号
  - IMEI 番号
  - IP アドレス
  - Wi-Fi MacAddress
  - ICCID
- 次のアクティビティに関するデータを含む、監査ログ情報
  - 管理
  - 作成
  - 更新 (編集)
  - 削除
  - 割り当て
  - リモート タスク
- サポート情報
  - 連絡先情報 (名前、電話番号、電子メール アドレス)
  - Microsoft のサポート、製品、またはカスタマー エクスペリエンスのチーム メンバーとの電子メールによるディスカッション
- アクセス制御情報 
  - 静的認証子 (顧客のパスワード)
  - 証明書のプライバシー キー 
- 管理者とアカウント情報
  - 管理者ユーザーの姓と名
  - 管理者ユーザー名
  - UPN (電子メール)
  - 電話番号
  - アカウント所有者の電子メール アドレス
  - 顧客の各 IT 管理者の Active Directory ID
  - 顧客への課金に対する支払いデータ
  - サブスクリプション キー
- 次のようなアプリケーション インベントリ
  - アプリ名
  - のバージョン
  - アプリ ID
  - サイズ
  - インストール場所
  - アプリケーション インベントリ データは、管理者が企業所有のデバイスとしてマークした場合、または準拠しているアプリの機能がオンになっている場合にのみ収集されます。  
- 顧客のサード パーティ テナント ID (Apple ID など)
- デバイス データ
  - Intune デバイス ID
  - Azure Active Directory デバイス ID
  - Intune デバイス管理 ID
  - テナント ID
  - アカウント ID
  - EAS デバイス ID
  - プラットフォーム固有の ID
  - iOS/iPadOS デバイスの AppleID
  - Mac デバイスの MAC アドレス
  - Windows デバイスの Windows ID
- マネージド アプリケーション情報
  - マネージド アプリケーション ID
  - マネージド アプリケーション デバイス タグ
  - Intune デバイス管理 ID
  - Azure Active Directory デバイス ID
  - 暗号化キー
- すべての Intune テナントからの管理者の使用状況データ (たとえば、管理コンソールとのやり取りで選択された管理コントロール)
- テナント アカウント情報 (このデータは、Intune ブレードから入手できます)
  - 登録したデバイスまたはユーザーの数
  - 識別されたデバイス プラットフォームの数  
  - インストールされているデバイスの数
  - installedDeviceCount: アプリケーションがインストールされているデバイスの数。
  - notApplicableDeviceCount: アプリケーションが適用できないデバイスの数。
  - notInstalledDeviceCount: アプリケーションは適用できるがインストールされていないデバイスの数。
  - pendingInstallDeviceCount: アプリケーションは適用できるがインストールが保留中のデバイスの数。

## <a name="optional-data"></a>オプション データ

オプション カテゴリのデータは、製品またはサービス エクスペリエンスにとって重要ではありません。 お客様は、オプション データのコレクションを制御できます。 Intune では、お客様は、オプション データ コレクションをオプトインまたはオプトアウトできます。 オプション データの例として、診断およびテレメトリ用に Intune によって収集されるデータがあります。 このオプション データの共有には、新しいエクスペリエンスやより充実したエクスペリエンスの機会を生み出すという理由がある一方で、これらを自身で選択するための機会をユーザーに提供することも重要であると Microsoft は理解していることに注意してください。 

オプションの診断データの例として、アプリケーションの使用状況データ、エラー、パフォーマンス データがあります。 Microsoft 365 Apps for enterprise アプリケーションおよびサービスの使用時に Microsoft によって収集されるすべての診断データは、ISO/IEC 19944:2017 (8.3.3 節) 標準で定義されているように匿名化されます。

## <a name="certain-end-user-data-or-content-is-never-collected"></a>収集されない特定のエンド ユーザー データまたはコンテンツ

Intune では、エンド ユーザーの通話、Web 閲覧の履歴、個人の電子メール、テキスト メッセージ、連絡先、個人アカウントのパスワード、予定表のイベント、または写真 (写真アプリやカメラ内のものを含む) は収集されず、管理者がこれらを表示することもできません。 [デバイス登録の概要](../enrollment/device-enrollment.md)に関する記事をご覧ください。

データの種類と定義について詳しくは、「[Microsoft によるオンライン サービスのデータの分類方法](https://www.microsoft.com/trust-center/privacy/customer-data-definitions)」を参照してください。 

## <a name="next-steps"></a>次のステップ

Intune が個人データを[格納と処理](privacy-data-store-process.md)および[共有](privacy-data-secure-share.md)する方法について確認します。 
