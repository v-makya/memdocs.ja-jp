---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 08/24/2020
ms.openlocfilehash: ff48e8117437e45be42551ebffff7cdcf5bce184
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820301"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
以下のプロファイルは、テナントのアタッチ シナリオを通じて、Configuration Manager Current Branch 2006 以降で管理するデバイスについてサポートされています。
<!--The following profiles are supported for devices you manage with Configuration Manager Technical Preview 2007 or later, through the tenant attach scenario:-->

- プラットフォーム:**Windows 10 および Windows Server**

  - プロファイル:**Microsoft Defender ウイルス対策ポリシー (ConfigMgr)**
  
    テナントのアタッチを使用する場合は、[Configuration Manager デバイスの ウイルス対策ポリシー設定](../../protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md)を管理します。

    このプロファイルは、テナントがアタッチされ、次のプラットフォームを実行するデバイスでサポートされています。
    - Windows 10 以降 (x86、x64、ARM64)
    - Windows 8.1 (x84、x64)
    - Windows Server 2019 以降 (x64)
    - Windows server 2016 (x64)
    - Windows Server 2012 R2 (x64)
    - Windows Server 2008 R2 SP1 (x64)
