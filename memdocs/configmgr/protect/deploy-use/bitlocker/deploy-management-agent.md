---
title: BitLocker 管理の展開
titleSuffix: Configuration Manager
description: BitLocker 管理エージェントを Configuration Manager クライアントに展開し、回復サービスを管理ポイントに展開します
ms.date: 07/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 39aa0558-742c-4171-81bc-9b1e6707f4ea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a7eca5c2f5c00ae559a8567d5fce1e4e36df19c0
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129275"
---
# <a name="deploy-bitlocker-management"></a>BitLocker 管理の展開

*適用対象:Configuration Manager (Current Branch)*

<!--3601034-->

Configuration Manager の BitLocker 管理には、次のコンポーネントが含まれています。

- **BitLocker 管理エージェント**:[ポリシーを作成](#create-a-policy)して[コレクションに展開](#deploy-a-policy)すると、Configuration Manager によってデバイス上でこのエージェントが有効になります。

- **回復サービス**:クライアントから BitLocker 回復データを受信するサーバー コンポーネント。 詳細については、「[回復サービス](#recovery-service)」 をご覧ください。

BitLocker 管理ポリシーを作成して展開する前に、次の操作を行います。

- [前提条件](../../plan-design/bitlocker-management.md#prerequisites)を確認します。

- 必要に応じて、サイト データベース内の[回復キーを暗号化](encrypt-recovery-data.md)します

## <a name="create-a-policy"></a>ポリシーの作成

このポリシーを作成して展開すると、Configuration Manager クライアントによってデバイス上の BitLocker 管理エージェントが有効になります。

> [!NOTE]
> BitLocker 管理ポリシーを作成するには、Configuration Manager での**完全な権限を持つ管理者**ロールが必要です。

1. Configuration Manager コンソールで **[資産とコンプライアンス]** ワークスペースに移動し、 **[Endpoint Protection]** を展開して、 **[BitLocker Management]** ノードを選択します。

1. リボンで、 **[BitLocker 管理制御ポリシーの作成]** を選択します。

1. **[全般]** ページで、名前と必要に応じて説明を指定します。 次のコンポーネントを選択し、クライアントでこのポリシーを有効にします。  

    - **オペレーティング システム ドライブ**:OS ドライブが暗号化されているかどうかを管理します

    - **固定ドライブ**:デバイスでの追加のデータ ドライブの暗号化を管理します

    - **リムーバブル ドライブ**:USB キーなど、デバイスから取り外すことができるドライブの暗号化を管理します

    - **クライアント管理**:BitLocker ドライブ暗号化回復情報のキー回復サービスのバックアップを管理します  

1. **[セットアップ]** ページで、BitLocker ドライブ暗号化用に次のグローバル設定を構成します。

    > [!NOTE]
    > BitLocker を有効にすると、Configuration Manager によってこれらの設定が適用されます。 ドライブが既に暗号化されている場合、または暗号化が進行中の場合は、これらのポリシー設定を変更しても、デバイスでのドライブ暗号化は変更されません。
    >
    > これらの設定を無効にした場合、または構成しなかった場合、BitLocker では既定の暗号化方法 (AES 128 ビット) が使用されます。

    - Windows 8.1 デバイスの場合、 **[Drive encryption method and cipher strength] (ドライブの暗号化方法と暗号強度)** のオプションを有効にします。 次に、暗号化方法を選択します。

    - Windows 10 デバイスの場合、 **[Drive encryption method and cipher strength (Windows 10)]\(ドライブの暗号化方法と暗号強度 (Windows 10)\)** のオプションを有効にします。 次に、OS ドライブ、固定データ ドライブ、およびリムーバブル データ ドライブの暗号化方法を個別に選択します。

    このページに記載されたこれらの設定とその他の設定の詳細については、[設定のリファレンス - セットアップ](../../tech-ref/bitlocker/settings.md#setup)に関する記事をご覧ください。

1. **[オペレーティング システム ドライブ]** ページで、次の設定を指定します。  

    - **Operating System Drive Encryption Settings (オペレーティング システム ドライブの暗号化設定)** :この設定を有効にした場合、ユーザーは OS ドライブを保護する必要があり、ドライブは BitLocker によって暗号化されます。 無効にした場合、ユーザーはドライブを保護できません。  

    互換性のある TPM を装備したデバイスでは、暗号化されたデータの保護を強化するためにスタートアップ時に 2 種類の認証方法を使用できます。 コンピューターの起動時に、認証に TPM のみを使用することも、個人識別番号 (PIN) の入力を要求することもできます。 次の設定を構成します。

    - **Select protector for operating system drive (オペレーティング システム ドライブのプロテクターを選択)** :TPM と PIN、または TPM のみが使用されるように構成します。

    - **スタートアップに対する PIN の長さの最小値を構成する**:PIN が必要なとき、ユーザーはこの長さ以上の値を指定する必要があります。 ユーザーはこの PIN を、コンピューターが起動されドライブのロックを解除するときに入力します。 既定では、PIN の長さの最小値は `4` です。

    このページに記載されたこれらの設定とその他の設定の詳細については、[設定のリファレンス - OS ドライブ](../../tech-ref/bitlocker/settings.md#os-drive)に関する記事をご覧ください。

1. **[固定ドライブ]** ページで、次の設定を指定します。

    - **固定データ ドライブの暗号化**:この設定を有効にした場合、BitLocker では、すべての固定データ ドライブを保護の対象とするようにユーザーに要求します。 その後、それらのデータ ドライブが暗号化されます。 このポリシーを有効にする場合は、自動ロック解除を有効にするか、 **[固定データ ドライブのパスワード ポリシー]** の設定を有効にします。

    - **Configure auto-unlock for fixed data drive (固定データ ドライブの自動ロック解除を構成する)** :暗号化されたデータ ドライブを BitLocker で自動的にロック解除することを許可または必須とします。 自動ロック解除を使用するには、BitLocker で OS ドライブを暗号化する必要もあります。

    このページに記載されたこれらの設定とその他の設定の詳細については、[設定のリファレンス - 固定ドライブ](../../tech-ref/bitlocker/settings.md#fixed-drive)に関する記事をご覧ください。

1. **[リムーバブル ドライブ]** ページで、次の設定を指定します。

    - **リムーバブル データ ドライブの暗号化**:この設定を有効にし、ユーザーが BitLocker による保護を適用できるようにすると、Configuration Manager クライアントによって、リムーバブル ドライブに関する回復情報が管理ポイントの回復サービスに保存されます。 この動作により、ユーザーは保護機能 (パスワード) を忘れたり紛失したりしても、ドライブを回復できます。

    - **リムーバブル データ ドライブに BitLocker 保護を適用できるようにする**:ユーザーは、リムーバブル ドライブの BitLocker 保護を有効にすることができます。

    - **Removable data drive password policy (リムーバブル データ ドライブのパスワード ポリシー)** :これらの設定を使用すると、BitLocker で保護されているリムーバブル ドライブのロックを解除するためのパスワードの制約を設定できます。

    このページに記載されたこれらの設定とその他の設定の詳細については、[設定のリファレンス - リムーバブル ドライブ](../../tech-ref/bitlocker/settings.md#removable-drive)に関する記事をご覧ください。

1. **[クライアント管理]** ページで、次の設定を指定します。

    > [!IMPORTANT]
    > HTTPS 対応の Web サイトを使用している管理ポイントがない場合は、この設定を構成しないでください。 詳細については、「[回復サービス](#recovery-service)」 をご覧ください。

    - **BitLocker 管理サービスの構成**:この設定を有効にすると、Configuration Manager によってキーの回復情報がサイト データベースに自動的に通知なしでバックアップされます。 この設定を無効にした場合、または構成しなかった場合は、Configuration Manager によってキーの回復情報は保存されません。

        - **格納する BitLocker 回復情報を選択する**:回復パスワードとキー パッケージ、または回復パスワードのみを使用する場合に構成します。

        - **回復情報をプレーン テキストで保存することを許可する**:BitLocker 管理の暗号化証明書がない場合、Configuration Manager によってキーの回復情報がプレーン テキストで保存されます。 詳細については、「[回復データの暗号化](encrypt-recovery-data.md)」をご覧ください。

    このページに記載されたこれらの設定とその他の設定の詳細については、[設定のリファレンス - クライアント管理](../../tech-ref/bitlocker/settings.md#client-management)に関する記事をご覧ください。

1. ウィザードを完了します。

既存のポリシーの設定を変更するには、一覧でそのポリシーを選択して、 **[プロパティ]** を選択します。

複数のポリシーを作成する場合は、それらの相対的な優先順位を構成できます。 複数のポリシーを 1 つのクライアントに展開する場合は、優先順位の値を使用してその設定が決められます。

## <a name="deploy-a-policy"></a>ポリシーの展開

1. **[BitLocker 管理]** ノードで既存のポリシーを選択します。 リボンで、 **[展開]** を選択します。

1. 展開のターゲットとしてデバイス コレクションを選択します。

1. デバイスでいつでもドライブを暗号化または暗号化解除できるようにするには、 **[メンテナンス期間以外の修復を許可する]** オプションを選択します。 コレクションにメンテナンス期間がある場合でも、この BitLocker ポリシーは修復されます。

1. **簡易**スケジュールまたは**カスタム** スケジュールを構成します。 クライアントでは、スケジュールで指定された設定に基づいてコンプライアンスが評価されます。

1. **[OK]** を選択してポリシーを展開します。

同じポリシーの複数の展開を作成できます。 各展開に関する追加情報を表示するには、 **[BitLocker 管理]** ノードでポリシーを選択してから、詳細ウィンドウで **[展開]** タブに切り替えます。

> [!IMPORTANT]
> リモート デスクトップ プロトコル接続がアクティブな場合、MBAM クライアントによって BitLocker ドライブ暗号化アクションは開始されません。 BitLocker ドライブ暗号化が開始される前に、すべてのリモート コンソール接続が閉じられ、ユーザーが物理コンソール セッションにログオンしている必要があります。


## <a name="monitor"></a>モニター

**[BitLocker 管理]** ノードの詳細ウィンドウに、ポリシーの展開に関する基本的なコンプライアンスの統計情報が表示されます。

- コンプライアンスの数
- 失敗数
- 非コンプライアンスの数

**[展開]** タブに切り替えると、コンプライアンス対応率と推奨されるアクションを確認できます。 展開を選択し、リボンで **[状態の表示]** を選択します。 この操作により、ビューが **[監視]** ワークスペースの **[展開]** ノードに切り替わります。 他の構成ポリシー展開の展開と同様に、このビューでは、より詳細なコンプライアンスの状態を確認できます。

クライアントから BitLocker 管理ポリシーに準拠していないと報告される理由については、「[非コンプライアンス コード](../../tech-ref/bitlocker/non-compliance-codes.md)」をご覧ください。

トラブルシューティングに関する詳細については、「[BitLocker のトラブルシューティング](../../tech-ref/bitlocker/troubleshoot.md)」をご覧ください。

監視とトラブルシューティングを行うには、次のログを使用します。

### <a name="client-logs"></a>クライアント ログ

- MBAM のイベント ログ: Windows イベント ビューアーで、[アプリケーションとサービス]、[Microsoft]、[Windows]、[MBAM] の順に移動します。  詳細については、「[BitLocker イベント ログ](../../tech-ref/bitlocker/about-event-logs.md)」と「[クライアント イベント ログ](../../tech-ref/bitlocker/client-event-logs.md)」をご覧ください。

- クライアントのログのパスは、**BitlockerMangementHandler.log** で既定では `%WINDIR%\CCM\Logs`

### <a name="management-point-logs-recovery-service"></a>管理ポイントのログ (回復サービス)

- 回復サービスのイベント ログ: Windows イベント ビューアーで、[アプリケーションとサービス]、[Microsoft]、[Windows]、[MBAM-Web] の順に移動します。 詳細については、[BitLocker イベント ログの概要](../../tech-ref/bitlocker/about-event-logs.md)に関する記事と「[サーバー イベント ログ](../../tech-ref/bitlocker/server-event-logs.md)」をご覧ください。

- 回復サービスのトレース ログ: `<Default IIS Web Root>\Microsoft BitLocker Management Solution\Logs\Recovery And Hardware Service\trace*.etl`

## <a name="recovery-service"></a>回復サービス

BitLocker 回復サービスとは、Configuration Manager クライアントから BitLocker 回復データを受信するサーバー コンポーネントです。 BitLocker 管理ポリシーを作成すると、サイトによって回復サービスが展開されます。 Configuration Manager では、HTTPS 対応の Web サイトを使用して、各管理ポイントに回復サービスを自動的にインストールします。

Configuration Manager では、回復情報をサイト データベースに保存します。 BitLocker 管理の暗号化証明書がない場合、Configuration Manager によってキーの回復情報がプレーン テキストで保存されます。

詳細については、「[回復データの暗号化](encrypt-recovery-data.md)」をご覧ください。

## <a name="migration-considerations"></a>移行に関する注意事項

Microsoft BitLocker Administration and Monitoring (MBAM) を現在使用している場合は、管理を Configuration Manager にシームレスに移行できます。 Configuration Manager で BitLocker 管理ポリシーを展開すると、クライアントでは回復キーとパッケージが Configuration Manager の回復サービスに自動的にアップロードされます。

> [!IMPORTANT]
> スタンドアロンの MBAM から Configuration Manager の BitLocker 管理に移行するときに、スタンドアロン MBAM の既存の機能が必要な場合は、スタンドアロンの MBAM サーバーまたはコンポーネントを Configuration Manager の BitLocker 管理で再利用しないでください。 こうしたサーバーを再利用すると、Configuration Manager の BitLocker 管理でそれらのサーバーにコンポーネントがインストールされたときに、スタンドアロンの MBAM が動作しなくなります。 MBAMWebSiteInstaller.ps1 スクリプトを実行して、スタンドアロンの MBAM サーバーで BitLocker ポータルをセットアップしないでください。 Configuration Manager の BitLocker 管理をセットアップする場合は、別のサーバーを使用してください。

### <a name="group-policy"></a>グループ ポリシー

- BitLocker の管理設定は、MBAM グループ ポリシー設定と完全な互換性があります。 デバイスでグループ ポリシー設定と Configuration Manager ポリシーの両方を受信する場合は、それらを一致するように構成します。

  > [!NOTE]
  > スタンドアロン MBAM に対してグループ ポリシー設定が存在する場合、それは、Configuration Manager によって試行される同等の設定よりもオーバーライドされます。 スタンドアロン MBAM によって使用されるのはドメイン グループ ポリシーですが、Configuration Manager によって設定されるのは BitLocker 管理用のローカル ポリシーです。 ドメイン ポリシーは、ローカルの Configuration Manager の BitLocker 管理ポリシーよりもオーバーライドされます。 スタンドアロンの MBAM ドメイン グループ ポリシーが Configuration Manager のポリシーと一致しない場合、Configuration Manager の BitLocker 管理は失敗します。 たとえば、キー回復サービス用のスタンドアロン MBAM サーバーがドメイン グループ ポリシーで設定される場合、管理ポイントに対してそれと同じ設定を、Configuration Manager の BitLocker 管理で設定することはできません。 この動作により、管理ポイント上の Configuration Manager の BitLocker 管理キー回復サービスに、クライアントは回復キーを報告しなくなります。

- Configuration Manager では、MBAM のすべてのグループ ポリシー設定を実装しているわけではありません。 グループ ポリシーで追加の設定を構成した場合は、Configuration Manager クライアント上の BitLocker 管理エージェントによってそれらの設定が受け入れられます。

  > [!IMPORTANT]
  > Configuration Manager の BitLocker 管理によって既に指定されている設定には、グループ ポリシーを設定しないでください。 Configuration Manager の BitLocker 管理に現在存在していない設定に対してのみ、グループ ポリシーを設定します。 Configuration Manager バージョン 2002 には、スタンドアロン MBAM に対する機能パリティが用意されています。 Configuration Manager バージョン 2002 以降では、ほとんどの場合、BitLocker ポリシーを構成するためにドメイン グループ ポリシーを設定する理由はなくなります。 競合と問題を回避するには、BitLocker にグループ ポリシーを使用しないようにしてください。 Configuration Manager の BitLocker 管理ポリシーを使用してすべての設定を構成します。

### <a name="tpm-password-hash"></a>TPM パスワード ハッシュ

- 以前の MBAM クライアントでは、TPM パスワード ハッシュが Configuration Manager にアップロードされません。 このクライアントでは、TPM パスワード ハッシュが 1 回だけアップロードされます。

- この情報を Configuration Manager の回復サービスに移行する必要がある場合は、デバイス上の TPM を消去します。 再起動後に、新しい TPM パスワード ハッシュが回復サービスにアップロードされます。

### <a name="re-encryption"></a>再暗号化

Configuration Manager では BitLocker ドライブ暗号化で既に保護されているドライブを再暗号化しません。 ドライブの現在の保護状態に一致しない BitLocker 管理ポリシーを展開した場合は、非準拠として報告されます。 ドライブは引き続き保護されます。

たとえば、MBAM を使用して、AES-XTS 128 暗号化アルゴリズムでドライブを暗号化しましたが、Configuration Manager ポリシーでは AES-XTS 256 が要求されているとします。 このドライブは、暗号化されているけれども、ポリシーには準拠していません。

この動作を回避するには、最初にデバイスで BitLocker を無効にします。 次に、新しいポリシーを新しい設定で展開します。

## <a name="co-management-and-intune"></a>共同管理と Intune

<!-- SCCMDocs#2321 -->

BitLocker の Configuration Manager クライアント ハンドラーは、共同管理に対応しています。 デバイスが共同管理されており、[Endpoint Protection ワークロード](../../../comanage/workloads.md#endpoint-protection)を Intune に切り替える場合、Configuration Manager クライアントはその BitLocker ポリシーを無視します。 デバイスは、Intune から Windows 暗号化ポリシーを取得します。

暗号化管理機関を切り替え、必要な暗号化アルゴリズムも変わる場合は、[再暗号化](#re-encryption)を計画する必要があります。

Intune での BitLocker の管理に関する詳細については、次の記事を参照してください。

- [Intune でデバイスの暗号化を使用する](../../../../intune/protect/encrypt-devices.md)
- [Microsoft Intune での BitLocker ポリシーのトラブルシューティング](../../../../intune/protect/troubleshoot-bitlocker-policies.md)

## <a name="next-steps"></a>次のステップ

[BitLocker のレポートとポータルのセットアップ](setup-websites.md)
