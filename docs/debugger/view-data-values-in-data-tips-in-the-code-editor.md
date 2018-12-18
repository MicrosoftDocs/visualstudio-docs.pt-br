---
title: Exibir valores de variáveis em DataTips | Microsoft Docs
ms.custom: seodec18
ms.date: 11/21/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugging [Visual Studio], DataTips
- DataTips tool
ms.assetid: ffa7bd18-439b-4685-a9b3-c7884b5de41f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c84c6c9049fe11de16267267df86c88851cfcdfe
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53066844"
---
# <a name="view-data-values-in-datatips-in-the-code-editor"></a>Exibir os valores de dados em DataTips no editor de códigos

Os DataTips fornecem um modo conveniente de exibir informações sobre variáveis em seu programa durante a depuração. Os DataTips funcionam apenas no modo de interrupção e apenas com variáveis que estejam no escopo de execução atual. Se essa for a primeira vez que você tentou depurar o código, você talvez queira ler [corrigir bugs, escrevendo melhor C# código](../debugger/write-better-code-with-visual-studio.md) e [depuração para iniciantes absolutos](../debugger/debugging-absolute-beginners.md) antes de prosseguir com este artigo.

Se esta for sua primeira vez em que depuração, você talvez queira ler [gravar melhor C# usando o Visual Studio de código](../debugger/write-better-code-with-visual-studio.md) e [depuração para iniciantes absolutos](../debugger/debugging-absolute-beginners.md) antes de ler este artigo.
  
## <a name="work-with-datatips"></a>Trabalhar com DataTips

DataTips aparecem apenas no modo de interrupção e somente em variáveis que estão no escopo atual de execução.

### <a name="display-a-datatip"></a>Exibir um DataTip  
  
1. Defina um ponto de interrupção em seu código e iniciar a depuração pressionando **F5** ou selecionando **Debug** > **iniciar depuração**.
  
1. Quando em pausa no ponto de interrupção, passe o mouse sobre qualquer variável no escopo atual. Um DataTip aparece, mostrando o nome e o valor atual da variável.

### <a name="make-a-datatip-transparent"></a>Criar um DataTip transparente  

Para fazer um DataTip transparente para ver o código que está abaixo dela, enquanto no DataTip, pressione **Ctrl**. O DataTip permanecerá transparente enquanto você mantiver pressionada a **Ctrl** chave. Isso não funciona para DataTips fixados ou flutuantes.  
### <a name="pin-a-datatip"></a>Fixar um DataTip

Para fixar um DataTip, para que ela permaneça aberta, selecione o pino **fixar à origem** ícone. 

![Fixar um DataTip](../debugger/media/dbg-tips-data-tips-pinned.png "fixar um DataTip")

Você pode mover um DataTip fixado, arrastando-o ao redor da janela de código. Um ícone de tachinha aparece na medianiz ao lado da linha que o DataTip é fixado. 

>[!NOTE]
>DataTips são sempre avaliados no contexto em que a execução é suspensa, não o cursor atual ou o local de DataTip. Se você passar o mouse sobre uma variável em outra função que tem o mesmo nome que uma variável no contexto atual, o valor da variável no contexto atual é exibido.
  
### <a name="unpin-a-datatip-from-source"></a>Desafixar um DataTip da fonte

Para flutuar um DataTip fixado, passe o mouse sobre o DataTip e selecione o ícone de pino no menu de contexto. 

O ícone de pino muda para a posição desafixada, e o DataTip agora flutua ou pode ser arrastado acima de todas as janelas abertas. DataTips flutuantes fechar quando termina a sessão de depuração.  
  
### <a name="repin-a-datatip"></a>Refixar um DataTip  
  
Para refixar um DataTip flutuante para código-fonte, passe o mouse sobre ele no editor de código e selecione o ícone de pino. O ícone de pino muda para a posição fixada, e o DataTip é fixado novamente somente para a janela de código. 

Se um DataTip é flutuante em uma janela de código sem origem, o ícone de pino está disponível e o DataTip não pode ser remarcado. Para acessar o ícone de anotações, retorne o DataTip à janela do editor de código, arrastando-o ou fornecendo o foco da janela de código. 
  
### <a name="close-a-datatip"></a>Fechar um DataTip  
  
Para fechar um DataTip, passe o mouse sobre o DataTip e selecione o fechamento (**x**) ícone no menu de contexto.  
  
### <a name="close-all-datatips"></a>Fechar todos os DataTips  
  
Para fechar todos os DataTips, diante de **Debug** menu, selecione **limpar todos os DataTips**.  
  
### <a name="close-all-datatips-for-a-specific-file"></a>Fechar todos os DataTips para um arquivo específico  
  
Para fechar todos os DataTips para um arquivo específico, na **depurar** menu, selecione **limpar todos os DataTips fixados \<Filename >**.  
  
## <a name="expand-and-edit-information"></a>Expandir e editar informações  
Você pode usar os DataTips para expandir uma matriz, uma estrutura ou um objeto para exibir seus membros. Você também pode editar o valor de uma variável de um DataTip.  
  
### <a name="expand-a-variable"></a>Expandir uma variável

Para expandir um objeto em um DataTip para ver seus elementos, passe o mouse sobre as setas de expansão antes dos nomes de item para exibir os elementos na forma da árvore. Para um DataTip fixado, selecione a **+** antes da variável de nome e, em seguida, expanda a árvore. 

![Expanda um DataTip](../debugger/media/dbg-tour-data-tips.png "expandir um DataTip")

Você pode usar o mouse ou as teclas de direção no teclado para mover para cima para baixo na exibição expandida. 

Você também pode fixar itens expandidos para o DataTip fixado focalizá-los e selecionando os ícones de pino. Os elementos, em seguida, aparecem no DataTip fixado depois que a árvore é recolhida. 

### <a name="edit-the-value-of-a-variable"></a>Editar o valor de uma variável

Para editar o valor de uma variável ou um elemento em um DataTip, selecione o valor, digite um novo valor e pressione **Enter**. Seleção está desabilitada para valores somente leitura.  

## <a name="visualize-complex-data-types"></a>Visualizar os tipos de dados complexos  

Um ícone de lupa ao lado de uma variável ou um elemento em um DataTip significa que um ou mais [visualizadores](../debugger/create-custom-visualizers-of-data.md), como o [Visualizador de texto](../debugger/string-visualizer-dialog-box.md), estão disponíveis para a variável. Visualizadores de exibem informações de uma maneira mais significativa, às vezes, gráfica.
  
Para exibir o elemento usando o visualizador padrão para o tipo de dados, selecione o ícone de lupa ![ícone do visualizador](../debugger/media/dbg-tips-visualizer-icon.png "ícone do visualizador"). Selecione a seta ao lado do ícone de lupa para selecionar em uma lista de visualizadores para o tipo de dados.  

## <a name="add-a-variable-to-a-watch-window"></a>Adicionar uma variável para uma janela Inspeção  

Se você quiser continuar a inspecionar uma variável, você pode adicioná-lo para um **inspeção** janela a partir de um DataTip. A variável no DataTip com o botão direito e selecione **Adicionar inspeção**. 

A variável é exibida na **inspeção** janela. Se sua edição do Visual Studio oferece suporte a mais de um **Watch** , a variável será exibida na **inspeção 1**. 
  
## <a name="import-and-export-datatips"></a>Importar e exportar DataTips  

Você pode exportar DataTips para um arquivo XML, que você pode compartilhar ou editar usando um editor de texto. Você também pode importar um arquivo XML DataTip recebida ou editado. 
  
**Para exportar DataTips:** 
  
1. Selecione **Debug** > **exportar DataTips**.  
   
1. No **exportar DataTips** caixa de diálogo, navegue até o local para salvar o arquivo XML, digite um nome para o arquivo e, em seguida, selecione **salvar**.  
  
**Para importar DataTips:** 
  
1. Selecione **Debug** > **importar DataTips**.  
   
1. No **importar DataTips** caixa de diálogo, selecione o arquivo XML DataTips que você deseja abrir e, em seguida, selecione **abrir**.  

## <a name="see-also"></a>Consulte também  
 [O que é depuração?](../debugger/what-is-debugging.md)  
 [Corrigir bugs escrevendo um melhor código C#](../debugger/write-better-code-with-visual-studio.md)  
 [Introdução à depuração](../debugger/debugger-feature-tour.md) [exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)   
 [Janelas Inspeção e QuickWatch](../debugger/watch-and-quickwatch-windows.md)   
 [Criar visualizadores personalizados](../debugger/create-custom-visualizers-of-data.md)   

