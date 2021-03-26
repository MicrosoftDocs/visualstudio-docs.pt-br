---
description: Obtém o nome do indexador padrão.
title: 'IDebugClassField:: GetDefaultIndexer | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::GetDefaultIndexer
helpviewer_keywords:
- IDebugClassField::GetDefaultIndexer method
ms.assetid: 47ce4f45-3816-4b40-909c-5032d0692d75
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8ce8a492ea4d45a54a295617d7863b0623fd6a87
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088543"
---
# <a name="idebugclassfieldgetdefaultindexer"></a>IDebugClassField::GetDefaultIndexer
Obtém o nome do indexador padrão.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetDefaultIndexer( 
   BSTR* pbstrIndexer
);
```

```csharp
int GetDefaultIndexer(
   out string pbstrIndexer
);
```

## <a name="parameters"></a>Parâmetros
`pbstrIndexer` fora Retorna uma cadeia de caracteres que contém o nome do indexador padrão.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK ou retornará S_FALSE se não houver um indexador padrão. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 O indexador padrão de uma classe é a propriedade marcada como a `Default` propriedade para acessos de matriz. Isso é específico do [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] . Aqui está um exemplo de um indexador padrão declarado em [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] e como ele é usado.

```vb
Imports System.Collections;

Public Class Class1
    Private myList as Hashtable

    Default Public Property Item(ByVal Index As Integer) As Integer
        Get
            Return CType(List(Index), Integer)
        End Get
        Set(ByVal Value As Integer)
            List(Index) = Value
        End Set
    End Property
End Class

Function GetItem(Index as Integer) as Integer
    Dim classList as Class1 = new Class1
    Dim value as Integer

    ' Access array through default indexer
    value = classList(2)

    ' Access array through explicit property
    value = classList.Item(2)

    Return value
End Function
```

## <a name="see-also"></a>Confira também
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
