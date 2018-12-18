---
title: IDiaSession | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession interface
ms.assetid: 69dab9bf-2c68-4f70-9678-3b50fba3e6fa
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7b2791f318a921a25535d5e9a8f17e2c595f1f56
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31468327"
---
# <a name="idiasession"></a>IDiaSession
Fornece um contexto de consulta para símbolos de depuração.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDiaSession : IUnknown  
```  
  
## <a name="methods"></a>Métodos  
 A tabela a seguir mostra os métodos de `IDiaSession`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDiaSession::get_loadAddress](../../debugger/debug-interface-access/idiasession-get-loadaddress.md)|Recupera o endereço de carregamento para o arquivo executável que corresponde aos símbolos neste armazenamento de símbolo. Este é o mesmo valor que foi passado para o `put_loadAddress` método.|  
|[IDiaSession::put_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)|Define o endereço de carregamento para o arquivo executável que corresponde aos símbolos neste armazenamento de símbolo. **Observação:** é importante chamar esse método quando você receber um `IDiaSession` de objeto e antes de começar a usar o objeto.|  
|[IDiaSession::get_globalScope](../../debugger/debug-interface-access/idiasession-get-globalscope.md)|Recupera uma referência ao escopo global.|  
|[IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)|Recupera um enumerador para todas as tabelas contidas no repositório de símbolos.|  
|[IDiaSession::getSymbolsByAddr](../../debugger/debug-interface-access/idiasession-getsymbolsbyaddr.md)|Recupera um enumerador para todos os símbolos nomeados em locais estáticos.|  
|[IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)|Recupera todos os filhos de um identificador do pai especificado que correspondem ao tipo e um símbolo.|  
|[IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)|Recupera um tipo de símbolo especificado que contém ou está mais próximo de um endereço especificado.|  
|[IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)|Recupera um tipo de símbolo especificado que contém ou está mais próximo de um endereço relativo virtual (RVA) especificado.|  
|[IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)|Recupera um tipo de símbolo especificado que contém ou está mais próximo de um endereço virtual especificado (VA).|  
|[IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)|Recupera o símbolo que contém um token de metadados especificado.|  
|[IDiaSession::symsAreEquiv](../../debugger/debug-interface-access/idiasession-symsareequiv.md)|Verifica se os dois símbolos são equivalentes.|  
|[IDiaSession::symbolById](../../debugger/debug-interface-access/idiasession-symbolbyid.md)|Recupera um símbolo por seu identificador exclusivo.|  
|[IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)|Recupera um tipo de símbolo especificado que contém ou está mais próximo de um endereço virtual relativo especificado e o deslocamento.|  
|[IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)|Recupera um tipo de símbolo especificado que contém ou está mais próximo de um endereço virtual especificado e o deslocamento.|  
|[IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)|Recupera um arquivo de origem por compiland e nome.|  
|[IDiaSession::findFileById](../../debugger/debug-interface-access/idiasession-findfilebyid.md)|Recupera um arquivo de origem pelo identificador de arquivo de origem.|  
|[IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md)|Recupera os números de linha dentro de um identificador de arquivo compiland e de origem especificado.|  
|[IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)|Recupera as linhas em um compiland especificado que contém um endereço especificado.|  
|[IDiaSession::findLinesByRVA](../../debugger/debug-interface-access/idiasession-findlinesbyrva.md)|Recupera as linhas que contêm um endereço virtual relativo especificado em um compiland especificado.|  
|[IDiaSession::findLinesByVA](../../debugger/debug-interface-access/idiasession-findlinesbyva.md)|Localiza as informações de número de linha para linhas contidas em um intervalo de endereços especificado.|  
|[IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)|Recupera as linhas em um compiland especificado pelo número de arquivos e linhas de origem.|  
|[IDiaSession::findInjectedSource](../../debugger/debug-interface-access/idiasession-findinjectedsource.md)|Recupera uma fonte que foi colocada no repositório de símbolos por provedores de atributo ou outros componentes do processo de compilação.|  
|[IDiaSession::getEnumDebugStreams](../../debugger/debug-interface-access/idiasession-getenumdebugstreams.md)|Recupera uma sequência enumerada depuração de fluxos de dados.|  
|[IDiaSession::findInlineFramesByAddr](../../debugger/debug-interface-access/idiasession-findinlineframesbyaddr.md)|Recupera uma enumeração que permite que um cliente iterar por todos os quadros embutido em um determinado endereço.|  
|[IDiaSession::findInlineFramesByRVA](../../debugger/debug-interface-access/idiasession-findinlineframesbyrva.md)|Recupera uma enumeração que permite que um cliente iterar por todos os quadros embutido em um endereço relativo virtual (RVA) especificado.|  
|[IDiaSession::findInlineFramesByVA](../../debugger/debug-interface-access/idiasession-findinlineframesbyva.md)|Recupera uma enumeração que permite que um cliente iterar por todos os quadros embutido em um dado endereço virtual (VA).|  
|[IDiaSession::findInlineeLines](../../debugger/debug-interface-access/idiasession-findinlineelines.md)|Recupera uma enumeração que permite que um cliente iterar por meio das informações de número de linha de todas as funções embutidas, diretamente ou indiretamente, pelo símbolo de pai especificado.|  
|[IDiaSession::findInlineeLinesByAddr](../../debugger/debug-interface-access/idiasession-findinlineelinesbyaddr.md)|Recupera uma enumeração que permite que um cliente iterar por meio das informações de número de linha de todas as funções embutidas, diretamente ou indiretamente, pelo símbolo de pai especificado e está contida dentro do intervalo especificado.|  
|[IDiaSession::findInlineeLinesByRVA](../../debugger/debug-interface-access/idiasession-findinlineelinesbyrva.md)|Recupera uma enumeração que permite que um cliente iterar por meio das informações de número de linha de todas as funções embutidas, diretamente ou indiretamente, pelo símbolo de pai especificado e está contida dentro do endereço relativo virtual (RVA) especificado.|  
|[IDiaSession::findInlineeLinesByVA](../../debugger/debug-interface-access/idiasession-findinlineelinesbyva.md)|Recupera uma enumeração que permite que um cliente iterar por meio das informações de número de linha de todas as funções embutidas, diretamente ou indiretamente, pelo símbolo de pai especificado e está contida dentro do endereço virtual especificado (VA).|  
|[IDiaSession::findInlineeLinesByLinenum](../../debugger/debug-interface-access/idiasession-findinlineelinesbylinenum.md)|Recupera uma enumeração que permite que um cliente iterar por meio das informações de número de linha de todas as funções que são embutidos, diretamente ou indiretamente, o número de arquivos e linhas de origem especificada.|  
|[IDiaSession::findInlineesByName](../../debugger/debug-interface-access/idiasession-findinlineesbyname.md)|Recupera uma enumeração que permite que um cliente iterar por meio das informações de número de linha de todas as funções embutidas que corresponde a um nome especificado.|  
|[IDiaSession::findSymbolsForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasession-findsymbolsforacceleratorpointertag.md)|Retorna uma enumeração de símbolos para que o valor da marca especificado corresponde à variável na função de stub do acelerador pai.|  
|[IDiaSession::findSymbolsByRVAForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasession-findsymbolsbyrvaforacceleratorpointertag.md)|Dado um valor de marca correspondente, esse método retorna uma enumeração de símbolos que estão contidos em uma função de stub do acelerador pai especificado em um endereço virtual relativo especificado.|  
|[IDiaSession::findAcceleratorInlineesByName](../../debugger/debug-interface-access/idiasession-findacceleratorinlineesbyname.md)|Retorna uma enumeração de símbolos para quadros embutidos correspondente ao nome da função embutida especificado.|  
|[IDiaSession::findAcceleratorInlineesByLinenum](../../debugger/debug-interface-access/idiasession-findacceleratorinlineesbylinenum.md)|Retorna uma enumeração de símbolos para os quadros entre linhas que correspondem ao local de origem especificado.|  
  
## <a name="remarks"></a>Comentários  
 É importante chamar o [: Put_loadaddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md) método depois de criar o `IDiaSession` objeto — e o valor passado para o `put_loadAddress` método deve ser diferente de zero — de qualquer propriedade de endereço virtual (VA) de símbolos para ser acessível. O endereço de carregamento vêm de qualquer programa carregado o arquivo executável que está sendo depurado. Por exemplo, você pode chamar a função Win32 `GetModuleInformation` para recuperar o endereço de carregamento para o executável, recebe um identificador para o executável.  
  
## <a name="example"></a>Exemplo  
 Este exemplo mostra como obter o `IDiaSession` interface como parte de uma inicialização geral do SDK do DIA.  
  
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
 Cabeçalho: Dia2.h  
  
 Biblioteca: diaguids.lib  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces (SDK de acesso à Interface de depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [Visão geral](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)   
 [Exe](../../debugger/debug-interface-access/exe.md)   
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)   
 [: Opensession](../../debugger/debug-interface-access/idiadatasource-opensession.md)   
 [: Findchildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)   
 [Consultando o arquivo .Pdb](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)