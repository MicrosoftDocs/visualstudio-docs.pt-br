---
title: IDiaSymbol::get_addressSection | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_addressSection method
ms.assetid: fe80d479-3bb5-4f55-9b62-1bd58d0a60ce
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2d5f06658cb6d2faad13112813731208075460cb
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464355"
---
# <a name="idiasymbolget_addresssection"></a>IDiaSymbol::get_addressSection
Recupera a parte da seção de um local de endereço. Use quando a [Enumeração LocationType](../../debugger/debug-interface-access/locationtype.md) for definida como `LocIsStatic` .

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_addressSection ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna a parte da seção de um local de endereço.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 Para membros estáticos localizados em uma DLL externa, a seção retornada por esse método pode ser 0, pois esse método depende da obtenção do endereço virtual do membro. Os endereços virtuais serão válidos somente se o método [IDiaSession::p ut_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md) na interface [IDiaSession](../../debugger/debug-interface-access/idiasession.md) tiver sido chamado com um parâmetro diferente de zero especificando o endereço de carregamento da dll.

 Para obter a parte de deslocamento de um endereço, chame o método [IDiaSymbol:: get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md) .

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 7.0|

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração LocationType](../../debugger/debug-interface-access/locationtype.md)