---
title: IDiaPropertyStorage::ReadMultiple | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadMultiple
ms.assetid: 6ccc9397-ce41-4f72-b261-72ac252cd4a5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8681032840f09bcc4a90df66b3a6f37d664739ab
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466570"
---
# <a name="idiapropertystoragereadmultiple"></a>IDiaPropertyStorage::ReadMultiple
Lê as propriedades especificadas do conjunto de propriedades atual.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT ReadMultiple( 
   ULONG          cpspec,
   PROPSPEC const rgpspec,
   PROPVARIANT    rgvar
);
```

#### <a name="parameters"></a>Parâmetros
 `cpspec`

no Contagem de propriedades especificadas na `rgpspec` matriz. Se for zero, o método não retornará Propriedades, mas retornará `S_OK` como um código de êxito.

 `rgpspec`

no Uma matriz de propriedades a ser lida. As propriedades podem ser especificadas por uma ID de propriedade ou por um nome de cadeia de caracteres opcional. Não é necessário especificar propriedades em qualquer ordem específica na matriz. A matriz pode conter Propriedades duplicadas, resultando em valores de propriedade duplicados no retorno para propriedades simples. As propriedades não simples devem retornar acesso negado em uma tentativa de abri-las uma segunda vez. A matriz pode conter uma mistura de IDs de propriedade e IDs de cadeia de caracteres. Essa matriz deve ter pelo menos o `cpspec` número de valores de propriedade.

 `rgvar`

[entrada, saída] Uma matriz de `PROPVARIANT` estruturas (no namespace Microsoft. VisualStudio. OLE. Interop) a ser preenchida com valores para cada propriedade. A matriz deve ter pelo menos `cpspec` elementos de tamanho. O chamador não precisa inicializar os valores na matriz.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se uma ou mais das propriedades não foram encontradas. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Se uma propriedade não for encontrada, a entrada correspondente na `rgvar` matriz conterá um `VARIANT` com o tipo de `VT_EMPTY` .

## <a name="see-also"></a>Veja também
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)