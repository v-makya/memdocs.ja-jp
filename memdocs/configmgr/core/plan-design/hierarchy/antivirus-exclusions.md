---
title: ウイルス対策の除外
titleSuffix: Configuration Manager
description: 考えられる問題をトラブルシューティングするときに使用する、推奨されるウイルス対策の除外について説明します。
ms.date: 10/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb470e3-6f6b-4ccf-b3d8-1598d79d3490
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: df951bfb44313cfec8dacb8c0df34abb7beb0c56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703740"
---
# <a name="recommended-antivirus-exclusions-for-configuration-manager"></a>Configuration Manager の推奨されるウイルス対策の除外

*適用対象:Configuration Manager (Current Branch)*

この記事には、Configuration Manager サイト サーバー、サイト システム、およびクライアントのサポートされているバージョンを実行しているコンピューターが、ウイルス対策ソフトウェアと共に使用されている場合の、潜在的な不安定さの原因を、管理者が特定するのに役立つ推奨事項が含まれています。

> [!IMPORTANT]
>
> - システムを評価するために、これらの手順を一時的に適用することをお勧めします。 この記事に記載されている推奨事項によって、お使いのシステムのパフォーマンスや安定性が向上した場合は、指示やそのウイルス対策ソフトウェアの更新されたバージョンについて、お使いのウイルス対策ソフトウェアのベンダーにお問い合わせください。
> - この記事には、セキュリティ設定を低くする方法や、コンピューター上のセキュリティ機能を一時的に無効にする方法などを示す情報が含まれています。 これらの変更を行うことで、特定の問題の性質を理解することができます。 これらの変更を行う前に、お客様の特定の環境でこの回避策を実装することに関連するリスクを、評価することをお勧めします。

## <a name="possible-symptoms"></a>考えられる現象 

ウイルス対策のリアルタイム保護は、Configuration Manager サイト サーバー、サイト システム、およびクライアント上で、多くの問題の原因となる可能性があります。

次に、考えられる現象の、包括的でない一覧を示します。

- リモート サイト システムのコンポーネントがインストールされていない。 SiteComp.log、Distmgr.log、hman.log、またはその他の Configuration Manager ログ ファイルに、エラー 80070005 などのエラーが含まれている場合があります。
- クライアント プッシュを使用して構成マネージャー クライアントをインストールできない。
- クライアントのインベントリ情報が、不正確であるか、存在しないか、または古くなっている。
- <*インストール ディレクトリ*>\Program Files\Microsoft Configuration Manager\Inboxes フォルダーにバックログが生成される。
- ソフトウェア センターが、クライアント システムに展開されたソフトウェアによって設定されていない、または起動しない。 また、CCMRepair.log ファイルに、次の例のようなエラーが含まれている場合があります。

  > 次の結果により、データベースの検証に失敗しました:0x80004005 ただし、DB:C:\Windows\CCM\filename.sdf を開くことはできました (DB の修復をスキップ)。

- クライアントに展開されているソフトウェアをインストールできない。
- ソフトウェア展開のコンプライアンス データが不正確。

## <a name="exclusions"></a>除外

このような問題を回避するために、次のリアルタイム保護の除外を追加することをお勧めします。

### <a name="default-installation-folders"></a>既定のインストール フォルダー

|  |  |
| - | - |
|"*ConfigMgr のインストール フォルダー*"  |  %ProgramFiles%\Microsoft Configuration Manager  |  
|"*MP のインストール フォルダー*"  |%ProgramFiles%\SMS_CCM  |  
|"*クライアントのインストール フォルダー*"  |%Windir%\CCM  |  

### <a name="folder-exclusions-for-site-servers"></a>サイト サーバー用のフォルダーの除外

- <*ConfigMgr のインストール フォルダー*>\Inboxes
- <*ConfigMgr のインストール フォルダー*>\Logs
- <*ConfigMgr のインストール フォルダー*>\EasySetupPayload

### <a name="folder-exclusions-for-site-systems"></a>サイト システム用のフォルダーの除外

- 管理ポイント
  - <*MP のインストール フォルダー*>\ServiceData
  - 次のいずれか:
    - <*ConfigMgr のインストール フォルダー*>\MP\OUTBOXES
    - <*インストール ドライブ*>\SMS\MP\OUTBOXES
- 配布ポイント
  - <*クライアントのインストール フォルダー*>\ServiceData
  - <*コンテンツ ライブラリのドライブ*>\SMS_DP$
  - <*コンテンツ ライブラリのドライブ*>\SMSPKG<*ドライブ文字*>$
  - <*コンテンツ ライブラリのドライブ*>\SMSPKG
  - <*コンテンツ ライブラリのドライブ*>\SMSPKGSIG
  - <*コンテンツ ライブラリのドライブ*>\SMSSIG$
- サイト データベース サーバー
  - [SQL Server を稼働しているコンピューター上で実行する、ウイルス対策ソフトウェアを選択する方法](https://support.microsoft.com/en-us/help/309422)

### <a name="folder-exclusions-for-clients"></a>クライアント用のフォルダーの除外

- <*クライアントのインストール フォルダー*>\\\*.sdf
- <*クライアントのインストール フォルダー*>\ServiceData
- C:\Windows\CCMCache
- C:\Windows\CCMSetup
- <*クライアントのインストール フォルダー*>\Logs

### <a name="file-exclusions-for-mps"></a>MP 用のフォルダーの除外

- 次に含まれる POL00000.pol
  - <*MP のインストール フォルダー*>\PolReqStaging

### <a name="process-exclusions"></a>プロセスの除外

プロセスの除外が必要になるのは、アグレッシブなウイルス対策プログラムによって、Configuration Manager のプログラム ファイル (.exe ファイル) が、危険度の高いプロセスと見なされる場合のみです。

- <*ConfigMgr のインストール フォルダー*>\bin\64\Smsexec.exe
- 次のいずれかのプロセス:
  - <*クライアントのインストール フォルダー*>\Ccmexec.exe
  - <*MP のインストール フォルダー*>\Ccmexec.exe
- <*クライアントのインストール フォルダー*>\CmRcService.exe (クライアント側)
- <*ConfigMgr のインストール フォルダー*>\bin\64\Sitecomp.exe
- <*ConfigMgr のインストール フォルダー*>\bin\64\Smswriter.exe
- <*ConfigMgr のインストール フォルダー*>\bin\64\Smssqlbkup.exe、または SMS_*SQLFQDN*\bin\x64\Smssqlbkup.exe
- <*ConfigMgr のインストール フォルダー*>\bin\64\Cmupdate.exe
- <*クライアントのインストール フォルダー*>\Ccmrepair.exe (クライアント側)
- %*windir*%\CCMSetup\Ccmsetup.exe (クライアント側)

## <a name="next-steps"></a>次のステップ

ウイルス対策の除外について詳しくは、次の記事を参照してください。

[Configuration Manager Current Branch のウイルス対策の除外 -System Center Premier Field Engineer のブログ](https://blogs.technet.microsoft.com/systemcenterpfe/2017/05/24/configuration-manager-current-branch-antivirus-update/)

[OSD とブート イメージに関する詳細情報を含む、更新された System Center 2012 Configuration Manager のウイルス対策の除外](https://blogs.technet.microsoft.com/systemcenterpfe/2013/01/11/updated-system-center-2012-configuration-manager-antivirus-exclusions-with-more-details-on-osd-and-boot-images-etc/)

[SQL Server を稼働しているコンピューター上で実行する、ウイルス対策ソフトウェアを選択する方法](https://support.microsoft.com/en-us/help/309422/how-to-choose-antivirus-software-to-run-on-computers-that-are-running-sql-server)

[現在サポートされているバージョンの Windows を稼働している Enterprise コンピューター向けの、ウイルス スキャンに関する推奨事項](https://support.microsoft.com/en-us/help/822158/virus-scanning-recommendations-for-enterprise-computers-that-are-running-currently-supported-versions-of-windows)
