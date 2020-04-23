---
title: ユーザーとデバイスの関連付け
titleSuffix: Configuration Manager
description: オペレーティング システムを展開するときに、ユーザーをセットアップ先のコンピューターと関連付けるように、Configuration Manager を構成します。
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f3a77e06dd2502b9007244ff9a3c9c9922fea592
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709010"
---
# <a name="associate-users-with-a-destination-computer-in-configuration-manager"></a>Configuration Manager でユーザーをセットアップ先のコンピューターに関連付ける

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager を使ってオペレーティング システムを展開するときに、ユーザーを展開先のコンピューターと関連付けることができます。 このオプションは、展開先コンピューターのプライマリ ユーザーが 1 人でも複数でも機能します  

ユーザーとデバイスのアフィニティは、アプリケーションを展開するときにユーザー中心の管理をサポートします。 OS をインストールするセットアップ先のコンピューターにユーザーを関連付けると、後でそのユーザーにアプリケーションを展開することにより、セットアップ先のコンピューターにアプリケーションが自動的にインストールされるようになります。 OS を展開するときにユーザーとデバイスのアフィニティのサポートを構成できますが、ユーザーとデバイスのアフィニティを使用して OS を展開することはできません。  

ユーザーとデバイスのアフィニティの詳細については、「[ユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)」をご覧ください。  

複数の方法を使用して、OS の展開にユーザーとデバイスのアフィニティを統合できます。 ユーザーとデバイスのアフィニティは、PXE 展開、起動可能なメディアの展開、事前設定されたメディアの展開に統合することができます。  


### <a name="create-a-task-sequence-that-includes-the-smstsassignusersmode-variable"></a>**SMSTSAssignUsersMode** 変数を含むタスク シーケンスを作成する

[タスク シーケンス変数の設定](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)ステップを使用することで、タスク シーケンスの最初に **SMSTSAssignUsersMode** 変数を追加します。 この変数は、タスク シーケンスでのユーザー情報の処理方法を指定します。

詳しくは、「[タスク シーケンス変数](../understand/task-sequence-variables.md#SMSTSAssignUsersMode)」をご覧ください。


### <a name="create-a-prestart-command-that-gathers-the-user-information"></a>ユーザー情報を収集する起動前コマンドを作成する

起動前コマンドには、入力ボックスを含む VBScript を使用できます。 ユーザーが入力したデータを検証する HTML アプリケーション (HTA) にすることもできます。 

この起動前コマンドでは、タスク シーケンスの実行時に使用される **SMSTSUDAUsers** 変数を設定する必要があります。 この変数は、コンピューター、コレクション、あるいはタスク シーケンスの変数にも設定することができます。

詳しくは、「[タスク シーケンス変数](../understand/task-sequence-variables.md#SMSTSUDAUsers)」をご覧ください。


### <a name="configure-how-distribution-points-and-media-associate-the-user-with-the-destination-computer"></a>配布ポイントとメディアによるユーザーと展開先コンピューターの関連付けを構成する

配布ポイントまたはメディアでは、OS が展開されている展開先コンピューターとユーザーの関連付けがサポートされています。 次のいずれかの方法を使用します。 

- [PXE ブート要求を受け入れるための配布ポイントを構成する](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)  
- [起動可能なメディアの作成](../deploy-use/create-bootable-media.md)  
- [事前設定されたメディアを作成する](../deploy-use/create-prestaged-media.md)  


ユーザーとデバイスのアフィニティのサポートの構成には、ユーザー ID を検証する方法は組み込まれていません。 この動作は、技術者がコンピューターをプロビジョニングするときに、ユーザーに代わって情報を入力するときに重要になります。 タスク シーケンスによるユーザー情報の処理方法の設定に加えて、配布ポイントとメディアにこれらのオプションを構成することで、PXE ブートや特定の種類のメディアからの展開開始を制限することができます。
