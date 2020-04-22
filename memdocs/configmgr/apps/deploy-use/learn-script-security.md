---
title: PowerShell スクリプトのセキュリティの詳細情報
titleSuffix: Configuration Manager
description: PowerShell スクリプトのセキュリティの詳細を確認するのに役立つリソースです。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a0edf83c736c2737f4af2f040159a71bb0348aee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689310"
---
# <a name="learn-more-about-powershell-script-security"></a>PowerShell スクリプトのセキュリティの詳細情報

*適用対象:Configuration Manager (Current Branch)*

環境内で提案された PowerShell および PowerShell パラメーターの使用方法を検証するのは管理者の責任です。 ここでは、PowerShell の機能と潜在的なリスク領域について管理者を教育するのに役立つリソースをいくつか示します。 これは、潜在的なリスク領域を減らし、安全なスクリプトを使用できるようにするためのものです。

## <a name="powershell-script-security"></a>PowerShell スクリプトのセキュリティ
スクリプトの実行には、環境内で実行するように要求されるスクリプトを視覚的に確認して承認する機能が組み込まれています。 管理者は、PowerShell スクリプトに難読化されたスクリプトが含まれている可能性があることを認識する必要があります。このようなスクリプトは悪意があり、スクリプトの承認プロセス時の目視検査で検出するのは困難です。 PowerShell スクリプトを視覚的に確認することに加え、特定の検査ツールを使用することをお勧めします。これらは疑わしいスクリプトの問題を検出するのに役立ちます。 必ずしもこれらのツールで PowerShell の作成者の意図を判断し、疑わしいスクリプトに注意を向けさせることができるわけではありません。 ただし、ツールを使用する場合、悪意のある、または意図的なスクリプト構文があるかどうかを管理者が判断する必要があります。

## <a name="recommendations"></a>推奨事項
- 以下のさまざまな参照リンクを使用して、PowerShell のセキュリティに関するベスト プラクティスをよく理解しておいてください。
- **スクリプトに署名する**:スクリプトを安全な状態に保つための別の方法です。スクリプトの検査と署名後に、インポートして使用するようにします。
- PowerShell スクリプトにはシークレット (パスワードなど) を格納しないでください。シークレットの処理方法の詳細を確認してください。


## <a name="general-information-about-powershell-security-best-practices"></a>PowerShell のセキュリティのベスト プラクティスに関する一般情報

このリンク コレクションは、Configuration Manager 管理者が PowerShell のセキュリティに関するベスト プラクティスを確認する際の開始点を示すために選択されたものです。  

[PowerShell のセキュリティのベスト プラクティスの概要](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ )

[PowerShell のセキュリティのベスト プラクティス (PowerPoint)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[PowerShell 攻撃に対する防御 (PowerShell チーム ブログ)](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/)

[PowerShell 攻撃に対する防御に関するツイッター (Microsoft PowerShell およびセキュリティ アドボケート Lee Holmes より)](https://twitter.com/Lee_Holmes/status/922462821081694208)

[悪意のあるコード インジェクションに対する防御](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/)

[PowerShell The Blue Team (詳細なスクリプト ブロック ログ、保護されたイベント ログ、マルウェア対策スキャン インターフェイス、セキュリティで保護されたコード生成 API に関するディスカッション)](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

[Windows 10 の場合、マルウェア対策スキャン インターフェイスの API がある](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## <a name="powershell-parameters-security"></a>PowerShell のパラメーターのセキュリティ
パラメーターの受け渡しは、スクリプトに柔軟性を持たせ、実行時まで決定を延期する方法です。 別のリスク領域を開くことにもなります。 悪意のあるパラメーターまたはスクリプト インジェクションを防ぐためのベスト プラクティスを以下に示します。

- 定義済みパラメーターの使用のみを許可します。
- 正規表現機能を使用して、許可されているパラメーターを検証します。
    - 例:特定範囲の値のみが許可されている場合、正規表現を使用して、範囲を構成できる文字または値のみを確認します。
    - パラメーターの検証は、ユーザーが引用符など、エスケープ可能な特定の文字の使用を試行できないようにするのに役立ちます。 複数の種類の引用符が存在する可能性があるため、正規表現を使用して、決定したどの文字が許容されるかを検証することは、多くの場合、許容されないすべての入力の定義を試行するよりも簡単であることに注意してください。
- PowerShell ギャラリーの PowerShell モジュール ["インジェクション ハンター"](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) を利用します。
    - 誤検知である可能性があるため、疑わしいものとしてフラグが設定されている場合は、その意図を探り、実際の問題であるかどうかを判断してください。 
- Microsoft Visual Studio には Script Analyzer があります。これは、PowerShell 構文を確認するのに役立ちます。
- 以下の"DEF CON 25 - Lee Holmes - Get $pwnd:Attacking Battle Hardened Windows Server" (堅牢な Windows Server で攻撃に対抗) というタイトルのビデオでは、保護できる問題の種類の概要が示されています (特に、セクション 12:20 から 17:50)。    <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>環境の推奨事項
PowerShell 管理者用の一般的な推奨事項です。
1. Windows 10 に組み込まれている最新バージョン (バージョン 5 以降など) の PowerShell を展開します。 または、[Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616) を展開することもできます。 
2. PowerShell ログを有効にして収集します (必要に応じて、保護されているイベント ログを含む)。 これらのログを署名、ハンティング、およびインシデント応答ワークフローに組み込みます。
3. 高価値システムに Just Enough Administration を実装し、これらのシステムへの制限のない管理アクセスをなくす、または減らします。
4. PowerShell 言語の限定されたサブセットに対する対話型および未承認の使用を制限しながら、事前承認済みの管理タスクで PowerShell 言語の全機能を使用できるようにする Windows Defender アプリケーション制御ポリシーを展開します。
5. Windows 10 を展開して、PowerShell を含む Windows Scripting Host で処理されるすべてのコンテンツ (実行時に生成または難読化解除されたコンテンツを含む) へのフル アクセス権をウイルス対策プロバイダーに付与します。
