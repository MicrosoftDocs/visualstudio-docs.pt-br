---
title: Consultando o. Arquivo PDB | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- PDB files
- .pdb files, querying
ms.assetid: 8da07d1c-2712-45f9-8fbf-f34040408a8a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a13f98e9d1507c0044057099d61b625e1142929e
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44282047"
---
# <a name="querying-the-pdb-file"></a>Consultando o arquivo .Pdb
Um arquivo de banco de dados do programa (extensão. PDB) é um arquivo binário que contém o tipo e informações de depuração simbólicas coletados ao longo do compilando e vinculando o projeto. Um arquivo PDB é criado quando você compila um programa C/C++ com **/ZI** ou **/Zi** ou uma [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)], [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)], ou [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] programar com o **/Debug** opção. Arquivos de objeto contêm referências no arquivo. PDB para informações de depuração. Para obter mais informações sobre arquivos pdb, consulte [arquivos PDB](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/yd4f8bd1(v=vs.100)). Um aplicativo de DIA pode usar as seguintes etapas gerais para obter detalhes sobre os vários símbolos, objetos e elementos de dados dentro de uma imagem executável.  
  
### <a name="to-query-the-pdb-file"></a>Para consultar o arquivo. PDB  
  
1.  Adquirir uma fonte de dados com a criação de um [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md) interface.  
  
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
  
2.  Chame [idiadatasource:: Loaddatafrompdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) ou [idiadatasource:: Loaddataforexe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) para carregar as informações de depuração.  
  
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
  
3.  Chame [idiadatasource:: Opensession](../../debugger/debug-interface-access/idiadatasource-opensession.md) para abrir um [IDiaSession](../../debugger/debug-interface-access/idiasession.md) para acessar as informações de depuração.  
  
    ```C++  
    CComPtr<IDiaSession> psession;  
    if ( FAILED( pSource->openSession( &psession ) ) )   
    {  
        Fatal( "openSession" );  
    }  
    ```  
  
4.  Use os métodos em `IDiaSession` para consultar os símbolos na fonte de dados.  
  
    ```C++  
    CComPtr<IDiaSymbol> pglobal;  
    if ( FAILED( psession->get_globalScope( &pglobal) ) )  
    {  
        Fatal( "get_globalScope" );  
    }  
    ```  
  
5.  Use o `IDiaEnum*` interfaces para enumerar e examinar os símbolos ou outros elementos de informações de depuração.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)