---
title: グループ ポリシーを使用して Endpoint Protection を管理する
titleSuffix: Configuration Manager
description: グループ ポリシーを使用して Endpoint Protection を管理する方法を説明します。
ms.date: 08/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6c43ca9e1007c62835015a8c26a478af7da34ebb
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2020
ms.locfileid: "87819994"
---
# <a name="use-group-policy-settings-to-manage-endpoint-protection-in-previous-versions-of-windows"></a>グループ ポリシー設定を使用して、以前のバージョンの Windows で Endpoint Protection を管理する

**適用対象:**

- [Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP)](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE2O8jv)
- 次の下位レベルのデバイス上の System Center Endpoint Protection:
    - Windows Server 2012 R2
    - Windows 8.1
    - Windows Server 2012
    - Windows 8
    - Windows Server 2008 R2 SP1
    - Windows 7 SP1
    - Windows Server 2008 SP2
    - Windows Vista

場合によっては、Endpoint Protection により有効化されているが、Configuration Manager 階層の外に存在する下位レベルまたは従来の Windows デバイスが多数あることがあります。 たとえば、非武装地帯内のデバイスや、合併や買収によって統合されたデバイスなどです。 

このようなデバイスでは、以下のように、グループ ポリシー設定を使用して Endpoint Protection を管理できます。

- [Endpoint Protection ポリシー定義をコピーする](#copy-endpoint-protection-policy-definitions)
- Endpoint Protection ポリシー定義を次の場所に読み込みます。
    - [ドメイン コントローラー上のセントラル ストア (推奨)](#load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller)
    - [ローカル デバイス](#load-endpoint-protection-group-policy-settings-into-your-local-device)

> [!NOTE]
> グループ ポリシー設定を使用して Windows 10、Windows Server 2019、および Windows Server 2016 で Microsoft Defender ウイルス対策を管理する方法については、「[グループ ポリシー設定を使用して Microsoft Defender ウイルス対策を構成および管理する](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-antivirus/use-group-policy-microsoft-defender-antivirus)」を参照してください。

## <a name="copy-endpoint-protection-policy-definitions"></a>Endpoint Protection ポリシー定義をコピーする

Endpoint Protection によって管理される下位レベルの Windows デバイス上で、Endpoint Protection ポリシー定義ファイルをコピーします。

1. **C:\Program Files\Microsoft Security Client\Admx** に移動します。 

2. 次のファイルを zip ファイルに圧縮します (**SCEP_admx.zip** など)。
    - **EndPointProtection.adml**
    - **EndPointProtection.admx**
3. zip ファイルを一時フォルダーにコピーします (**C:\temp_SCEP_GPO_admx** など)。
4. ファイルを展開します。 

> [!NOTE]
> Endpoint Protection ポリシー設定を構成するためのレジストリ キーは、**Hkey_Local_Machine\Software\Policies\Microsoft\Microsoft Antimalware** にあります。

## <a name="load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller"></a>Endpoint Protection グループ ポリシー設定をドメイン コントローラーのセントラル ストアに読み込む

[グループ ポリシー管理用テンプレートのセントラル ストア](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra)を使用している場合は、次の手順に従って Endpoint Protection グループ ポリシー設定を読み込んで構成します。 これが推奨される方法です。

1. Endpoint Protection ポリシー定義ファイルの展開先のフォルダーに移動します。
2. .admx と .adml ファイルをドメイン コントローラーの **PolicyDefinitions** フォルダーにコピーします。
    1. **EndPointProtection.admx** を **\\\\\<forest.root\>\\SYSVOL\\\<domain\>\\Policies\\PolicyDefinitions** にコピーします。 
    2. **EndPointProtection.adml** を **\\\\\<forest.root\>\\SYSVOL\\\<domain\>\\Policies\\PolicyDefinitions\\en-US** にコピーします。  

    次に例を示します。
    
    - **EndPointProtection.admx** を **\\DC\SYSVOL\contoso.com\Policies\PolicyDefinitions** にコピーします。
    - **EndPointProtection.adml** を **\\DC\SYSVOL\contoso.com\Policies\PolicyDefinitions\en-US** にコピーします。
    
    ここで、**DC** はドメイン コントローラーの名前、**contoso.com** はお使いのドメインです。

3. [グループ ポリシー管理コンソール](https://docs.microsoft.com/internet-explorer/ie11-deploy-guide/group-policy-and-group-policy-mgmt-console-ie11)を開き、ドメインに新しいグループ ポリシー オブジェクト (GPO) を作成します (**Endpoint Protection** など)。
4. Endpoint Protection の GPO を右クリックし、 **[編集]** クリックします。
5. [グループ ポリシー管理エディター] で、 **[コンピューターの構成]**  >  **[ポリシー]**  >  **[管理用テンプレート: ポリシー定義]**  >  **[Windows コンポーネント]**  >  **[Endpoint Protection]** に移動します。

   Endpoint Protection グループ ポリシーの一覧が表示されます。

6. 構成する設定が含まれているセクションを展開し、設定をダブルクリックして開き、構成を変更します。

## <a name="load-endpoint-protection-group-policy-settings-into-your-local-device"></a>Endpoint Protection グループ ポリシー設定をローカル デバイスに読み込む

Endpoint Protection ポリシー定義の読み込みにセントラル ストアを使用する代わりに、それらをデバイスにローカルに保存することもできます。

1. Endpoint Protection ポリシー定義ファイルの展開先のフォルダーに移動します。
2. .admx と .adml ファイルをローカルの PolicyDefinitions フォルダーにコピーします。
    1. **EndPointProtection.admx** を **%SystemRoot%/PolicyDefinitions** にコピーします。 
    2. **EndPointProtection.adml** を **%SystemRoot%/PolicyDefinitions/en-US** にコピーします。
    
    次に例を示します。

    - **EndPointProtection.admx** を **C:\Windows\PolicyDefinitions** にコピーします。
    - **EndPointProtection.adml** を **C:\Windows\PolicyDefinitions\en-US** にコピーします。
    
3. ローカル グループ ポリシー エディターを開きます。
4. **[コンピューターの構成]**  >  **[管理用テンプレート]**  >  **[Windows コンポーネント]**  >  **[Endpoint Protection]** に移動します。

    Endpoint Protection グループ ポリシーの一覧が表示されます。

5. 構成する設定が含まれているセクションを展開し、設定をダブルクリックして開き、構成を変更します。

## <a name="next-steps"></a>次の手順
- Endpoint Protection の概要については、「[Endpoint Protection](endpoint-protection.md)」を参照してください。
- スタンドアロン クライアント上で Endpoint Protection を手動で構成する方法については、「[スタンドアロン クライアントでの Endpoint Protection の構成](endpoint-protection-configure-standalone-client.md)」を参照してください。
