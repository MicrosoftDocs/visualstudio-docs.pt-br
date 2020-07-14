---
title: Exibir o código de desmontagem no depurador | Microsoft Docs
ms.custom: seodec18
ms.date: 10/30/2018
ms.topic: how-to
f1_keywords:
- vs.debug.disassembly
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- assembly language, debugging inline assembly code
- breakpoints, Disassembly window
- Disassembly window
- machine code
ms.assetid: eaf84dd0-c82d-481b-af51-690b74e7794c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0570aec5e8571e75cf64418a2c8c7c95cf507d31
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348698"
---
# <a name="view-disassembly-code-in-the-visual-studio-debugger-c-c-visual-basic-f"></a>Exibir o código de desmontagem no depurador do Visual Studio (C#, C++, Visual Basic, F #)

A janela **Desmontagem** mostra o código assembly correspondente às instruções criadas pelo compilador. Se você estiver depurando código gerenciado, essas instruções de assembly corresponderão ao código nativo criado pelo compilador JIT (just-in-time), não pela MSIL (Microsoft Intermediate Language) criado pelo compilador do Visual Studio.

> [!NOTE]
> Para aproveitar ao máximo a janela de **desmontagem** , entenda ou Aprenda os conceitos básicos da [programação de linguagem de assembly](https://wikipedia.org/wiki/Assembly_language).

Esse recurso só estará disponível se a depuração no nível de endereço estiver habilitada. Ele não está disponível para depuração de script ou SQL.

Além das instruções de assembly, a janela **Desmontagem** pode mostrar as seguintes informações opcionais:

- Endereço de memória onde cada instrução está localizada. Para aplicativos nativos, é o endereço de memória real. Para Visual Basic ou C#, é um deslocamento do início da função.

- O código-fonte do qual o código do assembly deriva.

- Bytes de código, ou seja, as representações de byte do computador ou das instruções MSIL reais.

- Nomes do símbolo para os endereços de memória.

- Números de linha que correspondem ao código-fonte.

As instruções de linguagem de assembly consistem em *mnemônicos*, que são abreviações de nomes de instrução e *símbolos* para variáveis, registros e constantes. Cada instrução de linguagem de computador é representada por um mnemônico de linguagem de assembly, opcionalmente seguido por um ou mais símbolos.

O código do assembly depende muito dos registros do processador ou, para o código gerenciado, Common Language Runtime registra. Você pode usar a janela de **desmontagem** junto com a janela de **registros** , que permite examinar o conteúdo do registro.

Para exibir as instruções de código do computador em sua forma numérica bruta, em vez de na linguagem do assembly, use a janela **memória** ou selecione **bytes de código** no menu de atalho na janela **desmontagem** .

## <a name="use-the-disassembly-window"></a>Usar a janela Desmontagem

Para habilitar a janela de **desmontagem** , em **ferramentas**  >  **Opções** (ou **ferramentas**  >  **Opções**) > **depuração**, selecione **Habilitar depuração no nível de endereço**.

Para abrir a janela de **desmontagem** durante a depuração **Windows**, selecione  >  **desmontagem** do Windows ou pressione **ALT** + **8**.

> [!NOTE]
> As caixas de diálogo e os comandos de menu encontrados podem diferir daqueles descritos na Ajuda, dependendo das configurações ativas ou edição. Para alterar suas configurações, selecione **Importar e Exportar Configurações** no menu **Ferramentas** . Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

Para ativar ou desativar as informações opcionais, clique com o botão direito do mouse na janela **desmontagem** e defina ou desmarque as opções desejadas no menu de atalho.

Uma seta amarela na margem esquerda marca o ponto de execução atual. Para código nativo, o ponto de execução corresponde ao contador de programa da CPU. Este local mostra a próxima instrução que será executada em seu programa.

## <a name="see-also"></a>Veja também

* [Paginação para cima ou para baixo na memória](../debugger/how-to-page-up-or-down-in-memory.md)
* [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)
* [Como: usar a janela de registros](../debugger/how-to-use-the-registers-window.md)