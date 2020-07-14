---
title: IDiaSymbol::get_backEndMinor | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_backEndMinor method
ms.assetid: 37f38d19-6685-440d-a477-7127c4f8699e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2e65b2af4654949cdfd7198f54eefea386b905cc
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464243"
---
# <a name="idiasymbolget_backendminor"></a>IDiaSymbol::get_backEndMinor
Recupera o número de versão secundária de back-end do compilador.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_backEndMinor ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o número de versão secundária do back-end. Consulte Observações.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 Normalmente, um compilador é composto por dois elementos principais: o front-end (o analisador), que lida com a análise do código-fonte em um formulário intermediário e um back-end (gerador de código), que converte o formulário intermediário em assembly. Não é incomum que o front-end tenha uma versão diferente do back-end.

 Um número de versão de front-end ou de back-end é composto por três partes: \<major> . \<minor> . \<build> , em que \<major> é o número de versão principal, \<minor> é o número de versão secundária e \<build> é o número da compilação. Por exemplo, 13.10.3077.

## <a name="requirements"></a>Requisitos

|Requisito|Descrição|
|-----------------|-----------------|
|Cabeçalho:|dia2.h|
|Versão:|DIA SDK v 7.0|

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)