---
title: アプリケーションの更新とインベントリからの削除
titleSuffix: Configuration Manager
description: Configuration Manager を使用して、展開済みのアプリケーションを、改訂、置き換え、またはアンインストールします。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7770f1db0e311186a908890dc339401ed3cbeb4b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689890"
---
# <a name="update-and-retire-applications-with-configuration-manager"></a>Configuration Manager によるアプリケーションの更新とインベントリからの削除

*適用対象:Configuration Manager (Current Branch)*


いずれはアプリケーションに変更を加えたり、アンインストールしたり、既に展開されているアプリケーションを新しいアプリケーションに置き換えたりすることが必要になる可能性があります。 Configuration Manager では、アプリケーションの更新とインベントリからの削除に役立つ、以下の機能が提供されます。  

- **アプリケーションの改訂**。 アプリケーションや展開の種類を変更するときに、Configuration Manager は変更の履歴を保持します。 いつでも以前のリビジョンにアプリケーションを戻すことができます。 プロパティの表示、旧リビジョンのアプリケーションの復元、または旧リビジョンの削除を行うこともできます。  

  詳細については、「[アプリケーションのリビジョン](revise-and-supersede-applications.md#application-revisions)」を参照してください。  

- **アプリケーションの置き換え**。 置き換えの関係を使用して、既存のアプリケーションをアップグレードするか置き換えることができます。 アプリケーションを置き換える場合は、置換対象のアプリケーションの展開の種類を置き換える新しい展開の種類を指定できます。 また、既存のものを置き換えるアプリケーションがインストールされる前に、新しいもので置き換えられるアプリケーションをアップグレードするかアンインストールするかを設定することもできます。  

  詳細については、「[アプリケーションの置き換え](revise-and-supersede-applications.md#application-supersedence)」を参照してください。  

- **アプリケーションのアンインストール**。 Configuration Manager では簡単にアプリケーションをアンインストールできます。 これは、アプリケーションまたはデバイスのユーザーが操作を一切行うことなく、自動実行できます。  

  詳細については、「[アプリケーションのアンインストール](uninstall-applications.md)」を参照してください。  
