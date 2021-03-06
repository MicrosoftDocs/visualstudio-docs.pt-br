---
description: Essa função retorna recursos adicionais com suporte pelo plug-in de controle do código-fonte.
title: Função SccGetExtendedCapabilities | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetExtendedCapabilities
helpviewer_keywords:
- SccGetExtendedCapabilities function
ms.assetid: 588c6a92-2147-4d8b-a357-96ca7da0a092
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e1409753559088c0f8129ebacd17387bfb7d111e
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102220775"
---
# <a name="sccgetextendedcapabilities-function"></a>Função SccGetExtendedCapabilities
Essa função retorna recursos adicionais com suporte pelo plug-in de controle do código-fonte.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccGetExtendedCapabilities(
   LPVOID pContext,
   LONG lSccExCaps,
   LPBOOL pbSupported
);
```

### <a name="parameters"></a>Parâmetros
 pContext

no O ponteiro de contexto do plug-in de controle do código-fonte.

 lSccExCaps

no Um sinalizador que especifica um recurso estendido para testar (consulte a tabela de código de funcionalidade estendida em [sinalizadores de capacidade](../extensibility/capability-flags.md) para os possíveis sinalizadores).

 pbSupported

fora Retorna um valor diferente de zero ( `TRUE` ) se houver suporte para o recurso especificado; caso contrário, retornará zero ( `FALSE` ).

## <a name="return-value"></a>Retornar valor
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A operação obter funcionalidade foi concluída com êxito.|
|SCC_E_UNKNOWNERROR<br /><br /> SCC_E_NONSPECIFICERROR|Ocorreu um erro desconhecido ou não especificado.|

## <a name="remarks"></a>Comentários
 Esse método é chamado sob demanda; ou seja, quando um recurso precisa ser testado, esse método é chamado para determinar se há suporte para esse recurso. Apenas um sinalizador por vez é especificado.

## <a name="see-also"></a>Confira também
- [Funções da API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [Códigos de erro](../extensibility/error-codes.md)
- [Sinalizadores de capacidade](../extensibility/capability-flags.md)
