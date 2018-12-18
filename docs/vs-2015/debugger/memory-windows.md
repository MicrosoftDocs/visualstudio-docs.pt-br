---
title: Memória Windows | Microsoft Docs
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
- vs.debug.memory
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
- Memory window
- strings [Visual Studio], viewing
- debugger [Visual Studio], Memory window
- memory [Visual Studio], debugging
- debugging [Visual Studio], Memory window
- buffers, viewing
ms.assetid: 7f7a0439-10e4-4966-bb2d-51f04cda4fe2
caps.latest.revision: 37
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 704c0ff20dbd11b4640b2d81670a4cdeaf3f1ea0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51724247"
---
# <a name="memory-windows"></a>Janelas de memória
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O **memória** janela fornece uma exibição no espaço de memória que é usado pelo seu aplicativo. O **Watch** janela, **QuickWatch** caixa de diálogo **Autos** janela, e **Locals** janela Mostrar o conteúdo de variáveis, que são armazenados em locais específicos na memória. Mas o **memória** janela mostra a imagem em grande escala. Esta exibição pode ser conveniente para examinar grandes partes de dados (buffers ou grandes cadeias de caracteres, por exemplo) que não são exibidas corretamente nas outras janelas. No entanto, o **memória** janela não é limitada a exibir dados. Ela exibirá tudo no espaço de memória, não importa se o conteúdo for dados, código ou bits aleatórios de lixo na memória não atribuída.  
  
 O **memória** janela está disponível somente se a depuração do nível de endereços estiver habilitada na **opções** caixa de diálogo**depuração** nó. O **memória** janela não está disponível para o Script ou SQL, que são linguagens que não reconhecem o conceito de memória.  
  
## <a name="opening-a-memory-window"></a>Abrindo uma janela de memória  
  
#### <a name="to-open-a-memory-window"></a>Para abrir uma janela de memória  
  
1.  Inicie a depuração, se você já não estiver no modo de depuração.  
  
2.  No **Debug** , aponte para **Windows**. Em seguida, aponte para **memória** e, em seguida, clique em **Memory 1**, **memória 2**, **memória 3**, ou **memória 4**. (Edições de nível inferior [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] têm apenas uma única **memória** janela. Se você estiver usando uma dessas edições, basta clicar **memória**.)  
  
## <a name="paging-in-the-memory-window"></a>Paginação na janela de memória  
 O **memória** janela tem uma barra de rolagem vertical que opera de maneira não padrão. O espaço de endereço de um computador moderno é muito grande e você pode preferir arrastar a caixa de rolagem para um local aleatório. Por esse motivo, a caixa de rolagem é carregada e sempre permanece no centro da barra de rolagem. Em aplicativos de código nativo, você pode rolar a página para cima ou para baixo, mas não pode rolar livremente.  
  
 Um endereço de memória mais alto aparece na parte inferior da janela. Para exibir um endereço mais alto, role para baixo, não para cima.  
  
#### <a name="to-page-up-or-down-in-memory"></a>Para mover para cima ou para baixo na memória  
  
1.  Para rolar a página para baixo (mover para um endereço de memória mais alto), clique abaixo da caixa de rolagem na barra de rolagem vertical.  
  
2.  Para rolar a página para cima (mover para um endereço de memória mais baixo), clique acima da caixa de rolagem na barra de rolagem vertical.  
  
## <a name="selecting-a-memory-location"></a>Selecionando um local de memória  
 Se você quiser mover imediatamente para um local selecionado na memória, você poderá fazer isso usando uma operação de arrastar e soltar ou editando o valor de **endereço** caixa. O **endereço** caixa aceita não somente valores numéricos, mas também expressões que são avaliadas como endereços. Por padrão, o **memória** janela trata um **endereço** expressão como uma expressão em tempo real, que é reavaliada à medida que seu programa é executado. As expressões dinâmicas podem ser muito úteis. Por exemplo, você pode usá-las para exibir a memória que é tocada por um ponteiro.  
  
#### <a name="to-select-a-memory-location-by-dragging-and-dropping"></a>Para selecionar um local de memória arrastando e soltando  
  
1.  Em qualquer janela, selecione um endereço de memória ou variável de ponteiro que contém um endereço de memória.  
  
2.  Arraste o endereço ou ponteiro para o **memória** janela.  
  
#### <a name="to-select-a-memory-location-by-editing"></a>Para selecionar um local de memória editando  
  
1.  No **memória** janela, selecione a **endereço** caixa.  
  
2.  Digite ou cole o endereço que você deseja ver e, em seguida, pressione **ENTER**.  
  
## <a name="changing-the-way-the-memory-window-displays-information"></a>Alterando o modo como a janela de memória exibe informações  
 Você pode personalizar a maneira como o **memória** janela mostra o conteúdo da memória. Por padrão, o conteúdo da memória aparece como inteiros de um byte em formato hexadecimal e o número de colunas é determinado automaticamente pela largura atual da janela.  
  
#### <a name="to-change-the-format-of-the-memory-contents"></a>Para alterar o formato do conteúdo de memória  
  
1.  Clique com botão direito do **memória** janela.  
  
2.  Escolha o formato que você deseja.  
  
#### <a name="to-change-the-number-of-columns-in-the-memory-window"></a>Para alterar o número de colunas na janela de memória  
  
1. Na barra de ferramentas na parte superior a **memória** janela, localize a **colunas** lista.  
  
2. No **colunas** , selecione o número de colunas que você deseja exibir ou selecione **automático** para ajuste automático para se ajustar à largura da janela.  
  
   Se você não quiser que o conteúdo do **memória** janela alterar como o seu programa é executado, você pode desativar a avaliação da expressão dinâmica.  
  
#### <a name="to-toggle-live-evaluation"></a>Para ativar/desativar a avaliação dinâmica  
  
1. Clique com botão direito do **memória** janela.  
  
2. No menu de atalho, clique em **reavaliar automaticamente**.  
  
    Se a avaliação dinâmica estiver ativa, a opção será selecionada e clicar nela a desativará. Se a avaliação dinâmica estiver inativa, a opção não será selecionada e clicar nela a ativará.  
  
   Você pode ocultar ou exibir a barra de ferramentas na parte superior do **memória** janela. Você não terá acesso à caixa de endereço ou outras ferramentas enquanto a barra de ferramentas estiver oculta.  
  
#### <a name="to-toggle-the-toolbar"></a>Para ativar/desativar a barra de ferramentas  
  
1.  Clique com botão direito um **memória** janela.  
  
2.  No menu de atalho, clique em **Mostrar barra de ferramentas**.  
  
     A barra de ferramentas é exibida ou desaparece, dependendo do seu estado anterior.  
  
## <a name="following-a-pointer-through-memory"></a>Seguindo um ponteiro pela memória  
 Em aplicativos de código nativo, você poderá usar nomes de registro como expressões dinâmicas. Por exemplo, você pode usar o ponteiro de pilhas para seguir a pilha.  
  
#### <a name="to-follow-a-pointer-through-memory"></a>Para seguir um ponteiro pela memória  
  
1.  No **memória** janela **endereço** , digite uma expressão de ponteiro. A variável de ponteiro deve estar no escopo atual. Dependendo da linguagem, você poderá ter que remover a referência a ele.  
  
2.  Pressione **ENTER**.  
  
     Agora, quando você usa um comando de execução como **etapa**, o endereço de memória que é exibido automaticamente será alterado quando o ponteiro muda.  
  
## <a name="see-also"></a>Consulte também  
 [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)





