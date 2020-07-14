---
title: IDiaDataSource::loadDataForExe | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
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
ms.openlocfilehash: 2ed61f8ffc95d0004213483d5b5d507c45ef2647
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468514"
---
# <a name="idiadatasourceloaddataforexe"></a>IDiaDataSource::loadDataForExe
Abre e prepara os dados de depuração associados ao arquivo. exe/. dll.

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

no Caminho para o arquivo. exe ou. dll.

searchPath

no Caminho alternativo para pesquisar dados de depuração.

pCallback

no Uma `IUnknown` interface para um objeto que dá suporte a uma interface de retorno de chamada de depuração, como [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md), [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md), [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)e/ou as interfaces [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md) .

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. A tabela a seguir mostra alguns dos possíveis códigos de erro para esse método.

|Valor|Descrição|
|-----------|-----------------|
|E_PDB_NOT_FOUND|Falha ao abrir o arquivo ou o arquivo tem um formato inválido.|
|E_PDB_FORMAT|Tentativa de acessar um arquivo com um formato obsoleto.|
|E_PDB_INVALID_SIG|A assinatura não corresponde.|
|E_PDB_INVALID_AGE|A idade não corresponde.|
|E_INVALIDARG|Parâmetro inválido.|
|E_UNEXPECTED|A fonte de dados já foi preparada.|

## <a name="remarks"></a>Comentários
O cabeçalho de depuração do arquivo. exe/. dll nomeia o local de dados de depuração associado.

Esse método lê o cabeçalho de depuração e, em seguida, pesquisa e prepara os dados de depuração. O progresso da pesquisa pode, opcionalmente, ser relatado e controlado por meio de retornos de chamada. Por exemplo, o [IDiaLoadCallback:: NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md) é invocado quando o `IDiaDataSource::loadDataForExe` método localiza e processa um diretório de depuração.

As interfaces [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md) e [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md) permitem que o aplicativo cliente forneça métodos alternativos para ler dados do arquivo executável quando o arquivo não pode ser acessado diretamente por meio de e/s de arquivo padrão.

Para carregar um arquivo. pdb sem validação, use o método [IDiaDataSource:: loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) .

Para validar o arquivo. pdb em relação a critérios específicos, use o método [IDiaDataSource:: loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md) .

Para carregar um arquivo. pdb diretamente da memória, use o método [IDiaDataSource:: loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md) .

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

## <a name="see-also"></a>Confira também
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
- [IDiaLoadCallback::NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)
- [IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)
- [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)
