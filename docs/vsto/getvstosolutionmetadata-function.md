---
title: Função GetVstoSolutionMetadata
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: aebbedaab7e7ac342f6d6ace191d820f6a0c8090
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520179"
---
# <a name="getvstosolutionmetadata-function"></a>Função GetVstoSolutionMetadata
  Esta API dá suporte à infraestrutura do Office e não se destina a ser usada diretamente do seu código.

## <a name="syntax"></a>Sintaxe

```csharp
HRESULT WINAPI GetVstoSolutionMetadata(
    LPCWSTR lpwszSolutionMetadataKey,
    ISolutionMetadata** ppSolutionInfo
);
```

### <a name="parameters"></a>Parâmetros

|Parâmetro|Descrição|
|---------------|-----------------|
|*lpwszSolutionMetadataKey*|Não use.|
|*ppSolutionInfo*|Não use.|

## <a name="return-value"></a>Retornar valor
 Se a função for realizada com sucesso, ela retornará **S_OK**. Se a função falhar, será exibido um código de erro.
