---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: a61bf84a872458f37826c3de07ede05b1b658f0c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127310"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->

共同管理を有効にする場合は、Azure パブリック クラウド、Azure US Government クラウド、または Microsoft Azure China 21Vianet (バージョン 2006 で追加) を使用できます。 Configuration Manager バージョン 1906 以降で共同管理を有効化するには、次の手順に従います。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[Cloud Services]** を展開して **[共同管理]** を選択します。 リボン内の **[共同管理の構成]** を選択し、**共同管理構成ウィザード**を開きます。

1. ウィザードの **[テナントのオンボード]** ページで、使用する **Azure 環境**を構成します。 以下のいずれかの環境を選択します。

   - Azure パブリック クラウド
   - Azure US Government クラウド<!--4075452-->
   - Azure China Cloud (バージョン 2006 で追加)<!--7133238-->
      - Azure China Cloud にオンボードする前に、ご使用のデバイスで Configuration Manager クライアントを最新バージョンに更新します。 <!--7630213--> 

   Azure China Cloud または Azure US Government クラウドを選択すると、[[tenant attach]\(テナントのアタッチ\)](../../tenant-attach/device-sync-actions.md) の **[Upload to Microsoft Endpoint Manager admin center]\(Microsoft エンドポイント マネージャー管理センターへのアップロード\)** オプションが無効になります。

1. **[サインイン]** を選択します。 Azure AD グローバル管理者としてサインインし、 **[次へ]** を選択します。 このウィザードの目的でのサインインは、この 1 回だけです。 サインイン情報が他の場所に保存されたり、再利用されることはありません。

1. **[有効化]** ページで、次の設定を選択します。

   - **[Automatic enrollment into Intune]\(Intune への自動登録\)** - 既存の Configuration Manager クライアントに対して、Intune で自動クライアント登録が有効になります。 このオプションにより、クライアントのサブセットで共同管理を有効にして初期テストを行ってから、段階的アプローチでロールアウトできます。 デバイスがユーザーによって登録解除された場合、ポリシーの次の評価の際に再登録されます。 <!--3330596-->

      - **[パイロット]** - **Intune 自動登録**コレクションのメンバーである Configuration Manager クライアントのみが Intune に自動的に登録されます。
      - **[すべて]** - Windows 10、バージョン 1709 以降、クライアントに対して、自動登録を有効にします。

   - **[Intune 自動登録]** - このコレクションには、共同管理に取り入れるすべてのクライアントを含める必要があります。 基本的には、その他すべてのステージング コレクションのスーパーセットになります。

   ![Intune 自動登録の指定 ](../media/3555750-co-management-onboarding-enablement.png)
      
      自動登録はすべてのクライアントに対してすぐには行われません。 この動作は、大規模な環境に対する登録のスケーリング向上に役立ちます。 Configuration Manager は、クライアントの数に基づいて登録をランダム化します。 たとえば、環境に 100,000 のクライアントがある場合、この設定を有効にすると、登録は数日間にわたって行われます。<!--1358003-->

      > [!Note]  
      > バージョン 1906 以降:
      >
      > - 新しい共同管理デバイスが、その Azure Active Directory (Azure AD) "*デバイス*" トークンに基づいて、Microsoft Intune サービスに自動的に登録されるようになりました。 自動登録を開始するのに、ユーザーがデバイスにサインインするのを待機する必要はありません。 この変更により、登録状態が "*ユーザー サインインの保留中*" のデバイスの数を減らすことができます。<!-- 4454491 --> この動作をサポートするには、デバイスで Windows 10 バージョン 1803 以降が実行されている必要があります。 詳細については、「[共同管理の状態](../how-to-monitor.md#co-management-enrollment-status)」を参照してください。
      >
      > - 既に共同管理に登録されているデバイスがある場合は、[前提条件](../overview.md#prerequisites)を満たせば、新しいデバイスがすぐに登録されるようになりました。<!--4321130-->

1. Intune に登録済みのインターネットベースのデバイスについては、**[有効化]** ページのコマンド ラインをコピーして保存ください。 このコマンド ラインを利用して、Intune のインターネットベースのデバイス用アプリとして、Configuration Manager クライアントをインストールできます。 ここでこのコマンド ラインを保存しない場合は、いつでも共同管理の設定を確認してこのコマンド ラインを取得するできます。

1. **[ワークロード]** ページで、各ワークロードについて、Intune による管理のために移動するデバイス グループを選択します。 詳細については、「[ワークロード](../workloads.md)」を参照してください。 共同管理を有効にするだけの場合、今すぐワークロードを切り替える必要はありません。 後でワークロードを切り替えることができます。 詳細については、[ワークロードを切り替える方法](../how-to-switch-workloads.md)に関するページをご覧ください。  

    - **[パイロット Intune]** - **[ステージング]** ページで指定したパイロット コレクション内のデバイスに対してのみ、関連付けられたワークロードを切り替えることができます。 各ワークロードは、異なるパイロット コレクションを持つことができます。
    - **[Intune]**: 共同管理されるすべての Windows 10 デバイスに対する関連ワークロードを切り替えます。  

    > [!Important]
    > ワークロードを切り替える前に、それに対応するワークロードが Intune で適切に構成され、展開されていることを確認します。 デバイス用の管理ツールのいずれかでワークロードが常に管理されていることを確認します。  

1. **[ステージング]** ページで、**パイロット Intune** に設定された各ワークロードのパイロット コレクションを指定します。

   ![Intune 自動登録の指定 ](../media/3555750-co-management-onboarding-staging.png)

1. 共同管理を有効にするには、ウィザードを終了します。
