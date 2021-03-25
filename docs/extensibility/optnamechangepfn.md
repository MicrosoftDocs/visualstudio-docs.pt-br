---
title: OPTNAMECHANGEPFN | Microsoft Docs
description: Saiba mais sobre a função de retorno de chamada OPTNAMECHANGEPFN, que comunica alterações de nome do plug-in de controle do código-fonte no IDE do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 4e6cb58aebbe76eff5c66dc29ecfad8c77c8717c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090363"
---
# <a name="optnamechangepfn"></a>OPTNAMECHANGEPFN
Essa é uma função de retorno de chamada especificada em uma ligação para o [SccSetOption](../extensibility/sccsetoption-function.md) (usando a opção `SCC_OPT_NAMECHANGEPFN` ) e é usada para comunicar alterações de nome feitas pelo plug-in de controle do código-fonte de volta para o IDE.

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

no Valor de usuário especificado em uma chamada anterior para o [SccSetOption](../extensibility/sccsetoption-function.md) (usando a opção `SCC_OPT_USERDATA` ).

 pszOldName

no O nome original do arquivo.

 pszNewName

no O nome para o qual o arquivo foi renomeado.

## <a name="return-value"></a>Retornar valor
 Nenhum.

## <a name="remarks"></a>Comentários
 Se um arquivo for renomeado durante uma operação de controle de origem, o plug-in de controle do código-fonte poderá notificar o IDE sobre a alteração do nome por meio desse retorno de chamada.

 Se o IDE não oferecer suporte a esse retorno de chamada, ele não chamará o [SccSetOption](../extensibility/sccsetoption-function.md) para especificá-lo. Se o plug-in não oferecer suporte a esse retorno de chamada, ele retornará `SCC_E_OPNOTSUPPORTED` da `SccSetOption` função quando o IDE tentar definir o retorno de chamada.

## <a name="see-also"></a>Confira também
- [Funções de retorno de chamada implementadas pelo IDE](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccSetOption](../extensibility/sccsetoption-function.md)
