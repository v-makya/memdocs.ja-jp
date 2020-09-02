---
title: macOS アプリにポータル サイトを追加する
titleSuffix: Microsoft Intune
description: macOS のポータル サイト アプリを追加します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/16/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1eb64f8ed2bc67b4800a4583010dea150ade421d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914159"
---
# <a name="add-the-macos-company-portal-app"></a>macOS のポータル サイト アプリを追加します

ユーザーが、ユーザー アフィニティがある macOS デバイスをデバイス管理し、オプション アプリをインストールし、条件付きアクセスで保護されたリソースにアクセスするには、ポータル サイト アプリをインストールし、それにサインインする必要があります。 これには、macOS のポータル サイトをインストールするようご自分のユーザーに指示するか、既に Intune に直接登録されているデバイスにそれをインストールする必要があります。

macOS のアプリにポータル サイトをインストールするには、以下のいずれかの方法を使用します。
- [ユーザーにポータル サイトをダウンロードしてインストールするよう指示する](#instruct-users-to-download-and-install-company-portal)
- [macOS の LOB アプリとして macOS のポータル サイトをインストールする](#install-company-portal-for-macos-as-a-macos-lob-app)
- [macOS のシェル スクリプトを使用して macOS のポータル サイトをインストールする](#install-company-portal-for-macos-by-using-a-macos-shell-script)

ポータル サイト アプリには、一度インストールしたアプリのセキュリティを強化し、最新の状態に保つ Microsoft AutoUpdate (MAU) が付属しています。

> [!NOTE]
> ポータル サイト アプリは、直接登録またはデバイスの自動登録を使用して既に登録されている Intune を使用しているデバイスにのみ、自動的にインストールできます。 個人のデバイスの場合、または手動で登録されたものである場合、ポータル サイト アプリはダウンロードしてインストールし、登録を開始する必要があります。 「[ユーザーにポータル サイトをダウンロードしてインストールするよう指示する](#instruct-users-to-download-and-install-company-portal)」を参照してください。
## <a name="instruct-users-to-download-and-install-company-portal"></a>ユーザーにポータル サイトをダウンロードしてインストールするよう指示する

ユーザーに、macOS 用のポータル サイトをダウンロード、インストール、サインインするように指示することができます。 ポータル サイトのダウンロード、インストール、サインインの手順については、「[ポータル サイト アプリを使用して macOS デバイスを登録する](../user-help/enroll-your-device-in-intune-macos-cp.md)」を参照してください。

##  <a name="install-company-portal-for-macos-as-a-macos-lob-app"></a>macOS の LOB アプリとして macOS のポータル サイトをインストールする

macOS のポータル サイトは、[macOS の LOB アプリ](lob-apps-macos.md)機能を使用してダウンロードおよびインストールできます。 ダウンロードされるバージョンは、常にインストールされるバージョンであり、ユーザーが初回登録時に確実に最適なエクスペリエンスを得られるように、定期的に更新される必要がある場合があります。

1. macOS のポータル サイトは、 https://go.microsoft.com/fwlink/?linkid=853070 からダウンロードできます。 

2. macOS の LOB アプリの作成手順については、[macOS の LOB アプリ](lob-apps-macos.md)に関する説明を参照してください。

> [!NOTE]
> 一度インストールされると、macOS アプリのポータル サイトは Microsoft AutoUpdate (MAU) を使用して自動的に更新されます。
## <a name="install-company-portal-for-macos-by-using-a-macos-shell-script"></a>macOS のシェル スクリプトを使用して macOS のポータル サイトをインストールする

macOS のポータル サイトは、[macOS のシェル スクリプト](macos-shell-scripts.md)機能を使用してダウンロードおよびインストールできます。 このオプションでは、常に macOS の最新バージョンのポータル サイトがインストールされますが、[macOS の LOB アプリ](lob-apps-macos.md)でアプリケーションを展開するときに通常提供されるアプリケーションのインストール レポートは提供されません。

1. macOS 用のポータル サイトをインストールするサンプル スクリプトは、[Intune シェル スクリプトのサンプル - ポータルサイト](https://github.com/microsoft/shell-intune-samples/tree/master/Apps/Company%20Portal)に関するページからダウンロードしてください。

2. macOS のシェル スクリプトを展開するには、[macOS のシェル スクリプト](macos-shell-scripts.md)に関する説明を使用します。 
    - **[サインインしたユーザーとしてスクリプトを実行する]** を **[いいえ]** に設定し (システム コンテキストで実行し) ます。
    - **[Maximum number of retries if script fails]** \(スクリプトが失敗した場合の再試行回数の最大値\) を **3** に設定します。

> [!NOTE]
> このスクリプトでは、macOS 用の現在のバージョンのポータル サイトのダウンロードに、インターネット アクセスを必要です。 
## <a name="next-steps"></a>次のステップ
- アプリの割り当てに関する詳細については、[グループへのアプリの割り当て](apps-deploy.md)に関するページを参照してください。
- デバイスの自動登録の構成の詳細については、[Device Enrollment Program - macOS の登録](../enrollment/device-enrollment-program-enroll-macos.md)に関する説明を参照してください。
- macOS で Microsoft AutoUpdate の設定を構成する方法の詳細については、[Mac の更新プログラム](/windows/security/threat-protection/microsoft-defender-atp/mac-updates)に関するページを参照してください。