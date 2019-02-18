---
title: IDiaDataSource::loadDataForExe | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadDataForExe method
ms.assetid: d94a1068-f53f-44b5-b6fb-00dec361a7f2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b078e918f399019b2532e7fe3adea220fc09e012
ms.sourcegitcommit: 61dc40d6c707f8c79779ec1091b296530d5a7b81
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "55987542"
---
# <a name="idiadatasourceloaddataforexe"></a>IDiaDataSource::loadDataForExe
Abre e prepara os dados de depuração associados ao arquivo.exe/.dll.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT loadDataForExe (
   LPCOLESTR executable,
   LPCOLESTR searchPath,
   IUnknown* pCallback
);
```

#### <a name="parameters"></a>Parâmetros
executável  
[in] Caminho para o arquivo .exe ou. dll.

searchPath  
[in] Caminho alternativo para procurar dados de depuração.

pCallback  
[in] Uma `IUnknown` interface para um objeto que dá suporte a uma interface de retorno de chamada de depuração, como o [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md), [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md), o [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md), e/ou o [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md) interfaces.

## <a name="return-value"></a>Valor de retorno
Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro. A tabela a seguir mostra alguns dos possíveis códigos de erro para esse método.

|Valor|Descrição|
|-----------|-----------------|
|E_PDB_NOT_FOUND|Falha ao abrir o arquivo ou o arquivo tem um formato inválido.|
|E_PDB_FORMAT|Tentativa de acessar um arquivo com um formato obsoleto.|
|E_PDB_INVALID_SIG|Assinatura não corresponde.|
|E_PDB_INVALID_AGE|Não corresponde a idade.|
|E_INVALIDARG|Parâmetro inválido.|
|E_UNEXPECTED|Fonte de dados já foi preparada.|

## <a name="remarks"></a>Comentários
O cabeçalho de depuração do arquivo.exe/.dll nomeia o local de dados de depuração associados.

Esse método lê o cabeçalho de depuração e, em seguida, procura e prepara os dados de depuração. O progresso da pesquisa pode, opcionalmente, relatado e controlado por meio de retornos de chamada. Por exemplo, o [idialoadcallback:: Notifydebugdir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md) é invocado quando o `IDiaDataSource::loadDataForExe` método localiza e processa um diretório de depuração.

O [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md) e [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md) interfaces permitem que o aplicativo cliente fornecer métodos alternativos para ler dados do executável arquivo quando o arquivo não pode ser acessado diretamente por meio de e/s de arquivo padrão.

Para carregar um arquivo. PDB sem validação, use o [idiadatasource:: Loaddatafrompdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) método.

Para validar o arquivo. PDB em relação a critérios específicos, use o [idiadatasource:: Loadandvalidatedatafrompdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md) método.

Para carregar um arquivo. PDB diretamente da memória, use o [idiadatasource:: Loaddatafromistream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md) método.

## <a name="example"></a>Exemplo

```C++
class MyCallBack: public IDiaLoadCallback
{
...
};
MyCallBack callback;
...
HRESULT hr = pSource->loadDataForExe( L"myprog.exe", L".\debug", (IUnknown*)&callback);
if (FAILED(hr))
{
    // Report error
}
```

## <a name="see-also"></a>Consulte também
[IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)  
[IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)  
[IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)  
[IDiaLoadCallback::NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md)  
[IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)  
[IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)  
[IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)  
[IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)  
[IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)
