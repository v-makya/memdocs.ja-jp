---
title: 共同管理での条件付きアクセス
titleSuffix: Configuration Manager
description: Intune からコンプライアンス規則に基づいて組織のリソースへのユーザー アクセスを制御する
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d35f36b6578359f62f21b4e2208a70ace22cf0d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691260"
---
# <a name="conditional-access-with-co-management"></a>共同管理での条件付きアクセス

条件付きアクセスでは、信頼されたユーザーのみが信頼されたアプリを使用して、信頼されたデバイス上の組織のリソースに確実にアクセスできるようにします。 これはクラウドで最初から構築されます。 Intune でデバイスを管理するか、共同管理で Configuration Manager 展開を拡張するかに関係なく、同じように動作します。

次のビデオでは、シニア プログラム マネージャーの Joey Glocke とプロダクト マーケティング マネージャーの Locky Ainley が共同管理での条件付きアクセスについて説明し、デモを行っています。

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

共同管理では、Intune でネットワーク内のすべてのデバイスを評価し、どの程度信頼できるかを判断します。 この評価は次の 2 つの方法で行われます。

1. Intune で、デバイスまたはアプリが管理されており、安全に構成されていることが確認されます。 この確認は、組織のコンプライアンス ポリシーを設定する方法によって異なります。 たとえば、すべてのデバイスで暗号化が有効になっており、脱獄されていないことを確認します。  

    - この評価はセキュリティ違反前のものであり、構成ベースとなります  

    - 共同管理デバイスの場合、Configuration Manager で構成ベースの評価も行われます。 たとえば、必要な更新プログラムまたはアプリのコンプライアンスです。 Intune では、この評価を独自の判断と組み合わせます。  

2. Intune で、デバイス上のアクティブなセキュリティ インシデントを検出します。 [Microsoft Defender Advanced Threat Protection](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (以前の Windows Defender ATP) およびその他の[モバイル脅威対策プロバイダー](https://www.lookout.com/about/partners/microsoft)のインテリジェント セキュリティが使用されます。 これらのパートナーは、デバイス上で継続的な行動分析を実行します。 この分析ではアクティブなインシデントを検出してから、この情報を、リアルタイムのコンプライアンス評価のために Intune に渡します。  

    - この評価はセキュリティ違反後のものであり、インシデント ベースとなります  

Microsoft 社の副社長である Brad Anderson が、Ignite 2018 の基調講演時にライブ デモで条件付きアクセスの詳細について説明しています。 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

条件付きアクセスでは、ネットワークに接続されているすべてのデバイスの正常性を 1 か所で確認することもできます。 Configuration Manager の実稼働インスタンスのテストで特に有用な、クラウド規模の利点が得られます。


## <a name="benefits"></a>利点

すべての IT チームは、ネットワーク セキュリティのことで頭がいっぱいです。 すべてのデバイスが、ネットワークにアクセスする前に、セキュリティとビジネスの要件を満たしていることを確認する必要があります。 条件付きアクセスでは、次の要因を判断できます。 
- すべてのデバイスが暗号化されているかどうか  
- マルウェアがインストールされているかどうか  
- その設定が更新されているかどうか  
- それが脱獄またはルート化されているかどうか  

条件付きアクセスでは、組織のデータのより詳細な制御を、あらゆる場所のあらゆるデバイスでの従業員の生産性を最大化するユーザー エクスペリエンスと組み合わせます。

次のビデオでは、[Advanced Threat Protection](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) が、定期的に発生する一般的なシナリオにどのように統合されるかが示されています。

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

共同管理では、Intune で、必要な更新プログラムまたはアプリのセキュリティ標準への準拠を評価することに対する Configuration Manager の責任を組み込むことができます。 この動作は、複雑なアプリおよび修正プログラムの管理に Configuration Manager を引き続き使用する必要がある、すべての IT 組織にとって重要です。

条件付きアクセスは、[ゼロ トラスト ネットワーク](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/) アーキテクチャの開発の重要な部分でもあります。 条件付きアクセスでは、ゼロ トラスト ネットワークの基礎レイヤーが準拠デバイス アクセス制御の対象となります。 この機能は、今後、組織をセキュリティで保護する方法の大きな部分となります。

詳細については、「[Enhancing conditional access with machine-risk data from Microsoft Defender Advanced Threat Protection](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559)」 (Microsoft Defender Advanced Threat Protection からのマシンリスク データによる条件付きアクセスの拡張) のブログ投稿を参照してください。



## <a name="case-studies"></a>導入事例

IT コンサルティング会社の Wipro では条件付きアクセスを使って、91,000 人のすべての従業員が使用するデバイスを保護して管理しています。 最近の導入事例で、Wipro の IT 部門の副社長は、次のように語っています。

> *条件付きアクセスの実現は、Wipro にとって大きな利点となります。現在、すべての従業員は必要に応じて、情報にモバイル アクセスすることができます。* 
> *セキュリティ体制と従業員の生産性が向上しました。現在、91,000 人の従業員が、あらゆる場所のあらゆるデバイスからの 100 個を超えるアプリへの高度にセキュアなアクセスの利点を得ています。*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

その他の例は次のとおりです。 

- Nestlé では、150,000 人を超える従業員のためにアプリベースの条件付きアクセスを使用しています  

- 自動化ソフトウェア会社の Cadence では、現在、"マネージド デバイスのみから、Teams などの Office 365 アプリや会社のイントラネットにアクセスできる" ようにしています。 従業員が "Workday や Salesforce などに他のクラウドベース アプリにより安全にアクセスできるようにもしています"。 Intune での Cadence のエクスペリエンスの詳細については、「[Cadence increases the pace of business with mobile collaboration tools in Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365)」 (Cadence では Microsoft 365 でモバイル コラボレーション ツールを使用することでビジネスのペースを上げた) を参照してください。

Intune は、Cisco ISE、Aruba Clear Pass、Citrix NetScaler などのパートナーとも完全に統合されています。 これらのパートナーと共に、Intune 登録とこれらの他のプラットフォーム全体でのデバイスのコンプライアンス状態に基づいて、アクセス制御を維持できます。

詳細については、以下のビデオをご覧ください。
- [Brad Anderson による条件付きアクセスの詳細なデモ](https://youtu.be/8321obNofgM?t=547)  
- [Endpoint Zone 1805 からの追加の詳細情報](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>価値提案

条件付きアクセスと ATP を統合することで、すべての IT 組織の基本要素 (セキュア クラウド アクセス) を強化します。

すべてのデータ侵害のうち、63% を超える侵害で、攻撃者は脆弱、既定、あるいは盗んだユーザー資格情報で組織のネットワークにアクセスしています。 条件付きアクセスはユーザー ID をセキュリティで保護することに重点を置いているため、資格情報の盗難が抑制されます。 条件付きアクセスでは ID を管理して保護します。特権であるか非特権であるかは関係ありません。 デバイスとそのデバイス上にあるデータを保護するのに、これ以上優れた方法はありません。

条件付きアクセスは Enterprise Mobility + Security (EMS) のコア コンポーネントであるため、オンプレミスでの設定やアーキテクチャは必要ありません。 Intune と Azure Active Directory (Azure AD) を使用することで、クラウドでの条件付きアクセスをすばやく構成できます。 現在、Configuration Manager を使用している場合は、ご利用の環境を共同管理でクラウドに簡単に拡張し、その使用をすぐに開始できます。

ATP 統合の詳細については、このブログ投稿「[Microsoft Defender ATP device risk score exposes new cyberattack, drives Conditional access to protect networks](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/)」 (Microsoft Defender ATP デバイス リスク スコアで新しいサイバー攻撃を見つけて、条件付きアクセスでネットワークを保護する) を参照してください。 高度なハッカー グループがかつてないツールをどのように使用したかについて詳しく説明されています。 Microsoft クラウドではそれらを検出し、阻止しました。これは、ターゲットとなったユーザーが条件付きアクセスを利用していたためです。 侵入時に、デバイスのリスクベース条件付きアクセス ポリシーがアクティブになりました。 攻撃者は既にネットワークでの足掛かりを築いていましたが、悪用されたマシンでは自動的に、Azure AD によって管理されていた組織のサービスとデータへのアクセスが制限されました。



## <a name="configure"></a>構成

[共同管理を有効](how-to-enable.md)にすれば、条件付きアクセスは簡単に使用できます。 **コンプライアンス ポリシー** ワークロードを Intune に移動する必要があります。 詳細については、「[How to switch Configuration Manager workloads to Intune](how-to-switch-workloads.md)」 (Configuration Manager のワークロードを Intune に切り替える) を参照してください。 

条件付きアクセスの使用の詳細については、次の記事を参照してください。 

- [Azure AD の条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Intune のデバイス コンプライアンス ポリシー](https://docs.microsoft.com/intune/device-compliance)  

- [Intune でのアプリ ベースの条件付きアクセス](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> 条件付きアクセス機能は、ハイブリッド Azure AD 参加済みデバイスですぐに使用できるようになります。 これらの機能には、多要素認証とハイブリッド Azure AD 参加のアクセス制御が含まれます。 この動作は、Azure AD プロパティに基づいているためです。 Intune と Configuration Manager からの構成ベースの評価を利用するには、共同管理を有効にします。 この構成では、準拠しているデバイス用の Intune から直接アクセスを制御できます。 Intune のコンプライアンス ポリシー評価機能も提供されます。  

