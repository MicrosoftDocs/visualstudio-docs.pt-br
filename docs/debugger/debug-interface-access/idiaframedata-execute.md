---
title: IDiaFrameData::execute | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::execute method
ms.assetid: 7a6c7d03-1ff1-4059-bd54-5f407eeebc26
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2587d10b613200b1bf850636f613abbb497e04de
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85467445"
---
# <a name="idiaframedataexecute"></a>IDiaFrameData::execute
Executa o desenrolamento de pilha e retorna os resultados em uma interface de quadro de movimentação de pilha.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT execute ( 
   IDiaStackWalkFrame* frame
);
```

#### <a name="parameters"></a>Parâmetros
 `frame`

no Um objeto [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md) que contém o estado dos registros de quadro.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. A tabela a seguir mostra os possíveis valores de retorno para esse método.

|Valor|Descrição|
|-----------|-----------------|
|E_DIA_INPROLOG|Não é possível executar um registro de ativação no código de prólogo.|
|E_DIA_SYNTAX|Erro de análise encontrado no programa de quadro.|
|E_DIA_FRAME_ACCESS|Não é possível acessar os registros ou a memória.|
|E_DIA_VALUE|Erro na computação de um valor (por exemplo, divisão por zero).|

## <a name="remarks"></a>Comentários
 Esse método é chamado durante a depuração para desenrolar a pilha. O objeto [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md) é implementado pelo aplicativo cliente para receber atualizações para os registros e para fornecer métodos usados pelo `execute` método.

## <a name="see-also"></a>Veja também
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)