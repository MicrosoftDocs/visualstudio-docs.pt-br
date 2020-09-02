---
title: Consultando o. Arquivo PDB | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- PDB files
- .pdb files, querying
ms.assetid: 8da07d1c-2712-45f9-8fbf-f34040408a8a
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9b9013d41ac4d5ca890e7cc9e09b5eb9415cb640
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "65691325"
---
# <a name="querying-the-pdb-file"></a>Consultando o arquivo .Pdb
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um arquivo de banco de dados do programa (Extension. pdb) é um arquivo binário que contém informações sobre tipo e depuração simbólicas coletadas ao longo do curso da compilação e vinculação do projeto. Um arquivo PDB é criado quando você compila um programa C/C++ com **/Zi** ou **/Zi** , ou [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] um [!INCLUDE[csprcs](../../includes/csprcs-md.md)] programa, ou [!INCLUDE[jsprjscript](../../includes/jsprjscript-md.md)] com a opção **/debug** . Os arquivos de objeto contêm referências ao arquivo. pdb para informações de depuração. Para obter mais informações sobre arquivos PDB, consulte [arquivos PDB](https://msdn.microsoft.com/1761c84e-8c2c-4632-9649-b5f99964ed3f). Um aplicativo DIA pode usar as seguintes etapas gerais para obter detalhes sobre os vários símbolos, objetos e elementos de dados em uma imagem executável.  
  
### <a name="to-query-the-pdb-file"></a>Para consultar o arquivo. pdb  
  
1. Adquira uma fonte de dados criando uma interface [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md) .  
  
    ```cpp#  
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
  
    ```cpp#  
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
  
    ```cpp#  
    CComPtr<IDiaSession> psession;  
    if ( FAILED( pSource->openSession( &psession ) ) )   
    {  
        Fatal( "openSession" );  
    }  
    ```  
  
4. Use os métodos em `IDiaSession` para consultar os símbolos na fonte de dados.  
  
    ```cpp#  
    CComPtr<IDiaSymbol> pglobal;  
    if ( FAILED( psession->get_globalScope( &pglobal) ) )  
    {  
        Fatal( "get_globalScope" );  
    }  
    ```  
  
5. Use as `IDiaEnum*` interfaces para enumerar e examinar os símbolos ou outros elementos de informações de depuração.  
  
    ```cpp#  
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
  
## <a name="see-also"></a>Consulte Também  
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
