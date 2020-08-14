---
title: セルフサービス ポータルのカスタマイズ
titleSuffix: Configuration Manager
description: 組織固有のカスタム情報を BitLocker 管理セルフサービス ポータルに追加する
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 6bc26e36-9914-4606-ae8d-f7b23218942f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 220ebb558a0e01f701cab621381ad951a8fd0738
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88123903"
---
# <a name="customize-the-self-service-portal"></a>セルフサービス ポータルのカスタマイズ

*適用対象:Configuration Manager (Current Branch)*

<!--3601034-->

[BitLocker セルフサービス ポータルをインストール](setup-websites.md)した後に、お客様の組織に合わせてセルフサービス ポータルをカスタマイズできます。 カスタム通知、組織名、およびその他の組織固有の情報を追加します。

## <a name="branding"></a>ブランド化

組織の名前、ヘルプ デスクの URL、通知テキストを使用して、セルフサービス ポータルをブランド化します。

1. セルフサービス ポータルをホストする Web サーバーで、管理者としてサインインします。

1. **インターネット インフォメーション サービス (IIS) マネージャー**を起動します (**inetmgr.exe** を実行します)。

1. **[サイト]** 、 **[既定の Web サイト]** の順に展開し、 **[SelfService]** ノードを選択します。 詳細ウィンドウの **[ASP.NET]** グループで、 **[アプリケーション設定]** を開きます。

    [![IIS マネージャーの SelfService アプリケーション設定のスクリーンショット例](media/bitlocker-self-service-iis-app-settings.png)](media/bitlocker-self-service-iis-app-settings.png#lightbox)

1. 変更する項目を選択し、 **[操作]** ウィンドウで **[編集]** を選択します。 **[値]** を、使用する新しい名前に変更します。

    > [!CAUTION]
    > **[名前]** の値は変更しないでください。 たとえば、`CompanyName` を変更するのではなく、`Contoso IT` を変更します。 **[名前]** の値を変更すると、セルフサービス ポータルが動作しなくなります。

変更は直ちに有効になります。

### <a name="supported-branding-values"></a>サポートされているブランド値

設定できる値については、次の表を参照してください。

|名前|[説明]|Default&nbsp;value|
|--- |--- |--- |
|CompanyName|セルフサービス ポータルで、すべてのページの上部にヘッダーとして表示される組織名。|`Contoso IT`|
|DisplayNotice|ユーザーが確認する必要がある初期通知を表示します。|`true`|
|HelpdeskText|[For all other related issues]\(その他すべての関連する問題\) の下の右ウィンドウに表示される文字列。|`Contact Helpdesk or IT Department`|
|HelpdeskUrl|HelpdeskText 文字列のリンク。|(空)|
|NoticeTextPath|ユーザーが確認する必要がある初期通知のテキスト。 既定では、Web サーバー上の完全なファイル パスは `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt` です。 このファイルを、プレーン テキスト エディターで編集して保存します。 このパス値は、SelfService アプリケーションの相対パスです。|`Notice.txt`|

<!-- Not sure if we support changing these values. At a minimum need a description.
|ClientValidationEnabled||`true`|
|UnobtrusiveJavaScriptEnabled||`true`|
-->

既定のセルフサービス ポータルのスクリーンショットについては、「[BitLocker セルフサービス ポータル](self-service-portal.md)」を参照してください。

> [!TIP]
> 必要に応じて、これらの文字列の一部をローカライズして、異なる言語で表示することができます。 詳細については、「[ローカリゼーション](#bkmk_localize)」を参照してください。

## <a name="session-time-out"></a>セッションのタイムアウト

指定した非アクティブ時間が経過するとユーザーのセッションが期限切れになるようにするには、セルフサービス ポータルのセッション タイムアウト設定を変更します。

1. セルフサービス ポータルをホストする Web サーバーで、管理者としてサインインします。

1. **インターネット インフォメーション サービス (IIS) マネージャー**を起動します (**inetmgr.exe** を実行します)。

1. **[サイト]** 、 **[既定の Web サイト]** の順に展開し、 **[SelfService]** ノードを選択します。 詳細ウィンドウの **[ASP.NET]** グループで、 **[セッション状態]** を開きます。

1. **[Cookie の設定]** グループで、 **[タイムアウト (分)]** の値を変更します。 この分数が経過すると、ユーザーのセッションが期限切れになります。 既定値は `5` です。 タイムアウトが発生しないように設定を無効にするには、値を `0` に設定します。

1. **[操作]** ウィンドウで、 **[適用]** を選択します。

## <a name="localize-helpdesk-text-and-url"></a><a name="bkmk_localize"></a> ヘルプデスクのテキストと URL をローカライズする

セルフサービス ポータルの `HelpdeskText` ステートメントと `HelpdeskUrl` リンクのローカライズされたバージョンを構成できます。 この文字列は、ポータルを使用するときに追加のヘルプを入手する方法をユーザーに通知します。 ローカライズされたテキストを構成すると、その言語の Web ブラウザーにはローカライズされたバージョンがポータルに表示されます。 ローカライズされたバージョンが見つからない場合は、`HelpdeskText` と `HelpdeskUrl` の設定の既定値が表示されます。

1. セルフサービス ポータルをホストする Web サーバーで、管理者としてサインインします。

1. **インターネット インフォメーション サービス (IIS) マネージャー**を起動します (**inetmgr.exe** を実行します)。

1. **[サイト]** 、 **[既定の Web サイト]** の順に展開し、 **[SelfService]** ノードを選択します。 詳細ウィンドウの **[ASP.NET]** グループで、 **[アプリケーション設定]** を開きます。

1. **[操作]** ウィンドウで、 **[追加]** を選択します。

1. **[アプリケーション設定の追加]** ウィンドウで、次の値を構成します。

    - **名前**: 「`HelpdeskText_<language>`」と入力します。ここで、`<language>` はそのテキストの言語コードです。

      たとえば、スペイン語 (スペイン) でローカライズされた `HelpdeskText` ステートメントを作成する場合、名前は `HelpdeskText_es-es` になります。

    - **値**: [For all other related issues]\(その他すべての関連する問題\) の下の、セルフサービス ポータルの右ウィンドウに表示されるローカライズされた文字列。

1. **[OK]** を選択して、新しい設定を保存します。

1. この手順を繰り返して、関連する `HelpdeskText_<language>` 設定と一致する `HelpdeskUrl_<language>` の新しいアプリケーション設定を追加します。

組織でサポートするすべての言語について、この手順を繰り返して、設定のペアを追加します。

## <a name="localize-the-notice-file"></a>通知ファイルをローカライズする

セルフサービス ポータルでユーザーが確認する必要がある初期通知のローカライズされたバージョンを構成できます。 既定では、Web サーバー上の完全なファイル パスは `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt` です。

ローカライズされた通知テキストを表示するには、ローカライズされた notice.txt ファイルを作成します。 次に、このファイルを特定の言語フォルダーに保存します。 たとえば、スペイン語 (スペイン) の場合は、`Self Service Website\es-es\Notice.txt` です。

セルフサービス ポータルでは、次のルールに基づいて通知テキストが表示されます。

- 既定の通知ファイルがない場合は、既定のファイルがないことを示すメッセージがポータルに表示されます。

- ローカライズされた通知ファイルを適切な言語フォルダーに作成すると、ローカライズされた通知テキストが表示されます。

- Web サーバーがローカライズされたバージョンの通知ファイルを見つけられない場合は、既定の通知が表示されます。

- ユーザーのブラウザーが、ローカライズされた通知が存在しない言語に設定されている場合は、既定の通知がポータルに表示されます。

### <a name="create-a-localized-notice-file"></a>ローカライズされた通知ファイルを作成する

1. セルフサービス ポータルをホストする Web サーバーで、管理者としてサインインします。

1. `Self Service Website` アプリケーション パスに、サポートされている言語ごとに `<language>` フォルダーを作成します。 たとえば、スペイン語 (スペイン) の場合は、`es-es` を作成します。 既定では、完全なパスは `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es` です。

    使用できる言語コードの一覧については、「[各国語サポート (NLS) API リファレンス](https://docs.microsoft.com/windows/win32/intl/locale-identifiers#predefined-locale-identifiers)」を参照してください。

    > [!TIP]
    > 言語フォルダーの名前は、言語に依存しない名前にすることもできます。 たとえば、スペイン語 (スペイン ) の **es-es** や、スペイン語 (アルゼンチン) の **es-ar** の代わりに、スペイン語に **es** を使用できます。 ユーザーが **es**にブラウザーを設定し、その言語フォルダーが存在しない場合、web サーバーは親のロケールフォルダー (**es**) を再帰的に確認します。 (親ロケールは .NET で定義されています)。たとえば、`Self Service Website\es\Notice.txt` のようになります。 この再帰的フォールバックは、.NET リソースの読み込みルールを模倣します。

1. ローカライズされたテキストを含む、既定の通知ファイルのコピーを作成します。 このファイルを、その言語コードのフォルダーに保存します。 たとえば、スペイン語 (スペイン) の場合の完全なパスは、既定では `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es\Notice.txt` です。

組織でサポートするすべての言語について、この手順を繰り返して、ローカライズされた通知ファイルを作成します。

## <a name="next-steps"></a>次のステップ

これで、セルフサービス ポータルのインストールとカスタマイズが完了しました。お試しください。 詳細については、「[BitLocker セルフサービス ポータル](self-service-portal.md)」を参照してください。
