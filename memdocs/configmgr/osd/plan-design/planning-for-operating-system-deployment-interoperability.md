---
title: OS の展開の相互運用性
titleSuffix: Configuration Manager
description: 単一の階層内の異なる Configuration Manager サイトで異なるバージョンを使用する場合の相互運用性の問題について理解します。
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5931c43f0f8513ea1819e00f4eac7ecfd35dc717
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708080"
---
# <a name="plan-for-os-deployment-interoperability"></a>OS の展開の相互運用性に関する計画

*適用対象:Configuration Manager (Current Branch)*

単一の階層内の異なる Configuration Manager サイトで異なるバージョンを使用する場合、Configuration Manager の一部の機能が使用できなくなります。 通常、Configuration Manager の新しいバージョンの機能は、古いバージョンを実行しているサイトで、またはクライアントによって使用することはできません。 詳細については、「[異なるバージョンの Configuration Manager 間の相互運用性](../../core/plan-design/hierarchy/interoperability-between-different-versions.md)」を参照してください。  


## <a name="objects"></a>オブジェクト

階層内の最上位サイトをアップグレードし、階層内の他のサイトは古いバージョンの Configuration Manager を実行する場合、次のオブジェクトを考慮してください。  

### <a name="client-installation-package"></a>クライアント インストール パッケージ  

- 既定のクライアント インストール パッケージのソースが自動的にアップグレードされます。 階層内のすべての配布ポイントがこの新しいクライアント インストール パッケージによって更新されます。 この動作は、古いバージョンの階層内のサイトにある配布ポイントにおいても発生します。  

- 新しいバージョンのクライアントを、まだ新しいバージョンにアップグレードされていないサイトに割り当てることはできません。 割り当ては管理ポイントでブロックされます。  

### <a name="boot-images"></a>ブート イメージ  

- 最上位サイトを Configuration Manager の最新バージョンにアップグレードすると、既定のブート イメージ (x86 および x64) が自動的に更新されます。 更新プログラムでは、Windows PE 10 を含む Windows 10 用 Windows ADK が使用されます。 既定のブート イメージと関連付けられているファイルは、Configuration Manager の最新バージョンのファイルで更新されます。 サイトでは、カスタム ブート イメージは自動的に更新されません。 カスタム ブート イメージは、古いバージョンの Windows PE を含め、手動で更新する必要があります。  

- サイト階層内に複数バージョンの Configuration Manager が含まれる場合、動的メディアは使用しないでください。 代わりに、サイトベースのメディアを使用して特定の管理ポイントに接続します。 すべてのサイトを同じバージョンの Configuration Manager に更新したら、再度動的メディアを使用できます。

- 最新の Configuration Manager ブート イメージにカスタマイズが含まれていることを確認します。 次に、新しいバージョンのサイトにあるすべての配布ポイントを新しいブート イメージの最新バージョンに更新します。  

### <a name="user-state-migration-tool-usmt"></a>ユーザー状態移行ツール (USMT)  

最上位サイトを Configuration Manager の最新バージョンにアップグレードすると、既定の USMT パッケージが最新のバージョンに自動的に更新されます。 カスタム USMT パッケージは自動的に更新されません。 これらのパッケージは手動で更新する必要があります。  

### <a name="new-task-sequence-steps"></a>新しいタスク シーケンス ステップ  

定期的に、新しいバージョンの Configuration Manager のサイトが含まれる場合、動的メディアは使用しないでください。 新しいステップのあるタスク シーケンスを古いクライアントに展開すると、タスク シーケンスのステップは失敗します。 新しいステップのあるタスク シーケンスを展開する前に、ターゲット コレクション内のクライアントが新しいバージョンに更新されていることをご確認ください。  

### <a name="os-deployment-media"></a>OS 展開メディア  

サイトが新しいバージョンに更新されたら、すべてのメディアを新しい Configuration Manager クライアント パッケージで更新する必要があります。 これらのメディアの種類には、起動可能、キャプチャ、事前設定済み、スタンドアロンなどがあります。

### <a name="third-party-extensions-to-os-deployment"></a>OS の展開に対するサード パーティ製の拡張機能  

OS の展開に対するサード パーティ製の拡張機能があり、Configuration Manager サイトまたは Configuration Manager クライアントにさまざまなバージョンがある場合、拡張に関する問題がある可能性があります。  


## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>混在階層における最新バージョンの Configuration Manager  サイト  

あるサイトを最新バージョンの Configuration Manager にアップグレードすると、既定のクライアント インスタンス パッケージを参照するタスク シーケンスによって、最新バージョンの Configuration Manager クライアントの展開が自動的に開始されます。

カスタム クライアント インストール パッケージを参照するタスク シーケンスによって、そのカスタム パッケージに含まれるバージョンのクライアントが引き続き展開されます。 カスタム パッケージには、以前のバージョンの Configuration Manager クライアントが含まれている可能性があります。 タスク シーケンスの展開エラーを回避するには、すべてのカスタム クライアント インストール パッケージを最新バージョンに更新します。

カスタム クライアント インストール パッケージを使用するタスク シーケンスを構成する場合、次のいずれかのアクションを行います。

- クライアント インストール パッケージの最新の Configuration Manager バージョンを使用するように、タスク シーケンス ステップを更新します
- 最新の Configuration Manager クライアント インストール ソースを使用するように、カスタム パッケージを更新します

> [!IMPORTANT]  
> 最新の Configuration Manager クライアント インストール パッケージを参照するタスク シーケンスは、古い Configuration Manager サイトのクライアントに展開しないでください。 古い Configuration Manager サイトに割り当てられているクライアントが最新の Configuration Manager クライアント バージョンにアップグレードされた場合、Configuration Manager は、古い Configuration Manager サイトへの割り当てをブロックします。 これらのクライアントはどのサイトにも割り当てられなくなります。 手動でクライアントを最新の Configuration Manager サイトに割り当てるか、古いバージョンの Configuration Manager クライアントをコンピューターに再インストールするまで、それらのクライアントは管理対象ではなくなります。


## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>混在階層における古いバージョンの Configuration Manager サイト  

中央管理サイトを最新バージョンの Configuration Manager にアップグレードする場合、展開する OS 展開タスク シーケンスによって、それらのクライアントが管理されていない状態のままになっていないことを確認してください。 たとえば、最新の Configuration Manager バージョンにまだアップグレードしていない古い Configuration Manager サイトに割り当てられているクライアントに展開する場合です。

最新バージョンの Configuration Manager サイト内のクライアントに展開するために使用するタスク シーケンスをコピーします。 次に、古い Configuration Manager サイト内のクライアントに展開できるように、そのタスク シーケンスを変更します。 古い Configuration Manager クライアント インストール ソースを使用するカスタム クライアント インストール パッケージを参照するように、タスク シーケンスを構成します。 古い Configuration Manager クライアント インストール ソースを参照するカスタム クライアント インストール パッケージがまだない場合は、手動で作成します。  

> [!Important]  
> バージョン 1902 以降では、5.7730 以前のクライアント バージョンにパッケージまたはタスク シーケンスを展開することはできません。 この制限を回避するには、以降のバージョンにクライアントをアップグレードします。<!-- SCCMDocs-pr issue #3493 -->
