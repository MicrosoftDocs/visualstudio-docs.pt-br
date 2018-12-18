---
title: 'Passo a passo: Depurando um aplicativo multithread | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- multithreaded debugging, walkthrough
- walkthroughs, multithreaded debugging
ms.assetid: 590ffd57-0556-43d8-8962-ee27e5b2b7d7
caps.latest.revision: 42
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d5dd742411710698cb2dd626e211cb0e73b8379e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51798619"
---
# <a name="walkthrough-debugging-a-multithreaded-application"></a>Instruções passo a passo: depurando um aplicativo multithread
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] Fornece um melhor **Threads** janela e outro usuário aperfeiçoamentos de interface para tornar mais fácil de depurar aplicativos multi-threaded. Este passo a passo só levará alguns minutos e o ajudará a se familiarizar com os recursos da nova interface para depurar aplicativos de vários threads.  
  
 Para iniciar este passo a passo, você precisará de um projeto de aplicativo de vários threads. Siga as etapas listadas aqui para criar o projeto.  
  
#### <a name="to-create-the-walkthrough-project"></a>Para criar o projeto passo a passo  
  
1.  Sobre o **arquivo** menu, escolha **New** e, em seguida, clique em **projeto**.  
  
     A caixa de diálogo **Novo Projeto** é exibida.  
  
2.  No **tipo de projeto**s caixa, clique na linguagem de sua escolha: **Visual Basic**, **Visual c#**, ou **Visual C++**.  
  
3.  No **modelos** , escolha **aplicativo de Console** ou **aplicativo de Console CLR**.  
  
4.  No **nome** caixa, digite o nome MyThreadWalkthroughApp.  
  
5.  Clique em **OK**.  
  
     Um novo projeto de console é exibido. Quando o projeto tiver sido criado, um arquivo de origem aparecerá. Dependendo da linguagem escolhida, o arquivo de origem poderá ser chamado Module1.vb, Program.cs ou MyThreadWalkthroughApp.cpp  
  
6.  Exclua o código que aparece no arquivo de origem e substitua-o com o código de exemplo que aparece na seção "Criando um Thread" do tópico [criando Threads e passando dados na hora de início](http://msdn.microsoft.com/library/52b32222-e185-4f42-91a7-eaca65c0ab6d).  
  
7.  Sobre o **arquivo** menu, clique em **Salvar tudo**.  
  
#### <a name="to-begin-the-walkthrough"></a>Para iniciar o passo a passo  
  
-   Na janela de origem, procure o seguinte código:  
  
    ```vb  
    Thread.Sleep(3000)   
    Console.WriteLine(  
    ```  
  
```csharp  
Thread.Sleep(3000);  
Console.WriteLine();  
```  
  
```cpp  
Thread::Sleep(3000);  
Console.WriteLine();  
```  
  
#### <a name="to-start-debugging"></a>Para iniciar a depuração  
  
1.  Clique com botão direito do `Console.WriteLine` instrução, aponte para **ponto de interrupção** e, em seguida, clique em **Inserir ponto de interrupção**.  
  
     Na medianiz no lado esquerdo da janela de origem, uma bola vermelha aparece. Isso indica que um ponto de interrupção agora está definido nesse local.  
  
2.  No menu **Depuração**, clique em **Iniciar Depuração**.  
  
     A depuração é iniciada, seu aplicativo de console começa a ser executado e, em seguida, para no ponto de interrupção.  
  
3.  Se a janela do aplicativo de console tiver o foco neste momento, clique na janela do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para retornar o foco para o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
4.  Na janela de origem, localize a linha que contém o seguinte código:  
  
    ```vb  
    Thread.Sleep(5000)   
    ```  
  
```csharp  
Thread.Sleep(3000);  
```  
  
```cpp  
Thread::Sleep(3000);  
```  
  
1.  
  
#### <a name="to-discover-the-thread-marker"></a>Para descobrir o marcador de thread  
  
1. Com o botão direito no **Threads** janela, em seguida, clique em **Mostrar Threads em origem**.  
  
2. Examine a medianiz no lado esquerdo da janela. Nessa linha, você verá um ícone semelhante a dois threads de pano. Um thread é vermelho e o outro é azul. O marcador de thread indica que um thread está parado nesse local. Possivelmente, o thread está parado nesse local.  
  
3. Passe o ponteiro sobre o marcador de thread. Um DataTip que aparece. O DataTip mostra o nome e o número de ID do thread para cada thread parado. Nesse caso, há apenas um thread, cujo nome é provavelmente `<noname>`.  
  
4. Clique com o botão direito no marcador de thread. Observe as opções no menu de atalho.  
  
   Esse ícone é um *marcador de thread*:  
  
   ![Marcador de thread](../debugger/media/threadmarker.gif "ThreadMarker")  
  
## <a name="flagging-and-unflagging-threads"></a>Sinalizando e removendo a sinalização de threads  
 No [!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)], você pode sinalizar os threads para os quais deseja dar atenção especial. Sinalizar threads é uma boa maneira de manter o controle de threads importantes e ignorar threads com os quais você não precisa se preocupar.  
  
#### <a name="to-flag-threads"></a>Para sinalizar threads  
  
1.  Na **modo de exibição** , aponte para **barras de ferramentas**.  
  
     Certifique-se de que o **local de depuração** barra de ferramentas está selecionada.  
  
2.  Vá para o **local de depuração** barra de ferramentas e clique no **Thread** lista.  
  
    > [!NOTE]
    >  Você pode reconhecer essa barra de ferramentas por três listas importantes: **processo**, **Thread**, e **quadro de pilha**.  
  
3.  Observe quantos threads aparecem na lista.  
  
4.  Volte para a janela de origem e o botão direito do mouse a **Thread** marcador novamente.  
  
5.  No menu de atalho, aponte para **sinalizador**e, em seguida, clique no nome do thread e o número de ID.  
  
6.  Volte para **local de depuração** barra de ferramentas e clique no **Thread** lista novamente.  
  
     Somente o thread sinalizado agora aparece na lista. O que está à direita do botão de sinalizador a **Thread** lista. O ícone de sinalizador no botão estava esmaecido antes. Agora, é um vermelho contínuo e brilhante.  
  
7.  Passe o ponteiro sobre o ícone do sinalizador.  
  
     Um pop-up será exibido. Este Popup informa em qual modo o **Thread** lista está na: **Mostrar somente Threads sinalizados**.  
  
8.  Clique no botão para voltar ao sinalizador **Mostrar todos os Threads** modo.  
  
9. Clique o **Thread** listar novamente e verifique se que agora você pode ver todos os threads novamente.  
  
10. Clique no botão para voltar ao sinalizador **Mostrar somente Threads sinalizados**.  
  
11. Sobre o **Debug** , aponte para **Windows** e, em seguida, clique em **Threads**.  
  
     O **Threads** janela é exibida. Um thread tem um ícone de sinalizador destacado anexado.  
  
12. Na janela de origem, clique com o botão direito no marcador de thread novamente.  
  
     Observe quais opções estão disponíveis no menu de atalho. Em vez de **sinalizador**, você agora verá **Remover sinalização**. Não clique **Remover sinalização**.  
  
13. Vá para o próximo procedimento sobre como remover a sinalização do thread.  
  
#### <a name="to-unflag-threads"></a>Para remover a sinalização de threads  
  
1.  Sobre o **Threads** janela, clique na linha correspondente ao thread sinalizado.  
  
     Um menu de atalho é exibido. Ele tem opções para **Remover sinalização** e **Remover sinalização de todos os**.  
  
2.  Para remover a sinalização do thread, clique em **Remover sinalização**.  
  
3.  Clique no ícone de sinalizador vermelho.  
  
4.  Examine os **local de depuração** barra de ferramentas novamente. O sinalizador do botão ficará esmaecido novamente. Você removerá a sinalização do único thread sinalizado. Como não há nenhum thread sinalizado, a barra de ferramentas voltou para **Mostrar todos os Threads** modo. Clique o **Thread** listar e verificar que você pode ver todos os threads.  
  
5.  Volte para o **Threads** janela e examinar as colunas de informações.  
  
     Na parte superior de cada coluna, a maioria dos botões têm títulos que identificam a coluna. No entanto, a primeira coluna à esquerda não tem título. Em vez disso, tem um ícone, que é o contorno de um sinalizador. Você observará o mesmo contorno em cada linha da lista de thread. O contorno significa que a sinalização foi removida do thread.  
  
6.  Clique nos contornos do sinalizador para dois threads, o segundo e o terceiro da parte inferior da lista.  
  
     Os ícones de sinalizador ficam vermelho contínuo, em vez de contornos vazado.  
  
7.  Clique no botão na parte superior da coluna do sinalizador.  
  
     A ordem da lista de thread foi alterada quando você clicou no botão. A lista de thread agora é classificada com os threads sinalizados na parte superior.  
  
8.  Novamente, clique no botão na parte superior da coluna do sinalizador.  
  
     A ordem de classificação foi modificada novamente.  
  
## <a name="more-about-the-threads-window"></a>Mais sobre a janela de threads  
  
#### <a name="to-learn-more-about-the-threads-window"></a>Para saber mais sobre a janela de threads  
  
1.  No **Threads** janela, examine a terceira coluna da esquerda. O botão na parte superior desta coluna diz **ID**.  
  
2.  Clique em **ID**.  
  
     A lista de thread agora é classificada pelo número de identificação do thread.  
  
3.  Clique com o botão direito em qualquer thread na lista. No menu de atalho, clique em **exibição Hexadecimal**.  
  
     O formato dos números da ID de thread é alterado.  
  
4.  Passe o ponteiro de mouse sobre qualquer thread na lista.  
  
     Depois de um atraso momentâneo, um DataTip é exibido. Ele mostra uma pilha de chamadas parcial para o thread.  
  
5.  Examine a quarta coluna da esquerda, que é rotulada **categoria**. Os threads são classificados em categorias.  
  
     O primeiro thread criado em um processo é chamado de thread principal. Localize-o na lista de thread.  
  
6.  O thread principal com o botão direito e, em seguida, clique em **alternar para Thread**.  
  
     Aparece uma caixa de diálogo de aviso. Ela indica que o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] não pode exibir o código-fonte do thread principal.  
  
     Clique em **OK**.  
  
7.  Examine os **pilha de chamadas** janela e o **local de depuração** barra de ferramentas.  
  
     O conteúdo a **pilha de chamadas** janela foram alterados.  
  
## <a name="switching-the-active-thread"></a>Alternando o thread ativo  
  
#### <a name="to-switch-threads"></a>Para alternar segmentos  
  
1.  No **Threads** janela, examine a segunda coluna da esquerda. O botão na parte superior dessa coluna não tem texto ou ícone. Esta coluna é o **Thread ativo** coluna.  
  
2.  Examine os **Thread ativo** coluna e observe que um thread tem uma seta amarela. Esse é o *indicador de thread ativo*.  
  
3.  Anote o número de ID do thread onde o indicador de thread ativo está localizado. Você moverá o indicador de thread ativo para outro thread, mas terá que colocá-lo de volta onde terminou.  
  
4.  Outro thread com o botão direito e, em seguida, clique em **alternar para Thread**.  
  
5.  Examine os **pilha de chamadas** janela na janela de origem. O conteúdo foi alterado.  
  
6.  Examine os **local de depuração** barra de ferramentas. O thread ativo foi alterado lá também.  
  
7.  Vá para o **local de depuração** barra de ferramentas. Clique o **Thread** caixa e escolha um thread diferente na lista suspensa.  
  
8.  Examine os **Threads** janela. O indicador de thread ativo foi alterado.  
  
9. Na janela de origem, clique com o botão direito em u marcador de thread. No menu de atalho, aponte para **alternar para** e clique em um número de nome/ID do thread.  
  
     Agora você já viu três maneiras de alterar o thread ativo: usando o **Threads** janela, o **Thread** caixa a **local de depuração** barra de ferramentas e o indicador de thread no janela de origem.  
  
     Com o indicador de thread, você pode alternar somente para threads que pararam nesse local específico. Usando o **Threads** janela e **local de depuração** barra de ferramentas, você pode alternar para qualquer thread.  
  
## <a name="freezing-and-thawing-thread-execution"></a>Congelando e descongelando a execução de thread  
  
#### <a name="to-freeze-and-unfreeze-threads"></a>Para congelar e descongelar threads  
  
1.  No **Threads** janela, clique em qualquer thread e, em seguida, clique em **congelar**.  
  
2.  Examine a coluna de thread ativo. O par de barras verticais agora aparece ali. Essas duas barras azuis indicam que o thread está congelado.  
  
3.  Examine os **Suspend** coluna. A contagem de suspensão para o thread agora é 1.  
  
4.  Clique com botão direito no thread congelado e, em seguida, clique em **descongelar**.  
  
     A coluna thread ativo e o **Suspend** alteração de coluna.  
  
## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos multithread](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [Como mudar para outro thread durante a depuração](../debugger/how-to-switch-to-another-thread-while-debugging.md)



