---
title: VDI クライアントを管理する
titleSuffix: Configuration Manager
description: 仮想デスクトップ インフラストラクチャ (VDI) で Configuration Manager クライアントを管理します。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6df9238cd81f14a64a42c45136c778357acb89c4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126952"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>仮想デスクトップ インフラストラクチャ (VDI) で Configuration Manager クライアントを管理します

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager では、次の仮想デスクトップ インフラストラクチャ (VDI) シナリオでの Configuration Manager クライアントのインストールがサポートされています。

- **パーソナル仮想マシン**:仮想マシン (VM) では、セッション間でユーザーのデータと設定が保持されます。

- **リモート デスクトップ サービス セッション**:集中管理されているサーバー上で複数の同時実行クライアント セッションをホストします。 ユーザーはセッションに接続し、そのサーバーでアプリケーションを実行します。

- **プール仮想マシン**:VM はセッション間で維持されません。 ユーザーがセッションを終了すると、この仮想環境では、すべてのデータと設定が破棄されます。 プール仮想マシンは、リモート デスクトップ サービスを使用できない場合に便利です。 たとえば、必要なアプリケーションを、クライアントセッションをホストする Windows Server で実行できない場合です。

- **Windows Virtual Desktop**:Microsoft Azure 上で実行されるデスクトップおよびアプリの仮想化サービスです。 バージョン 1906 以降では、Configuration Manager を使用して、Azure で Windows が実行されているこれらの仮想デバイスを管理できます。

## <a name="personal-vms"></a>パーソナル VM

Configuration Manager では、パーソナル VM を物理コンピューターと同じものとして扱います。 Configuration Manager クライアントは VM イメージにプレインストールするか、イメージのプロビジョニング後にプレインストールできます。

詳細については、[仮想環境のサポート](../../../plan-design/configs/support-for-virtualization-environments.md)に関するページを参照してください。

## <a name="remote-desktop-services"></a>リモート デスクトップ サービス

Configuration Manager クライアントは、個別のリモート デスクトップ セッションのためにインストールしません。 リモート デスクトップ サービスをホストするサーバーに 1 回インストールします。 リモート デスクトップ サービス サーバーですべての Configuration Manager クライアント機能を使用できます。

詳細については、「[リモート デスクトップ サービスへようこそ](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/welcome-to-rds)」を参照してください。

## <a name="pooled-vms"></a>プール VM

プール仮想マシンの使用を停止すると、Configuration Manager によって行われた変更が失われます。

VM は短い期間だけ運用される可能性があるため、一部の Configuration Manager 機能からは関連データが返されないことがあります。 たとえば、ハードウェア インベントリ、ソフトウェア インベントリ、ソフトウェア使用状況測定などです。 インベントリ タスクからプール VM を除外することを考慮してください。

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

詳細については、「[クライアントとデバイスのサポートされるオペレーティング システム](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)」をご覧ください。

## <a name="other-considerations"></a>その他の考慮事項

仮想化では、同一の物理コンピューターでの複数の Configuration Manager クライアントの実行がサポートされるため、多くのクライアント操作には、スケジュールされた操作で、組み込みのランダム待機時間があります。 たとえば、ハードウェアおよびソフトウェア インベントリ、マルウェア対策スキャン、ソフトウェアのインストール、ソフトウェア更新プログラムのスキャンなどです。 この待機時間に、Configuration Manager クライアントを実行する複数の VM を持つサーバーの CPU 処理とデータ転送を分散することができます。

保守モードの Windows Embedded クライアントを除き、仮想化環境にない Configuration Manager クライアントでも、このランダム待機時間が使用されます。 この動作により、ネットワーク帯域幅のピークを回避できます。 また、管理ポイントやサイト サーバーなど、サイト システムで CPU 処理が減ります。 待機時間の間隔は、Configuration Manager の機能によって変わります。 たとえば、クライアント設定に関するページの「[期限のランダム化を無効にする](../about-client-settings.md#disable-deadline-randomization)」を参照してください。

複数のユーザー セッションをサポートする仮想環境で Configuration Manager クライアントのパフォーマンスを上げるため、既定ではユーザー ポリシーが無効になります。 バージョン 1910 以降、このシナリオでユーザー ポリシーを有効にすることができます。 詳細については、クライアント設定に関するページの「[複数のユーザー セッションに対してユーザー ポリシーを有効にします](../about-client-settings.md#enable-user-policy-for-multiple-user-sessions)」を参照してください。
