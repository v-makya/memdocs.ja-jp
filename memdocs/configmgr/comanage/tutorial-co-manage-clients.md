---
title: チュートリアル&#58; 既存のクライアントの共同管理を有効にする
titleSuffix: Configuration Manager
description: 既に Configuration Manager を使用して Windows 10 デバイスを管理している場合に、Microsoft Intune との共同管理を構成します。
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc05ae5a9be6c437fab60f8c4c5a45d61e8c3e65
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694884"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>チュートリアル: 既存の Configuration Manager クライアントの共同管理を有効にする

共同管理では、Configuration Manager を使用して組織の PC を管理するための既に確立されているプロセスを保持できます。 同時に、セキュリティと最新のプロビジョニングのために Intune の使用を通してクラウドに投資します。  

このチュートリアルでは、Configuration Manager に既に登録されている Windows 10 デバイスの共同管理を設定します。 このチュートリアルは、既に Configuration Manager を使用して Windows 10 デバイスを管理しているという前提から始まります。

このチュートリアルは、以下に該当する場合に使用します。  

- ハイブリッド Azure AD 構成の中で Azure Active Directory (Azure AD) に接続できるオンプレミスの Active Directory がある。

  オンプレミスの AD を Azure AD に参加させるハイブリッド Azure Active Directory (AD) をデプロイできない場合は、[新しいインターネット ベースの Windows 10 デバイスの共同管理の有効化](tutorial-co-manage-new-devices.md)に関する手引きのチュートリアルに従うことをお勧めします。
- クラウドに接続したい既存の Configuration Manager クライアントがある。

**このチュートリアルでは、以下を行います。**  
> [!div class="checklist"]
> * Azure とオンプレミス環境の前提条件を確認する
> * ハイブリッド Azure AD をセットアップする  
> * Azure AD に登録するように Configuration Manager クライアント エージェントを構成する  
> * デバイスを自動登録するように Intune を構成する  
> * Configuration Manager で共同管理を有効にする  

## <a name="prerequisites"></a>[前提条件]  

### <a name="azure-services-and-environment"></a>Azure サービスと環境

- Azure サブスクリプション ([無料試用版](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Microsoft Intune サブスクリプション
  > [!TIP]  
  > Enterprise Mobility + Security (EMS) のサブスクリプションには、Azure Active Directory Premium と Microsoft Intune の両方が含まれています。 EMS サブスクリプション ([無料試用版](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial))。  

環境にまだ存在しない場合は、このチュートリアルの中で以下を実行します。

- オンプレミスの Active Directory と Azure Active Directory (AD) テナントの間に [Azure AD Connect](/azure/active-directory/hybrid/how-to-connect-install-select-installation) を構成します。

> [!TIP]
> ユーザーに対して個別の Intune または EMS ライセンスを購入して割り当てる必要はなくなりました。 詳細については、「[Configuration Manager のブランチとライセンスに関してよく寄せられる質問](../core/understand/product-and-licensing-faq.md#bkmk_mem)」を参照してください。

### <a name="on-premises-infrastructure"></a>オンプレミス インフラストラクチャ

- Configuration Manager Current Branch の[サポートされているバージョン](../core/servers/manage/updates.md#supported-versions)
- Intune に対して、モバイル デバイス管理 (MDM) 機関を構成する必要があります。  

### <a name="permissions"></a>アクセス許可

このチュートリアルでは、次のアクセス許可を使用してタスクを完了します。

- オンプレミス インフラストラクチャ上で "*ドメイン管理者*" であるアカウント  
- Configuration Manager の "*すべての*" スコープで "*完全な権限を持つ管理者*" であるアカウント
- Azure Active Directory (Azure AD) の "*全体管理者*" であるアカウント
   - テナントへのサインインに使用するアカウントに Intune ライセンスを割り当てていることを確認してください。 そうしないと、サインインが失敗し、"User not recognized (ユーザーが認識されません)" というエラー メッセージが表示されます。 <!--mem issue 169-->

## <a name="set-up-hybrid-azure-ad"></a>ハイブリッド Azure AD をセットアップする

ハイブリッド Azure AD の設定で実際に行っているのは、Azure AD Connect と Active Directory Federated Services (ADFS) を使用してオンプレミスの AD を Azure AD に統合することです。 正しく構成されると、ワーカーは各自のオンプレミスの AD 資格情報を使用して外部システムにシームレスにサインインできます。

> [!IMPORTANT]  
> このチュートリアルでは、マネージド ドメインに対してハイブリッド Azure AD を設定するための、必要最小限のプロセスについて説明します。 このプロセスに慣れておくことをお勧めします。また、ハイブリッド Azure AD を理解してデプロイするためのガイドとして、このチュートリアルだけに頼らないようにすることをお勧めします。
>
> ハイブリッド Azure AD の詳細については、Azure Active Directory のドキュメントの次の記事を参照することから始めてください。
>
> - [Azure AD 参加の実装を計画する](/azure/active-directory/devices/azureadjoin-plan)
> - [ハイブリッド Azure Active Directory 参加の実装を計画する](/azure/active-directory/devices/hybrid-azuread-join-plan)
> - [デバイスのハイブリッド Azure AD 参加を制御する](/azure/active-directory/devices/hybrid-azuread-join-control)
> - [フェデレーション ドメイン用のハイブリッド Azure Active Directory 参加を構成する](/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  

### <a name="set-up-azure-ad-connect"></a>Azure AD Connect を設定する

ハイブリッド Azure AD では、オンプレミスの Active Directory (AD) のコンピューター アカウントと Azure AD 上のデバイス オブジェクトを常に同期するための Azure AD Connect の構成が必要です。

バージョン 1.1.819.0 以降、Azure AD Connect には、ハイブリッド Azure AD 参加を構成するためのウィザードが用意されています。 このウィザードの使用によって、構成プロセスが簡略化されます。  

Azure AD Connect を構成するには、Azure AD のグローバル管理者の資格情報が必要です。  

> [!TIP]  
> 次の手順を Azure AD Connect を設定するための正式な手順とみなさないでください。ここに記載されているのは、Intune と Configuration Manager 間の共同管理の構成の流れを示するために役立つからです。 Azure AD を設定するための正規の内容と関連手順については、Azure AD ドキュメントの「[マネージド ドメイン用のハイブリッド Azure Active Directory 参加の構成](/azure/active-directory/devices/hybrid-azuread-join-managed-domains)」を参照してください。  

#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Azure AD Connect を使用してハイブリッド Azure AD 参加を構成する

1. [Azure AD Connect の最新バージョン](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 以降) を取得してインストールします。  
2. Azure AD Connect を起動し、 **[構成]** を選択します。
3. **[追加のタスク]** ページで、 **[デバイス オプションの構成]** を選択し、 **[次へ]** を選択します。
4. **[概要]** ページで、 **[次へ]** を選択します。
5. **[Azure AD へ接続]** ページで、Azure AD のグローバル管理者の資格情報を入力します。
6. **[デバイスのオプション]** ページで、 **[ハイブリッド Azure AD 参加の構成]** を選択し、 **[次へ]** を選択します。
7. **[デバイスのオペレーティング システム]** ページで、Active Directory 環境のデバイスで使用されているオペレーティング システムを選択し、 **[次へ]** を選択します。  

   Windows ダウンレベル ドメイン参加済みデバイスをサポートするオプションを選択できますが、デバイスの共同管理は Windows 10 に対してのみサポートされることを忘れないでください。
8. **[SCP]** ページで、Azure AD Connect にサービス接続ポイント (SCP) を構成する各オンプレミス フォレストに対して、次の手順を実行した後、 **[次へ]** を選択します。  
   1. フォレストを選択します。  
   2. 認証サービスを選択します。  フェデレーション ドメインがある場合は、ご自身の組織に Windows 10 クライアントのみがあり、コンピューター/デバイスの同期を構成しているか、ご自身の組織で [SeamlessSSO](/azure/active-directory/hybrid/how-to-connect-sso) を使用している場合を除いて、AD FS サーバーを選択します。  
   3. **[追加]** をクリックし、エンタープライズ管理者の資格情報を入力します。  
9. マネージド ドメインがある場合は、この手順をスキップします。  

   **[フェデレーション構成]** ページで、ご自身の AD FS 管理者の資格情報を入力し、 **[次へ]** を選択します。
10. **[構成の準備完了]** ページで、 **[構成]** を選択します。
11. **[構成が完了しました]** ページで、 **[終了]** を選択します。

ドメイン参加済み Windows デバイスに対するハイブリッド Azure AD 参加の完了で問題が発生した場合は、「[Windows の現在のデバイスのハイブリッド Azure AD 参加のトラブルシューティング](/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current)」を参照してください。

## <a name="configure-client-settings-to-direct-clients-to-register-with-azure-ad"></a>Azure AD への登録をクライアントに指示するようにクライアント設定を構成する

[クライアント設定] を使用して、Azure AD に自動的に登録するように Configuration Manager クライアントを構成します。  

1. **Configuration Manager コンソール** >  **[管理]**  >  **[概要]**  >  **[クライアント設定]** を開き、 **[既定のクライアント設定]** を編集します。  

2. **[クラウド サービス]** を選択します。  

3. **[既定の設定]** ページで、 **[新しい Windows 10 ドメインに参加しているデバイスを自動的に Azure Active Directory に登録する]** を **[はい]** に設定します。  

4. **[OK]** を選択して、この構成を保存します。  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Intune へのデバイスの自動登録を構成する

次に、Intune でのデバイスの自動登録を設定します。 自動登録によって、Configuration Manager を使用して管理するデバイスが Intune に自動的に登録されます。

自動登録では、ユーザーに自分の Windows 10 デバイスを Intune に登録させることもできます。 デバイスは、ユーザーが個人的に所有しているデバイスに職場アカウントを追加するか、企業が所有しているデバイスが Azure Active Directory に参加したときに登録されます。  

1. [Azure portal](https://portal.azure.com/) にサインインし、 **[Azure Active Directory]**  >  **[モビリティ (MDM および MAM)]**  >  **[Microsoft Intune]** を選択します。  

2. **[MDM ユーザー スコープ]** を構成します。 次のいずれかを指定して、Microsoft Intune によって管理されるユーザーのデバイスを構成し、URL の値の既定値をそのまま使用します。  

   - **一部**: Windows 10 デバイスを自動的に登録できる**グループ**を選択します  

   - **すべて**:すべてのユーザーが自分の Windows 10 デバイスを自動的に登録できます

   - **なし**: MDM の自動登録を無効にします

   > [!IMPORTANT]  
   > **MAM ユーザー スコープ**と MDM の自動登録 (**MDM ユーザー スコープ**) の両方が有効な場合は、MAM のみが有効になります。 そのグループのユーザーが個人のデバイスを参加させたときに、それらに対してモバイル アプリケーション管理 (MAM) のみが追加されます。 デバイスは自動的には MDM に登録されません。  

3. **[保存]** を選択して、自動登録の構成を完了します。  

4. **[モビリティ (MDM および MAM)]** に戻り、 **[Microsoft Intune 登録]** を選択します。  

    > [!NOTE]
    > 一部のテナントでは、これらのオプションを構成することはできません。<!-- SCCMDocs#1230 -->
    >
    > **Microsoft Intune** を使うと、Azure AD に対して MDM アプリを構成できます。 **Microsoft Intune の登録**は、iOS および Android の登録に多要素認証ポリシーを適用するときに作成される特定の Azure AD アプリです。 詳細については、「[Intune へのデバイスの登録で多要素認証を要求する](/intune/enrollment/multi-factor-authentication)」を参照してください。

5. MDM ユーザー スコープで、 **[すべて]** を選択し、 **[保存]** を選択します。  

## <a name="enable-co-management-in-configuration-manager"></a>Configuration Manager で共同管理を有効にする

ハイブリッド Azure AD を設定し、Configuration Manager クライアントの構成を完了したら、スイッチを切り替えて Windows 10 デバイスの共同管理を有効にすることができます。  

> [!TIP]
> - 共同管理を有効にすると、 *[パイロット グループ]* としてコレクションが割り当てられます。 これは、共同管理構成をテストするための少数のクライアントを含むグループです。 手順を開始する前に、適切なコレクションを作成することをお勧めします。 その後、それを行う手順を終了せずにコレクションを選択できます。
> - Configuration Manager バージョン 1906 以降では、各ワークロードに対して異なる "*パイロット グループ*" を割り当てることができるため、複数のコレクションが必要となる場合があります。

### <a name="enable-co-management-starting-in-version-1906"></a>バージョン 1906 以降での共同管理の有効化

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>バージョン 1902 以前での共同管理の有効化

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="next-steps"></a>次のステップ

- [共同管理ダッシュ ボード](how-to-monitor.md)で、共同管理されているデバイスの状態を確認する
- 共同管理からの[イミディエイト値](quickstarts.md#immediate-value)の取得を開始する
- [条件付きアクセス](quickstart-conditional-access.md)と Intune のコンプライアンス規則を使用して、企業リソースへのユーザー アクセスを管理する