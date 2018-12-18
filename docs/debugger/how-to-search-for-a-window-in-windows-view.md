---
title: 'Como: procurar uma janela no modo de exibição do Windows | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- windows, searching in Windows view
ms.assetid: 30306970-b861-4315-acf8-f86a43d4e73b
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c187c3a4b8086b5b991f7288f2686d6010e79262
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49927392"
---
# <a name="how-to-search-for-a-window-in-windows-view"></a>Como procurar uma janela na exibição de janelas
Você pode procurar uma janela específica no modo de exibição do Windows, usando seu identificador, legenda, classe ou uma combinação de sua legenda e a classe como critérios de pesquisa. Você também pode especificar a direção inicial da pesquisa. Os campos na caixa de diálogo mostrará os atributos da janela selecionada na árvore de janela.  
  
 Iniciar com a árvore expandida para o segundo nível (todos os windows que são filhos da área de trabalho), para que você possa identificar windows de nível de área de trabalho por seu nome de classe e o título. Depois de ter escolhido uma janela de nível de área de trabalho, você pode expandir esse nível para encontrar uma janela filho específicos.  
  
### <a name="to-search-for-a-window-in-windows-view"></a>Para procurar uma janela no modo de exibição do Windows  
  
1. Organizar as janelas assim que Spy + +, o [modo de exibição do Windows](../debugger/windows-view.md) janela e a janela de destino estão visíveis.  
  
2. Dos **pesquisa** menu, escolha **localizar janela**.  
  
    O [caixa de diálogo de pesquisa de janela](../debugger/window-search-dialog-box.md) é aberta.  
  
   > [!TIP]
   >  Para reduzir a desordem na tela, selecione a **Spy ocultar** opção. Esta opção oculta a janela principal do Spy + + e deixa somente o **pesquisa de janela** caixa de diálogo visível na parte superior de seus outros aplicativos. A janela principal do Spy + + é restaurada quando você clica **Okey** ou **Cancelar**, ou quando você desmarca a **ocultar Spy + +** opção.  
  
3. Arraste o **ferramenta Descobridora** sobre a janela de destino. À medida que você arrasta a ferramenta, o **pesquisa de janela** caixa de diálogo exibe detalhes sobre a janela selecionada.  
  
   - ou –  
  
     Se você souber o identificador da janela desejado (por exemplo, do depurador), você pode digitar no **manipular** caixa.  
  
   - ou –  
  
     Se você souber a legenda e/ou a classe de janela que você deseja, você pode digitá-los a **legenda** e **classe** caixas de texto e desmarque o **manipular** caixa de texto.  
  
4. Escolher **para cima** ou **para baixo** para a direção inicial da pesquisa.  
  
5. Clique em **OK**.  
  
    Se uma janela correspondente for encontrada, ele é realçado na [modo de exibição do Windows](../debugger/windows-view.md) janela.