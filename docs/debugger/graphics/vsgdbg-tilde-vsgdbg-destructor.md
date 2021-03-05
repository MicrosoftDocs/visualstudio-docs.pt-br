---
description: Destrói uma instância da classe VsgDbg.
title: 'VsgDbg:: ~ VsgDbg (destruidor) | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7a3b97fb-d344-4df7-b195-9347d1edfcf7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d90664723695756ebd8acdc7c56bec1fcbd08a31
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102155220"
---
# <a name="vsgdbgvsgdbg-destructor"></a>VsgDbg::~VsgDbg (Destruidor)
Destrói uma instância da `VsgDbg` classe. Se as informações gráficas estiverem sendo registradas ativamente, o arquivo de log de gráficos será finalizado e fechado, e os recursos que foram usados durante a captura ativa das informações gráficas serão liberados.

## <a name="syntax"></a>Sintaxe

```C++
~VsgDbg();
```

## <a name="see-also"></a>Confira também
- [VsgDbg::VsgDbg (Construtor)](vsgdbg-vsgdbg-constructor.md)
