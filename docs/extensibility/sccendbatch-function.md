---
description: Essa função conclui um lote de operações de controle do código-fonte.
title: Função SccEndBatch | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccEndBatch
helpviewer_keywords:
- SccEndBatch function
ms.assetid: 100e7833-fe0a-45c0-9fca-3e61fd1165b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 11ff596f19d3a98b929f9346bbf579e0ad1258c5
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904585"
---
# <a name="sccendbatch-function"></a>Função SccEndBatch
Essa função conclui um lote de operações de controle do código-fonte. Esses lotes podem não estar aninhados.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccEndBatch(void);
```

## <a name="parameters"></a>Parâmetros
 Nenhum.

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Lote de operações concluídas com êxito.|
|SCC_E_UNKNOWNERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 Os lotes de controle do código-fonte são usados para executar as mesmas operações de controle do código-fonte em vários projetos ou vários contextos. Os lotes podem ser usados para eliminar caixas de diálogo redundantes da experiência do usuário durante uma operação em lote. O [SccBeginBatch](../extensibility/sccbeginbatch-function.md) e a função são usados como um par para indicar `SccEndBatch` o início e o fim de uma operação. Eles não podem ser aninhados.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccBeginBatch](../extensibility/sccbeginbatch-function.md)
