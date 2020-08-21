---
title: Windows Hello for Business の設定
titleSuffix: Configuration Manager
description: Windows Hello for Business を Configuration Manager と統合する方法について説明します。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4c8029cdda80d327cbed2a4c60c71ff1811e4723
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698699"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager"></a>Configuration Manager における Windows Hello for Business の設定

*適用対象:Configuration Manager (Current Branch)*

<!--1245704-->
Configuration Manager は、Windows Hello for Business と統合されます。 (この機能は、以前は Microsoft Passport for Work と呼ばれていました。)Windows Hello for Business は、Windows 10 デバイスの代替サインイン方法です。 ここでは、パスワード、スマート カード、または仮想スマート カードの代わりに、Active Directory または Azure Active Directory (Azure AD) アカウントを使用します。 Hello for Business を使用すると、パスワードの代わりに、"*ユーザー ジェスチャ*" を使用してサインインできます。 ユーザー ジェスチャには、暗証番号 (PIN)、生体認証、または指紋リーダーなどの外部デバイスがあります。

> [!Important]  
> バージョン 1910 以降では、Configuration Manager で Windows Hello for Business の設定を使用した証明書ベースの認証はサポートされていません。 詳しくは、[非推奨の機能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)に関するページをご覧ください。 キー ベースの認証は引き続き有効です。
>
> Active Directory フェデレーション サービス登録機関 (ADFS RA) の展開の方が簡単で、より優れたユーザー エクスペリエンスを提供しており、より決定論的な証明書の登録エクスペリエンスを備えています。 Windows Hello for Business を使用した証明書ベースの認証には ADFS RA を使用します。
>
> 共同管理デバイスの場合は、[**リソース アクセス ポリシー** ワークロード](../../comanage/workloads.md#resource-access-policies)を Intune に移行することを検討してください。 次に、Intune ポリシーを使用してこれらの証明書を管理します。 詳細については、[ワークロードを切り替える方法](../../comanage/how-to-switch-workloads.md)に関するページをご覧ください。

詳細については、「[Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-identity-verification)」を参照してください。

> [!Note]  
> Configuration Manager では、このオプション機能は既定で無効です。 この機能は、使用する前に有効にする必要があります。 詳細については、「[Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options)」 (更新プログラムのオプション機能の有効化) を参照してください。<!--505213-->  

Configuration Manager と Windows Hello for Business を統合するには、次の方法があります。  

- ユーザーがサインインに使用できるジェスチャと使用できないジェスチャを制御します。  

- Windows Hello for Business のキー格納プロバイダー (KSP) に認証証明書を格納します。 詳細については、「[Certificate profiles](introduction-to-certificate-profiles.md)」 (証明書プロファイル) をご覧ください。  

- Windows Hello for Business プロファイルを作成して展開し、ドメインに参加しており Configuration Manager クライアントを実行している Windows 10 デバイスの Windows Hello for Business 設定を制御します。 バージョン 1910 以降では、証明書ベースの認証は使用できません。 キー ベースの認証を使用している場合は、証明書プロファイルを展開する必要はありません。

## <a name="configure-a-profile"></a>プロファイルの構成  

1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** ワークスペースに移動します。 **[コンプライアンス設定]** 、 **[会社のリソースへのアクセス]** の順に展開して、 **[Windows Hello for Business プロファイル]** ノードを選択します。

1. リボンで、 **[Windows Hello for Business プロファイルの作成]** を選択してプロファイル ウィザードを開始します。

1. **[全般]** ページで、このプロファイルの名前と必要に応じて説明を指定します。

1. **[サポートされているプラットフォーム]** ページで、このプロファイルを適用する OS のバージョンを選択します。

1. **[設定]** ページで、次の設定を構成します。

    - **[Windows Hello for Business の構成]** :このプロファイルで Hello for Business を有効にするか、無効にするか、または構成しないかを指定します。

    - **[トラステッド プラットフォーム モジュール (TPM) の使用]** :TPM によってデータのセキュリティ層が追加されます。 次のいずれかの値を選択します。  

      - **必須**:アクセス可能な TPM を装備したデバイスのみが Windows Hello for Business をプロビジョニングできます。  

      - **優先**:デバイスは最初に TPM を使用しようとします。 これが使用できない場合、ソフトウェアの暗号化を使用できます。

    - **[認証方法]** :このオプションは、 **[未構成]** または **[キー ベース]** に設定します。

        > [!NOTE]
        > バージョン 1910 以降では、Configuration Manager で Windows Hello for Business の設定を使用した証明書ベースの認証はサポートされていません。

    - **PIN の最小長の構成**:ユーザーの PIN の最小長を定める場合は、このオプションを有効にして値を指定します。 有効にすると、既定値は `4` になります。

    - **PIN の最大長の構成**:ユーザーの PIN の最大長を定める場合は、このオプションを有効にして値を指定します。 有効にすると、既定値は `127` になります。

    - **PIN の有効期限を必要とする (日数)** :デバイス PIN の変更が必要になるまでの日数を指定します。

    - **前の PIN の再利用を防止**:以前に使用した PIN を使用することをユーザーに許可しません。

    - **PIN に英大文字が必要**:ユーザーが Windows Hello for Business の PIN に大文字を含める必要があるかどうかを指定します。 次の中から選択します。  

      - **[許可]** :ユーザーは PIN に大文字を使用することができますが、その必要はありません。

      - **必須**:ユーザーは PIN に大文字を 1 文字以上含める必要があります。  

      - **許可しない**:ユーザーは PIN に大文字を使用することができません。  

    - **PIN に英小文字が必要**:ユーザーが Windows Hello for Business の PIN に小文字を含める必要があるかどうかを指定します。 次の中から選択します。  

      - **[許可]** :ユーザーは PIN に小文字を使用することができますが、その必要はありません。

      - **必須**:ユーザーは PIN に小文字を 1 文字以上含める必要があります。  

      - **許可しない**:ユーザーは PIN に小文字を使用することができません。  

    - **特殊文字の構成**:PIN の特殊文字の使用を指定します。 次の中から選択します。  

        > [!NOTE]
        > 特殊文字には次のセットが含まれます。
        >
        > ``` characters
        > ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~
        > ```

      - **[許可]** :ユーザーは PIN に特殊文字を使用することができますが、その必要はありません。  

      - **必須**:ユーザーは PIN に特殊文字を 1 文字以上含める必要があります。  

      - **許可しない**:ユーザーは PIN に特殊文字を使用することができません。 この動作は、設定が **[未構成]** の場合にも行われます。  

    - **PIN での数字の使用の構成**:PIN での数字の使用を指定します。 次の中から選択します。

      - **[許可]** :ユーザーは PIN に数字を使用することができますが、その必要はありません。  

      - **必須**:ユーザーは PIN に数字を 1 文字以上含める必要があります。  

      - **許可しない**:ユーザーは PIN に数字を使用できません。

    - **生体認証のジェスチャを有効にする**:顔認識や指紋などの生体認証を使用します。 これらのモードは、Windows Hello for Business の PIN の代わりに使用できます。 ユーザーは、生体認証に失敗した場合のために、PIN を引き続き構成します。  

      **[はい]** に設定されている場合は、Windows Hello for Business で生体認証を利用できます。 **[いいえ]** に設定されている場合、Windows Hello for Business ではどのアカウントの種類に対しても生体認証を利用できません。  

    - **高度なスプーフィング対策の使用**:デバイスでサポートされている場合に拡張スプーフィング対策を構成します。 **[はい]** に設定すると、サポートされている場合、Windows のすべてのユーザーが、顔の特徴のスプーフィング対策を使用する必要があります。  

    - **[電話によるサインインの使用]** :携帯電話による 2 要素認証を構成します。

1. ウィザードを完了します。

次のスクリーンショットは、Windows Hello for Business プロファイル設定の例です。  

![使用可能な設定の一覧を表示する Windows Hello for Business ポリシー ウィザード](../media/hello-for-business-settings.png)

## <a name="configure-permissions"></a>アクセス許可を構成します

1. ドメイン管理者または同等の資格情報として、次のオプション機能がインストールされている、セキュリティで保護された管理ワークステーションにサインインします。RSAT:Active Directory Domain Services とライトウェイト ディレクトリ サービス ツール。

1. **[Active Directory ユーザーとコンピューター]** コンソールを開きます。

1. ドメインを選択し、 **[アクション]** メニューに進み、 **[プロパティ]** を選択します。

1. **[セキュリティ]** タブに切り替え、 **[詳細設定]** を選択します。

    > [!TIP]
    > **[セキュリティ]** タブが表示されない場合は、[プロパティ] ウィンドウを閉じます。 **[表示]** メニューに移動し、 **[拡張機能]** を選択します。

1. **[追加]** を選択します。

1. **[プリンシパルの選択]** を選択し、「`Key Admins`」と入力します。

1. **[適用先]** リストから **[Descendant User objects (子孫ユーザー オブジェクト)]** を選択します。

1. ページの下部にある **[すべてクリア]** を選択します。

1. **[プロパティ]** セクションで **[Read msDS-KeyCredentialLink (msDS-KeyCredentialLink を読む)]** を選択します。

1. **[OK]** を選択して変更を保存し、すべてのウィンドウを閉じます。

## <a name="next-steps"></a>次のステップ

[証明書プロファイル](introduction-to-certificate-profiles.md)