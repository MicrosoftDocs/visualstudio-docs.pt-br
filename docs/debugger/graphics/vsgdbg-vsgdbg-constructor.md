---
description: Constrói uma instância da classe VsgDbg com ou sem preparar o componente no aplicativo de diagnóstico de gráficos para capturar e gravar ativamente informações de gráficos por padrão, com base no parâmetro booliano especificado.
title: 'VsgDbg:: VsgDbg (Construtor) | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 670651e6-5e79-4845-b0c2-671beb7055a8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ae4259b1af1bcb51b05431131db596d2a26da895
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102160437"
---
# <a name="vsgdbgvsgdbg-constructor"></a>VsgDbg::VsgDbg (Construtor)
Constrói uma instância da `VsgDbg` classe com ou sem preparar o componente no aplicativo de diagnóstico de gráficos para capturar e gravar ativamente informações de gráficos por padrão, com base no parâmetro booliano especificado.

## <a name="syntax"></a>Sintaxe

```C++
VsgDbg(
  bDefaultInit
);
```

#### <a name="parameters"></a>Parâmetros
 `bDefaultInit``true`para especificar que o componente no aplicativo do diagnóstico de gráficos seja preparado para capturar e registrar informações de gráficos ativamente; `false` para especificar que o aplicativo não deve estar preparado para capturar e registrar informações de gráficos ativamente neste momento.

## <a name="remarks"></a>Comentários
 Quando o construtor é chamado com `bDefaultInit` definido como `true` , o nome de arquivo do arquivo de log de gráficos é determinado pelo modo como os `DONT_SAVE_VSGLOG_TO_TEMP` `VSG_DEFAULT_RUN_FILENAME` símbolos de pré-processador e são definidos antes de `vsgcapture.h` serem incluídos em seu aplicativo.

 Quando o construtor é chamado com `bDefaultInit` definido como `false` , o componente no aplicativo do diagnóstico de gráficos pode ser preparado para capturar e gravar ativamente informações de gráficos em um momento posterior chamando a `Init` função.

## <a name="see-also"></a>Confira também
- [VsgDbg::~VsgDbg (Destruidor)](vsgdbg-tilde-vsgdbg-destructor.md)
- [Init](init.md)
- [DONT_SAVE_VSGLOG_TO_TEMP](dont-save-vsglog-to-temp.md)
- [VSG_DEFAULT_RUN_FILENAME](vsg-default-run-filename.md)
