---
title: '1606 基準メディアを使用したサイトのインストール '
titleSuffix: Configuration Manager
description: System Center Configuration Manager 用 LTSB をインストールするか、アップグレードします。
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d70611aff329f48c8223a47dfa238e5a4559972
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707010"
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media"></a>バージョン 1606 基準メディアでのインストールとアップグレード

*適用対象:System Center Configuration Manager (Long-Term Servicing Branch)*

Configuration Manager のバージョン 1606 基準メディアからセットアップを実行すると、System Center Configuration Manager の Long-Term Servicing Branch サイトをインストールできます。

基準メディアは、Microsoft System Center 2016 に付属する DVD または System Center Configuration Manager Long-Term Servicing Branch バージョン 1606 から使用できます。 基準メディアの詳細については、「[Baseline and update versions](../servers/manage/updates.md#bkmk_Baselines)」(基準バージョンと更新プログラムのバージョン) を参照してください。


バージョン 1606 構成基準メディアを使用するときにインストールまたはアップグレードするサイト:
- *Current Branch サイト*。1511 構成基準メディアを利用して最初にインストールし、バージョン 1606 に更新し、さらに 1606 修正プログラム KB3186654 を適用したサイトと同等のサイト。
- *LTSB サイト*。バージョン 1606 に加えて 1606 修正プログラム KB3186654 を実行する Current Branch サイトと同等のサイト。 この構成基準メディアには、この修正プログラム ロールアップが既に含まれています  ただし、LTSB では、Current Branch で利用できる機能の一部をご利用いただけません。詳細は、「[Introduction to the Long-Term Servicing Branch of System Center Configuration Manager](introduction-to-the-ltsb.md)」 (System Center Configuration Manager の Long-Term Servicing Branch の概要) にあります。

Configuration Manager のブランチが不明な場合は、「[適切な Configuration Manager のブランチを選択する](which-branch-should-i-use.md)」を参照してください。




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>1606 構成基準メディアによるセットアップの変更点
1606 構成基準メディアでは、Configuration Manager のセットアップで次のような変更点を導入しています。

### <a name="branch-and-edition"></a>ブランチとエディション
セットアップを実行すると、ライセンス ページが表示されます。そのページで、インストールする Configuration Manager ブランチを選択できます。 Current Branch と LTSB のいずれかを「ライセンスを取得した」インストールとして選択できます。あるいは、「ライセンスのない」インストールとして Current Branch の評価版を選択できます。

詳細については、「[Configuration Manager のライセンスとブランチ](learn-more-editions.md)」を参照してください。

### <a name="software-assurance-expiration"></a>ソフトウェア アシュアランスの有効期限
セットアップ中、「**ソフトウェア アシュアランスの有効期限**」値を入力するオプションが与えられます。 これは便利なリマインダーとして指定できる任意の値です。

> [!NOTE]
> Microsoft では、お客様が入力した有効期限の日付を確認していません。また、ライセンスを検証する場合もこの日付を使用しません。  お客様は有効期限を通知するアラームとして、この日付を使用することができます。 Configuration Manager ではオンラインで新しいソフトウェア更新プログラムが提供されていないか定期的に確認します。このような追加の更新プログラムを取得するためにはソフトウェア アシュアランス ライセンスが最新の状態になっている必要があります。このため有効期限を通知するアラーム機能は便利です。    

- Configuration Manager バージョン 1606 の基準メディアからセットアップを実行する場合は、セットアップ ウィザードの **[プロダクト キー]** ページで日付値を指定できます。
- この日付は、Configuration Manager コンソールで **[階層設定のプロパティ]**  >  **[ライセンス]** の順に選択して指定することもできます。

詳細については、「[Configuration Manager のライセンスとブランチ](learn-more-editions.md)」の「ソフトウェア アシュアランス契約」を参照してください。


### <a name="additional-pre-upgrade-configurations"></a>追加のアップグレード前の構成
System Center 2012 Configuration Manager を LTSB にアップグレードする前に、アップグレード前のチェックリストとして、次の追加手順を実行する必要があります。  
LTSB でサポートされていないサイト システムの役割をアンインストールする:
- 資産インテリジェンス同期ポイント
- Microsoft Intune コネクタ
- クラウドベースの配布ポイント

詳細については、「[System Center Configuration Manager へのアップグレード](../servers/deploy/install/upgrade-to-configuration-manager.md)」を参照してください。


### <a name="new-scripted-installation-options"></a>スクリプト化された新しいインストール オプション
バージョン 1606 構成基準メディアでは、新しい上位サイトのスクリプト化インストールのために無人のスクリプト ファイル キーに対応しています。 これは新しいスタンドアロン プライマリ サイトのインストールやサイト拡張シナリオの中央管理サイトの追加に適用されます。

ライセンスされるブランチを無人スクリプトでインストールするときは、次のセクション、キー名、値をスクリーンショットのオプション セクションに追加する必要があります。 Current Branch の評価版インストールをスクリプト化する場合、これらの値を使用する必要はありません。  

 **SABranchOptions**
- **キー名:SAActive**
  - 値:0 または 1。  
  - 詳細:0 の場合、Current Branch の「ライセンスなし」評価版がインストールされます。1 の場合、「ライセンスを取得した」製品版がインストールされます。   

- **CurrentBranch**
  - 値:0 または 1。  
  - 詳細:0 の場合、Long-Term Servicing Branch がインストールされます。1 の場合、Current Branch がインストールされます。  

たとえば、Current Branch のライセンス取得版をインストールするには、次の値を利用します。

**キー名:SABranchOptions**
- **SAActive = 1**
- **CurrentBranch = 1**


> [!IMPORTANT]  
> **SABranchOptions** は、構成基準メディアからのセットアップでのみ機能します。 バージョン 1606 構成基準メディアを利用して以前にインストールしたサイトの CD.Latest フォルダーからセットアップを実行するときは適用されません。
>
> **SABranchOptions** は System Center 2012 Configuration Manager からのスクリプト化アップグレードには適用されず、常に Current Branch になります。

詳細については、「[コマンド ラインを使用して System Center Configuration Manager サイトをインストールする](../servers/deploy/install/use-a-command-line-to-install-sites.md)」を参照してください。


## <a name="install-a-new-site"></a>新しいサイトをインストールする
1606 基準メディアを利用していずれかのブランチの新しいサイトをインストールするときに、[Configuration Manager サイトのインストール](../servers/deploy/install/installing-sites.md)に関するトピックにあるサイト計画、準備、インストール手順を利用します。さらに、セットアップに関して次の事項を考慮します。

- セットアップ中、インストールする Configuration Manager のブランチを選択する必要があります。ソフトウェア アシュアランス契約の詳細を指定できます。
- 同じ階層内のすべてのサイトは同じブランチを実行する必要があります。 異なるサイトに LTSB と Current Branch が混在している階層の使用はサポートされません。
- スクリプト化された新しいインストール。 詳細については、この記事の "スクリプト化された新しいインストール オプション" を参照してください。

## <a name="expand-a-stand-alone-primary-site"></a>スタンドアロン プライマリ サイトを拡張する
LTSB を実行するスタンドアロンのプライマリ サイトを拡張できます。  このプロセスは、Current Branch サイトに使用されるプロセスと変わりませんが、1 つ注意点があります。

- 新しい中央管理サイトをインストールするとき、LTSB サイトのインストールで使用した元のソース メディアからのセットアップを利用する必要があります。 このシナリオは CD.Latest フォルダーからセットアップすることはできません。

サイトの拡張に関する詳細については、「[Install a site using the Setup Wizard](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md)」 (セットアップ ウィザードを利用してサイトをインストールする) の "スタンドアロン プライマリ サイトを拡張する" を参照してください。

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>System Center 2012 Configuration Manager からアップグレードする
System Center 2012 Configuration Manager からアップグレードするとき、[Configuration Manager へのアップグレード](../servers/deploy/install/upgrade-to-configuration-manager.md)に関するトピックにあるサイト計画、準備、手順を利用しますが、次の変更点があります。

**Current Branch にアップグレードする:**
- セットアップ中、Current Branch を選択する必要があります。ソフトウェア アシュアランス契約の詳細を指定できます。
- スクリプト化された新しいインストール。 詳細については、この記事の "スクリプト化された新しいインストール オプション" を参照してください。

**LTSB へのアップグレード:**  
- アップグレード前チェックリストの追加手順。
- セットアップ中、LTSB を選択する必要があります。ソフトウェア アシュアランス契約の詳細を指定できます。
- System Center 2012 Configuration Manager Service Pack 1、System Center 2012 Configuration Manager Service Pack 2、System Center 2012 R2 Configuration Manager Service Pack 1、または System Center 2012 R2 Configuration Manager (Service Pack なし) を実行しているサイトだけをアップグレードできます。

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>1606 構成基準メディアの一括アップグレード パス
1606 基準メディアを利用し、次を Configuration Manager の製品版にアップグレードできます。
- System Center 2012 R2 Configuration Manager Service Pack 1
- Service Pack なしの System Center 2012 R2 Configuration Manager (2016 年 12 月 15 日に再リリースされたバージョン 1606 の構成基準メディアの使用が必要です。)
- System Center 2012 Configuration Manager Service Pack 2
- System Center 2012 Configuration Manager Service Pack 1 (2016 年 12 月 15 日に再リリースされたバージョン 1606 の構成基準メディアの使用が必要です)。


また、このメディアを利用し、Current Branch の評価版を製品版にアップグレードできます。

このメディアは、次のアップグレードに対応していません。
- その他のバージョンの System Center 2012 Configuration Manager。
- Configuration Manager 2007 以前。
- Configuration Manager のリリース候補版のインストール。

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>CD.Latest フォルダーと LTSB について
次は、サイト サーバーの CD.Latest フォルダーで Configuration Manager により作成されるメディアの利用に関する制限です。 これらの制限は LTSB を実行するサイトに適用されます。

CD.Latest フォルダーのメディアのサポート対象:
- サイトの回復。
- サイトの保守。
- 追加の子プライマリ サイトのインストール。

CD.Latest フォルダーのメディアのサポート対象外:  
- サイト拡張シナリオの一部として中央管理サイトをインストールする。

詳細については、「[CD.Latest フォルダー](../servers/manage/the-cd.latest-folder.md)」を参照してください。

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>LTSB のバックアップ、復元、サイト保守
LTSB を実行しているサイトでバックアップ、復元、サイト保守を実行するには、[Configuration Manager のバックアップと回復](../servers/manage/backup-and-recovery.md)に関するページのガイドと手順を利用してください。  

LTSB サイトのバックアップの CD.Latest フォルダーからの Configuration Manager のセットアップを使用します。
