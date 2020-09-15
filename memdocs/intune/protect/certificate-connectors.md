---
title: Microsoft Intune 用の C 証明書コネクタ - Azure | Microsoft Docs
description: Microsoft Intune での Simple Certificate Enrollment Protocol (SCEP) または Public Key Cryptography Standards (PKCS) 証明書と証明書プロファイル用の証明書コネクタについて説明します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9f891e7989ad3f0f8d798dd9a5f0207a19ac5b95
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2020
ms.locfileid: "89428900"
---
# <a name="certificate-connectors-for-microsoft-intune"></a>Microsoft Intune 用の証明書コネクタ

Intune では、認証での証明書の使用、および S/MIME を使用した電子メールの署名と暗号化をサポートするために、証明書コネクタの使用が必要となります。 証明書コネクタはオンプレミス サーバーにインストールするソフトウェアです。 コネクタを使用すると、クラウドで管理されたデバイスで、発行元の証明機関と同様に、オンプレミスのインフラストラクチャから証明書をプロビジョニングすることができます。

この記事では、使用可能なコネクタ、そのライフサイクル、使用に関する前提条件、およびそれらを最新の状態に保つ方法について説明します。  

## <a name="available-connectors"></a>使用可能なコネクタ

Intune 用の証明書コネクタは 2 つあります。 それぞれに独自の用途と要件があります。

### <a name="pfx-certificate-connector-for-microsoft-intune"></a>PFX Certificate Connector for Microsoft Intune

**PFX Certificate Connector** では、PCKS #12 証明書要求に対する証明書の展開がサポートされ、特定のユーザーに対して S/MIME 電子メール暗号化を行うために Intune にインポートされた PFX ファイルの要求が処理されます。

> [!TIP]
> このコネクタの 8 月の更新プログラムの前は、PKCS #12 証明書要求は *Intune Certificate Connector* によって処理されていました。 8 月の更新プログラムでは、すべての PKCS 証明書要求の機能が *PFX Certificate Connector* に統合されました。これにより、コネクタの新しいバージョンへの自動更新がサポートされます。また、.NET Framework バージョン 4.7.2 の使用が必要となります。
>
> Microsoft Intune コネクタの機能は非推奨とはなっておらず、引き続き PKCS 証明書プロファイルで使用できます。 ただし、SCEP を使用しない場合や、NDES を使用する必要がある場合は、PFX Certificate Connector に切り替えて、サーバーから NDES を削除することができます。 

**PFX Certificate Connector**:

- 各 Intune テナントに対してこのコネクタの複数のインスタンスがサポートされます。 コネクタの各インスタンスは Windows Server にインストールし、アップロードした PFX ファイルのパスワードの暗号化に使用された秘密キーへのアクセス権を付与する必要があります。
- "*Microsoft Intune コネクタ*" のインスタンスがホストされているのと同じサーバーにインストールできます。
- 新しいバージョンへの[自動更新](#automatic-update)がサポートされています。 新しいバージョンを自動的にインストールするには、コネクタがホストされているコンピューターからポート **443** で **autoupdate.msappproxy.net** にコンタクトする必要があります。 コネクタの自動更新に失敗した場合は、コネクタを手動で更新できます。
- 証明書の失効がサポートされます (コネクタがバージョン **6.2008.60.607** 以降で実行される必要があります)
- ネットワーク要件は、[マネージド デバイス](../fundamentals/intune-endpoints.md#access-for-managed-devices)と同じです

  詳細については、「[Microsoft Intune のネットワーク エンドポイント](../fundamentals/intune-endpoints.md)」および「[Intune のネットワーク構成の要件と帯域幅](../fundamentals/network-bandwidth-use.md)」をご覧ください。

**コネクタのインストール先の Windows Server**:

- Windows Server 2012 R2 以降が実行されている必要があります。
- .NET 4.7.2 Framework が実行されている必要があります。  

**PFX Certificate Connector をインストールするには**:

このコネクタのインストールに関するガイダンスについては、[PFX Certificate Connector のダウンロード、インストール、および構成](certficates-pfx-configure.md)に関する記事を参照してください。

### <a name="microsoft-intune-connector"></a>Microsoft Intune コネクタ

**Microsoft Intune コネクタ**は、*Microsoft Intune Certificate Connector* と呼ばれることもあります。 このコネクタでは、*Simple Certificate Enrollment Protocol* (SCEP) を使用し、Active Directory 証明書サービスの証明機関 (CA) がある場合に、証明書の展開がサポートされます。 この種類の CA は *Microsoft CA* とも呼ばれます。

Microsoft CA で SCEP を使用する場合は、**ネットワーク デバイス登録サービス** (NDES) も構成する必要があります。 このため、このコネクタは "*NDES 証明書コネクタ*" と呼ばれることがよくあります。

[サードパーティの証明機関](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration)を使用する場合は、このコネクタを使用する必要はありません。NDES も必要ありません。

**Microsoft Intune コネクタ**:

- Windows Server にインストールします。ここでは *PFX Certificate Connector* をホストすることもできます。
- テナントごとにこのコネクタの最大 100 個のインスタンスがサポートされており、各インスタンスは個別の Windows Server 上にあります。 複数のコネクタを使用する場合:
  - 環境内の "*Microsoft Intune コネクタ*" のすべてのインスタンスは、同じバージョンである必要があります。
  - ご使用のインフラストラクチャで冗長と負荷分散がサポートされます。使用可能などのコネクタ インスタンスでも証明書要求を処理できるためです。
- 新しいバージョンのコネクタをインストールするには、[手動更新](#manual-update)が必要です。 手動更新では、現在のコネクタをアンインストールしてから、新しいバージョンのコネクタをインストールする必要があります。 追加のアクションは必要ありません。
- *Federal Information Processing Standard* (FIPS) モードがサポートされています。 FIPS は必須ではありません。 FIPS が有効になっている場合は、証明書の発行および失効を行うことができます。
- ネットワーク要件は、[マネージド デバイス](../fundamentals/intune-endpoints.md#access-for-managed-devices)と同じです。

  詳細については、「[Microsoft Intune のネットワーク エンドポイント](../fundamentals/intune-endpoints.md)」および「[Intune のネットワーク構成の要件と帯域幅](../fundamentals/network-bandwidth-use.md)」をご覧ください。

**コネクタのインストール先の Windows Server**:

- Windows Server 2012 R2 以降が実行されている必要があります。
- .NET 4.5 Framework が実行されている必要があります。 このコネクタを *PFX Certificate Connector* と同じサーバーにインストールする場合は、PFX コネクタで必要とされる .NET 4.7.2 Framework を使用する必要があります。
- 発行元の証明機関 (CA) がホストされているのと同じサーバーとすることはできません。
- Microsoft CA で SCEP に使用する場合は、NDES を実行するサーバーへのアクセスが必要です。 NDES は Windows Server 上で実行されます。このコネクタと同じサーバーで実行できます。

**NDES が必要な場合**:

- Internet Explorer セキュリティ強化の構成は、[NDES がホストされているサーバー](/previous-versions/windows/it-pro/windows-server-2003/cc775800(v=ws.10))と "*Microsoft Intune コネクタ*" がホストされているサーバーで無効にする必要があります。
- コネクタには、NDES と通信するための追加の構成が必要です。 NDES をインストールして構成する手順については、"*Microsoft Intune コネクタ*" をインストールする手順を参照してください。

  NDES の詳細については、「[ネットワーク デバイス登録サービスのガイダンス](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11))」を参照してください。

**Microsoft Intune コネクタをインストールするには**:

このコネクタのインストールに関するガイダンスについては、「[Intune を使用して SCEP をサポートするようにインフラストラクチャを構成する](certificates-scep-configure.md)」を参照してください。

## <a name="connector-lifecycle"></a>コネクタのライフサイクル

証明書コネクタの更新されたバージョンが定期的にリリースされます。 新しいコネクタのリリースのアナウンスは、Intune 向けの記事 (新機能](../fundamentals/whats-new.md) と、この記事の最後近くにある「[コネクタの新機能](#whats-new-for-connectors)」に表示されます。

新しいバージョンがリリースされると、以前のバージョンのサポートは、継続使用の猶予期間が限定された状態で非推奨となります。 猶予期間が終了すると、その非推奨バージョンのサポートが終了し、いつでも機能が停止する可能性があります。 猶予期間は 6 か月です。

最初の機会に、コネクタを最新バージョンに更新することを計画してください。 各コネクタの更新パスは異なります。

- **PFX Certificate Connector for Microsoft Intune** - 自動更新がサポートされています。
- **Microsoft Intune コネクタ** - 手動更新が必要です。

### <a name="automatic-update"></a>自動更新

コネクタの種類と環境によってサポートされている場合、そのコネクタのバージョンがリリースされた後すぐに、Intune によってコネクタを最新のバージョンに自動的に更新することができます。  

自動的に更新するには、コネクタがホストされているサーバーが **Azure 更新サービス**にアクセスする必要があります。

- ポート: **443**
- エンドポイント: **autoupdate.msappproxy.net**

ファイアウォール、インフラストラクチャ、またはネットワーク構成で自動更新のアクセスが制限されている場合は、ブロックの問題を解決するか、またはコネクタを新しいバージョンに手動で更新してください。

### <a name="manual-update"></a>手動更新

証明書コネクタを手動で更新するプロセスは、コネクタを再インストールする場合と同じです。

自動更新がサポートされている場合でも、証明書コネクタを手動で更新できます。 たとえば、ネットワーク構成によって自動更新がブロックされている場合は、コネクタを手動で更新できます。  

### <a name="to-reinstall-a-certificate-connector"></a>証明書コネクタをインストールするには

1. コネクタがホストされている Windows Server で、**Windows のアプリと機能**を使用してコネクタをアンインストールします。

2. 新しいバージョンをインストールするには、新しいバージョンのコネクタをインストールする手順を使用します。 新しいバージョンのコネクタをインストールするときは、新しいまたは更新された前提条件を確認してください。
   - SCEP: [Intune を使用して SCEP をサポートするようにインフラストラクチャを構成する](certificates-scep-configure.md)
   - PKCS: [PFX Certificate Connector for Microsoft Intune のダウンロード、インストール、および構成](certficates-pfx-configure.md)

## <a name="connector-status-and-version"></a>コネクタの状態とバージョン

Microsoft エンドポイント マネージャー管理センターで、証明書コネクタを選択して、その状態に関する情報を表示し、そのバージョンを確認できます。

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) にサインインします。

2. **[テナント管理]**  >  **[コネクタとトークン]**  >  **[証明書のコネクタ]** の順に移動します。

3. 状態を表示するコネクタを選択します。

コネクタの状態を表示する場合:

- 非推奨のコネクタは、**警告**と共に表示されます。 6 か月の猶予期間が経過すると、警告はエラーに変わります。
- 猶予期間を超えたコネクタには、エラーが表示されます。 これらのコネクタはサポートされなくなったため、いつでも動作を停止することができます。

## <a name="whats-new-for-connectors"></a>コネクタの新機能

2 つの証明書コネクタの更新プログラムは、定期的にリリースされます。 コネクタが更新された場合、その変更についてここから確認することができます。

### <a name="pfx-certificate-connector-release-history"></a>PFX Certificate Connector のリリース履歴

*PFX Certificate Connector for Microsoft Intune* では、[自動更新がサポートされます](#automatic-update)。

#### <a name="august-26-2020"></a>2020 年 8 月 26 日

**バージョン 6.2008.60.607** - このリリースの変更点:

- .NET Framework バージョン 4.7.2 が必要とされます
- PKCS 証明書プロファイルでの使用について、*Microsoft Intune コネクタ*の使用が置き換えられます。 *PFX Certificate Connector* が、PCKS #12 またはインポートされた PFX 証明書を使用するために必要な唯一のコネクタとなります。
- Windows 8.1 を除く、サポートされているすべてのプラットフォームで PKCS 証明書プロファイルを使用するためのサポートが追加されます。
- Outlook S/MIME の証明書失効のサポートが追加されます。

#### <a name="november-18-2019"></a>2019 年 11 月 18 日

**バージョン: 6.1911.11.602** - このリリースの変更点:

- PFX インポートに対する S/MIME サポートが追加されました。  

#### <a name="may-17-2019"></a>2019 年 5 月 17 日

**バージョン 6.1905.0.404** - このリリースの変更点:

- コネクタで新しい要求の処理が停止される原因となる、既存の PFX 証明書の再処理が続行される問題を修正しました。 

#### <a name="may-6-2019"></a>2019 年 5 月 6 日

**バージョン 6.1905.0.402** - このリリースの変更点:

- コネクタのポーリング間隔が、5 分から 30 秒に短縮されました。

#### <a name="april-2-2019"></a>2019 年 4 月 2 日

**バージョン 6.1904.0.401** - このリリースの変更点:

- このコネクタで自動更新がサポートされるようになりました。
- グローバル管理者アカウントを使用してコネクタにサインインした後に、コネクタが Intune への登録に失敗することがある問題を修正しました。

### <a name="microsoft-intune-connector-release-history"></a>Microsoft Intune コネクタのリリース履歴

#### <a name="april-2-2019"></a>2019 年 4 月 2 日

**バージョン 6.1904.1.0** - このリリースの変更点:  

- グローバル管理者アカウントを使用してコネクタにサインインした後に、コネクタが Intune への登録に失敗することがある問題を修正しました。
- 証明書の失効への信頼性の修正が含まれています。
- PKCS 証明書の要求の処理速度を向上するパフォーマンスの修正が含まれています。

## <a name="next-steps"></a>次のステップ

使用する各プラットフォーム用に SCEP、PKCS、または PKCS のインポートされた証明書プロファイルを作成します。 続行するには、次の記事をご覧ください。

- [Intune を使用して SCEP 証明書をサポートするようにインフラストラクチャを構成する](certificates-scep-configure.md)  
- [Intune で PKCS 証明書を構成して管理する](certficates-pfx-configure.md)  
- [PKCS のインポートされた証明書プロファイルを作成する](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
