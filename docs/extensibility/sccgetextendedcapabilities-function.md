---
description: Essa função retorna recursos adicionais com suporte pelo plug-in de controle do código-fonte.
title: Função SccGetExtendedCapabilities | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccGetExtendedCapabilities
helpviewer_keywords:
- SccGetExtendedCapabilities function
ms.assetid: 588c6a92-2147-4d8b-a357-96ca7da0a092
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cc047fee2c92f47c181aef455b8175a4e7998176
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905586"
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

[in] O ponteiro de contexto do plug-in do controle do código-fonte.

 lSccExCaps

[in] Um sinalizador que especifica uma funcionalidade estendida para a qual testar (consulte a tabela Código de Funcionalidade Estendida em Sinalizadores de funcionalidade [para](../extensibility/capability-flags.md) os possíveis sinalizadores).

 pbSupported

[out] Retornará diferente de zero ( ) se a funcionalidade especificada tiver `TRUE` suporte; caso contrário, retornará zero ( `FALSE` ).

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A operação get capability foi concluída com êxito.|
|SCC_E_UNKNOWNERROR<br /><br /> SCC_E_NONSPECIFICERROR|Erro desconhecido ou não especificado.|

## <a name="remarks"></a>Comentários
 Esse método é chamado sob demanda; ou seja, quando uma funcionalidade precisa ser testada, esse método é chamado para determinar se há suporte para essa funcionalidade. Apenas um sinalizador de cada vez é especificado.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [Códigos de erro](../extensibility/error-codes.md)
- [Sinalizadores de funcionalidade](../extensibility/capability-flags.md)
