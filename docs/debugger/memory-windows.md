---
title: Exibir memória para variáveis no depurador | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2018
ms.topic: how-to
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 51070e06f684c2e873ded76ec8797ed7587745ff
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348314"
---
# <a name="use-the-memory-windows-in-the-visual-studio-debugger-c-c-visual-basic-f"></a>Usar as janelas de memória no depurador do Visual Studio (C#, C++, Visual Basic, F #)

Durante a depuração, a janela **memória** mostra o espaço de memória que seu aplicativo está usando.

Janelas do depurador como **Watch**, **autoies**, **locais**e a caixa de diálogo **QuickWatch** mostram as variáveis que são armazenadas em locais específicos na memória. A janela **memória** mostra a imagem geral. O modo de exibição de memória é conveniente para examinar grandes partes de dados (buffers ou cadeias de caracteres grandes, por exemplo) que não são exibidos bem nas outras janelas.

A janela de **memória** não está limitada à exibição de dados. Ele exibe tudo no espaço de memória, incluindo dados, código e bits aleatórios de lixo na memória não atribuída.

A janela **memória** não está disponível para depuração de script ou SQL. Esses idiomas não reconhecem o conceito de memória.

## <a name="open-a-memory-window"></a>Abrir uma janela de memória

Assim como outras janelas do depurador, as janelas de **memória** estão disponíveis somente durante uma sessão de depuração.

>[!IMPORTANT]
>Para habilitar as janelas de **memória** , **habilite a depuração de nível de endereço** deve ser selecionada em **ferramentas**  >  **Opções** (ou opções de **depuração**  >  **Options**) > **depuração**  >  **geral**.

**Para abrir uma janela de memória**

1. Verifique se **Habilitar depuração no nível de endereço** está selecionado em **ferramentas**  >  **Opções** (ou opções de **depuração**  >  **Options**) > **depuração**  >  **geral**.

1. Inicie a depuração selecionando a seta verde, pressionando **F5**ou selecionando **depurar**  >  **Iniciar Depuração**.

2. Em **depurar**  >  **Windows**  >  **memória**do Windows, selecione **memória 1**, **memória 2**, **memória 3**ou **memória 4**. (Algumas edições da [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] oferecem apenas uma janela de **memória** .)

## <a name="move-around-in-the-memory-window"></a>Mover-se na janela de memória

O espaço de endereço de um computador é grande e você pode facilmente perder seu lugar rolando na janela de **memória** .

Um endereço de memória mais alto aparece na parte inferior da janela. Para exibir um endereço mais alto, role para baixo. Para exibir um endereço inferior, role para cima.

Você pode ir instantaneamente para um endereço especificado na janela **memória** usando o recurso de arrastar e soltar ou inserindo o endereço no campo **endereço** . O campo **endereço** aceita endereços alfanuméricos e expressões que são avaliadas como endereços, como `e.User.NonroamableId` .

Para forçar a reavaliação imediata de uma expressão no campo **endereço** , selecione o ícone da seta arredondada **reavaliar automaticamente** .

Por padrão, a janela **memória** trata as expressões de **endereço** como expressões dinâmicas, que são avaliadas novamente à medida que o aplicativo é executado. As expressões dinâmicas podem ser úteis, por exemplo, para exibir a memória que é percoberta por uma variável de ponteiro.

**Para usar o recurso de arrastar e soltar para mover para um local de memória:**

1. Em qualquer janela do depurador, selecione um endereço de memória ou uma variável de ponteiro que contenha um endereço de memória.

2. Arraste e solte o endereço ou o ponteiro na janela **memória** . Esse endereço aparece no campo **endereço** e a janela **memória** é ajustada para exibir esse endereço na parte superior.

**Para mover para um local da memória inserindo-o no campo Endereço:**

- Digite ou cole o endereço ou a expressão no campo **endereço** e pressione **Enter**, ou escolha-o no menu suspenso no campo **endereço** . A janela **memória** é ajustada para exibir esse endereço na parte superior.

## <a name="customize-the-memory-window"></a>Personalizar a janela de memória

Por padrão, o conteúdo da memória aparece como inteiros de 1 byte no formato hexadecimal e a largura da janela determina o número de colunas mostradas. Você pode personalizar a maneira como a janela **Memória** mostra o conteúdo da memória.

**Para alterar o formato do conteúdo da memória:**

- Clique com o botão direito do mouse na janela **memória** e escolha os formatos desejados no menu de contexto.

**Para alterar o número de colunas na janela de memória:**

- Selecione a seta suspensa ao lado do campo **colunas** e selecione o número de colunas a serem exibidas ou selecione **automático** para ajuste automático com base na largura da janela.

Se você não quiser que o conteúdo da janela de **memória** mude à medida que seu aplicativo for executado, você poderá desativar a avaliação de expressão dinâmica.

**Para alternar a avaliação dinâmica:**

- Clique com o botão direito do mouse na janela **memória** e selecione **reavaliar automaticamente** no menu de contexto.

  >[!NOTE]
  >A avaliação de expressões dinâmicas é uma alternância e está ativada por padrão, portanto, selecionar **Reevaluate automaticamente** o desativa. A seleção **reavaliar automaticamente** o ativa novamente.

Você pode ocultar ou exibir a barra de ferramentas na parte superior da janela **Memória**. Você não terá acesso ao campo de **endereço** ou outras ferramentas quando a barra de ferramentas estiver oculta.

**Para alternar a exibição da barra de ferramentas:**

- Clique com o botão direito do mouse na janela **memória** e selecione **Mostrar barra de ferramentas** no menu de contexto. A barra de ferramentas é exibida ou desaparece, dependendo do seu estado anterior.

## <a name="follow-a-pointer-through-memory"></a>Seguir um ponteiro pela memória

Em aplicativos de código nativo, você pode usar nomes de registro como expressões dinâmicas. Por exemplo, você pode usar o ponteiro de pilhas para seguir a pilha.

**Para seguir um ponteiro por meio da memória:**

1. No campo **endereço** da janela de **memória** , insira uma expressão de ponteiro que esteja no escopo atual. Dependendo da linguagem, você poderá ter que remover a referência a ele.

2. Pressione **Enter**.

   Quando você usa um comando de depuração como **etapa**, o endereço de memória exibido no campo **endereço** e na parte superior da janela de **memória** é alterado automaticamente conforme o ponteiro é alterado.

## <a name="see-also"></a>Veja também
- [Exibir dados no depurador](../debugger/viewing-data-in-the-debugger.md)