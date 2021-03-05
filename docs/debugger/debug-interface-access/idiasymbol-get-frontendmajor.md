---
description: Recupera o número de versão principal de front-end.
title: IDiaSymbol::get_frontEndMajor | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_frontEndMajor method
ms.assetid: f8a067c5-3306-4fc5-bc20-8910a47ed504
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bf5bc125b00fa8194475c9f6101e697dbf66062a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162162"
---
# <a name="idiasymbolget_frontendmajor"></a>IDiaSymbol::get_frontEndMajor
Recupera o número de versão principal de front-end.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_frontEndMajor ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o número de versão principal de front-end. Consulte Observações.

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

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
