---
title: 'Como: definir pontos de interrupção em fluxos de trabalho | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: e41b21c9-c061-4358-8e2f-eb5e412864a8
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: b3dedba320ce8a783b7d54df54a30b0759a6bd00
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49896218"
---
# <a name="how-to-set-breakpoints-in-workflows"></a>Como: Definir pontos de interrupção em fluxos de trabalho
Quando você usa [!INCLUDE[wfd1](../includes/wfd1-md.md)], você pode definir pontos de interrupção nos fluxos de trabalho gráficos como você faria em Visual Basic ou no código em c. Como esperado, a execução de fluxo de trabalho que ele pare em cada ponto de interrupção esse definido.  
  
 Um ponto de interrupção tem três estados: *pendente*, *associado*, e *erro*. Quando você definir um ponto de interrupção, ele está pendente, e ele é representado por um ícone vermelho contínuo. Quando o tempo de execução carregado o tipo de fluxo de trabalho, transformações limite. Se você especificar um formato incorreto do ponto de interrupção, como um nome de atividade que não é válida, uma janela de erro aparece. O ponto de interrupção é adicionado ainda para a janela de ponto de interrupção, mas é marcado com um pequeno “x”.  
  
> [!NOTE]
>  Os pontos de interrupção em fluxos de trabalho chamados não são suportados.  
> 
> [!WARNING]
>  Certifique-se de que você selecione a opção **Habilitar Just My Code (somente gerenciado)** da **ferramentas**, **opções**, **depuração** menu antes de você depure. Se você tem duas sequências aninhadas dentro de outra sequência e você definir um ponto de interrupção na primeira sequência interna, pressionando **F11** não depurará na segunda sequência interna se o <strong>Habilitar Just My Code (somente gerenciado)</strong>opção não estiver selecionada.  
> 
> [!WARNING]
>  Os pontos de interrupção em um fluxo de trabalho não obterão a ocorrência se o caminho completo para a propriedade de arquivo XAML não é preciso. O caminho completo do arquivo XAML não é preciso após movido o projeto/solução para outra pasta ou a outro computador. Selecione Ctrl+S para salvar e atualiza a propriedade de caminho completo.  
  
### <a name="to-set-a-breakpoint-on-an-activity-in-the-design-view"></a>Para definir um ponto de interrupção em uma atividade no modo design  
  
1.  Selecione a atividade que você deseja que o depurador para interromper novamente.  
  
2.  Sobre o **Debug** menu, selecione **alternar ponto de interrupção**. Um ícone vermelho aparecerá na borda superior esquerda da atividade.  
  
     Como alternativa, você também pode pressionar o atalho **F9** da chave depois que a atividade ou você pode a atividade com o botão direito e selecione **ponto de interrupção** , em seguida, **Inserir ponto de interrupção**no menu de contexto.  
  
## <a name="see-also"></a>Consulte também  
 [Como: chamar o depurador de fluxo de trabalho](../workflow-designer/how-to-invoke-the-workflow-debugger.md)   
 [Depurando fluxos de trabalho com o Designer de fluxo de trabalho](../workflow-designer/debugging-workflows-with-the-workflow-designer.md)   
 [Como depurar XAML com o Designer de Fluxo de Trabalho](../workflow-designer/how-to-debug-xaml-with-the-workflow-designer.md)