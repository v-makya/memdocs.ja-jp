---
title: 自動操縦プロファイルの構成
description: Windows 自動操縦展開の実行中にデバイスプロファイルを構成する方法について説明します。
keywords: MDM, セットアップ, Windows, Windows 10, OOBE, 管理, 展開, Autopilot, ZTD, ゼロタッチ, パートナー, MSFB, Intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 648793f68aef98659d068009e278fe35dec062e4
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907970"
---
# <a name="configure-autopilot-profiles"></a>自動操縦プロファイルの構成

**適用対象**

-   Windows 10

Windows 自動運用展開サービスに定義されているデバイスごとに、展開時にそのデバイスの正確な動作を指定する設定のプロファイルを適用する必要があります。 プロファイル設定を構成してデバイスを登録する方法の詳細な手順については、「 [デバイスの登録](add-devices.md#registering-devices)」を参照してください。

## <a name="profile-settings"></a>プロファイルの設定

次のプロファイル設定を使用できます。

-   **Cortana、OneDrive、OEM 登録のセットアップページをスキップ**します。 Autopilot で登録されるすべてのデバイスでは、out-of-box experience (OOBE) プロセスの間にこれらのページが自動的にスキップされます。

-   **職場または学校用に自動的に設定**されます。 自動操縦に登録されているすべてのデバイスは、自動的に職場または学校のデバイスと見なされるため、この質問は OOBE プロセスでは表示されません。

-   **会社のブランドを使用したサインインエクスペリエンス**。 一般的な Azure Active Directory サインインページを表示するのではなく、自動操縦に登録されたすべてのデバイスに、Azure Active Directory で構成されている組織の名前、ロゴ、および追加のヘルプテキストを含むカスタマイズされたサインインページが表示されます。 これらの設定をカスタマイズするには [、「ディレクトリに会社のブランドを追加](/azure/active-directory/customize-branding#add-company-branding-to-your-directory) する」を参照してください。

-   **プライバシー設定をスキップ**します。 この Autopilot プロファイルのオプションの設定を使うと、OOBE プロセスの間は、プライバシーの設定について組織による確認は行われません。 通常は、Intune またはその他の管理ツールを使用して、組織がこれらの設定を構成できるようにすることをお勧めします。

-   **デバイスでのローカル管理者アカウントの作成を無効に**します。 デバイスをセットアップするユーザーがプロセス完了後に管理者アクセス権を持つ必要があるかどうかについて、組織による決定が可能です。

-   **使用許諾契約書 (EULA) をスキップ**します。 Windows 10 バージョン1709以降では、組織は、OOBE プロセス中に提示された EULA ページをスキップすることを決定できます。 つまり、組織はユーザーの代わりに EULA 条項に同意します。

-   **Windows コンシューマー機能を無効に**します。 Windows 10 バージョン1803以降では、ユーザーが初めてデバイスにサインインしたときに、デバイスが追加の Microsoft Store アプリを自動的にインストールしないように、Windows のコンシューマー機能を無効にすることができます。 詳細については、 [MDM のドキュメント](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures)を参照してください。

## <a name="related-topics"></a>関連トピック

[プロファイルのダウンロード](troubleshooting.md#profile-download)<br>
[デバイスの登録](add-devices.md)