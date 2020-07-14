---
title: IDiaSession | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession interface
ms.assetid: 69dab9bf-2c68-4f70-9678-3b50fba3e6fa
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e7fb8c5336a14180b3742fa02a91e6532b6e5831
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465345"
---
# <a name="idiasession"></a>IDiaSession
Fornece um contexto de consulta para símbolos de depuração.

## <a name="syntax"></a>Syntax

```
IDiaSession : IUnknown
```

## <a name="methods"></a>Métodos
A tabela a seguir mostra os métodos de `IDiaSession` .

|Método|Descrição|
|------------|-----------------|
|[IDiaSession::get_loadAddress](../../debugger/debug-interface-access/idiasession-get-loadaddress.md)|Recupera o endereço de carregamento do arquivo executável que corresponde aos símbolos neste repositório de símbolos. Esse é o mesmo valor que foi passado para o `put_loadAddress` método.|
|[IDiaSession::put_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)|Define o endereço de carregamento para o arquivo executável que corresponde aos símbolos neste repositório de símbolos. **Observação:**  É importante chamar esse método quando você recebe um `IDiaSession` objeto e antes de começar a usar o objeto.|
|[IDiaSession::get_globalScope](../../debugger/debug-interface-access/idiasession-get-globalscope.md)|Recupera uma referência ao escopo global.|
|[IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)|Recupera um enumerador para todas as tabelas contidas no repositório de símbolos.|
|[IDiaSession::getSymbolsByAddr](../../debugger/debug-interface-access/idiasession-getsymbolsbyaddr.md)|Recupera um enumerador para todos os símbolos nomeados em locais estáticos.|
|[IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)|Recupera todos os filhos de um identificador pai especificado que correspondem ao nome e ao tipo de símbolo.|
|[IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)|Recupera um tipo de símbolo especificado que contém ou está mais próximo de um endereço especificado.|
|[IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)|Recupera um tipo de símbolo especificado que contém ou está mais próximo de um endereço virtual relativo (RVA) específico.|
|[IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)|Recupera um tipo de símbolo especificado que contém ou está mais próximo de um endereço virtual especificado (VA).|
|[IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)|Recupera o símbolo que contém um token de metadados especificado.|
|[IDiaSession::symsAreEquiv](../../debugger/debug-interface-access/idiasession-symsareequiv.md)|Verifica se dois símbolos são equivalentes.|
|[IDiaSession::symbolById](../../debugger/debug-interface-access/idiasession-symbolbyid.md)|Recupera um símbolo por seu identificador exclusivo.|
|[IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)|Recupera um tipo de símbolo especificado que contém, ou está mais próximo de, um endereço virtual relativo especificado e um deslocamento.|
|[IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)|Recupera um tipo de símbolo especificado que contém ou está mais próximo de, um endereço virtual e um deslocamento especificados.|
|[IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)|Recupera um arquivo de origem por compiland e nome.|
|[IDiaSession::findFileById](../../debugger/debug-interface-access/idiasession-findfilebyid.md)|Recupera um arquivo de origem por identificador de arquivo de origem.|
|[IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md)|Recupera números de linha dentro de um compiland e identificador de arquivo de origem especificados.|
|[IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)|Recupera as linhas em um compiland especificado que contém um endereço especificado.|
|[IDiaSession::findLinesByRVA](../../debugger/debug-interface-access/idiasession-findlinesbyrva.md)|Recupera as linhas em um compiland especificado que contém um endereço virtual relativo especificado.|
|[IDiaSession::findLinesByVA](../../debugger/debug-interface-access/idiasession-findlinesbyva.md)|Localiza as informações de número de linha para as linhas contidas em um intervalo de endereços especificado.|
|[IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)|Recupera as linhas em um compiland especificado por arquivo de origem e número de linha.|
|[IDiaSession::findInjectedSource](../../debugger/debug-interface-access/idiasession-findinjectedsource.md)|Recupera uma fonte que foi colocada no repositório de símbolos por provedores de atributos ou outros componentes do processo de compilação.|
|[IDiaSession::getEnumDebugStreams](../../debugger/debug-interface-access/idiasession-getenumdebugstreams.md)|Recupera uma sequência enumerada de fluxos de dados de depuração.|
|[IDiaSession::findInlineFramesByAddr](../../debugger/debug-interface-access/idiasession-findinlineframesbyaddr.md)|Recupera uma enumeração que permite que um cliente Itere em todos os quadros embutidos em um determinado endereço.|
|[IDiaSession::findInlineFramesByRVA](../../debugger/debug-interface-access/idiasession-findinlineframesbyrva.md)|Recupera uma enumeração que permite que um cliente Itere em todos os quadros embutidos em um endereço virtual relativo (RVA) específico.|
|[IDiaSession::findInlineFramesByVA](../../debugger/debug-interface-access/idiasession-findinlineframesbyva.md)|Recupera uma enumeração que permite que um cliente Itere em todos os quadros embutidos em um endereço virtual especificado (VA).|
|[IDiaSession::findInlineeLines](../../debugger/debug-interface-access/idiasession-findinlineelines.md)|Recupera uma enumeração que permite que um cliente itere pelas informações de número de linha de todas as funções que são embutidas, direta ou indiretamente, pelo símbolo pai especificado.|
|[IDiaSession::findInlineeLinesByAddr](../../debugger/debug-interface-access/idiasession-findinlineelinesbyaddr.md)|Recupera uma enumeração que permite que um cliente itere pelas informações de número de linha de todas as funções que são embutidas, direta ou indiretamente, pelo símbolo pai especificado e estão contidas no intervalo de endereços especificado.|
|[IDiaSession::findInlineeLinesByRVA](../../debugger/debug-interface-access/idiasession-findinlineelinesbyrva.md)|Recupera uma enumeração que permite que um cliente itere pelas informações de número de linha de todas as funções que são embutidas, direta ou indiretamente, pelo símbolo pai especificado e estão contidas no endereço virtual relativo (RVA) especificado.|
|[IDiaSession::findInlineeLinesByVA](../../debugger/debug-interface-access/idiasession-findinlineelinesbyva.md)|Recupera uma enumeração que permite que um cliente itere pelas informações de número de linha de todas as funções que são embutidas, direta ou indiretamente, pelo símbolo pai especificado e estão contidas no endereço virtual (VA) especificado.|
|[IDiaSession::findInlineeLinesByLinenum](../../debugger/debug-interface-access/idiasession-findinlineelinesbylinenum.md)|Recupera uma enumeração que permite que um cliente itere pelas informações de número de linha de todas as funções que são embutidas, direta ou indiretamente, no arquivo de origem e no número de linha especificados.|
|[IDiaSession::findInlineesByName](../../debugger/debug-interface-access/idiasession-findinlineesbyname.md)|Recupera uma enumeração que permite que um cliente itere pelas informações de número de linha de todas as funções embutidas que correspondem a um nome especificado.|
|[IDiaSession::findSymbolsForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasession-findsymbolsforacceleratorpointertag.md)|Retorna uma enumeração de símbolos para a variável para a qual o valor de marca especificado corresponde na função de stub do acelerador pai.|
|[IDiaSession::findSymbolsByRVAForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasession-findsymbolsbyrvaforacceleratorpointertag.md)|Dado um valor de marca correspondente, esse método retorna uma enumeração de símbolos que estão contidos em uma função de stub de acelerador pai especificada em um endereço virtual relativo especificado.|
|[IDiaSession::findAcceleratorInlineesByName](../../debugger/debug-interface-access/idiasession-findacceleratorinlineesbyname.md)|Retorna uma enumeração de símbolos para quadros embutidos correspondentes ao nome da função embutida especificada.|
|[IDiaSession::findAcceleratorInlineesByLinenum](../../debugger/debug-interface-access/idiasession-findacceleratorinlineesbylinenum.md)|Retorna uma enumeração de símbolos para quadros embutidos que correspondem ao local de origem especificado.|

## <a name="remarks"></a>Comentários
É importante chamar o método [IDiaSession::p ut_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md) depois de criar o `IDiaSession` objeto — e o valor passado para o `put_loadAddress` método deve ser diferente de zero — para que qualquer propriedade de endereço virtual (VA) de símbolos seja acessível. O endereço de carregamento é proveniente de qualquer programa que carregou o executável que está sendo depurado. Por exemplo, você pode chamar a função do Win32 `GetModuleInformation` para recuperar o endereço de carregamento do executável, dado um identificador para o executável.

## <a name="example"></a>Exemplo
Este exemplo mostra como obter a `IDiaSession` interface como parte de uma inicialização geral do dia SDK.

```C++
CComPtr<IDiaDataSource> pSource;
ComPtr<IDiaSession> psession;

void InitializeDIA(const char *szFilename)
{
    HRESULT hr = CoCreateInstance( CLSID_DiaSource,
                                   NULL,
                                   CLSCTX_INPROC_SERVER,
                                   __uuidof( IDiaDataSource ),
                                  (void **) &pSource);
    if (FAILED(hr))
    {
        Fatal("Could not CoCreate CLSID_DiaSource. Register msdia80.dll." );
    }
    wchar_t wszFilename[ _MAX_PATH ];
    mbstowcs( wszFilename,
              szFilename,
              sizeof( wszFilename )/sizeof( wszFilename[0] ) );
    if ( FAILED( pSource->loadDataFromPdb( wszFilename ) ) )
    {
        if ( FAILED( pSource->loadDataForExe( wszFilename, NULL, NULL ) ) )
        {
            Fatal( "loadDataFromPdb/Exe" );
        }
    }
    if ( FAILED( pSource->openSession( &psession ) ) )
    {
        Fatal( "openSession" );
    }
}
```

## <a name="requirements"></a>Requisitos
Cabeçalho: dia2. h

Biblioteca: diaguids. lib

DLL: msdia80.dll

## <a name="see-also"></a>Veja também
- [Interfaces (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [Visão geral](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)
- [Exe](../../debugger/debug-interface-access/exe.md)
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
- [Consultando o arquivo .Pdb](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)
