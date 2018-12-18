---
title: Para visualizar a memória para variáveis no depurador | Microsoft Docs
ms.custom: H1Hack27Feb2017
ms.date: 10/04/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.memory
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- Memory window
- strings [Visual Studio], viewing
- debugger [Visual Studio], Memory window
- memory [Visual Studio], debugging
- debugging [Visual Studio], Memory window
- buffers, viewing
ms.assetid: 7f7a0439-10e4-4966-bb2d-51f04cda4fe2
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: cdf8e5fc5ee0ac34b4c295f6cc593e0a93b548ae
ms.sourcegitcommit: a7de99f36e9ead7ea9e9bac23c88d05ddfc38b00
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52257251"
---
# <a name="use-the-memory-windows-in-the-visual-studio-debugger-c-c-visual-basic-f"></a>Usar as janelas de memória no depurador do Visual Studio (C#, C++, Visual Basic, F#)

Durante a depuração, o **memória** janela mostra o espaço de memória que seu aplicativo está usando. 

Depurador do windows como o **Watch**, **Autos**, **locais**e o **QuickWatch** caixa de diálogo Mostrar variáveis, que são armazenadas em específico locais na memória. O **memória** janela mostra o quadro geral. O modo de exibição de memória é conveniente para examinar grandes partes de dados (buffers ou grandes cadeias de caracteres, por exemplo) que não são exibidos bem nas outras janelas. 

O **memória** janela não está limitada a exibir dados. Ela exibirá tudo no espaço de memória, incluindo dados, o código e o bits aleatórios de lixo na memória não atribuída.  

O **memória** janela não está disponível para depuração de SQL ou script. Essas linguagens não reconhecem o conceito de memória.  
  
## <a name="open-a-memory-window"></a>Abra uma janela de memória  
  
Como outras janelas do depurador, o **memória** windows estão disponíveis somente durante uma sessão de depuração. 

>[!IMPORTANT]
>Para habilitar o **memória** windows, **habilitar a depuração do nível de endereços** deve ser selecionado nos **ferramentas** > **opções** (ou **Debug** > **opções**) > **depuração** > **geral**. 

**Para abrir uma janela de memória**
  
1. Certifique-se **habilitar a depuração do nível de endereços** está selecionado no **ferramentas** > **opções** (ou **depurar**  >  **Opções**) > **depuração** > **geral**. 
   
1. Iniciar a depuração, selecionando a seta verde, pressionar **F5**, ou selecionando **Debug** > **iniciar depuração**.  
   
2. Sob **Debug** > **Windows** > **memória**, selecione **memória 1**, **dememória2**, **Memória 3**, ou **memória 4**. (Algumas edições do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] oferecer apenas um **memória** janela.)  

## <a name="move-around-in-the-memory-window"></a>Mover-se na janela de memória  

O espaço de endereço de um computador é grande, e você pode facilmente se perca rolando o **memória** janela. 

Um endereço de memória mais alto aparece na parte inferior da janela. Para exibir um endereço mais alto, role para baixo. Para exibir um endereço inferior, role para cima.  

Instantaneamente, você pode ir para um endereço especificado na **memória** janela usando arrastar e soltar, ou inserindo o endereço na **endereço** campo. O **endereço** campo aceita endereços alfanuméricos e expressões que são avaliadas como endereços, tais como `e.User.NonroamableId`. 

Para forçar a reavaliação imediata de uma expressão na **endereço** , selecione a seta arredondado **reavaliar automaticamente** ícone. 

Por padrão, o **memória** janela trata **endereço** expressões como expressões dinâmicas, que são reavaliadas como executar o aplicativo. Expressões em tempo real podem ser útil, por exemplo, para exibir a memória que é tocada por uma variável de ponteiro.  

**Para arrastar e soltar para mover para um local de memória:**  
   
1. Em qualquer janela de depurador, selecione um endereço de memória ou uma variável de ponteiro que contém um endereço de memória.  
   
2. Arraste e solte o endereço ou ponteiro na **memória** janela. Esse endereço, em seguida, aparece na **endereço** campo e o **memória** janela é ajustada para exibir esse endereço na parte superior. 
  
**Para mover para um local de memória inserindo-o no campo de endereço:**
  
- Digite ou cole o endereço ou a expressão na **endereço** campo e pressione **Enter**, ou escolha-o na lista suspensa o **endereço** campo. O **memória** janela é ajustada para exibir esse endereço na parte superior.
  
## <a name="customize-the-memory-window"></a>Personalizar a janela de memória 

Por padrão, o conteúdo de memória são exibidos como inteiros de 1 byte em formato hexadecimal e a largura da janela determina o número de colunas mostradas. Você pode personalizar a maneira como o **memória** janela mostra o conteúdo da memória.  
  
**Para alterar o formato do conteúdo da memória:**  
  
-  Clique com botão direito no **memória** janela e escolha os formatos que você deseja no menu de contexto.  
  
**Para alterar o número de colunas na janela de memória:**
  
- Selecione a seta suspensa ao lado de **colunas** campo e, em seguida, selecione o número de colunas para exibir ou selecionar **automático** para ajuste automático com base na largura da janela.  
  
Se você não quiser que o conteúdo do **memória** janela alterar seu aplicativo é executado, você pode desativar a avaliação da expressão dinâmica. 

**Para ativar/desativar a avaliação dinâmica:**  
  
- Clique com botão direito no **memória** janela e selecione **reavaliar automaticamente** no menu de contexto. 

  >[!NOTE]
  >Ao vivo de expressão de avaliação é um controle de alternância e é ativado por padrão, portanto, selecionando **reavaliar automaticamente** é desativado. Selecionando **reavaliar automaticamente** novamente a ativa novamente. 
  
Você pode ocultar ou exibir a barra de ferramentas na parte superior do **memória** janela. Você não terá acesso para o **endereço** campo ou outras ferramentas, quando a barra de ferramentas está oculto.  
  
**Para alternar a exibição da barra de ferramentas:**  
  
- Clique com botão direito no **memória** janela e selecione **Mostrar barra de ferramentas** no menu de contexto. A barra de ferramentas é exibida ou desaparece, dependendo do seu estado anterior.  
  
## <a name="follow-a-pointer-through-memory"></a>Siga um ponteiro pela memória  

Em aplicativos de código nativo, você pode usar nomes de registro como expressões dinâmicas. Por exemplo, você pode usar o ponteiro de pilhas para seguir a pilha.  
  
**Para seguir um ponteiro pela memória:**
  
1. No **memória** janela **endereço** , insira uma expressão de ponteiro que está no escopo atual. Dependendo da linguagem, você poderá ter que remover a referência a ele.  
  
2. Pressione **ENTER**.  
   
   Quando você usa um comando de depuração, como **etapa**, o endereço de memória exibido na **endereço** campo e, na parte superior dos **memória** janela altera automaticamente quando o ponteiro alterações.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir dados no depurador](../debugger/viewing-data-in-the-debugger.md)