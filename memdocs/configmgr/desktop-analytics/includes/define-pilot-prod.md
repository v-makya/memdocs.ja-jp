---
author: aczechowski
ms.author: aaroncz
ms.reviewer: acabello
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 431c88b07889f7c80d2723425aaef2245c7f06bc
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268787"
---
パイロットと運用を区別するには、次の定義を使用します。  

- **パイロット**:より大きなセットに展開する前に検証するデバイスのサブセットです。 Desktop Analytics を使用して、パイロット セットに固有としてデバイスをマークします。 資産がブロックされていない場合、パイロットのデバイスはアップグレードする準備ができています。 ブロックしている資産は、"*重大*" および "*アップグレードできません*" としてマークされています。  

- **Production**:Desktop Analytics に登録されているその他のデバイスはすべて、パイロットに含まれません。 すべての資産がサインオフされている場合、運用デバイスはアップグレードする準備ができています。 Desktop Analytics によって、重大ではない資産は自動的にサインオフされます。  
