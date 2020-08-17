---
title: macOS デバイスの登録をセットアップする
titleSuffix: Microsoft Intune
description: Intune で macOS デバイスの登録をセットアップする方法について説明します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/12/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 46429114-2e26-4ba7-aa21-b2b1a5643e01
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c0973805a0646ec7df87f36eea183a9456f7e39
ms.sourcegitcommit: 2ee50bfc416182362ae0b8070b096e1cc792bf68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87865508"
---
# <a name="set-up-enrollment-for-macos-devices-in-intune"></a>Intune で macOS デバイスの登録をセットアップする

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune を使用すると、macOS デバイスを管理して、会社の電子メールやアプリへのアクセスをユーザーに提供できます。

Intune 管理者は、会社所有の macOS デバイスと個人所有の macOS デバイス ("bring your own device" すなわち BYOD) の登録を設定できます。 

## <a name="prerequisites"></a>[前提条件]

macOS デバイスの登録を設定する前に、以下の前提条件を満たしている必要があります。

- [デバイスが Apple デバイス登録の対象であることを確認します](https://support.apple.com/en-us/HT204142#eligibility)。
- [ドメインを構成する](../fundamentals/custom-domain-name-configure.md)
- [MDM 機関を設定する](../fundamentals/mdm-authority-set.md)
- [グループの作成](../fundamentals/groups-add.md)
- [ポータル サイト アプリを構成する](../apps/company-portal-app.md)
- [Microsoft 365 管理センター](https://go.microsoft.com/fwlink/p/?LinkId=698854)でユーザー ライセンスを割り当てる
- [Apple MDM プッシュ証明書を取得する](../enrollment/apple-mdm-push-certificate-get.md)

## <a name="user-owned-macos-devices-byod"></a>ユーザー所有の macOS デバイス (BYOD)

ユーザーが自分の個人用デバイスを Intune の管理に登録できるようにすることができます。 これは、"Bring Your Own Device" または BYOD と呼ばれます。 前提条件を満たし、ユーザー ライセンスを割り当てたら、ユーザーは次の方法で各自のデバイスを登録できます。
- [ポータル サイト Web サイト](https://portal.manage.microsoft.com)にアクセスする、または
- [aka.ms/EnrollMyMac](https://aka.ms/EnrollMyMac) で Mac ポータル サイト アプリをダウンロードする

また、オンライン登録手順へのリンクをユーザーに送信することもできます。(「[Intune に macOS デバイスを登録する](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp)」) へのリンクを送信することもできます。

その他のエンドユーザー タスクの詳細については、次の記事を参照してください。

- [Microsoft Intune を使用したエンドユーザー エクスペリエンスに関するリソース](../fundamentals/end-user-educate.md)
- [macOS デバイスを Intune で使用する](../user-help/enroll-your-device-in-intune-macos-cp.md)

## <a name="company-owned-macos-devices"></a>会社所有の macOS デバイス
Intune は、ユーザーのデバイスを購入する組織のため、次の会社所有の macOS デバイスの登録方法をサポートします。
- [Apple の自動デバイス登録 (ADE)](device-enrollment-program-enroll-macos.md): 組織は ADE から macOS デバイスを購入できます。 ADE では、登録プロファイルを "無線で" 展開して、デバイスを管理対象にすることができます。
- [デバイス登録マネージャー (DEM)](device-enrollment-manager-enroll.md):DEM アカウントを使用して、最大で 1,000 台のデバイスを登録できます。
- [直接登録](device-enrollment-direct-enroll-macos.md): 直接登録では、デバイスはワイプされません。

## <a name="block-macos-enrollment"></a>macOS の登録をブロックする
既定では、Intune で macOS デバイスを登録できます。 macOS デバイスの登録をブロックする場合は、「[Set device type restrictions](enrollment-restrictions-set.md)」 (デバイスの種類の制限を設定する) を参照してください。

## <a name="enroll-virtual-macos-machines-for-testing"></a>テスト用に仮想 macOS マシンを登録する

> [!NOTE]
> macOS 仮想マシンは、テスト目的でのみサポートされます。 macOS 仮想マシンをエンドユーザーの実稼働デバイスとして使用しないでください。 

テスト目的の macOS 仮想マシンは、Parallels Desktop または VMware Fusion のいずれかを使用して登録することができます。 

Parallels Desktop の場合、Intune が認識できるように、ハードウェアの種類と仮想マシンのシリアル番号を設定する必要があります。 ハードウェアの種類と[シリアル番号](http://kb.parallels.com/123455)の設定に関する Parallels の指示に従って、テストに必要な設定を行います。 仮想マシンを実行しているデバイスのハードウェアの種類と、作成している仮想マシンのハードウェアの種類とを一致させることをお勧めします。 このハードウェアの種類は、 **[アップル メニュー]**  >  **[この Mac について]**  >  **[システム レポート]**  >  **[機種 ID]** で調べることができます。 

VMware Fusion の場合、[.vmx ファイルを編集して](https://kb.vmware.com/s/article/1014782)、仮想マシンのハードウェア モデルとシリアル番号を設定する必要があります。 仮想マシンを実行しているデバイスのハードウェアの種類と、作成している仮想マシンのハードウェアの種類とを一致させることをお勧めします。 このハードウェアの種類は、 **[アップル メニュー]**  >  **[この Mac について]**  >  **[システム レポート]**  >  **[機種 ID]** で調べることができます。 

## <a name="user-approved-enrollment"></a>ユーザー承認済みの登録

ユーザー承認済みの MDM 登録は、セキュリティ上重要な特定の設定を管理するために使用できる macOS の登録の種類です。 詳しくは、[Apple のサポート ドキュメント](https://support.apple.com/HT208019)をご覧ください。  
 
2020 年 6 月の時点では、自動デバイス登録 (ADE) によって実行されていないものを含む、Intune の新しい macOS MDM 登録はすべて、ユーザーが承認したものと見なされます。 エンド ユーザーは、 **[システム環境設定]**  >  **[プロファイル]** で管理プロファイルを手動でインストールし、管理プロファイルの承認を行う必要があります。 システム環境設定は、BYOD の macOS ユーザー用のポータル サイト アプリから自動的に起動されます。 [管理プロファイルをインストールする手順](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp)は、ポータル サイト アプリで提供されます。     

2020 年 6 月より前の BYOD の macOS MDM 登録は、エンド ユーザーが **[システム環境設定]**  >  **[プロファイル]** で管理プロファイルを手動で承認しなかった場合、ユーザーは承認されない可能性があります。 2020 年 6 月より後の BYOD 登録の場合、ポータル サイト アプリによって、ユーザー用の **[システム環境設定]** が起動され、ユーザーは [インストール] を選択する必要があります。 登録時に管理プロファイルを承認しなかった場合、ユーザーは **[システム環境設定]**  >  **[プロファイル]** に移動し、管理プロファイルを選択して **[承認]** を選択し、後でプロファイルを承認できます。

### <a name="find-out-if-a-device-is-user-approved"></a>デバイスがユーザー承認済みかどうかを確認する
1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[すべてのデバイス]** の順に選択してデバイスを選択し、 **[ハードウェア]** を選択します。
3. **[ユーザー承認済み登録]** フィールドを確認します。


## <a name="next-steps"></a>次のステップ

macOS デバイスを登録したら、[macOS デバイスのカスタム設定を作成](../configuration/custom-settings-macos.md)できます。
