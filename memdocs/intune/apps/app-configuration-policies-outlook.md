---
title: Intune を使用して iOS および Android 用の Outlook を管理する
description: iOS および Android 用の Outlook で Intune アプリ保護および構成ポリシーを使用して、確実にチーム コラボレーションのエクスペリエンスが常に保護付きでアクセスされるようにすることができます。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3db207e4c1c75706c1f54762bf74c1757d342ac1
ms.sourcegitcommit: c7afcc3a2232573091c8f36d295a803595708b6c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84973045"
---
# <a name="manage-messaging-collaboration-access-by-using-outlook-for-ios-and-android-with-microsoft-intune"></a>Microsoft Intune で iOS および Android 用の Outlook を使用してメッセージングおよびコラボレーションへのアクセスを管理する

iOS および Android 用の Outlook アプリは、メール、予定表、連絡先、その他のファイルを 1 か所にまとめることにより、組織内のユーザーが自身のモバイル デバイスからより多くのことを実行できるように設計されています。

Office 365 データの豊富で広範な保護機能は、Enterprise Mobility + Security スイートにサブスクライブすると利用できます。これには、条件付きアクセスなどの Microsoft Intune と Azure Active Directory Premium の機能が含まれます。 少なくとも、モバイル デバイスから iOS および Android 用の Outlook への接続を許可する条件付きアクセス ポリシーと、コラボレーション エクスペリエンスが保護されることを保証する Intune のアプリ保護ポリシーを展開することをお勧めします。

## <a name="apply-conditional-access"></a>条件付きアクセスを適用する
組織は Azure AD 条件付きアクセス ポリシーを使用して、ユーザーが iOS および Android 用の Outlook を使用して確実に職場または学校のコンテンツにのみアクセスできるようにすることができます。 これを行うには、可能性のあるすべてのユーザーを対象とする条件付きアクセス ポリシーが必要です。 このポリシーの作成の詳細については、[条件付きアクセスを使用してクラウド アプリへのアクセスにアプリ保護ポリシーを要求する方法](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access)に関するページを参照してください。

1. 「[シナリオ 1: Office 365 アプリで、承認済みアプリとアプリ保護ポリシーの使用を必須にする](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies)」の「ステップ 1: Office 365 用の Azure AD 条件付きアクセス ポリシーを構成する」に従い、iOS および Android 用の Outlook が Exchange Online に接続することを許可し、OAuth 対応 Exchange ActiveSync クライアントはブロックします。

   > [!NOTE]
   > このポリシーにより、モバイル ユーザーは適用可能なアプリを使用してすべての Office エンドポイントに確実にアクセスできます。

2. 「[シナリオ 1: Office 365 アプリで、承認済みアプリとアプリ保護ポリシーの使用を必須にする](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies)」の「ステップ 2: ActiveSync (EAS) を使用する Exchange Online 用の Azure AD 条件付きアクセス ポリシーを構成する」に従い、基本認証を利用する Exchange ActiveSync クライアントが、Exchange Online に接続できないようにします。

   上記のポリシーでは、許可の制御の[[アプリの保護ポリシーが必要]](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference) を利用します。これにより、アクセスを許可する前に、iOS および Android 用の Outlook 内の関連するアカウントに Intune のアプリ保護ポリシーが確実に適用されます。 ユーザーが Intune のアプリ保護ポリシーに割り当てられていない場合、Intune のライセンスが付与されていない場合、またはアプリが Intune アプリ保護ポリシーに含まれていない場合、ポリシーにより、そのユーザーがアクセス トークンを取得してメッセージング データにアクセスできないようにします。

3. 最後に、「[方法: 条件付きアクセスを使用して Azure AD へのレガシ認証をブロックする](https://docs.microsoft.com/azure/active-directory/conditional-access/block-legacy-authentication)」に従い、iOS および Android デバイス上の他の Exchange プロトコルのレガシ認証をブロックします。このポリシーでは、Office 365 Exchange Online クラウド アプリと、iOS および Android デバイス プラットフォームのみを対象にする必要があります。 これにより、基本認証を使用する Exchange Web サービス、IMAP4、または POP3 プロトコルを使用しているモバイル アプリは、Exchange Online に接続できなくなります。

## <a name="create-intune-app-protection-policies"></a>Intune のアプリ保護ポリシーを作成する

アプリ保護ポリシー (APP) では、組織データの使用を許可されるアプリとそのデータに対して実行できる操作を定義します。 APP で利用できる選択肢を使用することで、組織は固有のニーズに合わせて保護を調整できます。 場合によっては、完全なシナリオを実装するためにどのポリシー設定が必要であるかが明確ではないことがあります。 組織がモバイル クライアント エンドポイントのセキュリティ強化を優先できるよう、Microsoft では、iOS および Android モバイル アプリ管理のための APP データ保護フレームワークの分類を導入しました。

APP データ保護フレームワークは 3 つの異なる構成レベルに編成されており、各レベルは前のレベルを基に構築されています。

- **エンタープライズ基本データ保護** (レベル 1) では、アプリが PIN で保護され、暗号化されており、選択的ワイプ操作を実行できるようにします。 Android デバイスの場合、このレベルでは Android デバイスの構成証明を検証します。 これは、Exchange Online メールボックス ポリシーに類似したデータ保護制御を提供し、IT 部門およびユーザー集団に APP を経験させる、エントリ レベルの構成です。
- **エンタープライズ拡張データ保護** (レベル 2) では、APP データ漏えい防止メカニズムと OS の最小要件が導入されています。 この構成は、職場または学校のデータにアクセスするほとんどのモバイル ユーザーに適用されます。
- **エンタープライズ高度データ保護** (レベル 3) では、高度なデータ保護メカニズム、強化された PIN の構成、および APP Mobile Threat Defense が導入されています。 この構成は、危険度の高いデータにアクセスするユーザーに適しています。

各構成レベルおよび、最低限保護する必要のあるアプリに関する具体的な推奨事項については、「[アプリ保護ポリシーを使用するデータ保護フレームワーク](app-protection-framework.md)」を参照してください。

デバイスが統合エンドポイント管理 (UEM) ソリューションに登録されているかどうかに関係なく、「[アプリ保護ポリシーを作成して割り当てる方法](app-protection-policies.md)」の手順を使用して、iOS アプリと Android アプリの両方に対して Intune アプリ保護ポリシーを作成する必要があります。 これらのポリシーは、少なくとも次の条件を満たしている必要があります。

1. Microsoft Edge、Outlook、OneDrive、Office、Teams など、すべての Microsoft 365 モバイル アプリケーションを含める。これにより、ユーザーは Microsoft アプリ内の職場または学校のデータに対し、セキュリティで保護された方法でアクセスして操作できることが保証されます。

2. すべてのユーザーに割り当てられている。 これにより、iOS および Android 用の Outlook のどちらを使用しているかに関係なく、すべてのユーザーが確実に保護されます。

3. 要件を満たすフレームワーク レベルを決定する。 ほとんどの組織では、データ保護とアクセス要件の制御を可能にするために、**エンタープライズ拡張データ保護** (レベル 2) に定義されている設定を実装する必要があります。

利用可能な設定について詳しくは、「[Android アプリ保護ポリシー設定](app-protection-policy-settings-android.md)」と「[iOS アプリ保護ポリシー設定](app-protection-policy-settings-ios.md)」をご覧ください。

> [!IMPORTANT]
> Intune に登録されていない Android デバイス上のアプリに対して Intune アプリ保護ポリシーを適用するには、ユーザーが Intune ポータル サイトもインストールする必要があります。 詳しくは、「[アプリ保護ポリシーを使用して Android アプリを管理するときの注意点](../fundamentals/end-user-mam-apps-android.md)」を参照してください。

## <a name="utilize-app-configuration"></a>アプリ構成を利用する

iOS および Android 用の Outlook では、Microsoft Endpoint Manager などの統合エンドポイント管理の管理者がアプリの動作をカスタマイズできるようにするアプリ設定がサポートされています。

アプリ構成を配信するには、登録済みデバイスのモバイル デバイス管理 (MDM) OS チャネル (iOS 用の[マネージド アプリ構成](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html)チャネルまたは Android 用の [Android in the Enterprise](https://developer.android.com/work/managed-configurations) チャネル) を使用するか、または Intune アプリ保護ポリシー (APP) チャネルを使用します。 iOS および Android 用の Outlook では、次の構成シナリオがサポートされています。

- 職場または学校アカウントのみ許可
- 一般的なアプリ構成設定
- S/MIME 設定
- データ保護設定

iOS および Android 用 Outlook でサポートされるアプリ構成設定に関する特定の手順と詳細なドキュメントについては、「[Deploying Outlook for iOS and Android app configuration settings](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)」 (iOS および Android 用 Outlook のアプリ構成設定の展開) を参照してください。

## <a name="next-steps"></a>次のステップ

- [アプリ保護ポリシーとは?](app-protection-policy.md) 
- [Microsoft Intune 用アプリ構成ポリシー](app-configuration-policies-overview.md)