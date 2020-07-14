---
title: IDiaDataSource::openSession | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::openSession method
ms.assetid: a3319ed0-3979-483b-9852-c0af96852c48
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b49c90374975865edcac8a94c504e1fa991d711a
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468500"
---
# <a name="idiadatasourceopensession"></a>IDiaDataSource::openSession
Abre uma sessão para consultar símbolos.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT openSession ( 
   IDiaSession** ppSession
);
```

#### <a name="parameters"></a>Parâmetros
ppSession

fora Retorna um objeto [IDiaSession](../../debugger/debug-interface-access/idiasession.md) que representa a sessão aberta.

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. A tabela a seguir mostra os possíveis valores de retorno para esse método.

|Valor|Descrição|
|-----------|-----------------|
|E_UNEXPECTED|O objeto [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md) não foi inicializado anteriormente com uma fonte de símbolos.|
|E_INVALIDARG|Parâmetro `ppSession` inválido.|
|E_OUTOFMEMORY|Memória insuficiente para abrir a sessão.|

## <a name="remarks"></a>Comentários
Esse método abre um objeto [IDiaSession](../../debugger/debug-interface-access/idiasession.md) para uma fonte de dados.

`IDiaSession`objetos implementam consultas na fonte de dados. Uma sessão gerencia um espaço de endereço para cada conjunto de símbolos de depuração. Se o arquivo. exe ou. dll descrito pelos símbolos de fonte de dados estiver ativo em vários intervalos de endereços (por exemplo, porque vários processos foram carregados), uma sessão para cada intervalo de endereços deverá ser usada.

## <a name="example"></a>Exemplo

```C++
IDiaSession* pSession;
HRESULT hr = pSource->openSession( &pSession );
if (FAILED(hr))
{
   // report error
}
```

## <a name="see-also"></a>Confira também
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [Visão geral](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [Consultando o arquivo .Pdb](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)
