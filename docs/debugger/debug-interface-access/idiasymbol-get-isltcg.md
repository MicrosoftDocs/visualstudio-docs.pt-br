---
description: Recupera um sinalizador que especifica se o compiland) foi vinculado com a opção de vinculador/LTCG (geração de código de tempo de vinculação) (/CPP/Build/Reference/LTCG-link-time-Code-Generation), que ajuda na otimização de todo o programa.
title: IDiaSymbol::get_isLTCG | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isLTCG method
ms.assetid: 5f7f05b8-6b71-4958-9e1e-e4924ef9c59b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1b8306dabe6533287d7d28841ea76f2d6478e4a3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102160809"
---
# <a name="idiasymbolget_isltcg"></a>IDiaSymbol::get_isLTCG
Recupera um sinalizador que especifica se o [compiland](../../debugger/debug-interface-access/compiland.md) foi vinculado com o comutador do vinculador [/LTCG (geração de código de tempo de vinculação)](/cpp/build/reference/ltcg-link-time-code-generation), que ajuda na otimização completa do programa. Essa opção se aplica somente ao código gerenciado.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_iSLTCG(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>Parâmetros
 pFlag

fora Retorna `TRUE` se o `compiland` foi vinculado com a opção de vinculador/LTCG; caso contrário, retorna `FALSE` .

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 8.0|

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
