---
title: 'Como: implementar marcadores de erro | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - error markers
ms.assetid: e8e78514-5720-4fc2-aa43-00b6af482e38
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 3e4dd15f4cbb36ef1f81d3b7ca345a6a06bdaff4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51736195"
---
# <a name="how-to-implement-error-markers"></a>Como: implementar o marcador de erros
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Marcadores de erro (ou ondulados vermelhos) são as personalizações do editor de texto para implementar mais difícil. No entanto, os benefícios que eles oferecem aos usuários de seu VSPackage podem compensam o custo para fornecê-las. Marcadores de erro sutilmente marcam o texto que o analisador de linguagem considera incorreta com uma linha vermelha ondulada ou ondulada. Este indicador ajuda a programadores visualmente, exibindo um código incorreto.  
  
 Use marcadores de texto para implementar os sublinhados ondulados vermelhos. Como regra, serviços de linguagem adicionar ondulados vermelhos para o buffer de texto como uma passagem de plano de fundo, no tempo ocioso ou em um thread em segundo plano.  
  
### <a name="to-implement-the-red-wavy-underline-feature"></a>Para implementar o recurso de sublinhado vermelho ondulado  
  
1. Selecione o texto sob a qual você deseja colocar o sublinhado vermelho ondulado.  
  
2. Criar um marcador do tipo `MARKER_CODESENSE_ERROR`. Para obter mais informações, consulte [como: adicionar marcadores de texto padrão](../extensibility/how-to-add-standard-text-markers.md).  
  
3. Depois disso, passe um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> ponteiro de interface.  
  
   Esse processo também permite que você crie o texto da dica ou um menu de contexto especial sobre um marcador de determinado. Para obter mais informações, consulte [como: adicionar marcadores de texto padrão](../extensibility/how-to-add-standard-text-markers.md).  
  
   Os seguintes objetos são necessários antes de marcadores de erro podem ser exibidos.  
  
- Um analisador.  
  
- Um provedor de tarefa (ou seja, uma implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider2>) que mantém um registro das alterações nas informações de linha para identificar as linhas para ser analisado novamente.  
  
- Eventos de alteração de um filtro de exibição de texto que captura o cursor do modo de exibição usando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEvents.OnChangeCaretLine%2A>) método.  
  
  O analisador, o provedor de tarefas e o filtro de fornecem a infraestrutura necessária para que os marcadores de erro possível. As etapas a seguir fornecem o processo para exibir os marcadores de erro.  
  
1.  Em uma exibição que está sendo filtrada, o filtro obtém um ponteiro para o provedor de tarefas associado aos dados do modo de exibição.  
  
    > [!NOTE]
    >  Você pode usar o mesmo filtro de comando para dicas de método, preenchimento de declaração, marcadores de erro e assim por diante.  
  
2.  Quando o filtro recebe um evento indicando que você tenha movido para outra linha, uma tarefa é criada para verificar se há erros.  
  
3.  O manipulador de tarefa verifica se a linha está suja. Nesse caso, ele analisa a linha de erros.  
  
4.  Se forem encontrados erros, o provedor de tarefas cria uma instância de item de tarefa. Esta instância cria o marcador de texto que usa o ambiente como um marcador de erro no modo de exibição de texto.  
  
## <a name="see-also"></a>Consulte também  
 [Usar marcadores de texto com a API herdada](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [Como: adicionar marcadores de texto padrão](../extensibility/how-to-add-standard-text-markers.md)   
 [Como: criar marcadores de texto personalizado](../extensibility/how-to-create-custom-text-markers.md)   
 [Como usar marcadores de texto](../extensibility/how-to-use-text-markers.md)

