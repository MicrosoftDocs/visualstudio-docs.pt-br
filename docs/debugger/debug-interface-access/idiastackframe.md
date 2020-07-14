---
title: IDiaStackFrame | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame interface
ms.assetid: 486d25b8-a590-41c1-bdb5-faff3ae35632
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e3cadcfd8fed1818e18d276503c0843e0567addf
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464908"
---
# <a name="idiastackframe"></a>IDiaStackFrame
Expõe as propriedades de um quadro de pilha.

## <a name="syntax"></a>Syntax

```
IDiaStackFrame : IUnknown
```

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
Estes são os métodos com suporte nesta interface:

|Método|Descrição|
|------------|-----------------|
|[IDiaStackFrame::get_allocatesBasePointer](../../debugger/debug-interface-access/idiastackframe-get-allocatesbasepointer.md)|Recupera um sinalizador que indica que o ponteiro base está alocado para o código neste intervalo de endereços. Esse método é preterido.|
|[IDiaStackFrame::get_base](../../debugger/debug-interface-access/idiastackframe-get-base.md)|Recupera a base de endereço do quadro.|
|[IDiaStackFrame::get_cplusplusExceptionHandling](../../debugger/debug-interface-access/idiastackframe-get-cplusplusexceptionhandling.md)|Recupera um sinalizador que indica que a manipulação de exceção do C++ está em vigor.|
|[IDiaStackFrame::get_functionStart](../../debugger/debug-interface-access/idiastackframe-get-functionstart.md)|Recupera um sinalizador que indica que o bloco contém o ponto de entrada de uma função.|
|[IDiaStackFrame::get_lengthLocals](../../debugger/debug-interface-access/idiastackframe-get-lengthlocals.md)|Recupera o número de bytes de variáveis locais enviadas por push na pilha.|
|[IDiaStackFrame::get_lengthParams](../../debugger/debug-interface-access/idiastackframe-get-lengthparams.md)|Recupera o número de bytes de parâmetros enviados por push na pilha.|
|[IDiaStackFrame::get_lengthProlog](../../debugger/debug-interface-access/idiastackframe-get-lengthprolog.md)|Recupera o número de bytes do código de prólogo no bloco|
|[IDiaStackFrame::get_lengthSavedRegisters](../../debugger/debug-interface-access/idiastackframe-get-lengthsavedregisters.md)|Recupera o número de bytes de registros salvos enviados por push na pilha.|
|[IDiaStackFrame::get_localsBase](../../debugger/debug-interface-access/idiastackframe-get-localsbase.md)|Recupera a base de endereço dos locais.|
|[IDiaStackFrame::get_maxStack](../../debugger/debug-interface-access/idiastackframe-get-maxstack.md)|Recupera o número máximo de bytes enviados por push na pilha no quadro.|
|[IDiaStackFrame::get_rawLVarInstanceValue](../../debugger/debug-interface-access/idiastackframe-get-rawlvarinstancevalue.md)|Recupera o valor da variável local especificada como bytes brutos.|
|[IDiaStackFrame::get_registerValue](../../debugger/debug-interface-access/idiastackframe-get-registervalue.md)|Recupera o valor de um registro especificado.|
|[IDiaStackFrame::get_returnAddress](../../debugger/debug-interface-access/idiastackframe-get-returnaddress.md)|Recupera o endereço de retorno do quadro.|
|[IDiaStackFrame::get_size](../../debugger/debug-interface-access/idiastackframe-get-size.md)|Recupera o tamanho do quadro em bytes.|
|[IDiaStackFrame::get_systemExceptionHandling](../../debugger/debug-interface-access/idiastackframe-get-systemexceptionhandling.md)|Recupera um sinalizador que indica que a manipulação de exceção do sistema está em vigor.|
|[IDiaStackFrame::get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md)|Recupera o tipo de quadro.|

## <a name="remarks"></a>Comentários
Um registro de ativação é uma abstração de uma chamada de função durante sua execução.

## <a name="notes-for-callers"></a>Observações para chamadores
Obtenha essa interface chamando o método [IDiaEnumStackFrames:: Next](../../debugger/debug-interface-access/idiaenumstackframes-next.md) . Consulte a interface [IDiaEnumStackFrames](../../debugger/debug-interface-access/idiaenumstackframes.md) para obter um exemplo de como obter a `IDiaStackFrame` interface.

## <a name="example"></a>Exemplo
Este exemplo exibe vários atributos de um quadro de pilha.

```C++
void PrintStackFrame(IDiaStackFrame* pFrame)
{
    if (pFrame != NULL)
    {
        ULONGLONG bottom = 0;
        ULONGLONG top    = 0;

        if (pFrame->get_base(&bottom) == S_OK &&
            pFrame->get_registerValue( CV_REG_ESP, &top ) == S_OK )
        {
            printf("range = 0x%08I64x - 0x%08I64x\n", bottom, top);
        }

        ULONGLONG returnAddress = 0;
        if (pFrame->get_returnAddress(&returnAddress) == S_OK)
        {
            printf("return address = 0x%08I64x\n", returnAddress);
        }

        DWORD lengthFrame     = 0;
        DWORD lengthLocals    = 0;
        DWORD lengthParams    = 0;
        DWORD lengthProlog    = 0;
        DWORD lengthSavedRegs = 0;
        if (pFrame->get_size(&lengthFrame) == S_OK &&
            pFrame->get_lengthLocals(&lengthLocals) == S_OK &&
            pFrame->get_lengthParams(&lengthParams) == S_OK &&
            pFrame->get_lengthProlog(&lengthProlog) == S_OK &&
            pFrame->get_lengthSavedRegisters(&lengthSavedRegs) == S_OK)
        {
            printf("stack frame size          = 0x%08lx bytes\n", lengthFrame);
            printf("length of locals          = 0x%08lx bytes\n", lengthLocals);
            printf("length of parameters      = 0x%08lx bytes\n", lengthParams);
            printf("length of prolog          = 0x%08lx bytes\n", lengthProlog);
            printf("length of saved registers = 0x%08lx bytes\n", lengthSavedRegs);
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
- [IDiaEnumStackFrames](../../debugger/debug-interface-access/idiaenumstackframes.md)
- [IDiaEnumStackFrames::Next](../../debugger/debug-interface-access/idiaenumstackframes-next.md)
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
