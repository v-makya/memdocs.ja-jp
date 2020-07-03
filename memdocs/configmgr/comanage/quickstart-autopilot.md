---
title: Windows Autopilot と共同管理
titleSuffix: Configuration Manager
description: Windows Autopilot と Configuration Manager の共同管理機能を利用し、新しい Windows 10 デバイスのセットアップを簡単にします。
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 91b938b5ab64616a35773406cd18b54de80b40e7
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590412"
---
# <a name="windows-autopilot-with-co-management"></a>Windows Autopilot と共同管理

新しい Windows 10 デバイスを手に入れることはうれしいことです。 しかしながら、生産的になるよう、すべての設定とアプリを構成するのに時間がかかります。 Windows Autopilot と共同管理でこのデバイス プロビジョニング問題を解決します。

Autopilot を利用すると、次のような状況で、管理者にとってもユーザーにとっても設定が簡単になります。
- 新しい Windows 10 デバイスを設定し、事前構成する  
- 既存のデバイスをリセット、リサイクル、復元する  

Autopilot を利用すると、デバイスの展開、管理、廃止に必要な時間が短くなり、リソースが少なくて済み、複雑性が緩和されます。 同時に、ユーザーにとっても操作性が合理的になり、最初の起動時から簡単に使用できます。

Windows Autopilot はいくつかのシナリオに対応しています。いずれのシナリオでも、Windows Autopilot は共同管理によって最大限に活用されます。

- ユーザーはハイブリッド Azure AD 参加または Azure Active Directory (Azure AD) を利用し、いずれかの Active Directory への新しいデバイスの独自のデプロイを推進できます  

- 共有デバイスやキオスクのために、Azure AD への新しいデバイスの自己デプロイを設定できます  

- 既存のデバイスに Windows Autopilot を有効にしている状態で、Configuration Manager を使用し、Windows 7 と Active Directory から Windows 10 と Azure AD に既存のデバイスを移行します  

次のビデオでは、シニア プログラム マネージャーの Danny Guillory とプリンシパル プログラム マネージャーの Andrew McMurray が Windows Autopilot と共同管理について説明し、デモを行います。

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>利点

共同管理と Autopilot を一緒に使用すると、ネットワークに追加した新しいデバイスの管理状態が同じになります。 このセットアップでは、デバイスは Intune に登録され、Configuration Manager クライアントが用意されます。  新しい Windows 10 プロビジョニング モデルを利用できます。カスタム OS イメージを作成、保守管理、更新する必要がありません。 

いずれのシナリオでも、Intune で自動的に[共同管理を有効にできます](how-to-prepare-Win10.md)。 この自動化はプロビジョニング プロセスとデバイスの継続的管理を支援します。

Autopilot を利用する場合、イメージやドライバーのことを気にする必要がありません。 共同管理から Intune と Configuration Manager を利用してイメージやドライバーのプロセスを自動化し、デバイスのプロビジョニングに集中してください。


共同管理と Autopilot を併用と次の効果がすぐに現れます。

#### <a name="reduce-time-costs-and-complexity"></a>時間の短縮、コストの節約、複雑性の緩和
Windows Autopilot では、デバイスにプレインストールされている OEM 最適化バージョンの Windows 10 が使用されます。 この構成によって、企業は、使用するデバイス モデルごとにカスタムのイメージやドライバーを保守管理する必要がなくなります。 デバイスのイメージを変更せずに、既存の Windows 10 インストールを "ビジネス対応" 状態に変換します。 設定とポリシーを適用し、アプリをインストールし、Windows 10 のエディションを変更します。 たとえば、高度な機能がサポートされるように、Windows 10 Pro から Windows 10 Enterprise にアップグレードします。

#### <a name="improve-the-user-experience"></a>ユーザー エクスペリエンスの向上
最高のユーザー エクスペリエンスは中断が最も少なく、自分の仕事に集中できます。 Windows Autopilot を利用すれば、ユーザーはわずか数回のクリックと Azure AD 資格情報ですぐにセットアップできます。 離れた場所にたくさんの従業員を抱える組織の場合、Windows Autopilot を使用し、新しいデバイスをメーカーから直送します。

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Autopilot と Configuration Manager を使用し、既存の Windows 7 デバイスを Windows 10 に移行する
既存のデバイスに Windows Autopilot を有効にしている状態で、構成ファイルを作成し、それを Configuration Manager タスク シーケンスで展開します。 このプロセスによって、Windows 7 から Windows 10 に既存のデバイスが簡単に移行されます。 Configuration Manager で特徴的な Windows 10 イメージを使用し、Autopilot 構成でそれを既存の Windows 7 デバイに適用します。 ユーザーはデバイスを開始するとき、Autopilot ユーザー駆動オンボード プロセスを使用します。

既存のデバイスに対する Autopilot の手順は次のようになります。

![既存デバイスの Windows Autopilot のプロセス概要](media/autopilot-for-existing-devices.png)

1. グループ ポリシーをデプロイし、既知のフォルダーを OneDrive にリダイレクトする
2. Autopilot 構成ファイルを生成する
3. タスク シーケンスをデプロイし、Windows 10 にアップグレードする
4. Windows 10 コンピューターが最初の起動で Autopilot を通過する

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>あらゆる種類の従業員に対するデバイス プロビジョニングを最新化する
Autopilot があれば、セルフデプロイ モードを利用することで手作業なしで無人デバイスや共有デバイスに OS をデプロイできます。 このセットアップは、あらゆる種類の従業員のニーズに応えます。 また、Windows Autopilot のリセット機能によって、新しいユーザーにデバイスを簡単に再プロビジョニングできます。 このプロセスによって、今まで季節労働者や契約社員を抱えているときに難しかった作業が簡単になります。 



## <a name="case-study"></a>導入事例

ドイツの物流/鉄道貨物運送会社である DB Schenker が Autopilot を利用して従業員の生産性を上げ、毎日のサポート作業から IT チームを解放しました。 DB Schenker は従来のイメージングを止め、クラウド経由のプロビジョニングに転向しました。 Azure AD 参加と Intune を利用し、新しいデバイスをすぐに導入できます。 

離れた場所にいる従業員に IT サービスのあるところまで来させ、時間を無駄にさせる代わりに、DB Schenker では現在、Windows Autopilot を利用しています。 従業員のハードウェアはメーカーから従業員の職場に直送されます。 従業員は新しいデバイスをインターネットに接続し、自分の Azure AD credentials. 資格情報でサインインします。 そのデバイスは、DB Schenker の IT 部門がユーザーの個別プロファイルに割り当てたアプリケーションとサービスに接続されます。

詳細については、「[Global logistics firm centralizes IT, unites employees with modern digital workplace](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10)」 (世界的な物流企業が IT を集中化し、最新のデジタル職場で従業員を団結させる) を参照してください。



## <a name="value-proposition"></a>価値提案

ユーザー エクスペリエンスを改善することで、満足度の高い職場を作ってください。 Windows Autopilot を利用すればコストが下がります。 他のプロジェクトに集中するための時間を増やし、組織の価値と影響力を上げてください。



## <a name="configure"></a>構成

詳細については、以下の記事を参照してください。

[Intune を使用し、Windows Autopilot プロファイルを作成する](https://docs.microsoft.com/intune/enrollment-autopilot)

[既存のデバイス向けの Windows Autopilot](../osd/deploy-use/windows-autopilot-for-existing-devices.md) タスク シーケンス

