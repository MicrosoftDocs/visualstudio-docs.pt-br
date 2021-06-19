---
title: Depurar funções de API do Windows | Microsoft Docs
description: Saiba como depurar uma função de API do Windows que tem símbolos NT carregados. No código de 32 bits, você usa a forma decorada do nome da função para definir o ponto de interrupção.
ms.custom: SEO-VS-2020
ms.date: 06/03/2020
ms.topic: how-to
f1_keywords:
- vs.debug.api
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], Windows API functions
- NT symbols and debugging Windows API functions
- Windows API functions, debugging
- Windows API, debugging API functions
- APIs, debugging
ms.assetid: 7c126f57-62ab-4d94-9805-632d696ba1f0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 89fdbcf9d18a7794e1fb2520384db0f9bcec3147
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386937"
---
# <a name="how-can-i-debug-windows-api-functions"></a>Como depurar funções de API do Windows?
Se você desejar depurar uma função de API do Windows que tenha os símbolos do NT carregados, deverá fazer o seguinte.

### <a name="to-set-a-breakpoint-on-a-windows-api-function-with-nt-symbols-loaded"></a>Para definir um ponto de interrupção em uma função de API do Windows com os símbolos do NT carregados

- No ponto [de interrupção da](../debugger/using-breakpoints.md#BKMK_Set_a_breakpoint_in_a_source_file)função , insira o nome da função junto com o nome da DLL em que a função reside (consulte o [operador de contexto](../debugger/context-operator-cpp.md)). No código de 32 bits, use a forma decorada do nome da função. Para definir um ponto de interrupção em **MessageBeep**, por exemplo, você precisa inserir o seguinte.

    ```cpp
    {,,USER32.DLL}_MessageBeep@4
    ```

     Para obter o nome decorado, consulte [Exibindo nomes decorados.](/previous-versions/5x49w699(v=vs.140))

     Você pode testar o nome decorado e exibi-lo no código de desmontagem. Enquanto estiver em pausa na função no Visual Studio depurador, clique com o botão direito do mouse na função no editor de códigos ou na janela da pilha de chamada e escolha Ir para **Desmontagem.**

- No código de 64 bits, você pode usar o nome não rateado.

    ```cpp
    {,,USER32.DLL}MessageBeep
    ```

## <a name="see-also"></a>Confira também
- [Perguntas frequentes sobre depuração de código nativo](../debugger/debugging-native-code-faqs.md)
- [Depurando código nativo](../debugger/debugging-native-code.md)
