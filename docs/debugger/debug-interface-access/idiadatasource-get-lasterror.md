---
title: IDiaDataSource::get_lastError | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::get_lastError method
ms.assetid: cf08850b-8b75-4e8c-90bd-bd0214756f99
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 231c6b082f7a641ee78d10003d544c3fb9644c1c
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468521"
---
# <a name="idiadatasourceget_lasterror"></a>IDiaDataSource::get_lastError
Recupera o nome do arquivo para o último erro de carregamento.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_lastError (
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 pRetVal

fora Retorna uma cadeia de caracteres que contém o nome do arquivo. PDB associado ao último erro de carregamento.

## <a name="return-value"></a>Valor Retornado
 Retorna o último código de erro causado por uma operação de carregamento. Retorna `E_INVALIDARG` se o `pRetVal` parâmetro é `NULL` .

## <a name="example"></a>Exemplo

```C++
BSTR    fileName;
HRESULT errorCode = pSource->get_lastError( &fileName );
```

## <a name="see-also"></a>Confira também
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)