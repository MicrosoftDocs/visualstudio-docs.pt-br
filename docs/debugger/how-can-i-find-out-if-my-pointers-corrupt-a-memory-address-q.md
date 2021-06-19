---
title: Descubra se meus ponteiros corromperam um endereço de memória | Microsoft Docs
description: Para determinar se o ponteiro está corrompida na memória, você pode procurar corrupção de heap e pode definir um ponto de interrupção de dados para descobrir como um valor é modificado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- addresses, pointers corrupting memory address
- memory, corruption
- pointers, corrupting memory addresses
- memory address corruption by pointers
- debugging [C++], memory corruption
- corrupted memory address
ms.assetid: a147c939-4fb1-415c-8410-cf303781e9e8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 836cc0363da0e20c45d83e1b2c13081e480fa919
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386963"
---
# <a name="how-can-i-find-out-if-my-pointers-corrupt-a-memory-address"></a>Como posso saber se meus ponteiros corrompem um endereço de memória?
## <a name="problem-description"></a>Descrição do problema
 Eu acho que um de meus ponteiros pode estar danificando a memória no endereço 0x00408000. Como posso descobrir o que está acontecendo lá?

## <a name="solution"></a>Solução

#### <a name="check-for-heap-corruption"></a>Verificação de danos do heap

- A maior parte das corrupções de memória acontece, na verdade, devido à corrupção da heap. Tente usar o utilitário global dos sinalizadores (gflags.exe) ou pageheap.exe. Consulte [/windows-hardware/drivers/depurador/gflags-and-pageheap](/windows-hardware/drivers/debugger/gflags-and-pageheap).

#### <a name="to-find-where-the-memory-address-is-modified"></a>Para localizar onde o endereço de memória foi alterado

1. Defina um ponto de interrupção de dados em 0x00408000. Confira [Definir um ponto de interrupção de alteração de dados (somente C++ nativo)](../debugger/using-breakpoints.md#BKMK_set_a_data_breakpoint_native_cplusplus).

2. Quando você atingir o ponto de interrupção, use a janela **Memória** para exibir o conteúdo da memória que começa em 0x00408000. Para obter mais informações, consulte [Memory Windows](../debugger/memory-windows.md).

## <a name="see-also"></a>Confira também
- [Perguntas frequentes sobre depuração de código nativo](../debugger/debugging-native-code-faqs.md)
- [Depurando código nativo](../debugger/debugging-native-code.md)
