---
title: IDiaDataSource | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource interface
ms.assetid: 6260ac76-4f9d-4144-ba22-32f8620b32c2
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b5126ea6da80bb6c029f9237ff01dfc805c9eaf6
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31460271"
---
# <a name="idiadatasource"></a>IDiaDataSource
Inicia o acesso a uma fonte de símbolos de depuração.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDiaDataSource : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 A tabela a seguir mostra os métodos de `IDiaDataSource`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDiaDataSource::get_lastError](../../debugger/debug-interface-access/idiadatasource-get-lasterror.md)|Recupera o nome do arquivo para o último erro de carga.|  
|[IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)|Abre e prepara um arquivo de banco de dados (. PDB) do programa como uma fonte de dados de depuração.|  
|[IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)|Abre e verifica se o arquivo de banco de dados (. PDB) de programa corresponde às informações de assinatura fornecidas; prepara o arquivo. PDB como uma fonte de dados de depuração.|  
|[IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)|Abre e prepara a depuração de dados associada ao arquivo.exe/.dll.|  
|[IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)|Prepara a depuração de dados armazenadas em um arquivo de banco de dados (. PDB) do programa acessado por meio de um fluxo de dados na memória.|  
|[IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)|Abre uma sessão de consulta de símbolos.|  
  
## <a name="remarks"></a>Comentários  
 Uma chamada para um dos métodos de carga a `IDiaDataSource` interface abrirá a fonte do símbolo. Uma chamada bem-sucedida para o [: Opensession](../../debugger/debug-interface-access/idiadatasource-opensession.md) método retorna um [IDiaSession](../../debugger/debug-interface-access/idiasession.md) interface que oferece suporte a consultas de fonte de dados. Se o método load retorna um erro relacionado ao arquivo o [: Get_lasterror](../../debugger/debug-interface-access/idiadatasource-get-lasterror.md) valor contém o nome do arquivo associado ao erro de retorno do método.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 Essa interface é obtida chamando o `CoCreateInstance` função com o identificador de classe `CLSID_DiaSource` e a ID de interface de `IID_IDiaDataSource`. O exemplo mostra como essa interface é obtida.  
  
## <a name="example"></a>Exemplo  
  
```C++  
  
      IDiaDataSource* pSource;  
HRESULT hr = CoCreateInstance(CLSID_DiaSource,  
                              NULL,  
                              CLSCTX_INPROC_SERVER,  
                              IID_IDiaDataSource,  
                              (void**) &pSource);  
if (FAILED(hr))  
{  
    // Report error and exit  
}  
```  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: Dia2.h  
  
 Biblioteca: diaguids.lib  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)