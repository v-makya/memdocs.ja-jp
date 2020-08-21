---
title: Windows デバイスを別のバージョンにアップグレードする
titleSuffix: Configuration Manager
description: Windows 10 デバイスを別の Windows エディションに自動的にアップグレードするには、Configuration Manager を使用します。
ms.date: 07/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 920f3c9aabcdec1242a6f5e5fc8e6b65c5cc0b53
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694612"
---
# <a name="upgrade-windows-devices-to-a-new-edition-with-configuration-manager"></a>Configuration Manager による Windows デバイスの新しいエディションへのアップグレード

*適用対象:Configuration Manager (Current Branch)*

**エディションのアップグレード ポリシー**では、異なるエディションに Windows 10 デバイスを自動的にアップグレードできます。

次のアップグレード パスがサポートされます。

- Windows 10 Pro から Windows 10 Enterprise
- Windows 10 Home から Windows 10 Education
- Windows 10 Mobile から Windows 10 Mobile Enterprise へのアップグレード パス

デバイスは、構成マネージャー クライアント ソフトウェアを実行する必要があります。 [オンプレミスの MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) によって管理されているデバイスはサポートされていません。

## <a name="before-you-start"></a>開始する前に

デバイスを最新バージョンにアップグレードし始める前に、次の前提条件を確認する必要があります。  

- Windows 10 のデスクトップ エディションの場合:ポリシーの対象とするすべてのデバイスでの Windows の新しいバージョンに対する有効なプロダクト キー。 このプロダクト キーは、マルチ ライセンス認証キー (MAK) または汎用ボリューム ライセンス キー (GVLK) でもかまいません。 GVLK は、キー管理サービス (KMS) クライアント セットアップ キーとも呼ばれます。 詳細については、「[ボリューム ライセンス認証の計画](/windows/deployment/volume-activation/plan-for-volume-activation-client)」を参照してください。 KMS クライアント セットアップ キーの一覧については、Windows Server のライセンス認証ガイドの「[付録 A](/windows-server/get-started/kmsclientkeys)」を参照してください。 <!--496871-->  

- Windows 10 Mobile の場合:Microsoft ボリューム ライセンス サービス センター (VLSC) から入手した XML ライセンス ファイル。 このファイルには、ポリシーの対象とするすべてのデバイスでの Windows の新しいバージョンに対するライセンス情報が含まれます。 ライセンス XML を含む **Windows 10 Mobile Enterprise** 用の ISO ファイルをダウンロードします。<!-- SCCMDocs#2033 -->

- この種類のポリシーを管理するには、Configuration Manager の**完全な権限を持つ管理者**のセキュリティ ロールである必要があります。

## <a name="configure-the-policy"></a>ポリシーを構成する  

1. Configuration Manager コンソールで **[資産とコンプライアンス]** ワークスペースに移動し、 **[コンプライアンス設定]** を展開して、 **[Windows 10 エディションのアップグレード]** ノードを選択します。  

2. リボンの **[ホーム]** タブの **[作成]** グループで、 **[エディション アップグレード ポリシーの作成]** を選択します。  

3. **[ポリシーを作成する]** を選択します。  

4. **エディション アップグレード ポリシーの作成ウィザード** の **[全般]** ページで、次の情報を指定します。  

    - **名前** - エディションのアップグレード ポリシーの名前を入力します  

    - **[説明]** (省略可能) - 必要に応じて、Configuration Manager コンソールで識別に役立ちそうなポリシーの説明を入力します  

    - **デバイスを以下のようにアップグレードする SKU** - ドロップダウン リストから、Windows 10 デスクトップまたは Windows 10 Mobile の対象エディションを選びます  

    - **ライセンス情報** - 次のいずれかのオプションを 1 つ選択します。  

        - **プロダクト キー** - 対象の Windows 10 デスクトップ エディションの有効なプロダクト キーを入力します  

            > [!NOTE]  
            > プロダクト キーを含むポリシーを作成した後でプロダクト キーを編集することはできません。 セキュリティ上の理由からキーは表示されません。 プロダクト キーを変更するには、キー全体を再入力します。  

        - **ライセンス ファイル** - **[参照]** を選択して、XML 形式の有効なライセンス ファイルを選びます。 Configuration Manager はこのライセンス ファイルを使って、Windows 10 Mobile デバイスをアップグレードします。  

5. ウィザードを完了します。  

## <a name="deploy-the-policy"></a>ポリシーを展開する  

1. Configuration Manager コンソールで **[資産とコンプライアンス]** ワークスペースに移動し、 **[コンプライアンス設定]** を展開して、 **[Windows 10 エディションのアップグレード]** ノードを選択します。  

2. 展開する Windows 10 エディションのアップグレード ポリシーを選択します。 リボンの **[ホーム]** タブの **[展開]** グループで、 **[展開]** を選択します。  

3. ポリシーを展開するデバイス コレクションを選択します。

4. クライアントがポリシーを評価するスケジュールを選びます。

5. ウィザードを完了します。

## <a name="next-steps"></a>次のステップ

**[監視]** ワークスペースの **[展開]** ノードから、この展開を監視します。 展開失敗を示す次のようなエラーが表示される場合があります。

- **このデバイスには該当しません**
- **データ型を変換できませんでした**

これらのエラーは、展開が失敗したことを意味しているわけではありません。 対象のデバイスで、アップグレードが正常に実行されたことを確認してください。

クライアントでは、対象ポリシーを評価した後、2 時間以内にアップグレードが適用されます。 [Windows の一部のバージョン](/windows/deployment/upgrade/windows-10-edition-upgrades)では、その時点で再起動が必要になる場合があります。 ポリシーを展開するすべてのユーザーに通知するか、ポリシーの実行をユーザーの業務時間外にスケジュール設定します。

クライアントの **DcmWmiProvider.log** に次のエラーが記録される場合は、ライセンス認証シナリオに対して適切なキーを使っていることを確認します。 詳細については、「[開始する前に](#before-you-start)」セクションを参照してください。 ライセンス認証にキー管理サービス (KMS) を使っている場合は、必ず [KMS クライアント セットアップ キー](/windows-server/get-started/kmsclientkeys)を使うようにしてください。  <!-- 496871 -->

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`

## <a name="see-also"></a>関連項目

- [ボリューム ライセンス認証の計画](/windows/deployment/volume-activation/plan-for-volume-activation-client)

- [Windows 10 エディションのアップグレード](/windows/deployment/upgrade/windows-10-edition-upgrades)

- [Microsoft Intune を使用してデバイス上の Windows 10 エディションをアップグレードするか S モードから切り替える](/intune/edition-upgrade-configure-windows-10)