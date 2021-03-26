---
description: Essa função limpa todas as alocações ou conexões abertas criadas por uma chamada anterior para o SccInitialize em preparação para desligar o plug-in de controle do código-fonte.
title: Função SccUninitialize | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 7d387167e2032cbb253e86f8d67da38f99fc1076
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063767"
---
# <a name="sccuninitialize-function"></a>Função SccUninitialize
Essa função limpa todas as alocações ou conexões abertas criadas por uma chamada anterior para o [SccInitialize](../extensibility/sccinitialize-function.md) em preparação para desligar o plug-in de controle do código-fonte.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccUninitialize (
   LPVOID pvContext
);
```

#### <a name="parameters"></a>Parâmetros
 pvContext

no O ponteiro para a estrutura de contexto de plug-in de controle do código-fonte criada no [SccInitialize](../extensibility/sccinitialize-function.md).

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A limpeza foi concluída com êxito.|

## <a name="remarks"></a>Comentários
 O plug-in de controle do código-fonte é responsável por se preparar para desligar e liberar memória que o plug-in alocou para a estrutura de contexto. A função é chamada uma vez para cada instância específica de um plug-in. Uma chamada para o [SccInitialize](../extensibility/sccinitialize-function.md) precede essa chamada. Nenhum projeto ainda pode estar aberto no momento da chamada para `SccUninitialize` .

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
