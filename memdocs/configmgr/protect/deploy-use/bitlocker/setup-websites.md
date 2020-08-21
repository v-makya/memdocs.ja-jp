---
title: BitLocker ポータルのセットアップ
titleSuffix: Configuration Manager
description: セルフサービス ポータルおよび管理と監視用 Web サイト用の BitLocker 管理コンポーネントをインストールします
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 1cd8ac9f-b7ba-4cf4-8cd2-d548b0d6b1df
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5dbd782c97d11f8077c18796c87c7880eb26f3f3
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129156"
---
# <a name="set-up-bitlocker-portals"></a>BitLocker ポータルのセットアップ

*適用対象:Configuration Manager (Current Branch)*

<!--3601034-->

Configuration Manager で次の BitLocker 管理コンポーネントを使用するには、最初に次をインストールする必要があります。

- ユーザー セルフサービス ポータル
- 管理と監視用 Web サイト (ヘルプデスク ポータル)

IIS がインストールされた既存のサイト サーバーまたはサイト システム サーバーにポータルをインストールしたり、スタンドアロンの Web サーバーを使用してそれらをホストしたりできます。

> [!NOTE]
> バージョン 2006 以降では、中央管理サイトに BitLocker セルフサービス ポータルと管理と監視用 Web サイトをインストールできます。<!-- 5925693 -->
>
> バージョン 2002 以前では、プライマリ サイト データベースを含むセルフサービス ポータルと管理と監視用 Web サイトのみをインストールしてください。 階層内で、各プライマリ サイトにこれらの Web サイトをインストールします。

開始する前に、これらのコンポーネント用の[前提条件](../../plan-design/bitlocker-management.md#prerequisites)を確認してください。

## <a name="run-the-script"></a>スクリプトを実行する

ターゲット Web サーバーで、次の操作を行います。

> [!NOTE]
> サイトの設計によっては、スクリプトを複数回実行することが必要になる場合があります。 たとえば、管理ポイントでスクリプトを実行して、管理と監視用 Web サイトをインストールします。 次に、スタンドアロンの Web サーバーでもう一度実行して、セルフサービス ポータルをインストールします。

1. サイト サーバー上の Configuration Manager のインストール フォルダーに含まれる `SMSSETUP\BIN\X64` から、次のファイルをターゲット サーバー上のローカル フォルダーにコピーします。

    - `MBAMWebSite.cab`
    - `MBAMWebSiteInstaller.ps1`

1. 管理者として PowerShell を実行した後、次のコマンド ラインのようなスクリプトを実行します。

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName <ServerName> -SqlInstanceName <InstanceName> -SqlDatabaseName <DatabaseName> -ReportWebServiceUrl <ReportWebServiceUrl> -HelpdeskUsersGroupName <DomainUserGroup> -HelpdeskAdminsGroupName <DomainUserGroup> -MbamReportUsersGroupName <DomainUserGroup> -SiteInstall Both
    ```

    例:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName sql.contoso.com -SqlInstanceName instance1 -SqlDatabaseName CM_ABC -ReportWebServiceUrl https://rsp.contoso.com/ReportServer -HelpdeskUsersGroupName "contoso\BitLocker help desk users" -HelpdeskAdminsGroupName "contoso\BitLocker help desk admins" -MbamReportUsersGroupName "contoso\BitLocker report users" -SiteInstall Both
    ```

    > [!IMPORTANT]
    > このコマンド ライン例では、使用方法を示すために使用可能なすべてのパラメーターが使用されています。 ご自分の環境の要件に従って、使用方法を調整してください。

インストール後、次の URL を使ってポータルにアクセスします。

- セルフサービス ポータル: `https://webserver.contoso.com/SelfService`
- administration and monitoring web サイト: `https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> Microsoft では HTTPS の使用をお勧めしますが、必須ではありません。 詳細については、[IIS 上で SSL を設定する方法](https://docs.microsoft.com/iis/manage/configuring-security/how-to-set-up-ssl-on-iis)に関するページをご覧ください。

## <a name="script-usage"></a>スクリプトの使用法

このプロセスでは、PowerShell スクリプト MBAMWebSiteInstaller.ps1 を使用して、Web サーバーにこれらのコンポーネントをインストールします。 次のパラメーターを指定できます。

- `-SqlServerName <ServerName>` (必須):プライマリ サイト データベース サーバーの完全修飾ドメイン名。

- `-SqlInstanceName <InstanceName>`: プライマリ サイト データベース用の SQL Server インスタンス名。 SQL で既定のインスタンスが使用される場合は、このパラメーターを含めないでください。

- `-SqlDatabaseName <DatabaseName>` (必須):プライマリ サイト データベースの名前 (`CM_ABC` など)。

- `-ReportWebServiceUrl <ReportWebServiceUrl>`: プライマリ サイトのレポート サービス ポイントの Web サービス URL。 これは、**Reporting Services Configuration Manager** の **[Web サービス URL]** の値です。

    > [!NOTE]
    > このパラメーターにより、管理と監視用 Web サイトからリンクされている**回復の監査レポート**がインストールされます。 既定では、Configuration Manager には他の BitLocker 管理レポートも含まれます。

- `-HelpdeskUsersGroupName <DomainUserGroup>`: たとえば、`contoso\BitLocker help desk users` となります。 ドメイン ユーザー グループの 1 つ。このグループのメンバーは、administration and monitoring web サイトの **[TPM の管理]** および **[ドライブの回復]** の領域にアクセスできます。 これらのオプションを使用する場合、この役割では、ユーザーのドメイン名とアカウント名など、すべてのフィールドに入力する必要があります。

- `-HelpdeskAdminsGroupName <DomainUserGroup>`: たとえば、`contoso\BitLocker help desk admins` となります。 管理と監視の Web サイトの、すべての回復領域にアクセスできるメンバーを含めるドメイン ユーザー グループです。 ユーザーによる各自のドライブの回復をサポートする場合、この役割では回復キーを入力するだけで済みます。

- `-MbamReportUsersGroupName <DomainUserGroup>`: たとえば、`contoso\BitLocker report users` となります。 管理と監視の Web サイトの、**レポート**領域に対する読み取り専用アクセス権を持つメンバーを含めるドメイン ユーザー グループです。

    > [!NOTE]
    > インストーラー スクリプトによって、 **-HelpdeskUsersGroupName**、 **-HelpdeskAdminsGroupName**、および **-MbamReportUsersGroupName** パラメーターで指定したドメイン ユーザー グループが作成されることはありません。 スクリプトを実行する前に、必ずこれらのグループを作成してください。
    >
    > **-HelpdeskUsersGroupName**、 **-HelpdeskAdminsGroupName**、および **-MbamReportUsersGroupName** パラメーターを指定する場合は、必ずドメイン名とグループ名の両方を指定してください。 「`"domain\user_group"`」の形式を使用します。 ドメイン名を除外しないでください。 ドメイン名またはグループ名にスペースまたは特殊文字が含まれている場合は、パラメーターを引用符 (`"`) で囲みます。

- `-SiteInstall Both`: インストールするコンポーネントを指定します。 有効なオプションは次のとおりです。
  - `Both`: 両方のコンポーネントをインストールする
  - `HelpDesk`: administration and monitoring web サイトのみをインストールします。
  - `SSP`: セルフサービス ポータルのみをインストールする

- `-IISWebSite`: スクリプトによって MBAM Web アプリケーションがインストールされる Web サイト。 既定では、IIS の既定の Web サイトが使用されます。 このパラメーターを使用する前に、カスタム Web サイトを作成してください。

- `-InstallDirectory`: スクリプトによって Web アプリケーションのファイルがインストールされるパス。 既定では、このパスは `C:\inetpub` です。 このパラメーターを使用する前に、カスタム ディレクトリを作成してください。

- `-Uninstall`: BitLocker 管理ヘルプデスク/セルフサービス Web ポータル サイトを、以前にインストールされていた Web サーバー上からアンインストールします。

## <a name="verify"></a>確認事項

次のログを使用して、監視とトラブルシューティングを行います。

- **Microsoft-Windows-MBAM-Web** にある Windows イベント ログ。 詳細については、[BitLocker イベント ログの概要](../../tech-ref/bitlocker/about-event-logs.md)に関する記事と「[サーバー イベント ログ](../../tech-ref/bitlocker/server-event-logs.md)」をご覧ください。

- 各コンポーネントのトレース ログは、次の既定の場所にあります。

  - セルフサービス ポータル: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Self Service Website`

  - administration and monitoring web サイト: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Help Desk Website`

トラブルシューティングに関する詳細については、「[BitLocker のトラブルシューティング](../../tech-ref/bitlocker/troubleshoot.md)」をご覧ください。

## <a name="next-steps"></a>次のステップ

[セルフサービス ポータルのカスタマイズ](customize-self-service-portal.md)

インストールしたコンポーネントの使用方法の詳細については、次の記事を参照してください。

- [BitLocker administration and monitoring web サイト](helpdesk-portal.md)
- [BitLocker セルフサービス ポータル](self-service-portal.md)
