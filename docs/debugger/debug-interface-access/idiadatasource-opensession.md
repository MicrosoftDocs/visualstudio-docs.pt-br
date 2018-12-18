---
title: 'Idiadatasource:: Opensession | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::openSession method
ms.assetid: a3319ed0-3979-483b-9852-c0af96852c48
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8266102e8bc2c347ed8a554a3c64d9504f1e863b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49933502"
---
# <a name="idiadatasourceopensession"></a>IDiaDataSource::openSession
Abre uma sessão para consultar os símbolos.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT openSession (   
   IDiaSession** ppSession  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 ppSession  
 [out] Retorna um [IDiaSession](../../debugger/debug-interface-access/idiasession.md) objeto que representa a sessão aberta.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro. A tabela a seguir mostra os possíveis valores retornados para esse método.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|E_UNEXPECTED|O [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md) objeto anteriormente não foi inicializado com uma origem de símbolos.|  
|E_INVALIDARG|Inválido `ppSession` parâmetro.|  
|E_OUTOFMEMORY|Memória insuficiente para abrir a sessão.|  
  
## <a name="remarks"></a>Comentários  
 Este método abre uma [IDiaSession](../../debugger/debug-interface-access/idiasession.md) objeto para uma fonte de dados.  
  
 `IDiaSession` objetos de implementação de consultas na fonte de dados. Uma sessão gerencia um espaço de endereço para cada conjunto de símbolos de depuração. Se o arquivo. dll ou. .exe descrito pelos símbolos de fonte de dados estiver ativo no endereço vários intervalos (por exemplo, porque vários processos tem carregado) e uma sessão para cada intervalo de endereços deve ser usada.  
  
## <a name="example"></a>Exemplo  
  
```C++  
IDiaSession* pSession;  
HRESULT hr = pSource->openSession( &pSession );  
if (FAILED(hr))  
{  
   // report error  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)   
 [Visão geral](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)   
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [Consultando o arquivo .Pdb](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)