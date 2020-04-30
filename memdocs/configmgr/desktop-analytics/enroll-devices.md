---
title: Desktop Analytics でデバイスを登録する
titleSuffix: Configuration Manager
description: Desktop Analytics でデバイスを登録する方法について説明します。
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9cca066d389ea8d3847737651f4994977a5e2f5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708170"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Desktop Analytics でデバイスを登録する方法

Desktop Analytics に [Configuration Manager を接続する](connect-configmgr.md)場合、Desktop Analytics にデバイスを登録するための設定を構成します。 これらの設定は、いつでも変更できます。 また、デバイスが最新の状態であることを確認します。

## <a name="update-devices"></a>デバイスの更新

Desktop Analytics では、次の 2 つの主要な Windows コンポーネントが使用されます。

- **互換性コンポーネント**:互換性コンポーネント (**Appraiser**) によって、Windows デバイスに対する診断が実行され、最新バージョンの Windows 10 との互換性の状態が評価されます。

- **接続ユーザー エクスペリエンスとテレメトリ サービス**:Windows の診断データを有効にすると、接続ユーザー エクスペリエンスとテレメトリ サービス (**DiagTrack**) によって、システム、アプリケーション、およびドライバーのデータが収集されます。 Microsoft によってこのデータが分析され、それが Desktop Analytics 経由でもう一度お客様と共有されます。

Desktop Analytics で最適なエクスペリエンスを得るために、これらのコンポーネントの最新バージョンをインストールしてください。

次の表に、サポートされる OS バージョンでの各コンポーネントの更新プログラムを示します。

| OS のバージョン | Appraiser | DiagTrack |
| --------------| ----------------------- | -------------------|
| Windows 10 1909 | 含まれる <sup>[注 1](#bkmk_note1)</sup> | [最新の累積的な更新プログラム](https://support.microsoft.com/help/4529964) |
| Windows 10 1903 | 含まれる | [最新の累積的な更新プログラム](https://support.microsoft.com/help/4498140) |
| Windows 10 1809 | 含まれる | [最新の累積的な更新プログラム](https://support.microsoft.com/help/4464619) |
| Windows 10 1803 | 含まれる | [最新の累積的な更新プログラム](https://support.microsoft.com/help/4099479) |
| Windows 10 1709 | 含まれる | [最新の累積的な更新プログラム](https://support.microsoft.com/help/4043454) |
| Windows 8.1 | [KB 2976978](https://support.microsoft.com/help/2976978) <sup>[注 2](#bkmk_note2)</sup> | [最新のマンスリー ロールアップ](https://support.microsoft.com/help/4009470) |
| Windows 7 SP1 | [KB 2952664](https://support.microsoft.com/help/2952664) <sup>[注 3](#bkmk_note3)</sup> | [最新のマンスリー ロールアップ](https://support.microsoft.com/help/4009469) |

> [!TIP]
> Configuration Manager を使用すると、これらの更新プログラムを自動的にインストールできます。 詳細については、「[ソフトウェアの更新の展開方法](../sum/deploy-use/deploy-software-updates.md)」を参照してください。
>
> 互換性に関する更新プログラムを初めてインストールした後は、デバイスを再起動してください。

### <a name="note-1-windows-10"></a><a name="bkmk_note1"></a> 注 1:Windows 10

Windows 10 にはこれらのコンポーネントが既定で含まれていますが、Windows 10 デバイスで Desktop Analytics のすべての機能を利用するには、最新の累積的な更新プログラムが必要です。 たとえば、最新の OS バージョンとの互換性についてデバイスを評価する場合や、展開と登録状態に関するほぼリアルタイムの情報を取得する場合などです。

### <a name="note-2-windows-81"></a><a name="bkmk_note2"></a> 注 2:Windows 8.1

このコンポーネントの更新プログラムは Microsoft により定期的に増分されますが、関連付けられている KB 番号は変わりません。 常に最新バージョンの更新プログラムを使用していることを確認してください。

このコンポーネントでは、Windows カスタマー エクスペリエンス向上プログラムに参加している Windows 8.1 システムに対して診断が実行されます。 この診断は、Windows 10 へのアップグレード時に互換性に関する問題があるかどうかを判断するのに役立ちます。

### <a name="note-3-windows-7"></a><a name="bkmk_note3"></a> 注 3:Windows 7

Windows 7 デバイスに "マンスリー品質ロールアップ" の更新プログラムを適用せず、"セキュリティのみ" の更新プログラムだけを適用する場合は、[KB 2952664 を置き換える更新プログラムの一覧](https://www.catalog.update.microsoft.com/ScopedViewInline.aspx?updateid=ad3652cd-2689-4726-b3ef-b086ded23c7c)に "セキュリティのみ" の更新プログラムがいくつか見つかります。 KB 2952664 の代わりに、より新しいこれらの更新プログラムをインストールできます。

> [!NOTE]
> Windows 8.1 の場合、Microsoft では、"マンスリー品質ロールアップ" の更新プログラムの一部として、KB 2976978 の改訂のみ行っています。

## <a name="device-enrollment"></a>デバイスの登録

Desktop Analytics サービスには、インストールするエージェントがありません。 デバイスを登録するには、監視対象のデバイス上で設定を構成する必要があります。 この設定によって、デバイスからどの Desktop Analytics インスタンスにデータを送信するかと、その他の構成オプションが制御されます。

> [!Note]  
> 以前に Windows Analytics を使用している場合は、その同じワークスペースを Desktop Analytics 用に使用します。 以前に Windows Analytics に登録していたデバイスを、Desktop Analytics に再登録する必要があります。
>
> Azure AD テナントごとに、1 つの Desktop Analytics ワークスペースのみを使用できます。 デバイスは、1 つのワークスペースにのみ診断データを送信できます。  

Configuration Manager には、これらの設定を管理してクライアントに展開するための、統合エクスペリエンスが用意されています。 最良のエクスペリエンスを実現するには、Configuration Manager をお使いください。

Configuration Manager を Desktop Analytics に接続する場合、デバイスを登録するための設定を構成します。 詳細については、[Configuration Manager を Desktop Analytics に接続する方法](connect-configmgr.md#bkmk_connect)に関する記事をご覧ください。

これらの設定を変更するには、次の手順を実行します。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[Cloud Services]** を展開して **[Azure サービス]** ノードを選択します。 Desktop Analytics への接続を選択し、リボンの **[プロパティ]** を選択します。

2. **[診断データ]** ページで、必要に応じて次の設定を変更します。  

    - **[商用 ID]** : この値には、ご自分の組織の ID が自動的に入力されます。 そうでない場合は、お使いのプロキシ サーバーが、必要なすべての[エンドポイント](enable-data-sharing.md#endpoints)が許可されるように構成されていることを確認してから、次に進んでください。 また、[Desktop Analytics ポータル](monitor-connection-health.md#bkmk_ViewCommercialID)から、商用 ID を手動で取得することもできます。

    - **[Windows 10 診断データのレベル]** :詳細については、「[診断データのレベル](enable-data-sharing.md#diagnostic-data-levels)」をご覧ください。  

    - **[診断データでデバイス名を許可する]** :詳細については、「[デバイス名](#device-name)」をご覧ください。  

    このページに変更を加えると、 **[利用可能な機能]** ページに、選択した診断データ設定を使用した Desktop Analytics 機能のプレビューが表示され ます。  

3. **[Desktop Analytics 接続]** ページで、必要に応じて次の設定を変更します。

    - **[表示名]** :Desktop Analytics ポータルでは、この名前を使用してこの Configuration Manager 接続が表示されます。  

    - **[ターゲット コレクション]** :このコレクションには、商用 ID と診断データの設定を使用して Configuration Manager によって構成されるすべてのデバイスが含まれます。 それは、Configuration Manager によって Desktop Analytics サービスに接続されるデバイスの完全なセットです。  

    - **ターゲット コレクション内のデバイスでは、送信方向の通信にユーザー認証済みプロキシが使用されます**:既定では、この値は **[いいえ]** です。 環境内で必要な場合は、 **[はい]** に設定します。 詳細については、「[プロキシ サーバー認証](enable-data-sharing.md#proxy-server-authentication)」をご覧ください。

    - **Desktop Analytics と同期する特定のコレクションを選択します**:ご自分の **[ターゲット コレクション]** 階層のコレクションを追加するには、 **[追加]** を選択します。 これらのコレクションは、Desktop Analytics ポータルで展開計画を使用してグループ化するために使用できます。 パイロット コレクションとパイロット除外コレクションが含まれていることを確認してください。  <!-- 4097528 -->

        > [!IMPORTANT]
        > これらのコレクションは、メンバーシップが変更されても引き続き同期されます。 たとえば、展開計画で、Windows 7 のメンバーシップ規則付きのコレクションを使用するとします。 これらのデバイスが Windows 10 にアップグレードされ、Configuration Manager によってコレクションのメンバーシップが評価されると、これらのデバイスはコレクションと展開計画から削除されます。

### <a name="windows-settings"></a>Windows の設定

Configuration Manager は、デバイスを Desktop Analytics に登録すると、Windows ポリシーを設定して Desktop Analytics 用にデバイスを構成します。 ほとんどの場合、Configuration Manager だけを使ってこれらの設定を構成します。 これらの設定は、ドメイン グループ ポリシー オブジェクトでは適用しないでください。

詳細については、「[Desktop Analytics のグループ ポリシーの設定](group-policy-settings.md)」を参照してください。

### <a name="device-name"></a>デバイス名

Windows 10 バージョン 1803 から、デバイス名は既定では収集されなくなりました。 診断データと共にデバイス名を収集するには、別のオプトインが必要です。 デバイス名がないと、新しいバージョンの Windows へのアップグレードを評価する際に、注意が必要なデバイスを特定するのがより難しくなります。

デバイス名を送信しない場合、Desktop Analytics で "不明" として表示されます。

!["不明" の名前を示す Desktop Analytics のデバイス一覧](media/unknown-device-name.png)

Desktop Analytics でこのオプションを構成するためのオプションが、Configuration Manager 設定にあります: **[診断データでデバイス名を許可する]** です。 この Configuration Manager 設定によって、[Windows のポリシー設定](group-policy-settings.md)の **AllowDeviceNameInTelemetry** が制御されます。

### <a name="conflict-resolution"></a>競合の解決

通常は、構成マネージャー コレクションを使用して、Desktop Analytics の設定と登録の対象を設定します。 コレクションに対してデバイスを含めたり除外したりするには、ダイレクト メンバーシップまたはクエリを使用します。 詳しくは、「[コレクションを作成する方法](../core/clients/manage/collections/create-collections.md)」をご覧ください。

値がまだ存在していない場合にのみ、Configuration Manager によって Windows の設定が構成されます。 一意のデバイス グループに対して異なる設定を構成する必要がある場合は、[グループ ポリシー](group-policy-settings.md)を使用できます。 グループ ポリシーの対象となる設定は、Configuration Manager 設定よりも優先されます。

診断データのレベルを構成する場合は、デバイスに対して上限を設定します。 Windows 10 バージョン 1803 以降の規定では、ユーザーがより低いレベルを設定することを選択できます。 この動作を制御するには、グループ ポリシー設定の **[Configure telemetry opt-in setting user interface]\(テレメトリのオプトイン設定のユーザー インターフェイスを構成する\)** を使用します。 詳細については、「[Desktop Analytics のグループ ポリシーの設定](group-policy-settings.md)」を参照してください。

### <a name="proxy-settings"></a>プロキシの設定

組織でインターネット アクセスにプロキシ サーバー認証を使用している場合は、そのプロキシ サーバー認証またはデバイスを正しく構成する必要があります。 詳細については、「[プロキシ サーバー認証](enable-data-sharing.md#proxy-server-authentication)」をご覧ください。

## <a name="next-steps"></a>次のステップ

次の記事に進み、Desktop Analytics で展開計画を作成します。
> [!div class="nextstepaction"]
> [展開計画を作成する](create-deployment-plans.md)
