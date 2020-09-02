---
title: Intune 用 Microsoft Defender ウイルス対策の macOS ウイルス対策ポリシーの設定 | Microsoft Docs
description: macOS の Microsoft Defender ウイルス対策プロファイルの設定一覧を参照してください。 このプロファイルは、Microsoft Intune の macOS のエンドポイント セキュリティ ウイルス対策ポリシーの一部です。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: samyada
ms.openlocfilehash: a75fe5bac4bb99b30e21ec842dcbbe3be83e9e5b
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909450"
---
# <a name="settings-for-microsoft-defender-atp-for-mac-in-microsoft-intune"></a>Microsoft Intune での Microsoft Defender ATP for Mac の設定

Microsoft Intune で、Mac 用の Microsoft Defender ATP 用に構成できる "*ウイルス対策*" プロファイル設定を確認します。 これらの設定の詳細については、Windows ドキュメントの「[Microsoft Defender Advanced Threat Protection for Mac](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)」を参照してください。

Intune で[エンドポイント セキュリティ ポリシー](../protect/endpoint-security-policy.md)を使用する方法について説明します。

**Microsoft Defender ATP**

- **リアルタイム保護**  
  リアルタイム監視機能を使用するには、macOS デバイス上に Defender が必要です。 リアルタイム監視を使用すると、マルウェアが検出され、デバイス上でインストールまたは実行されなくなります。 この設定を短時間オフにして、自動的にオンに戻すことができます。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます
  - **有効** - リアルタイム監視の使用を強制します。 デバイス ユーザーはこの設定を変更できません。
  - **無効** - この設定は無効になります。 デバイス ユーザーはこの設定を変更できません。

- **Cloud-delivered protection (クラウドによる保護)**  
  既定では、Defender から、検出された問題に関する情報が Microsoft に送信されます。 Microsoft ではその情報を分析し、お客様や他のユーザーに影響する問題の詳細を把握して、改善されたソリューションを提供しています。 *[サンプルの自動送信]* がオンに設定されている場合に保護は最適に機能します。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **有効** - クラウドで提供される保護が有効になります。 デバイス ユーザーはこの設定を変更できません。
  - **無効** - この設定は無効になります。 デバイス ユーザーはこの設定を変更できません。

- **サンプルの自動送信**  
  デバイス ユーザーと組織を潜在的な脅威から保護するため、Microsoft にサンプル ファイルを送信します。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **有効** - クラウドで提供される保護が有効になります。  デバイス ユーザーはこの設定を変更できません。
  - **無効** - この設定は無効になります。 デバイス ユーザーはこの設定を変更できません。

- **診断データ コレクション**

  診断結果と使用状況データを Microsoft と共有する方法を構成します。

  - **未構成** (*既定値*) - 設定はシステムの既定値に復元されます。
  - **必須**
  - **省略可能**

- **Folders excluded from scan (スキャンから除外されるフォルダー)**  
  **[追加]** を選択し、スキャン中に無視するフォルダーを指定します。

- **Files excluded from scan (スキャンから除外されるファイル)**  
  **[追加]** を選択し、スキャン中に無視するファイルを指定します。

- **File types excluded from scan (スキャンから除外されるファイルの種類)**  
  **[追加]** を選択し、スキャン中に無視するファイルの拡張子を指定します。

- **Processes excluded from scan (スキャンから除外されるプロセス)**  
  **[追加]** を選択し、スキャン中に無視するプロセスを指定します。