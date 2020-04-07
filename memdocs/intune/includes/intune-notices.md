---
title: ファイルを含める
description: インクルード ファイル
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: 0b3af293ebc83c14f85abeb0dbaa38ca5187b267
ms.sourcegitcommit: 6a6a713fc1090e03893d80f4259dc7300fb1d5ff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80438713"
---
以下の通知では、今後の Intune の変更と機能に備えるために役立つ重要な情報が提供されます。

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Windows 10 Mobile 終了のための Microsoft Intune のサポート<!--3544938-->
Windows 10 Mobile の Microsoft メインストリーム サポートは、2019 年 12 月に終了しました。 このサポートの声明に記載されているように、Windows 10 Mobile のユーザーは、新しいセキュリティ更新プログラム、セキュリティ以外の修正プログラム、無償のサポート オプション、Microsoft からのオンライン技術コンテンツ更新プログラムを受け取ることができなくなります。 Microsoft Intune は、すべてのモバイル OS のサポートに基づいて、2020 年 5 月 11 日に Windows 10 Mobile アプリと Windows 10 Mobile オペレーティング システムの両方のポータル サイトのサポートを終了することになりました。

#### <a name="how-does-this-affect-me"></a>ユーザーへの影響
Windows 10 Mobile のデバイスが組織に展開されている場合、今から 2020 年 5 月 11 日まで、新しいデバイスを登録したり、ポリシーとアプリを追加または削除したり、管理設定を更新したりできます。 5 月 11 日以降は、新しい登録が停止され、最終的に Intune UI から Windows 10 Mobile の管理が削除されます。 デバイスが Intune サービスにチェックインされなくなり、デバイスとポリシーのデータが削除されます。  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>この変更に対して必要な準備
Intune レポートをチェックして、影響を受ける可能性のあるデバイスまたはユーザーを確認できます。 **[デバイス]**  >  **[すべてのデバイス]** の順に移動し、OS でフィルター処理します。 さらに列を追加して、Windows 10 Mobile を稼働しているデバイスを持つ組織内のユーザーの特定に役立てることができます。 エンド ユーザーに対して、デバイスのアップグレードや、会社にアクセスするためのデバイスの使用中止を要求してください。


### <a name="updated-support-statement-for-adobe-acrobat-reader-for-intune-mobile-app--5746776--"></a>'Adobe Acrobat Reader for Intune' モバイル アプリのサポート ステートメントが更新されました<!--5746776-->
8 月の終わりに、MC188653 で、Adobe Acrobat Reader for Intune モバイル アプリが 2019 年 12 月 1 日に有効期限終了になり、Adobe が同社のメインの Acrobat Reader アプリ内で Intune のアプリ保護ポリシーのサポートを計画していることをお知らせしました。 その後、お客様から、IT 管理者が引き続きターゲットを指定して、エンド ユーザーが Adobe Acrobat Reader for Intune の使用を開始できるようにするために、もっと時間を提供してもらう必要があるというフィードバックを受け取りました。 エンド ユーザーのデバイスで Adobe Acrobat Reader for Intune の使用率が高く、エンタープライズ シナリオでのその重要性を考慮すると、あらゆるエクスペリエンスが、組織のアプリ保護のニーズを満たすようにする必要があります。 

Acrobat Reader モバイル アプリはアプリ保護ポリシーをサポートし、Intune SDK を統合しているため、一般的な Acrobat Reader モバイル アプリをポリシーでターゲット設定することを引き続きお勧めしますが、Adobe Acrobat Reader for Intune アプリは 2020 年 3 月 31 日まで引き続きサポートされます。 

#### <a name="how-does-this-affect-me"></a>ユーザーへの影響
このメッセージが表示されるのは、組織内の 1 つ以上のポリシーが Adobe Acrobat Reader for Intune アプリケーションを対象としているか、以前の EOL 通信を受け取った可能性があることを Microsoft のレポートで示しているためです。 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>この変更に対して必要な準備
この変更について、エンド ユーザーとヘルプデスクに通知します。 [ポータル サイトのサポート情報機能](../apps/company-portal-app.md#support-information)を使用して、Intune 関連の質問のためのチャネルを確立できます。

#### <a name="additional-information"></a>追加情報
https://helpx.adobe.com/acrobat/kb/intune-app-end-of-life.html

### <a name="take-action-use-microsoft-edge-for-your-protected-intune-browser-experience--5728447--"></a>アクションの実行: 保護されている Intune ブラウザーエクスペリエンスに Microsoft Edge を使用する<!--5728447-->
過去 1 年にわたってお伝えしているように、Microsoft Edge モバイルでは Managed Browser と同じ管理機能セットをサポートしながら、エンド ユーザー エクスペリエンスも大幅に向上しています。 Microsoft Edge で提供されている堅牢なエクスペリエンスを推進するため、Intune Managed Browser を廃止します。 2020 年 1 月 27 日から、Intune では Intune Managed Browser がサポートされなくなります。  

#### <a name="how-does-this-affect-me"></a>ユーザーへの影響 
2020 年 2 月 1 日以降、Intune Managed Browser は Google Play ストアまたは iOS アプリ ストアでは入手できなくなります。 この時点では、新しいアプリ保護ポリシーを Intune Managed Browser に適用することはできますが、新しいユーザーは Intune Managed Browser アプリをダウンロードできません。 また、iOS では、MDM に登録されたデバイスにプッシュされた新しい Web クリップは、Intune Managed Browser ではなく Microsoft Edge で開きます。  

2020 年 3 月 31 日に、Intune Managed Browser は Azure コンソールから削除されます。 これで、Intune Managed Browser に新しいポリシーを作成できなくなります。 既に設定されている Intune Managed Browser ポリシーは影響を受けません。 Intune Managed Browser は、コンソールでアイコンのない基幹業務アプリとして表示され、既存のポリシーは引き続きアプリの対象として表示されます。 この時点で、[アプリ保護] ポリシーの [データ保護] セクション内の Intune Managed Browser に Web コンテンツをリダイレクトするオプションも削除されます。  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>この変更に対して必要な準備 
Intune Managed Browser から Microsoft Edge へのスムーズな移行を実現するために、次のステップを事前に行うことをお勧めします。 

1. アプリ保護ポリシー (MAM とも呼ばれます) とアプリ構成設定を使用して、Microsoft Edge を iOS と Android の対象とします。 これらの既存のポリシーを Microsoft Edge にも適用することで、Microsoft Edge で Intune Managed Browser のポリシーを再利用できます。  
2. 環境内のすべての MAM で保護されたアプリで、アプリ保護ポリシーの設定 [その他のアプリでの Web コンテンツの転送を制限する] が [ポリシーで管理されているブラウザー] に設定されているようにします。 
3. MAM で保護されているものすべてのマネージド アプリ構成設定 "com.microsoft.intune.useEdge" を true に設定します。 翌月以降の 1911 のリリースで、ステップ 2 と 3 を簡単に実行できるようになります。[アプリ保護] ポリシーの [データ保護] セクションで [その他のアプリでの Web コンテンツの転送を制限する] の設定に "Microsoft Edge" を含めるだけです。 

iOS および Android での Web クリップのサポートが予定されています。 このサポートがリリースされたら、既存の Web クリップの対象を再設定して、それらが Managed Browser ではなく Microsoft Edge で開くようにする必要があります。 

#### <a name="additional-information"></a>追加情報
詳細については、[Microsoft Edge とアプリ保護ポリシーの使用](../apps/manage-microsoft-edge.md)に関するドキュメント、または[サポートのブログ記事](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Use-Microsoft-Edge-for-your-Protected-Intune-Browser-Experience/ba-p/1004269)を参照してください。

### <a name="end-of-support-for-legacy-pc-management"></a>従来の PC 管理のサポート終了

従来の PC 管理は 2020 年 10 月 15 日にサポートが終了します。 デバイスを Windows 10 にアップグレードし、Intune による管理が継続されるようにモバイル デバイス管理 (MDM) デバイスとして再登録してください。

[詳細情報](https://go.microsoft.com/fwlink/?linkid=2107122)


