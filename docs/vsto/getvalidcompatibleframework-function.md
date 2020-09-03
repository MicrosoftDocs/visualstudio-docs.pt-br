---
title: Função GetValidCompatibleFramework
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
ms.openlocfilehash: 2219417fe8ddae3d11d0e624ad12d3de80e290dd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "85520218"
---
# <a name="getvalidcompatibleframework-function"></a>Função GetValidCompatibleFramework
  Esta API dá suporte à infraestrutura do Office e não se destina a ser usada diretamente do seu código.

## <a name="syntax"></a>Sintaxe

```csharp
HRESULT WINAPI GetValidCompatibleFramework(
    LPCWSTR lpwszCompatibleFrameworksXML,
    BSTR* pbstrValidFrameworkTag
);
```

### <a name="parameters"></a>Parâmetros

|Parâmetro|Descrição|
|---------------|-----------------|
|*lpwszCompatibleFrameworksXML*|Não use.|
|*pbstrValidFrameworkTag*|Não use.|

## <a name="return-value"></a>Valor retornado
 Se a função for realizada com sucesso, ela retornará **S_OK**. Se a função falhar, será exibido um código de erro.
