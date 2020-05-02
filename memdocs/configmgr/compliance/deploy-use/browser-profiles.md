---
title: Microsoft Edge の設定の構成
titleSuffix: Configuration Manager
description: Windows 10 クライアントで Microsoft Edge Web ブラウザーの設定を構成する
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 91c11e133c74cd3b55db09e8bf80fd6c4df7774d
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210096"
---
# <a name="configure-microsoft-edge-settings-in-configuration-manager"></a>Configuration Manager で Microsoft Edge 設定を構成する

*適用対象:Configuration Manager (Current Branch)*

<!-- 1357310 -->
バージョン 1802 以降、Windows 10 クライアントで [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) Web ブラウザーを使用する場合、Configuration Manager のコンプライアンス設定ポリシーを作成し、Microsoft Edge の一部の設定を構成します。 

このポリシーは、Windows 10 バージョン 1703 以降のクライアントにのみ適用されます。 <!--511552-->


## <a name="policy-settings"></a>ポリシー設定
現在、このポリシーには次の設定が含まれます。
- **[Set Microsoft Edge browser as default]\(Microsoft Edge ブラウザーを既定として設定する\)** : Windows 10 既定アプリの設定で、Web ブラウザーを Microsoft Edge に構成します
- **[アドレス バーのドロップダウンを許可する]** :Windows 10 バージョン 1703 以降が必要です。 詳細については、[AllowAddressBarDropdown ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown)に関する説明を参照してください。
- **Microsoft のブラウザー間でお気に入りの同期を許可する**:Windows 10 バージョン 1703 以降が必要です。 詳細については、[SyncFavoritesBetweenIEAndMicrosoftEdge ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge)に関する説明を参照してください。
- **終了時に閲覧データをクリアすることを許可する**:Windows 10 バージョン 1703 以降が必要です。 詳細については、[ClearBrowsingDataOnExit ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit)に関する説明を参照してください。
- **トラッキング拒否ヘッダーを許可する**:詳細については、[AllowDoNotTrack ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)に関する記事を参照してください。
- **オートコンプリートを使用する**:詳細については、[AllowAutofill ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill)に関する記事を参照してください。
- **Cookie を使用する**:詳細については、[AllowCookies ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)に関する記事を参照してください。
- **ポップアップ ブロックを許可する**:詳細については、[AllowPopups ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)に関する記事を参照してください。
- **アドレス バーで検索候補を許可する**:詳細については、[AllowSearchSuggestionsinAddressBar ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)に関する記事を参照してください。
- **Internet Explorer へのイントラネット トラフィックの送信を許可する**:詳細については、[SendIntranetTraffictoInternetExplorer ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer)に関する記事を参照してください。
- **Password Manager を許可する**:詳細については、[AllowPasswordManager ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)に関する記事を参照してください。
- **開発者ツールを許可する**:詳細については、[AllowDeveloperTools ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools)に関する記事を参照してください。
- **拡張機能を許可する**:詳細については、[AllowExtensions ブラウザー ポリシー](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions)に関する記事を参照してください。


### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Microsoft Edge 用に Windows Defender SmartScreen 設定を構成する
<!--1353701-->
バージョン 1806 以降では、このポリシーにより [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) に 3 つの設定が追加されます。 ポリシーには、 **[SmartScreen の設定]** ページの次の追加設定が含まれるようになりました。

- **SmartScreen を許可する**:Windows Defender SmartScreen を許可するかどうかを指定します。 詳細については、[AllowSmartScreen ブラウザー ポリシー](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)に関するページを参照してください。
- **サイトの SmartScreen プロンプトをユーザーがオーバーライドできる**:悪意のある可能性がある Web サイトに関する Windows Defender SmartScreen フィルターの警告をユーザーがオーバーライドできるかどうかを指定します。 詳細については、[PreventSmartScreenPromptOverride ブラウザー ポリシー](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)に関するページを参照してください。
- **ファイルの SmartScreen プロンプトをユーザーがオーバーライドできる**:確認されていないファイルのダウンロードに関する Windows Defender SmartScreen フィルターの警告をユーザーがオーバーライドできるかどうかを指定します。 詳細については、[PreventSmartScreenPromptOverrideForFiles ブラウザー ポリシー](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)に関するページを参照してください。



## <a name="create-the-microsoft-edge-browser-profile"></a>Microsoft Edge ブラウザー プロファイルを作成する

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動します。 **[コンプライアンス設定]** を展開し、 **[Microsoft Edge ブラウザーのプロファイル]** ノードを選びます。 リボンの **[Microsoft Edge のプロファイルを作成する]** オプションをクリックします。
2. ポリシーの **[名前]** を指定し、必要に応じて **[説明]** を入力してから、 **[次へ]** をクリックします。
3. **[全般設定]** ページで、このポリシーに含める設定の値を **[構成済み]** に変更して、 **[次へ]** をクリックします。 続行するには設定を **[Microsoft Edge ブラウザーを既定として設定する]** に構成する必要があります。
4. バージョン 1806 以降では、 **[SmartScreen の設定]** ページの設定を構成し、 **[次へ]** をクリックします。 
5. **[サポートされているプラットフォーム]** ページで、このポリシーを適用する OS のバージョンとアーキテクチャを選び、 **[次へ]** をクリックします。 
6. ウィザードを完了します。



## <a name="deploy-the-policy"></a>ポリシーを展開する

1. ポリシーを選び、リボンのオプション **[展開]** をクリックします。
2. **[参照]** をクリックして、ポリシーを展開するユーザー コレクションまたはデバイス コレクションを選びます。 
3. 必要に応じて、追加のオプションを選びます。  
     a. ポリシーに準拠していない場合は、アラートを生成します。  
     b. クライアントがこのポリシーについてデバイスのコンプライアンスを評価するスケジュールを設定します。 
4. **[OK]** をクリックして展開を作成します。



## <a name="next-steps"></a>次のステップ

他のコンプライアンス設定ポリシーと同様に、クライアントは指定されたスケジュールで設定を修復します。 Configuration Manager コンソールで、[デバイスのコンプライアンス対応を監視およびレポート](monitor-compliance-settings.md)します。
