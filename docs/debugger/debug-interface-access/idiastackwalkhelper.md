---
title: IDiaStackWalkHelper | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2 interface
ms.assetid: d66e5c84-565d-494e-8486-f91db9a34548
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bdf2f54c585a8a5406a0772dc1c580112036671d
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464621"
---
# <a name="idiastackwalkhelper"></a>IDiaStackWalkHelper
Facilita a movimentação da pilha usando o arquivo de banco de dados de depuração do programa (. pdb).

## <a name="syntax"></a>Syntax

```

IDiaStackWalkHelper: IUnknown

```

## <a name="methods-in-vtable-order"></a>Métodos em ordem VTable
 A tabela a seguir mostra os métodos de `IDiaStackWalkHelper` :

|Método|Descrição|
|------------|-----------------|
|[IDiaStackWalkHelper::get_registerValue](../../debugger/debug-interface-access/idiastackwalkhelper-get-registervalue.md)|Recupera o valor de um registro.|
|[IDiaStackWalkHelper::put_registerValue](../../debugger/debug-interface-access/idiastackwalkhelper-put-registervalue.md)|Define o valor de um registro.|
|[IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)|Lê um bloco de dados da imagem do executável na memória.|
|[IDiaStackWalkHelper::searchForReturnAddress](../../debugger/debug-interface-access/idiastackwalkhelper-searchforreturnaddress.md)|Pesquisa o quadro de pilha especificado para o endereço de retorno de função mais próximo.|
|[IDiaStackWalkHelper::searchForReturnAddressStart](../../debugger/debug-interface-access/idiastackwalkhelper-searchforreturnaddressstart.md)|Pesquisa o quadro de ativação especificado em busca de um endereço de retorno no endereço de pilha especificado ou próximo dele.|
|[IDiaStackWalkHelper::frameForVA](../../debugger/debug-interface-access/idiastackwalkhelper-frameforva.md)|Recupera o quadro de pilha que contém o endereço virtual especificado.|
|[IDiaStackWalkHelper::symbolForVA](../../debugger/debug-interface-access/idiastackwalkhelper-symbolforva.md)|Recupera o símbolo que contém o endereço virtual especificado. **Observação:**  O símbolo deve ter o tipo `SymTagFunctionType` (um valor da enumeração de [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md) ).|
|[IDiaStackWalkHelper::pdataForVA](../../debugger/debug-interface-access/idiastackwalkhelper-pdataforva.md)|Retorna o bloco de dados PDATA associado ao endereço virtual especificado.|
|[IDiaStackWalkHelper::imageForVA](../../debugger/debug-interface-access/idiastackwalkhelper-imageforva.md)|Recupera o endereço virtual inicial de um executável, dado um endereço virtual em algum lugar no espaço de memória do executável.|

## <a name="remarks"></a>Comentários
 Essa interface é chamada pelo código do DIA para obter informações sobre o executável a fim de construir uma lista de quadros de pilha durante a execução do programa.

## <a name="notes-for-callers"></a>Observações para chamadores
 Um aplicativo cliente implementa essa interface para dar suporte à movimentação da pilha durante a execução do programa. Uma instância dessa interface é passada para os métodos [IDiaStackWalker:: getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md) ou [IDiaStackWalker:: getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md) .

## <a name="requirements"></a>Requisitos
 Cabeçalho: dia2. h

 Biblioteca: diaguids. lib

 DLL: msdia80.dll

## <a name="see-also"></a>Veja também
- [Interfaces (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaStackWalker::getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md)
- [IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)