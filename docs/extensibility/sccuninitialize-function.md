---
description: Essa função limpa todas as alocações ou conexões abertas criadas por uma chamada anterior ao SccInitialize em preparação para desligar o plug-in de controle do código-fonte.
title: Função SccUninitialize | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccUninitialize
helpviewer_keywords:
- SccUninitialize function
ms.assetid: 17cf5337-d251-4422-bc96-93fe7d48f2ae
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0d46aedd3e962d0684689ff29a34061b777fe08e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904068"
---
# <a name="sccuninitialize-function"></a>Função SccUninitialize
Essa função limpa todas as alocações ou conexões abertas criadas por uma chamada anterior ao [SccInitialize](../extensibility/sccinitialize-function.md) em preparação para desligar o plug-in de controle do código-fonte.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccUninitialize (
   LPVOID pvContext
);
```

#### <a name="parameters"></a>Parâmetros
 pvContext

[in] O ponteiro para a estrutura de contexto de plug-in do controle do código-fonte criada no [SccInitialize.](../extensibility/sccinitialize-function.md)

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A limpeza foi concluída com êxito.|

## <a name="remarks"></a>Comentários
 O plug-in de controle do código-fonte é responsável por se preparar para ser desligado e liberar memória alocada pelo plug-in para a estrutura de contexto. A função é chamada uma vez para cada determinada instância de um plug-in. Uma chamada para [sccInitialize](../extensibility/sccinitialize-function.md) precede essa chamada. Nenhum projeto ainda pode ser aberto no momento da chamada para `SccUninitialize` .

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
