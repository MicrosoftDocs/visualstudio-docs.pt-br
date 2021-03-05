---
title: Depurar funções da API do Windows | Microsoft Docs
description: Saiba como depurar uma função da API do Windows que tenha símbolos do NT carregados. No código de 32 bits, você usa a forma decorada do nome da função para definir o ponto de interrupção.
ms.custom: SEO-VS-2020, seodec18
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
ms.openlocfilehash: d84bdc20ab4601798e1f967c1352468e750fa9bd
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102155207"
---
# <a name="how-can-i-debug-windows-api-functions"></a>Como depurar funções de API do Windows?
Se você desejar depurar uma função de API do Windows que tenha os símbolos do NT carregados, deverá fazer o seguinte.

### <a name="to-set-a-breakpoint-on-a-windows-api-function-with-nt-symbols-loaded"></a>Para definir um ponto de interrupção em uma função de API do Windows com os símbolos do NT carregados

- No [ponto de interrupção da função](../debugger/using-breakpoints.md#BKMK_Set_a_breakpoint_in_a_source_file), insira o nome da função junto com o nome da dll na qual a função reside (consulte o operador de [contexto](../debugger/context-operator-cpp.md)). No código de 32 bits, use a forma decorada do nome da função. Para definir um ponto de interrupção em **MessageBeep**, por exemplo, você precisa inserir o seguinte.

    ```cpp
    {,,USER32.DLL}_MessageBeep@4
    ```

     Para obter o nome decorado, consulte [exibindo nomes decorados](/previous-versions/5x49w699(v=vs.140)).

     Você pode testar o nome decorado e exibi-lo no código de desmontagem. Enquanto estiver em pausa na função no depurador do Visual Studio, clique com o botão direito do mouse na função no editor de código ou na janela pilha de chamadas e escolha **ir para desmontagem**.

- No código de 64 bits, você pode usar o nome não decorado.

    ```cpp
    {,,USER32.DLL}MessageBeep
    ```

## <a name="see-also"></a>Confira também
- [Perguntas frequentes sobre depuração de código nativo](../debugger/debugging-native-code-faqs.md)
- [Depurando código nativo](../debugger/debugging-native-code.md)
