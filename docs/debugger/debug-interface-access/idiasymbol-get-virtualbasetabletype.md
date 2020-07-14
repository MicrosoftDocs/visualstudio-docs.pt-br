---
title: IDiaSymbol::get_virtualBaseTableType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_virtualBaseTableType method
ms.assetid: e0581c4f-0343-49b5-9754-a48477460e9f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 858f149abb0bec444c43ea706e638def4ff930ce
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461437"
---
# <a name="idiasymbolget_virtualbasetabletype"></a>IDiaSymbol::get_virtualBaseTableType
Recupera o tipo de um ponteiro de tabela base virtual.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_virtualBaseTableType(
   IDiaSymbol *pRetVal
};
```

#### <a name="parameters"></a>Parâmetros

|Parâmetro|Descrição|
|---------------|-----------------|
|`pRetVal`|fora Retorna um objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que especifica o tipo de tabela base.|

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 Um ponteiro de tabela base virtual ( `vbtptr` ) é um ponteiro oculto em uma [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] vtable que manipula a herança de classes base virtuais. Um `vbtptr` pode ter tamanhos diferentes dependendo das classes herdadas.

 Esse método retorna um objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que pode ser usado para determinar o tamanho do vbtptr.

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 8.0|

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)