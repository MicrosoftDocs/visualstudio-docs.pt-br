---
title: Exibir o código de desmontagem no depurador | Microsoft Docs
ms.custom: seodec18
ms.date: 10/30/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c35432bdd01b9b79c2afaa266d8078caf04bd62b
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53063830"
---
# <a name="view-disassembly-code-in-the-visual-studio-debugger-c-c-visual-basic-f"></a>Exibir o código de desmontagem no depurador do Visual Studio (C#, C++, Visual Basic, F#)

A janela **Desmontagem** mostra o código assembly correspondente às instruções criadas pelo compilador. Se você estiver depurando código gerenciado, essas instruções de assembly correspondem ao código nativo criado pelo compilador Just-in-Time (JIT), não a Microsoft intermediate language (MSIL criado pelo compilador do Visual Studio).

> [!NOTE]
> Para aproveitar ao máximo os **desmontagem** janela, entender ou aprender os fundamentos da [programação da linguagem de assembly](https://wikipedia.org/wiki/Assembly_language).

Esse recurso só estará disponível se a depuração do nível de endereços estiver habilitada. Ele não está disponível para depuração de SQL ou script.

Além das instruções de assembly, a janela **Desmontagem** pode mostrar as seguintes informações opcionais:

- Endereço de memória onde cada instrução está localizada. Para aplicativos nativos, ele é o endereço de memória real. Para o Visual Basic ou C#, ele é um deslocamento do início da função.

- O código-fonte do qual o código do assembly deriva.

- Código de bytes, ou seja, as representações de byte do computador real ou instruções MSIL.

- Nomes do símbolo para os endereços de memória.

- Números de linha que correspondem ao código-fonte.

Instruções de linguagem assembly consistem *mnemônicos*, que são abreviações para nomes de instrução, e *símbolos* para variáveis, registros e constantes. Cada instrução de linguagem de máquina é representada por um mnemônico da linguagem assembly opcionalmente seguido por um ou mais símbolos.

Código de assembly depende intensamente registros do processador ou, para código gerenciado, registradores common language runtime. Você pode usar o **desmontagem** janela juntamente com o **registra** janela, que permite que você examine o conteúdo do registro.

Para exibir instruções de código de máquina em sua forma bruta de numérica, em vez de linguagem assembly, use o **memória** janela ou selecione **Bytes de código** no menu de atalho no **desmontagem**  janela.

## <a name="use-the-disassembly-window"></a>Use a janela de desmontagem

Para habilitar o **desmontagem** janela, em **ferramentas** > **opções** (ou **ferramentas**  >  **As opções**) > **Debugging**, selecione **Habilitar depuração no nível do endereço**.

Para abrir o **desmontagem** janela durante a depuração, selecione **Windows** > **desmontagem** ou pressione **Alt** + **8**.

> [!NOTE]
> As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

Para ativar ou desativar informações opcionais, clique com botão direito no **desmontagem** janela e defina ou desmarque as opções desejadas no menu de atalho.

Uma seta amarela na margem esquerda marca o ponto de execução atual. Para código nativo, o ponto de execução corresponde ao contador de programa da CPU. Este local mostra a próxima instrução que será executada em seu programa.

## <a name="see-also"></a>Consulte também

* [Paginação para cima ou para baixo na memória](../debugger/how-to-page-up-or-down-in-memory.md)
* [Exibição de dados no depurador](../debugger/viewing-data-in-the-debugger.md)
* [Como: Usar a janela registros](../debugger/how-to-use-the-registers-window.md)