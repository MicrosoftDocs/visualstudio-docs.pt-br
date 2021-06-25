---
title: OPTNAMECHANGEPFN | Microsoft Docs
description: Saiba mais sobre a função de retorno de chamada OPTNAMECHANGEPFN, que comunica alterações de nome do plug-in de controle do código-fonte para o Visual Studio IDE.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- OPTNAMECHANGEPFN
helpviewer_keywords:
- OPTNAMECHANGEPFN callback function
ms.assetid: 147303f3-c7f1-438a-81b7-db891ea3d076
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 340012663ad7d21c0b5c2ef81283f5d780d6011c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901520"
---
# <a name="optnamechangepfn"></a>OPTNAMECHANGEPFN
Essa é uma função de retorno de chamada especificada em uma chamada para [sccSetOption](../extensibility/sccsetoption-function.md) (usando a opção ) e é usada para comunicar as alterações de nome feitas pelo plug-in de controle do código-fonte de volta para o `SCC_OPT_NAMECHANGEPFN` IDE.

## <a name="signature"></a>Assinatura

```cpp
typedef void (*OPTNAMECHANGEPFN)(
   LPVOID pvCallerData,
   LPCSTR pszOldName,
   LPCSTR pszNewName
);
```

## <a name="parameters"></a>Parâmetros
 pvCallerData

[in] Valor do usuário especificado em uma chamada anterior para [sccSetOption](../extensibility/sccsetoption-function.md) (usando a opção `SCC_OPT_USERDATA` ).

 pszOldName

[in] O nome original do arquivo.

 pszNewName

[in] O nome para o que o arquivo foi renomeado.

## <a name="return-value"></a>Valor retornado
 Nenhum.

## <a name="remarks"></a>Comentários
 Se um arquivo for renomeado durante uma operação de controle do código-fonte, o plug-in de controle do código-fonte poderá notificar o IDE sobre a alteração de nome por meio desse retorno de chamada.

 Se o IDE não dá suporte a esse retorno de chamada, ele não chamará [o SccSetOption](../extensibility/sccsetoption-function.md) para especificá-lo. Se o plug-in não dá suporte a esse retorno de chamada, ele retornará da função quando o `SCC_E_OPNOTSUPPORTED` `SccSetOption` IDE tentar definir o retorno de chamada.

## <a name="see-also"></a>Confira também
- [Funções de retorno de chamada implementadas pelo IDE](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccSetOption](../extensibility/sccsetoption-function.md)
