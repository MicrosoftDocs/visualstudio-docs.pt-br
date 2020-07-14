---
title: IDiaFrameData | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData interface
ms.assetid: 2f1b4986-341b-4641-89a4-226e261e9d93
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ee2f68066de6a41e6fd6a1cf4143613a7597d6f1
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85467179"
---
# <a name="idiaframedata"></a>IDiaFrameData
Expõe os detalhes de um quadro de pilha.

## <a name="syntax"></a>Syntax

```
IDiaFrameData : IUnknown
```

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
A tabela a seguir mostra os métodos de `IDiaFrameData` .

|Método|Descrição|
|------------|-----------------|
|[IDiaFrameData::get_addressSection](../../debugger/debug-interface-access/idiaframedata-get-addresssection.md)|Recupera a parte da seção do endereço do código para o quadro.|
|[IDiaFrameData::get_addressOffset](../../debugger/debug-interface-access/idiaframedata-get-addressoffset.md)|Recupera a parte de deslocamento do endereço do código para o quadro.|
|[IDiaFrameData::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiaframedata-get-relativevirtualaddress.md)|Recupera o endereço virtual relativo da imagem (RVA) do código para o quadro.|
|[IDiaFrameData::get_virtualAddress](../../debugger/debug-interface-access/idiaframedata-get-virtualaddress.md)|Recupera o endereço virtual (VA) do código para o quadro.|
|[IDiaFrameData::get_lengthBlock](../../debugger/debug-interface-access/idiaframedata-get-lengthblock.md)|Recupera o comprimento, em bytes, do bloco de código descrito pelo quadro.|
|[IDiaFrameData::get_lengthLocals](../../debugger/debug-interface-access/idiaframedata-get-lengthlocals.md)|Recupera o número de bytes de variáveis locais enviadas por push na pilha.|
|[IDiaFrameData::get_lengthParams](../../debugger/debug-interface-access/idiaframedata-get-lengthparams.md)|Recupera o número de bytes de parâmetros enviados por push na pilha.|
|[IDiaFrameData::get_maxStack](../../debugger/debug-interface-access/idiaframedata-get-maxstack.md)|Recupera o número máximo de bytes enviados por push na pilha no quadro.|
|[IDiaFrameData::get_lengthProlog](../../debugger/debug-interface-access/idiaframedata-get-lengthprolog.md)|Recupera o número de bytes do código de prólogo no bloco.|
|[IDiaFrameData::get_lengthSavedRegisters](../../debugger/debug-interface-access/idiaframedata-get-lengthsavedregisters.md)|Recupera o número de bytes de registros salvos enviados por push na pilha.|
|[IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)|Recupera a cadeia de caracteres do programa que é usada para calcular o conjunto de registros antes da chamada para a função atual.|
|[IDiaFrameData::get_systemExceptionHandling](../../debugger/debug-interface-access/idiaframedata-get-systemexceptionhandling.md)|Recupera um sinalizador que indica que a manipulação de exceção do sistema está em vigor.|
|[IDiaFrameData::get_cplusplusExceptionHandling](../../debugger/debug-interface-access/idiaframedata-get-cplusplusexceptionhandling.md)|Recupera um sinalizador que indica que a manipulação de exceção do C++ está em vigor.|
|[IDiaFrameData::get_functionStart](../../debugger/debug-interface-access/idiaframedata-get-functionstart.md)|Recupera um sinalizador que indica que o bloco contém o ponto de entrada de uma função.|
|[IDiaFrameData::get_allocatesBasePointer](../../debugger/debug-interface-access/idiaframedata-get-allocatesbasepointer.md)|Recupera um sinalizador que indica que o ponteiro base está alocado para o código neste intervalo de endereços. Esse método é preterido.|
|[IDiaFrameData::get_type](../../debugger/debug-interface-access/idiaframedata-get-type.md)|Recupera o tipo de quadro específico do compilador.|
|[IDiaFrameData::get_functionParent](../../debugger/debug-interface-access/idiaframedata-get-functionparent.md)|Recupera a interface de dados de quadro para a função de circunscrição.|
|[IDiaFrameData::execute](../../debugger/debug-interface-access/idiaframedata-execute.md)|Executa o desenrolamento de pilha e retorna o estado atual dos registros em uma interface de quadro de movimentação de pilha.|

## <a name="remarks"></a>Comentários
 Os detalhes disponíveis para um quadro são para pontos de execução dentro do intervalo de endereços indicado pelo endereço e pelo comprimento do bloco.

## <a name="notes-for-callers"></a>Observações para chamadores
 Obtenha essa interface chamando os métodos [IDiaEnumFrameData:: Next](../../debugger/debug-interface-access/idiaenumframedata-next.md) ou [IDiaEnumFrameData:: item](../../debugger/debug-interface-access/idiaenumframedata-item.md) . Consulte a interface [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md) para obter detalhes.

## <a name="example"></a>Exemplo
 Este exemplo imprime as propriedades de um `IDiaFrameData` objeto. Consulte a interface [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md) para obter um exemplo de como a `IDiaFrameData` interface é obtida.

```C++
void PrintFrameData(IDiaFrameData* pFrameData){
    DWORD dwSect;
    DWORD dwOffset;
    DWORD cbBlock;
    DWORD cbLocals; // Number of bytes reserved for the function locals
    DWORD cbParams; // Number of bytes reserved for the function arguments
    DWORD cbMaxStack;
    DWORD cbProlog;
    DWORD cbSavedRegs;
    BOOL  bSEH;
    BOOL  bEH;
    BOOL  bStart;
    BSTR  wszProgram;

    if(pFrameData->get_addressSection(&dwSect) == S_OK &&
       pFrameData->get_addressOffset(&dwOffset) == S_OK &&
       pFrameData->get_lengthBlock(&cbBlock) == S_OK &&
       pFrameData->get_lengthLocals(&cbLocals) == S_OK &&
       pFrameData->get_lengthParams(&cbParams) == S_OK &&
       pFrameData->get_maxStack(&cbMaxStack) == S_OK &&
       pFrameData->get_lengthProlog(&cbProlog) == S_OK &&
       pFrameData->get_lengthSavedRegisters(&cbSavedRegs) == S_OK &&
       pFrameData->get_systemExceptionHandling(&bSEH) == S_OK &&
       pFrameData->get_cplusplusExceptionHandling(&bEH) == S_OK &&
       pFrameData->get_functionStart(&bStart) == S_OK )
    {
        wprintf(L"Frame address  : %04X:%08X\n", dwSect, dwOffset);
        wprintf(L"Block size     : 0x%8X\n", cbBlock);
        wprintf(L"Locals size    : 0x%8X\n", cbLocals);
        wprintf(L"Parms size     : 0x%8X\n", cbParams);
        wprintf(L"Max stack used : 0x%8X\n", cbMaxStack);
        wprintf(L"Prolog size    : 0x%8X\n", cbProlog);
        wprintf(L"Saved regs size: 0x%8X\n", cbSavedRegs);
        wprintf(L"System Exception Handling: %c\n", bSEH ? L'Y' : L'N');
        wprintf(L"C++ Exception Handling   : %c\n", bEH ? L'Y' : L'N');
        wprintf(L"Function starts in block : %c\n", bStart ? L'Y' : L'N');

        if (pFrameData->get_program(&wszProgram) == S_OK)
        {
            wprintf(L"Program used for register set: %s\n", wszProgram);
            SysFreeString(wszProgram);
        }
        else
        {
            wprintf(L"\n");
        }
    }
}
```

## <a name="requirements"></a>Requisitos
Cabeçalho: dia2. h

Biblioteca: diaguids. lib

DLL: msdia80.dll

## <a name="see-also"></a>Veja também
- [Interfaces (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
- [IDiaEnumFrameData::Item](../../debugger/debug-interface-access/idiaenumframedata-item.md)
- [IDiaEnumFrameData::Next](../../debugger/debug-interface-access/idiaenumframedata-next.md)
