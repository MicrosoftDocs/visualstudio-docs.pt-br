---
title: Consultando o. Arquivo PDB | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- PDB files
- .pdb files, querying
ms.assetid: 8da07d1c-2712-45f9-8fbf-f34040408a8a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7a7cff092d06b8845993dcf1a35b271da0c0a33c
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461157"
---
# <a name="querying-the-pdb-file"></a>Consultando o arquivo .Pdb
Um arquivo de banco de dados do programa (Extension. pdb) é um arquivo binário que contém informações sobre tipo e depuração simbólicas coletadas ao longo do curso da compilação e vinculação do projeto. Um arquivo PDB é criado quando você compila um programa C/C++ com **/Zi** ou **/Zi** , ou [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] um [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] programa, ou [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] com a opção **/debug** . Os arquivos de objeto contêm referências ao arquivo. pdb para informações de depuração. Para obter mais informações sobre arquivos PDB, consulte [arquivos PDB](/previous-versions/visualstudio/visual-studio-2010/yd4f8bd1(v=vs.100)). Um aplicativo DIA pode usar as seguintes etapas gerais para obter detalhes sobre os vários símbolos, objetos e elementos de dados em uma imagem executável.

### <a name="to-query-the-pdb-file"></a>Para consultar o arquivo. pdb

1. Adquira uma fonte de dados criando uma interface [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md) .

    ```C++
    CComPtr<IDiaDataSource> pSource;
    hr = CoCreateInstance( CLSID_DiaSource,
                           NULL,
                           CLSCTX_INPROC_SERVER,
                           __uuidof( IDiaDataSource ),
                          (void **) &pSource);

    if (FAILED(hr))
    {
        Fatal("Could not CoCreate CLSID_DiaSource. Register msdia80.dll." );
    }
    ```

2. Chame [IDiaDataSource:: loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) ou [IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) para carregar as informações de depuração.

    ```C++
    wchar_t wszFilename[ _MAX_PATH ];
    mbstowcs( wszFilename, szFilename, sizeof( wszFilename )/sizeof( wszFilename[0] ) );
    if ( FAILED( pSource->loadDataFromPdb( wszFilename ) ) )
    {
        if ( FAILED( pSource->loadDataForExe( wszFilename, NULL, NULL ) ) )
        {
            Fatal( "loadDataFromPdb/Exe" );
        }
    }
    ```

3. Chame [IDiaDataSource:: openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md) para abrir um [IDiaSession](../../debugger/debug-interface-access/idiasession.md) para obter acesso às informações de depuração.

    ```C++
    CComPtr<IDiaSession> psession;
    if ( FAILED( pSource->openSession( &psession ) ) )
    {
        Fatal( "openSession" );
    }
    ```

4. Use os métodos em `IDiaSession` para consultar os símbolos na fonte de dados.

    ```C++
    CComPtr<IDiaSymbol> pglobal;
    if ( FAILED( psession->get_globalScope( &pglobal) ) )
    {
        Fatal( "get_globalScope" );
    }
    ```

5. Use as `IDiaEnum*` interfaces para enumerar e examinar os símbolos ou outros elementos de informações de depuração.

    ```C++
    CComPtr<IDiaEnumTables> pTables;
    if ( FAILED( psession->getEnumTables( &pTables ) ) )
    {
        Fatal( "getEnumTables" );
    }
    CComPtr< IDiaTable > pTable;
    while ( SUCCEEDED( hr = pTables->Next( 1, &pTable, &celt ) ) && celt == 1 )
    {
        // Do something with each IDiaTable.
    }
    ```

## <a name="see-also"></a>Veja também
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
