---
title: Windows 10 をアップグレードする
titleSuffix: Configuration Manager
description: デバイスを Windows 10 バージョン 1709 以降 (共同管理に必要) にアップグレードする
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e11a6130fb9f7d86b7d3377cc4120d4e61c43d2d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691200"
---
# <a name="upgrade-windows-10-for-co-management"></a>共同管理のために Windows 10 をアップグレードする

共同管理への組織のオンボードに向けて取り組んでいる場合、現状を把握することは、一部の顧客にとって大きな壁となります。 共同管理には [Windows 10 バージョン 1709](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709) 以降が必要です。 Windows を更新し、自動登録を構成すると、クライアントは自動的に共同管理に登録されます。

次のビデオでは、シニア プログラム マネージャーの Rob York とプロダクト マーケティング マネージャーの Locky Ainley が共同管理のための Windows 10 へのアップグレードについて説明し、デモを行っています。

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>アップグレードする理由

プラットフォームの進歩は他にもありますが、特に Windows 10 バージョン 1709 以降では自動登録がサポートされます。 この動作により、デバイスは、Azure Active Directory (Azure AD) への参加時に Intune に自動的に登録されます。 

詳細については、「[Windows 10 の自動登録を有効にする](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)」を参照してください。


## <a name="how-to-do-it"></a>実行方法

数千もの顧客がすぐに現状を把握できるようにすることで学んだいくつかのヒントを以下に示します。

- 段階的な展開を使用して、適切なタイミングで適切な人員にこのアップグレードをロールアウトします。 詳しくは、「[段階的展開の作成](../osd/deploy-use/create-phased-deployment-for-task-sequence.md)」をご覧ください。  

- 事前キャッシュを使用して、ユーザー待機時間を減らします。 詳細については、「[コンテンツの事前キャッシュを構成する](../osd/deploy-use/configure-precache-content.md)」を参照してください。  

- 既定のインプレース アップグレード タスク シーケンスを使用します。 その後、アップグレードの前と後の手順、およびエラー アクションを構成します。 詳細については、「[推奨される処理後のタスク シーケンス ステップ](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-for-post-processing)」を参照してください。  

- ご利用の環境に高度なモバイル ワーカーが存在する場合、Configuration Manager ではクラウド管理ゲートウェイ (CMG) 経由でのインプレース アップグレードがサポートされます。 この機能では、Windows 10 クライアントがインターネットベースである場合、そのクライアントをアップグレードすることができます。 CMG の詳細については、「[CMG を通して Windows 10 の一括アップグレードを展開する](../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg)」を参照してください。  

- 早期導入者となることを望んでいるユーザーに、共同管理へのオプトインを提供します。 このアプローチでは初期導入が促進されます。 これらのユーザーを事前に識別することによって、確実にロールアウトの初期段階で適切に対応することができます。 変更内容に満足し、より頻繁なリリースに興味のあるユーザーからの検証およびフィードバックも受け取ります。 早期導入者プログラムは新しいテクノロジに興味を抱かせ、時間の経過と共に規模が大きくなります。  


## <a name="case-studies"></a>導入事例

Microsoft IT 部門では、Windows 10 を Microsoft の 96,000 人の分散ユーザーに展開しました。 展開先にはリモート ユーザーと、企業ネットワーク上のユーザーの両方が含まれていました。 展開は 9 週間で完了しました。 このエクスペリエンスの詳細については、「[Deploying Windows 10 at Microsoft as an in-place upgrade](https://www.microsoft.com/itshowcase/deploying-windows-10-at-microsoft-as-an-in-place-upgrade)」 (インプレース アップグレードとしての Microsoft での Windows 10 の展開) を参照してください。  

ヨーロッパの大規模なソフトウェア製造元では、早期導入者グループが適切に使用されています。 グループの初期テストとパイロット運用後に、約 2,000 人の従業員が最初の更新プログラム、アップグレード、およびソフトウェアを受け取ります。 このグループには、IT スタッフやオプトイン ボランティアが含まれます。 ユーザーとのこのレベルのエンゲージメントにより、テスト時により高いレベルの確実性が得られ、大規模なロールアウトの開始時により高い信頼性が得られます。



## <a name="contact-fasttrack"></a>FastTrack への問い合わせ

プロセスの任意の時点で Windows 10 のアップグレード サポートが必要な場合は、[Microsoft FastTrack](https://Microsoft.com/FastTrack/) に移動し、サインインしてサポートを要求してください。 

詳細については、[FastTrack からのサポートの取得](quickstart-fasttrack.md)に関するページを参照してください。 

