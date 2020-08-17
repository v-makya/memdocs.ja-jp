---
title: macOS デバイスの直接登録の使用
titleSuffix: Microsoft Intune
description: 直接登録を使用して macOS デバイスを登録する方法について説明します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/04/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: scottbreenmsft
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1f12b90dd49dc9a9783a39fb78d74c40c6838b1e
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2020
ms.locfileid: "87819973"
---
# <a name="use-direct-enrollment-for-macos-devices"></a>macOS デバイスの直接登録の使用

Intune によって、会社のデバイスについて、直接登録 (DE) を使用した macOS デバイスの登録がサポートされています。 直接登録では、デバイスはワイプされません。 デバイスは macOS 設定を介して登録されます。 この方法は、**ユーザー アフィニティなし**のデバイスのみに使用できます。

## <a name="prerequisites"></a>必須コンポーネント

- macOS デバイスへの物理的なアクセス
- [MDM 機関の設定](../fundamentals/mdm-authority-set.md)
- [Apple MDM プッシュ証明書](apple-mdm-push-certificate-get.md)
 - 登録する macOS デバイスの管理者権限

## <a name="create-an-apple-configurator-profile-for-devices"></a>デバイスの Apple Configurator プロファイルを作成する

デバイス登録プロファイルで、登録時に適用する設定を定義します。 これらの設定は、1 回だけ適用されます。 直接登録を使用して macOS デバイスを登録するための登録プロファイルを作成するには、次の手順に従います。

1. [Microsoft エンドポイント マネージャー管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[デバイス]**  >  **[デバイスの登録]**  >  **[Apple の登録]**  >  **[Apple Configurator]** の順に選択します。

2. **[プロファイル]**  >  **[作成]** を選択します。

3. **[登録プロファイルの作成]** で、管理用にプロファイルの **[名前]** と **[説明]** を入力します。 ユーザーにはこれらの詳細は表示されません。 この [名前] フィールドを使用して、Azure Active Directory で動的グループを作成できます。 この登録プロファイルに対応するデバイスを割り当てるために enrollmentProfileName パラメーターを定義する場合はプロファイル名を使用します。 Azure Active Directory の動的グループの詳細についてはこちらを参照してください。

4. **[ユーザー アフィニティ]** で、 **[ユーザー アフィニティなしで登録する]** を選択します。このオプションは、1 人のユーザーに関連付けられていないデバイスの場合に選択します。 ローカルのユーザー データにアクセスせずにタスクを実行するデバイスで使用します。 ユーザー アフィリエーションが必要なアプリ (基幹業務アプリのインストールに使用されるポータル サイト アプリを含む) は機能しません。 直接登録の場合は必須です。

     > [!NOTE]
     > 直接登録を使用する場合、 **[ユーザー アフィニティとともに登録する]** は macOS ではサポートされていません。 ユーザー アフィニティが必要なデバイスの場合は、自動デバイス登録を使用します。

6. **[作成]** を選択してプロファイルを保存します。

## <a name="direct-enrollment"></a>直接登録
直接登録では、ユーザー アフィニティなしの登録のみがサポートされるため、ポータル サイトを使用して、使用可能なアプリケーションをインストールすることはできません。

### <a name="export-the-profile-and-install-on-macos-devices"></a>macOS デバイスにプロファイルをエクスポートしてインストールする

1. [Microsoft エンドポイント マネージャー管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)で、 **[デバイス]**  >  **[デバイスの登録]**  >  **[Apple の登録]**  >  **[Apple Configurator]**  >  **[プロファイル]** の順に選択し、エクスポートするプロファイルを選択して **[プロファイルのエクスポート]** を選択します。
2. **[直接登録]** で、 **[プロファイルのダウンロード]** を選択して、ファイルを保存します。 

     > [!NOTE]
     > ダウンロードした登録プロファイルは、ダウンロードしてから 2 週間有効です。 このリンクを使用して、必要な数の登録プロファイルをダウンロードできます。 新しいプロファイルをダウンロードしても、以前のものは無効にはされませんが、以前にダウンロードしたファイルの有効期限が延長されることもありません。
         
3. ファイルを macOS コンピューターに転送して、直接インストールします。
4. 保存された **.mobileconfig** をダブルクリックして、プロファイルでファイルを開きます。
5. 管理プロファイルのインストールを求めるメッセージが表示されたら、 **[インストール]** を選択します。
6. 次のプロンプトで、 **[インストール]** を選択して、管理プロファイルをインストールすることを確認します。
7. macOS デバイスの管理者アカウントの資格情報を入力し、 **[OK]** をクリックします。
8. これで macOS デバイスが Intune に登録され、管理されるようになりました。対象のプロファイルのダウンロードが開始されます。

## <a name="next-steps"></a>次のステップ

macOS デバイスを登録したら、[それらの管理](../remote-actions/device-management.md)を開始できます。