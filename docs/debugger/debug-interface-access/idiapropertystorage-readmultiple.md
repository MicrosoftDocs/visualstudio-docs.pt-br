---
title: IDiaPropertyStorage::ReadMultiple | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: f3c507df19fad7dd9594aeca1a53b9cb89a2e936
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55035556"
---
# <a name="idiapropertystoragereadmultiple"></a>IDiaPropertyStorage::ReadMultiple
Leituras especificada de propriedades do conjunto de propriedade atual.  
  
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
 [in] Contagem de propriedades especificadas no `rgpspec` matriz. Se for zero, o método não retorna nenhuma propriedade, mas retornar `S_OK` como um código de êxito.  
  
 `rgpspec`  
 [in] Uma matriz de propriedades a serem lidos. Propriedades podem ser especificadas por uma ID de propriedade ou por um nome de cadeia de caracteres opcional. Não é necessário especificar as propriedades em uma ordem específica na matriz. A matriz pode conter propriedades duplicadas, resultando em valores de propriedade duplicados no retorno para propriedades simples. Propriedades simples não devem retornar o acesso negado em uma tentativa para abri-los em uma segunda vez. A matriz pode conter uma mistura de IDs de propriedade e IDs de cadeia de caracteres. Essa matriz deve ter pelo menos `cpspec` número de valores de propriedade.  
  
 `rgvar`  
 [no, out] Uma matriz de `PROPVARIANT` estruturas (no namespace Microsoft.VisualStudio.OLE.Interop) a ser preenchida com valores para cada propriedade. A matriz deve ser pelo menos `cpspec` elementos de tamanho. O chamador não precisar inicializar os valores na matriz.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se um ou mais das propriedades não foi encontrado. Caso contrário, retornará um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Se uma propriedade não foi encontrado, a entrada correspondente na `rgvar` matriz contém uma `VARIANT` com o tipo de `VT_EMPTY`.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)