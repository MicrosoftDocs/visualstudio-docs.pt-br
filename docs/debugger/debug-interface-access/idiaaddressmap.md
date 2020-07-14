---
title: IDiaAddressMap | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap interface
ms.assetid: e6467529-508c-4328-85d7-89444ae4d1c1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ddf4b1c2a6a22170fb52da200bbd53c2b6b96e62
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468528"
---
# <a name="idiaaddressmap"></a>IDiaAddressMap
Fornece controle sobre como o DIA SDK computa os endereços virtuais e virtuais relativos para objetos de depuração.

## <a name="syntax"></a>Syntax

```
IDiaAddressMap : IUnknown
```

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDiaAddressMap` .

|Método|Descrição|
|------------|-----------------|
|[IDiaAddressMap::get_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md)|Indica se um mapa de endereço foi estabelecido para uma sessão específica.|
|[IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)|Especifica se o mapa de endereço deve ser usado para converter endereços de símbolo.|
|[IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)|Indica se o cálculo e o uso de endereços virtuais relativos estão habilitados.|
|[IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)|Permite que o cliente habilite ou desabilite o cálculo de endereços virtuais relativos.|
|[IDiaAddressMap::get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md)|Recupera o alinhamento da imagem atual.|
|[IDiaAddressMap::put_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-put-imagealign.md)|Define o alinhamento da imagem.|
|[IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)|Define cabeçalhos de imagem para habilitar a tradução de endereços virtuais relativos.|
|[IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)|Fornece um mapa de endereços para dar suporte a traduções de layout de imagem.|

## <a name="remarks"></a>Comentários
 O controle fornecido por essa interface é encapsulado em dois conjuntos de dados que você fornece: cabeçalhos de imagem e mapas de endereço. A maioria dos clientes usa o método [IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) para localizar as informações de depuração apropriadas para uma imagem e o método normalmente pode descobrir todos os cabeçalhos necessários e mapear os próprios dados. No entanto, alguns clientes implementam processamento especializado e pesquisam dados. Esses clientes usam os métodos da `IDiaAddressMap` interface para fornecer o dia SDK com os resultados da pesquisa.

## <a name="notes-for-callers"></a>Observações para chamadores
 Essa interface está disponível no objeto de sessão DIA. O cliente chama o `QueryInterface` método na interface de objeto de sessão do dia, geralmente [IDiaSession](../../debugger/debug-interface-access/idiasession.md), para recuperar a `IDiaAddressMap` interface.

## <a name="requirements"></a>Requisitos
 Cabeçalho: dia2. h

 Biblioteca: diaguids. lib

 DLL: msdia80.dll

## <a name="see-also"></a>Veja também
- [Interfaces (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)