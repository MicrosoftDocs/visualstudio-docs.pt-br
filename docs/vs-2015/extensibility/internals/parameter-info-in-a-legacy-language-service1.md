---
title: Informações de parâmetro em uma função de linguagem herdado1 | Microsoft Docs
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
- language services, method tips
- method tips
- language services, parameter info tooltip
- IVsMethodData interface
- Parameter Info (IntelliSense)
ms.assetid: f367295e-45b6-45d2-9ec8-77481743beef
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 462702fb73cd48f324c02344da5c5ed7c3957f23
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51727933"
---
# <a name="parameter-info-in-a-legacy-language-service"></a>Informações de parâmetro em um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

A dica de ferramenta informações de parâmetro do IntelliSense fornece aos usuários com dicas sobre onde eles estão em um constructo de linguagem.  
  
 Serviços de linguagem herdado são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações, consulte [estender o Editor e os serviços de linguagem](../../extensibility/extending-the-editor-and-language-services.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitem que você tirar proveito dos novos recursos do editor.  
  
## <a name="how-parameter-info-tooltips-work"></a>Como funciona a dica de ferramenta de informações de parâmetro  
 Quando você digita uma instrução no editor, o VSPackage exibe uma janela de dica de ferramenta pequeno que contém a definição da instrução que está sendo digitada. Por exemplo, se você digitar uma instrução do Microsoft Foundation Classes (MFC) (tais como `pMainFrame ->UpdateWindow`) e pressione a tecla de parêntese de abertura para iniciar a lista de parâmetros, uma dica de método aparece exibindo a definição do `UpdateWindow` método.  
  
 Dica de ferramenta de informações de parâmetro é geralmente usadas em conjunto com a conclusão da instrução. Eles são mais úteis para linguagens que têm parâmetros ou outras informações formatadas após o nome do método ou a palavra-chave.  
  
 As dicas de ferramentas de informações do parâmetro são iniciadas pelo serviço de linguagem por meio de interceptação de comando. Para interceptar caracteres de usuário, o objeto de serviço de linguagem deve implementar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> da interface e passar a exibição de texto de um ponteiro para seu <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> implementação, chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> interface. O filtro de comando intercepta comandos digitados na janela de código. Monitore as informações de comando para saber quando exibir informações de parâmetro para o usuário. Você pode usar o mesmo filtro de comando para preenchimento de declaração, marcadores de erro e assim por diante.  
  
 Quando você digita uma palavra-chave para a qual o serviço de linguagem pode fornecer dicas, em seguida, o serviço de linguagem cria uma <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> objeto e chamadas a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> interface para notificar o IDE para exibir uma dica. Criar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> do objeto usando `VSLocalCreateInstance` e especificando a coclass `CLSID_VsMethodTipWindow`. `VsLocalCreateInstance` é uma função definida no vsdoc.h de arquivo de cabeçalho que chama `QueryService` para o registro local e chama `CreateInstance` nesse objeto para o `CLSID_VsMethodTipWindow`.  
  
## <a name="providing-a-method-tip"></a>Fornecer uma dica de método  
 Para fornecer uma dica de método, chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> método na <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> interface, passá-lo em sua implementação do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> interface.  
  
 Quando seu <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> classe é invocado, seus métodos são chamados na seguinte ordem:  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetContextStream%2A>  
  
     Retorna a posição e o comprimento dos dados relevantes no buffer de texto atual. Isso instrui o IDE não ocultar esses dados com a janela de dica de ferramenta.  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetCurMethod%2A>  
  
     Retorna o número de método (índice de base zero) a ser exibido inicialmente. Por exemplo, se você retornar zero, o primeiro método sobrecarregado inicialmente é apresentado.  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetOverloadCount%2A>  
  
     Retorna o número de métodos sobrecarregados que são aplicáveis no contexto atual. Se você retornar um valor maior que 1 para esse método, em seguida, a exibição de texto exibe para cima e para as setas para você. Se você clicar na seta para baixo, o IDE chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.NextMethod%2A> método. Se você clicar na seta para cima, o IDE chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.PrevMethod%2A> método.  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A>  
  
     O texto da dica de ferramenta informações do parâmetro é construído durante várias chamadas para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A> e <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A> métodos.  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterCount%2A>  
  
     Retorna o número de parâmetros para exibir no método.  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A>  
  
     Se você retornar um número de método correspondente com a sobrecarga que você deseja exibir, esse método é chamado, seguido por uma chamada para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A> método.  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A>  
  
     Informa ao seu serviço de linguagem para atualizar o editor quando uma dica de método é exibida. No <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A> método, chame o seguinte:  
  
    ```  
    <pTxWin> ->UpdateTipWindow(<pTip>, UTW_CONTENTCHANGED | UTW_CONTEXTCHANGED).  
    ```  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>  
  
     Você recebe uma chamada para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> método quando você fechar a janela de dica de método.

