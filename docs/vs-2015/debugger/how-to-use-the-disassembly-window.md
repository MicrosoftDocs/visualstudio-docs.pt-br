---
title: 'Como: usar a janela de desmontagem | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.disassembly
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- assembly language, debugging inline assembly code
- breakpoints, Disassembly window
- Disassembly window
- machine code
ms.assetid: eaf84dd0-c82d-481b-af51-690b74e7794c
caps.latest.revision: 34
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 67f9307f2f5fece64ee2ee11dd48863b9a951180
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51760912"
---
# <a name="how-to-use-the-disassembly-window"></a>Como usar a Janela de Desmontagem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Esse recurso está disponível somente se a depuração do nível de endereços estiver habilitada a **opções** caixa de diálogo **depuração** nó. Não está disponível para depuração de Script ou SQL.  
  
 O **desmontagem** janela mostra o código assembly correspondente às instruções criadas pelo compilador. Se você estiver depurando código gerenciado, essas instruções de assembly correspondem ao código nativo criado pelo compilador JIT (Just-in-Time), não a linguagem intermediária da Microsoft (MSIL) gerada pelo compilador do Visual Studio.  
  
 Além de instruções de assembly, o **desmontagem** janela pode mostrar as seguintes informações opcionais:  
  
- Endereço de memória onde cada instrução está localizada. Para aplicativos nativos, este é o endereço de memória real. Para o Visual Basic, C# ou código gerenciado, é um deslocamento do início da função.  
  
- O código-fonte do qual o código do assembly deriva.  
  
- As representações byte a byte de código do computador real ou instruções de MSIL.  
  
- Nomes do símbolo para os endereços de memória.  
  
- Números de linha que correspondem ao código-fonte.  
  
  As instruções da linguagem de assembly consistem em mnemônica, que são abreviações para nomes de instrução e símbolos que representam variáveis, registros e constantes. Cada instrução de linguagem de máquina é representada por um mnemônico de assembly da linguagem, geralmente seguido por uma ou mais variáveis, registros ou constantes.  
  
  Se você não puder ler a linguagem assembly e quiser aproveitar a janela Desmontagem, consulte um bom livro sobre programação da linguagem de assembly. A programação da linguagem de assembly está além do escopo do que podemos abordar nesta breve introdução à janela Desmontagem.  
  
  Como o código do assembly depende intensamente dos registros do processador ou, no caso do código gerenciado, os registros do Common Language Runtime, você normalmente achará útil usar a janela Desmontagem junto com a janela Registros, o que permite examinar o conteúdo do registro.  
  
  Você provavelmente jamais desejará ou precisará exibir instruções de código de máquina em seu formato bruto e numérico, em vez da linguagem de assembly. No entanto, se quiser fazer isso, poderá usar a janela Memória para essa finalidade ou escolher Bytes de Código no menu de atalho na janela Desmontagem.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### <a name="to-display-the-disassembly-window"></a>Para exibir a janela Desmontagem  
  
-   Sobre o **Debug** menu, escolha **Windows**e clique em **desmontagem**.  
  
     O depurador deve estar em execução ou no modo de interrupção.  
  
### <a name="to-turn-optional-information-on-or-off"></a>Para ativar ou desativar as informações opcionais  
  
-   Clique com botão direito do **desmontagem** janela e defina ou desmarque as opções desejadas no menu de atalho.  
  
     Uma seta amarela na margem esquerda marca o local do ponto de execução atual. Para o código nativo, isso corresponde ao contador do programa da CPU. Este local mostra a próxima instrução que será executada em seu programa.  
  
     Para obter mais informações, consulte [paginação para cima ou para baixo na memória](../debugger/how-to-page-up-or-down-in-memory.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)   
 [Como usar a janela Registros](../debugger/how-to-use-the-registers-window.md)





