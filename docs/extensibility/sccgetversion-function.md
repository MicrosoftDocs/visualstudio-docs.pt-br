---
description: Essa função obtém o número de versão da API de plug-in de controle do código-fonte com suporte pelo plug-in de controle do código-fonte.
title: Função SccGetVersion | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetVersion
helpviewer_keywords:
- SccGetVersion function
ms.assetid: a6e786bf-744e-4272-9e21-0be44d23b1a1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 42273951768591dc89f4c9e4b9a27de1d646e209
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063806"
---
# <a name="sccgetversion-function"></a>Função SccGetVersion
Essa função obtém o número de versão da API de plug-in de controle do código-fonte com suporte pelo plug-in de controle do código-fonte.

## <a name="syntax"></a>Sintaxe

```cpp
LONG SccGetVersion(void);
```

#### <a name="parameters"></a>Parâmetros
 Nenhum.

## <a name="return-value"></a>Valor Retornado
 Um `LONG` tipo de dados que contém o número de versão da API de plug-in de controle do código-fonte com suporte:

|WORD|Descrição|
|----------|-----------------|
|HIWORD|Versão principal|
|LOWORD|Versão secundária|

## <a name="remarks"></a>Comentários
 Por exemplo, se um plug-in de controle do código-fonte der suporte à versão 1,3 da API de plug-in de controle do código-fonte, essa função retornará 0x0103.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
