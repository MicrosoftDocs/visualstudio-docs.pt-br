---
title: Como exibir e editar o código usando Inspecionar Definição (Alt + F12) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 45f3dd20-902a-4047-8cca-9f18216123f4
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: cc99602fe1ca2003995594f75736d581fa37e0d0
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49254469"
---
# <a name="how-to-view-and-edit-code-by-using-peek-definition-altf12"></a>Como visualizar e editar códigos usando a janela Inspecionar definição (Alt+F12)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar o comando **Inspecionar Definição** para exibir e editar código sem abandonar o código que está escrevendo. **Inspecionar Definição** e **Ir Para Definição** mostram as mesmas informações, mas **Inspecionar Definição** faz a exibição em uma janela pop-up e **Ir Para Definição** mostra o código em uma janela de código separada. **Ir Para Definição** faz com que seu contexto (ou seja, a janela de código ativo, a linha atual e a posição do cursor) mude para a janela de código de definição. Usando **Inspecionar Definição**, você pode exibir e editar a definição e mover ao redor no arquivo de definição para manter seu local no arquivo original do código.  
  
 Você pode usar **Inspecionar Definição** com código C#, Visual Basic e C++. No Visual Basic, **Inspecionar Definição** mostra um link para o **Pesquisador de Objetos** de símbolos sem metadados de definição (por exemplo, os tipos internos do .NET Framework).  
  
> [!IMPORTANT]
>  Você não pode usar esse comando em qualquer versão Express do Visual Studio 2013.  
  
## <a name="working-with-peek-definition"></a>Trabalhando com Inspecionar Definição  
  
#### <a name="to-open-a-peek-definition-window"></a>Para abrir uma janela Inspecionar Definição  
  
1.  Você pode localizar **Inspecionar Definição** abrindo o menu de atalho de um método que deseja explorar. (Teclado: Alt+F12)  
  
     Esta ilustração mostra a janela **Inspecionar Definição** de um método que é chamado `Print()`:  
  
     ![Janela de Inspeção](../ide/media/peekwindow.png "PeekWindow")  
  
     A janela de definição aparece abaixo da linha `printer.Print(“Hello World!”)` no arquivo original. A janela não oculta nenhum dos códigos em seu arquivo original. As linhas após a chamada `printer.Print(“Hello World!”)` aparecem abaixo da janela de definição.  
  
2.  Você pode mover o cursor para locais diferentes na janela de definição de código. Você ainda se mover pela janela de código original acima ou abaixo da janela de definição.  
  
3.  Você pode copiar uma cadeia de caracteres da janela de definição e colá-la no código original. Também é possível arrastar e soltar a cadeia de caracteres da janela de definição para o código original sem excluí-la da janela de definição.  
  
4.  Você pode fechar a janela de definição pressionando a tecla ESC ou o botão **Fechar** na guia da janela de definição.  
  
#### <a name="to-open-a-peek-definition-window-from-within-a-peek-definition-window"></a>Para abrir uma janela Inspecionar Definição de uma janela Inspecionar Definição  
  
-   Se você já tiver uma janela **Inspecionar Definição** aberta, será possível chamar **Inspecionar Definição** novamente no código nessa janela. Outra janela de definição é aberta. Um conjunto de pontos de trilha aparece ao lado da guia da janela de definição, que você pode usar para navegar entre as janelas de definição. A dica de ferramenta em cada ponto mostra o nome do arquivo e o caminho do arquivo de definição que o ponto representa.  
  
     ![Janela de inspeção dentro de uma janela de inspeção](../ide/media/peekwithinpeek.png "PeekWithinPeek")  
  
#### <a name="to-use-peek-definition-with-multiple-results"></a>Para usar Inspecionar Definição com vários resultados  
  
-   Se você usar **Inspecionar Definição** no código com mais de uma definição (por exemplo, classes parciais), uma lista de resultados aparecerá à direita do modo de exibição de definição de código. É possível escolher qualquer resultado na lista para exibir sua definição.  
  
     ![Janela de inspeção de vários resultados](../ide/media/peekmultiple.png "PeekMultiple")  
  
#### <a name="to-edit-inside-the-peek-definition-window"></a>Para editar dentro da janela Inspecionar Definição  
  
-   Quando você começa a editar dentro de uma janela **Inspecionar Definição**, o arquivo que está sendo modificado é aberto automaticamente como uma guia separada no editor de código e reflete as alterações já feitas. Você pode continuar fazendo, desfazendo e salvando alterações na janela **Inspecionar Definição** e a guia continuará refletindo essas alterações. Mesmo que você feche a janela sem salvar as alterações, você pode fazer, desfazer e salvar mais alterações na guia, escolhendo o ponto exato em que parou quando saiu da janela.  
  
     ![Editando em uma janela de inspeção](../ide/media/peekedit.png "PeekEdit")  
  
#### <a name="to-use-keyboard-shortcuts-for-peek-definition"></a>Para usar atalhos de teclado para Inspecionar Definição  
  
-   Você pode usar estes atalhos de teclado com a janela **Inspecionar Definição**:  
  
    |Funcionalidade|Atalho de teclado|  
    |-------------------|-----------------------|  
    |Abrir a janela de definição|Alt+F12|  
    |Fechar a janela de definição|ESC|  
    |Promover a janela de definição para uma guia de documento regular|Shift+Alt+Home|  
    |Navegar entre janelas de definição|Ctrl+Alt+- e Ctrl+Alt+=|  
    |Navegar entre vários resultados|F8 e Shift+F8|  
    |Alternar entre a janela do editor de códigos e a janela de definição|Shift+Esc|  
  
    > [!NOTE]
    >  Você também pode usar os mesmos atalhos de teclado para editar código em uma janela **Inspecionar Definição**, como usa em qualquer outro lugar no Visual Studio.  
  
## <a name="see-also"></a>Consulte também  
 [Dicas de produtividade](../ide/productivity-tips-for-visual-studio.md)



