---
title: IDiaSession::findLinesByLinenum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findLinesByLinenum method
ms.assetid: 76d5622d-9a91-4c2a-a98f-263af5d1daef
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 240eb3196ac47bf48bc6d6c3ef3ca844ec010dde
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465660"
---
# <a name="idiasessionfindlinesbylinenum"></a>IDiaSession::findLinesByLinenum
Determina os números de linha do compiland que o número de linha especificado em um arquivo de origem está dentro ou próximo.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findLinesByLinenum ( 
    IDiaSymbol*           compiland,
    IDiaSourceFile*       file,
    DWORD                 linenum,
    DWORD                 column,
    IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>Parâmetros
`compiland`

no Um objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representa o compiland no qual Pesquisar os números de linha. O parâmetro não pode ser `NULL`.

`file`

no Um objeto [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) que representa o arquivo de origem para pesquisar. O parâmetro não pode ser `NULL`.

`linenum`

no Especifica um número de linha baseado em um.

> [!NOTE]
> Não é possível usar zero para especificar todas as linhas (use o método [IDiaSession:: findLines](../../debugger/debug-interface-access/idiasession-findlines.md) para localizar todas as linhas).

`column`

no Especifica o número da coluna. Use zero para especificar todas as colunas. Uma coluna é um deslocamento de byte em uma linha.

`ppResult`

fora Retorna um [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md) objta que contém uma lista dos números de linha recuperados.

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como abrir um arquivo de origem, enumerar o compilandos contribuído por esse arquivo e localizar os números de linha no arquivo de origem onde cada compiland é iniciado.

```C++
void ShowLinesInCompilands(IDiaSession *pSession, LPCOLESTR filename)
{
    IDiaEnumSourceFiles* pEnum;
    IDiaSourceFile*      pFile;
    DWORD                celt;

    pSession->findFile ( NULL, filename, nsFNameExt, &pEnum );
    while ( pEnum->Next ( 1, &pFile, &celt ) == S_OK ) // for each file
    {
        IDiaEnumSymbols* pEnumCompilands;
        IDiaSymbol* pCompiland;

        pFile->get_compilands ( &pEnumCompilands );
        // for each compiland
        while ( pEnumCompilands->Next ( 1, &pCompiland, &celt ) == S_OK )
        {
            IDiaEnumLineNumbers* pEnum;
            // Find first compiland closest to line 1 of the file.
            if (pSession->findLinesByLinenum( pCompiland, pFile, 1, 0, &pEnum ) == S_OK)
            {
                IDiaLineNumber *pLineNumber;
                DWORD lineCount;
                while ( pEnum->Next(1,&pLineNumber,&lineCount) == S_OK)
                {
                    DWORD lineNum;
                    if (pLineNumber->get_line(&lineNum) == S_OK)
                    {
                        printf("compiland starts in source at line number = %lu\n",lineNum);
                    }
                }
            }
        }
    }
}
```

## <a name="see-also"></a>Veja também
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
