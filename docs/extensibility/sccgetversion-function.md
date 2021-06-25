---
description: Essa função obtém o número de versão da API de plug-in de controle do código-fonte com suporte pelo plug-in de controle do código-fonte.
title: Função SccGetVersion | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
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
ms.openlocfilehash: f49d33ebe70390a364d0ae8336e7f69549b6876f
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901078"
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
 Um tipo de dados que contém o número de versão da API de Plug-in de Controle do `LONG` Código-Fonte com suporte:

|WORD|Descrição|
|----------|-----------------|
|Hiword|Versão principal|
|Loword|Versão secundária|

## <a name="remarks"></a>Comentários
 Por exemplo, se um plug-in de controle do código-fonte for compatível com a versão 1.3 da API de Plug-in de Controle do Código-Fonte, essa função retornará 0x0103.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
