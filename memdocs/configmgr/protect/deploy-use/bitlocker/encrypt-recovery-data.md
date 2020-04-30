---
title: 回復データの暗号化
titleSuffix: Configuration Manager
description: ネットワーク全体と Configuration Manager データベース内で、BitLocker 回復キー、回復パッケージ、および TPM パスワード ハッシュを暗号化します。
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 1ee6541a-e243-43ea-be16-d0349f7f0c6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79f50cf4b0d241df2fc8d12dc46c833af278bd5a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709350"
---
# <a name="encrypt-recovery-data"></a>回復データの暗号化

*適用対象:Configuration Manager (Current Branch)*

<!--3601034-->

BitLocker 管理ポリシーを作成すると、Configuration Manager によって管理ポイントに回復サービスが展開されます。 BitLocker 管理ポリシーの **[クライアント管理]** ページで、 **[BitLocker 管理サービスの構成]** を選択して構成すると、クライアントはキー回復情報をサイト データベースにバックアップします。 この情報には、BitLocker 回復キー、回復パッケージ、TPM パスワード ハッシュが含まれます。 保護されたデバイスからユーザーがロックアウトされた場合、この情報を使用して、デバイスへのアクセスを回復することができます。

この情報の機密性を考えると、次のような状況では情報を保護する必要があります。

- ネットワーク経由で転送中のデータを暗号化するために、Configuration Manager でクライアントと回復サービスの間に HTTPS 接続が必要になります。 次の 2 つのオプションがあります。

  - 管理ポイントの役割全体ではなく、回復サービスをホストする管理ポイント上の IIS Web サイトを HTTPS 対応にします。 このオプションは、Configuration Manager バージョン 2002 にのみ適用されます。<!-- 5925660 -->

  - HTTPS 用の管理ポイントを構成します。 管理ポイントのプロパティで、 **[クライアント接続]** 設定を **[HTTPS]** にする必要があります。 このオプションは、Configuration Manager バージョン 1910 または 2002 に適用されます。

    > [!NOTE]
    > 現在、拡張 HTTP はサポートされていません。

- このデータがサイト データベースに格納されている場合は、このデータも暗号化することを検討します。 独自の証明書を使用して SQL Server のセルレベルの暗号化を使用できます。

    BitLocker 管理暗号化証明書を作成しない場合は、回復データをプレーンテキストで保存することを選択します。 BitLocker 管理ポリシーを作成する際、 **[回復情報をプレーンテキストで保存することを許可する]** オプションを有効にします。

    > [!NOTE]
    > もう 1 つのセキュリティ層は、サイト データベース全体の暗号化です。 データベースで暗号化を有効にした場合、Configuration Manager で機能上の問題は発生しません。
    >
    > 特に大規模な環境では慎重に暗号化してください。 暗号化するテーブルと SQL のバージョンによっては、パフォーマンスが最大で 25% 低下する場合があります。 暗号化されたデータを正常に回復できるように、バックアップと復旧の計画を更新してください。

## <a name="certificate-requirements"></a>証明書の要件

### <a name="https-server-authentication-certificate"></a>HTTPS サーバー認証証明書

<!--5925660-->

Configuration Manager Current Branch バージョン 1910 で、BitLocker 回復サービスを統合するには、管理ポイントの HTTPS を有効にする必要がありました。 HTTPS 接続は、ネットワーク経由で Configuration Manager クライアントから管理ポイントへの回復キーを暗号化するために必要です。 多くのお客様にとって、HTTPS 用に管理ポイントとすべてのクライアントを構成することは困難です。

バージョン 2002 以降、HTTPS の要件は、管理ポイントの役割全体ではなく、回復サービスをホストする IIS Web サイトに対するものになります。 この変更により、証明書の要件が緩和され、転送中の回復キーは引き続き暗号化されます。

これで、管理ポイントの**クライアント接続**プロパティは、**HTTP** または **HTTPS** にすることができます。 管理ポイントが **HTTP** 用に構成されている場合、BitLocker 回復サービスをサポートするには、次のようにします。

1. サーバー認証証明書を取得します。 BitLocker 回復サービスをホストする管理ポイントで IIS Web サイトに証明書をバインドします。

2. サーバー認証証明書を信頼するように、クライアントを構成します。 この信頼は、次の 2 つの方法で実現できます。

    - グローバルで信頼されているパブリック証明書プロバイダーの証明書を利用します。 たとえば、DigiCert、Thawte、VeriSign です。この 3 つに限らず他にも存在します。 Windows クライアントには、このようなプロバイダーからの信頼されたルート CA (証明書機関) が含まれています。 このようなプロバイダーのいずれかが発行したサーバー認証証明書を利用することで、クライアントは自動的にそれを信頼する必要があります。

    - 組織の公開キー基盤 (PKI) からの CA によって発行された証明書を利用します。 ほとんどの PKI 実装によって、Windows クライアントに信頼されたルート CA が追加されます。 たとえば、Active Directory 証明書サービスとグループ ポリシーを使用します。 クライアントによって自動的に信頼されない CA からサーバー認証証明書を発行する場合は、CA の信頼されたルート証明書をクライアントに追加します。

> [!TIP]
> 回復サービスと通信する必要があるクライアントは、BitLocker 管理ポリシーの対象とすることを計画するクライアントのみであり、**クライアント管理規則**を含みます。

クライアントで **BitLockerManagementHandler.log** を使用して、この接続のトラブルシューティングを行います。 回復サービスに接続するために、ログにはクライアントが使用している URL が表示されます。 `Checking for Recovery Service at` で始まるエントリを検索します。

> [!NOTE]
> サイトに複数の管理ポイントがある場合は、BitLocker で管理されているクライアントが通信する可能性のある、サイトのすべての管理ポイントで HTTPS を有効にします。 HTTPS 管理ポイントが使用できない場合、クライアントは HTTP 管理ポイントにフェールオーバーしてから、その回復キーのエスクローに失敗する可能性があります。
>
> この推奨事項は、管理ポイントで HTTPS を有効にするオプションと、管理ポイントで回復サービスをホストする IIS Web サイトを有効にするオプションの両方に適用されます。

### <a name="sql-encryption-certificate"></a>SQL 暗号化証明書

この証明書を使用すると、BitLocker 回復データの SQL Server セルレベルの暗号化を有効にできます。 次の要件を満たしている限り、独自のプロセスを使用して BitLocker 管理暗号化証明書を作成し、展開することができます。

- BitLocker 管理暗号化証明書の名前は `BitLockerManagement_CERT`である必要があります。

- この証明書をデータベース マスター キーで暗号化します。

- 次の SQL ユーザーには、証明書に対する**コントロール**のアクセス許可が必要です。
  - RecoveryAndHardwareCore
  - RecoveryAndHardwareRead
  - RecoveryAndHardwareWrite

- 階層内のすべてのサイト データベースに同じ証明書を展開します。

- 環境内の最新バージョンの SQL Server で証明書を作成します。 次に例を示します。
  - SQL Server 2016 以降で作成された証明書は、SQL Server 2014 以前と互換性があります。
  - SQL Server 2014 以前で作成された証明書は、SQL Server 2016 以降と互換性がありません。

## <a name="example-scripts"></a>サンプル スクリプト

これらの SQL スクリプトは、Configuration Manager サイト データベースで BitLocker 管理暗号化証明書を作成して展開する例です。

### <a name="create-certificate"></a>証明書の作成

このサンプル スクリプトでは、次のアクションを実行します。

- 証明書を作成します。
- アクセス許可を設定します。
- データベース マスター キーを作成します。

運用環境でこのスクリプトを使用する前に、次の値を変更します。

- サイト データベース名 (`CM_ABC`)
- マスター キーを作成するためのパスワード (`MyMasterKeyPassword`)
- 証明書の有効期限日 (`20391022`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN
    CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
    WITH SUBJECT = 'BitLocker Management',
    EXPIRY_DATE = '20391022'

    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="back-up-certificate"></a>証明書のバックアップ

このサンプル スクリプトでは、証明書をバックアップします。 証明書をファイルに保存すると、その証明書を階層内の他のサイト データベースに[復元](#restore-certificate)できます。

運用環境でこのスクリプトを使用する前に、次の値を変更します。

- サイト データベース名 (`CM_ABC`)
- ファイルのパスと名前 (`C:\BitLockerManagement_CERT_KEY`)
- キー パスワードのエクスポート (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
BACKUP CERTIFICATE BitLockerManagement_CERT TO FILE = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        ENCRYPTION BY PASSWORD = 'MyExportKeyPassword')
```

> [!IMPORTANT]
> エクスポートした証明書ファイルと関連するパスワードを安全な場所に保存します。

### <a name="restore-certificate"></a>証明書の復元

このサンプル スクリプトでは、ファイルから証明書を復元します。 このプロセスを使用して、別のサイト データベースに作成した証明書を展開します。

運用環境でこのスクリプトを使用する前に、次の値を変更します。

- サイト データベース名 (`CM_ABC`)
- マスター キーのパスワード (`MyMasterKeyPassword`)
- ファイルのパスと名前 (`C:\BitLockerManagement_CERT_KEY`)
- キー パスワードのエクスポート (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN

CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
FROM FILE  = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        DECRYPTION BY PASSWORD = 'MyExportKeyPassword')

GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="verify-certificate"></a>証明書を確認する

この SQL スクリプトを使用して、必要なアクセス許可を持つ証明書が SQL によって正常に作成されたことを確認します。

``` SQL
USE CM_ABC
declare @count int
select @count = count(distinct u.name) from sys.database_principals u
join sys.database_permissions p on p.grantee_principal_id = u.principal_id or p.grantor_principal_id = u.principal_id
join sys.certificates c on c.certificate_id = p.major_id
where u.name in('RecoveryAndHardwareCore', 'RecoveryAndHardwareRead', 'RecoveryAndHardwareWrite') and
c.name = 'BitLockerManagement_CERT' and p.permission_name like 'CONTROL'
if(@count >= 3) select 1
else select 0
```

証明書が有効な場合、スクリプトは値 `1`を返します。

## <a name="see-also"></a>関連項目

これらの SQL コマンドの詳細については、次の記事を参照してください。

- [SQL Server とデータベースの暗号化キー](https://docs.microsoft.com/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine)
- [証明書の作成](https://docs.microsoft.com/sql/t-sql/statements/create-certificate-transact-sql)
- [証明書のバックアップ](https://docs.microsoft.com/sql/t-sql/statements/backup-certificate-transact-sql)
- [マスター キーの作成](https://docs.microsoft.com/sql/t-sql/statements/create-master-key-transact-sql)
- [バックアップ マスター キー](https://docs.microsoft.com/sql/t-sql/statements/backup-master-key-transact-sql)
- [証明書のアクセス許可の付与](https://docs.microsoft.com/sql/t-sql/statements/grant-certificate-permissions-transact-sql)
