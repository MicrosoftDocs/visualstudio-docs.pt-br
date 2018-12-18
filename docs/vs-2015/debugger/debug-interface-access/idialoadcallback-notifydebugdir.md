---
title: 'Idialoadcallback:: Notifydebugdir | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::NotifyDebugDir method
ms.assetid: bd04e2f6-0dbf-4742-a556-96f2cd99aa19
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 04a41e03a679a8910bb408162da57078e27eb654
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51769554"
---
# <a name="idialoadcallbacknotifydebugdir"></a>IDiaLoadCallback::NotifyDebugDir
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Chamado quando um diretório de depuração foi encontrado no arquivo .exe.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT NotifyDebugDir (   
   BOOL  fExecutable,  
   DWORD cbData,  
   BYTE  data[]  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `fExecutable`  
 [in] `TRUE` se o diretório de depuração é lido a partir de um executável (em vez de um arquivo. dbg).  
  
 `cbData`  
 [in] Contagem de bytes de dados no diretório de depuração.  
  
 `data[]`  
 [in] Uma matriz que é preenchida com o diretório de depuração.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro. O código de retorno normalmente é ignorado.  
  
## <a name="remarks"></a>Comentários  
 O [idiadatasource:: Loaddataforexe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) método invoca esse retorno de chamada quando ele encontra um diretório de depuração ao processar o arquivo executável.  
  
 Esse método remove a necessidade do cliente para o arquivo executável e/ou a depuração de engenharia reversa para dar suporte a informações de depuração que não seja encontrado no arquivo. PDB. Com esses dados, o cliente pode reconhecer o tipo de informações de depuração disponíveis e se ele reside no arquivo executável ou o arquivo. dbg.  
  
 A maioria dos clientes não precisarão esse retorno de chamada porque o `IDiaDataSource::loadDataForExe` método transparentemente abre os arquivos. PDB e. dbg quando necessário, para servir de símbolos.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)   
 [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)



