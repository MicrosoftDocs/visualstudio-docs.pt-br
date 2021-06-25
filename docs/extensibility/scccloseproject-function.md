---
description: Essa função fecha um projeto, marcando o final de uma sessão específica.
title: Função SccCloseProject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccCloseProject
helpviewer_keywords:
- SccCloseProject function
ms.assetid: 259c2069-d349-4814-810f-1c3151b7fb84
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 859b1ddea99e74cc1c1dec999611e50216c3c98a
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904689"
---
# <a name="scccloseproject-function"></a>Função SccCloseProject
Essa função fecha um projeto, marcando o final de uma sessão específica.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccCloseProject (
   LPVOID pvContext
);
```

### <a name="parameters"></a>Parâmetros
 pvContext A estrutura de contexto de plug-in do controle do código-fonte.

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|O projeto foi fechado com êxito.|
|SCC_E_PROJNOTOPEN|Nenhum projeto está aberto no momento.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar essa operação.|
|SCC_E_NONSPECIFICERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 O [SccOpenProject](../extensibility/sccopenproject-function.md) é sempre chamado antes dessa função. Uma chamada para essa função é seguida por uma chamada para a função ou `SccOpenProject` [sccUninitialize](../extensibility/sccuninitialize-function.md), que encerra completamente a conexão com o sistema de controle do código-fonte.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
