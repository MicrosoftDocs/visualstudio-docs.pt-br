---
description: Essa função inicia uma sequência em lote de operações de controle do código-fonte.
title: Função SccBeginBatch | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccBeginBatch
helpviewer_keywords:
- SccBeginBatch function
ms.assetid: 33968183-2e15-4e0d-955b-ca12212d1c25
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 08b9199b98e566a71bfeb95124ebd85781e69950
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904754"
---
# <a name="sccbeginbatch-function"></a>Função SccBeginBatch
Essa função inicia uma sequência em lote de operações de controle do código-fonte. O [SccEndBatch](../extensibility/sccendbatch-function.md) será chamado para encerrar o lote. Esses lotes podem não estar aninhados.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccBeginBatch(void);
```

### <a name="parameters"></a>Parâmetros
 Nenhum.

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|O lote de operações foi iniciado com êxito.|
|SCC_E_UNKNOWNERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 Os lotes de controle do código-fonte são usados para executar as mesmas operações em vários projetos ou vários contextos. Os lotes podem ser usados para eliminar caixas de diálogo redundantes por projeto da experiência do usuário durante uma operação em lote. A `SccBeginBatch` função e o [SccEndBatch](../extensibility/sccendbatch-function.md) são usados como um par de funções para indicar o início e o fim de uma operação. Eles não podem ser aninhados. `SccBeginBatch` define um sinalizador que indica que uma operação em lote está em andamento.

 Enquanto uma operação em lote estiver em vigor, o plug-in de controle do código-fonte deve apresentar no máximo uma caixa de diálogo para qualquer pergunta ao usuário e aplicar a resposta dessa caixa de diálogo em todas as operações subsequentes.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccEndBatch](../extensibility/sccendbatch-function.md)
