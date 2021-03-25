---
description: Contém informações de status sobre caminhos de pesquisa de símbolos que foram pesquisados.
title: MODULE_SYMBOL_SEARCH_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_SYMBOL_SEARCH_INFO
helpviewer_keywords:
- MODULE_SYMBOL_SEARCH_INFO structure
ms.assetid: 432aff03-08a5-4c5a-b2d5-e212090fc70a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 266d786df422e5260e212a4005feb7d3167af099
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057891"
---
# <a name="module_symbol_search_info"></a>MODULE_SYMBOL_SEARCH_INFO

Contém informações de status sobre caminhos de pesquisa de símbolos que foram pesquisados.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct _tagSYMBOL_SEARCH_INFO
{
    SYMBOL_SEARCH_INFO_FIELDS dwValidFields;
    BSTR                      bstrVerboseSearchInfo;
} MODULE_SYMBOL_SEARCH_INFO;
```

```csharp
public struct MODULE_SYMBOL_SEARCH_INFO {
    public uint   dwValidFields;
    public string bstrVerboseSearchInfo;
}
```

## <a name="members"></a>Membros

`dwValidFields`\
Uma combinação de sinalizadores da enumeração [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md) especificando o tipo de informações de pesquisa descritas nesta estrutura.

`bstrVerboseSearchInfo`\
Caminho de pesquisa e resultados concatenados em uma única cadeia de caracteres.

## <a name="remarks"></a>Comentários

Essa estrutura é retornada de uma chamada para o método [GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md) .

Se o `bstrVerboseSearchInfo` campo não estiver vazio, ele conterá uma lista de caminhos pesquisados e os resultados dessa pesquisa. A lista é formatada com um caminho, seguido por uma elipse ("..."), seguida pelo resultado. Se houver mais de um par de resultados de caminho, cada par será separado por um par "\r\n" (retorno de carro/alimentação de discagem). O padrão tem a seguinte aparência:

\<path>...\<result> \r\n \<path> . \<result> .. \r\n \<path> ...\<result>

Observe que a última entrada não tem uma sequência \r\n.

Aqui está uma `bstrVerboseSearchInfo` cadeia de caracteres possível que foi enviada para o padrão.

`c:\symbols\user32.pdb... File not found.`

`c:\winnt\symbols\user32.pdb... Version does not match.`

`\\symbols\symbols\user32.dll\0a8sd0ad8ad\user32.pdb... Symbols loaded.`

## <a name="requirements"></a>Requisitos

Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também

- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)
