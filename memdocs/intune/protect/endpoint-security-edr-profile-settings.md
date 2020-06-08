---
title: Intune のエンドポイント セキュリティのエンドポイントの検出と応答設定 |Microsoft Docs
description: Microsoft Intune のエンドポイント セキュリティのエンドポイントの検出と応答ポリシー設定
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/22/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: dd53ec47435ba9dc416d2b152719b393d1647f90
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83823998"
---
# <a name="endpoint-detection-and-response-policy-settings-for-endpoint-security-in-intune"></a>Intune のエンドポイント セキュリティのエンドポイントの検出と応答ポリシー設定

Intune のエンドポイント セキュリティ ノードにある[エンドポイントの検出と応答ポリシー](../protect/endpoint-security-edr-policy.md)のプロファイルで構成できる設定を確認します。

サポートされているプラットフォームとプロファイルは、次のとおりです。

- **Windows 10 以降**:Intune で管理されているデバイスに展開するポリシーには、このプラットフォームを使用します。
  - プロファイル:**エンドポイントの検出と応答 (MDM)**

- **Windows 10 および Windows Server**:Configuration Manager で管理されているデバイスに展開するポリシーには、このプラットフォームを使用します。
  - プロファイル:**エンドポイントの検出と応答 (ConfigMgr) (プレビュー)**
  
  *このプラットフォームとプロファイルは、パブリック プレビュー段階です*。

## <a name="endpoint-detection-and-response-mdm"></a>エンドポイントの検出と応答 (MDM)

**エンドポイントの検出と応答**:

- **Microsoft Defender ATP クライアント構成パッケージの種類**

  Microsoft Defender ATP クライアントのオンボードに使用する署名付き構成パッケージをアップロードします。

  - **[未構成]** ("*既定値*")
  - **Onboarding blob (オンボード BLOB)**  
  - **Offboarding blob (オフボード BLOB)**  

  *[Onboarding blob] (オンボード BLOB)* に設定すると、次の設定を構成できます。

  - **Advanced threat protection onboarding blob (Advanced Threat Protection のオンボード BLOB)**  
    **[Select onboarding file] (オンボード ファイルを選択する)** をクリックして *[Select onboarding File] (オンボード ファイルの選択)* ウィンドウを開き、`.onboarding` ファイルを指定します。

  *[Offboarding blob] (オフボード BLOB)* に設定すると、次の設定を構成できます。
  
  - **Advanced threat protection offboarding blob (Advanced Threat Protection のオフボード BLOB)**  
     **[Select offboarding file] (オフボード ファイルを選択する)** をクリックして *[Select offboarding File] (オフボード ファイルの選択)* ウィンドウを開き、`.offboarding` ファイルを指定します。

- **すべてのファイルのサンプル共有**:  

  Microsoft Defender Advanced Threat Protection サンプル共有の構成パラメーターを返すか設定します。  
  - **未構成** (*既定値*)
  - **あり**

- **テレメトリの報告頻度を早める**:

  - **未構成** (*既定値*)
  - **はい** - Microsoft Defender Advanced Threat Protection テレメトリの報告頻度を増やします。

## <a name="endpoint-detection-and-response-configmgr-preview"></a>エンドポイントの検出と応答 (ConfigMgr) (プレビュー)

**エンドポイントの検出と応答**:

- **すべてのファイルのサンプル共有**:  

  Microsoft Defender Advanced Threat Protection サンプル共有の構成パラメーターを返すか設定します。  
  - **未構成** (*既定値*)
  - **あり**

- **テレメトリの報告頻度を早める**:

  - **未構成** (*既定値*)
  - **はい** - Microsoft Defender Advanced Threat Protection テレメトリの報告頻度を増やします。

## <a name="next-steps"></a>次のステップ

[EDR のエンドポイント セキュリティ ポリシー](../protect/endpoint-security-edr-policy.md)
