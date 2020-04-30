---
title: クライアント イベント ログ
titleSuffix: Configuration Manager
description: Windows イベント ログで使用可能な BitLocker (MBAM) クライアント エントリのテクニカル リファレンス
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c38b6963-cb1f-40ed-a888-e19d401ec3fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4043af4aa30942a5e8e1f7d2a3d1017c1e72d89f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705970"
---
# <a name="client-event-logs"></a>クライアント イベント ログ

*適用対象:Configuration Manager (Current Branch)*

<!--3601034-->

BitLocker 管理ポリシーを展開する Configuration Manager クライアントで、Windows イベント ビューアーを使用して、BitLocker クライアント イベント ログを表示します。 **[アプリケーションとサービス ログ]** 、 **[Microsoft]** 、 **[Windows]** 、 **[MBAM]** に移動して、[[Admin]](#admin) イベント ログと [[Operational]](#operational) イベント ログを表示します。

## <a name="admin"></a>管理者

### <a name="2-volumeenactmentfailed"></a>2:VolumeEnactmentFailed

MBAM ポリシーを適用しているときにエラーが発生しました。

#### <a name="error-code--2144272219"></a>エラー コード: -2144272219

詳細:BitLocker ドライブ暗号化では、仮想プロビジョニングされた記憶域での使用領域のみの暗号化のみがサポートされます。

このエラーは、Windows 10 バージョン 1803 以前を実行している仮想マシンの暗号化に BitLocker を使用しようとした場合に発生します。 以前のバージョンの Windows 10 では、ディスク全体の暗号化はサポートされていません。 BitLocker 管理ポリシーは、ディスク全体の暗号化を適用します。

#### <a name="error-code--2147024774"></a>エラー コード: -2147024774

詳細:システム コールに渡されたデータ領域が小さすぎます。

問題を解決策するには、コンピューターを再起動してください。

### <a name="4-transferstatusdatafailed"></a>4:TransferStatusDataFailed

暗号化状態のデータを送信するときにエラーが発生しました。

### <a name="8-systemvolumenotfound"></a>8:SystemVolumeNotFound

システム ボリュームが見つかりません。 オペレーティング システム ドライブを暗号化するには、SystemVolume が必要です。

### <a name="9-tpmnotfound"></a>9:TPMNotFound

TPM ハードウェアが見つかりません。 TPM 保護機能を使用してオペレーティング システム ドライブを暗号化するには、TPM が必要です。

### <a name="10-machinehwexempted"></a>10:MachineHWExempted

このコンピューターは暗号化の対象から除外されています。 マシンのハードウェアの状態:除外

### <a name="11-machinehwunknown"></a>11:MachineHWUnknown

このコンピューターは暗号化の対象から除外されています。 マシンのハードウェアの状態:Unknown

### <a name="12-hwcheckfailed"></a>12:HWCheckFailed

ハードウェアの除外チェックに失敗しました。

### <a name="13-userisexempted"></a>13:UserIsExempted

このユーザーは暗号化の対象から除外されています。

### <a name="14-useriswaiting"></a>14:UserIsWaiting

ユーザーが除外を要求しました。

### <a name="15-userexemptioncheckfailed"></a>15:UserExemptionCheckFailed

ユーザーの除外チェックに失敗しました。

### <a name="16-userpostponed"></a>16:UserPostponed

ユーザーが暗号化プロセスを延期しました。

### <a name="17-tpminitializationfailed"></a>17:TPMInitializationFailed

TPM の初期化に失敗しました。 ユーザーが BIOS の変更を拒否しました。

### <a name="18-coreservicedown"></a>18:CoreServiceDown

MBAM 回復とハードウェア サービスに接続できません。

#### <a name="error-code--2147024809"></a>エラー コード: -2147024809

詳細:パラメーターが正しくありません。

このエラーは、Web サイトが HTTPS でない場合、またはクライアントに PKI 証明書がない場合に発生します。

### <a name="20-policymismatch"></a>20:PolicyMismatch

BitLocker 管理ポリシーが競合しているか、破損しています。

### <a name="21-conflictingosvolumepolicies"></a>21:ConflictingOSVolumePolicies

OS ボリューム暗号化ポリシーの競合を削除しました。 OS ドライブ保護機能に関係する BitLocker ポリシーを確認してください。

### <a name="22-conflictingfddvolumepolicies"></a>22:ConflictingFDDVolumePolicies

固定データ ドライブ ボリューム暗号化ポリシーの競合を削除しました。 固定データ ドライブのドライブ保護機能に関連する BitLocker ポリシーを確認してください。

### <a name="27-encryptionfailednodra"></a>27:EncryptionFailedNoDra

暗号化中にエラーが発生しました。 Windows 8.1 より前のコンピューターの FIPS モードでは、データ回復エージェント (DRA) 保護機能が必要です。

### <a name="34-tpmlockoutresetfailed"></a>34:TpmLockOutResetFailed

TPM ロックアウトをリセットできませんでした。

### <a name="36-tpmownerauthretrievalfailed"></a>36:TpmOwnerAuthRetrievalFailed

MBAM サービスから TPM OwnerAuth を取得できませんでした。

### <a name="37-wmiproviderdllsearchpathupdatefailed"></a>37:WmiProviderDllSearchPathUpdateFailed

WMI プロバイダーの DLL 検索パスを更新できませんでした。

### <a name="38-timedoutwaitingforwmiprovider"></a>38:TimedOutWaitingForWmiProvider

エージェントを停止しています。 MBAM WMI プロバイダー インスタンスを待機中にタイムアウトしました。

## <a name="operational"></a>操作可

### <a name="1-volumeenactmentsuccessful"></a>1:VolumeEnactmentSuccessful

BitLocker 管理ポリシーが正常に適用されました。

### <a name="3-transferstatusdatasuccessful"></a>3:TransferStatusDataSuccessful

暗号化状態のデータが正常に送信されました。

### <a name="19-coreserviceup"></a>19:CoreServiceUp

MBAM 回復とハードウェア サービスに正常に接続しました。

### <a name="28-tpmownerauthescrowed"></a>28:TpmOwnerAuthEscrowed

TPM OwnerAuth はエスクローされました。

### <a name="29-recoverykeyescrowed"></a>29:RecoveryKeyEscrowed

このボリュームの BitLocker 回復キーはエスクローされました。

### <a name="30-recoverykeyreset"></a>30:RecoveryKeyReset

このボリュームの BitLocker 回復キーは更新されました。

### <a name="31-enforcepolicydateset"></a>31:EnforcePolicyDateSet

ボリュームに対してポリシー適用の日付が設定されました

### <a name="32-enforcepolicydatecleared"></a>32:EnforcePolicyDateCleared

ボリュームに対してポリシー適用の日付が更新されました。

### <a name="33-tpmlockoutresetsucceeded"></a>33:TpmLockOutResetSucceeded

TPM ロックアウトが正常にリセットされました。

### <a name="35-tpmownerauthretrievalsucceeded"></a>35:TpmOwnerAuthRetrievalSucceeded

MBAM サービスから TPM OwnerAuth が正常に取得されました。

### <a name="39-removabledrivemounted"></a>39:RemovableDriveMounted

リムーバブル ドライブがマウントされました。

### <a name="40-removabledrivedismounted"></a>40:RemovableDriveDismounted

リムーバブル ドライブがマウント解除されました。

### <a name="41-failedtoenactendpointunreachable"></a>41:FailedToEnactEndpointUnreachable

MBAM 回復とハードウェア サービスに接続できなかったため、BitLocker 管理ポリシーが正常にボリュームに適用されませんでした。

### <a name="42-failedtoenactlockedvolume"></a>42:FailedToEnactLockedVolume

ロックされたボリュームの状態により、BitLocker 管理ポリシーが正常にボリュームに適用されませんでした。

### <a name="43-transferstatusdatafailedendpointunreachable"></a>43:TransferStatusDataFailedEndpointUnreachable

MBAM 準拠とステータス サービスに接続できなかったため、暗号化状態データを転送できませんでした。

## <a name="see-also"></a>関連項目

これらのログの使用方法の詳細については、「[BitLocker イベント ログ](about-event-logs.md)」を参照してください。

トラブルシューティングに関する詳細については、「[BitLocker のトラブルシューティング](troubleshoot.md)」をご覧ください。
