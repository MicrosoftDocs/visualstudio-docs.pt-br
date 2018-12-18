---
title: Informações de parâmetro em um Service1 de idioma herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services, method tips
- method tips
- language services, parameter info tooltip
- IVsMethodData interface
- Parameter Info (IntelliSense)
ms.assetid: f367295e-45b6-45d2-9ec8-77481743beef
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 50450d1968c626e0a5b32dee4c6f03d005d6ede9
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31132757"
---
# <a name="parameter-info-in-a-legacy-language-service"></a>Informações de parâmetro em um serviço de linguagem herdado
A dica de ferramenta de informações do parâmetro IntelliSense fornece aos usuários com dicas sobre onde eles estão em uma construção de linguagem.  
  
 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações, consulte [estendendo o Editor e o idioma serviços](../../extensibility/extending-the-editor-and-language-services.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API assim que possível. Isso melhorar o desempenho do seu serviço de linguagem e permitem que você aproveite os novos recursos do editor.  
  
## <a name="how-parameter-info-tooltips-work"></a>Como funciona a dica de ferramenta de informações de parâmetro  
 Quando você digita uma instrução no editor, o VSPackage exibe uma janela de dica de ferramenta pequeno que contém a definição da linha que está sendo digitada. Por exemplo, se você digitar uma instrução do Microsoft Foundation Classes (MFC) (como `pMainFrame ->UpdateWindow`) e pressione o parêntese de abertura tecla para iniciar a lista de parâmetros, uma dica de método aparece exibindo a definição do `UpdateWindow` método.  
  
 Dicas de ferramenta de informações de parâmetro são normalmente usadas em conjunto com a conclusão de instrução. Eles são mais úteis para os idiomas que têm parâmetros ou outras informações formatadas após o nome do método ou a palavra-chave.  
  
 As dicas de ferramentas de informações de parâmetro são iniciadas pelo serviço de idioma por meio de interceptação de comando. Para interceptar caracteres de usuário, o objeto de serviço de linguagem deve implementar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> de interface e passa o modo de exibição de texto um ponteiro para o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> implementação, chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> interface. O filtro de comando intercepta comandos digitados na janela de código. Monitore as informações de comando para saber quando exibir informações de parâmetro para o usuário. Você pode usar o mesmo filtro de comando para a conclusão de instrução, marcadores de erro e assim por diante.  
  
 Quando você digita uma palavra-chave para a qual o serviço de linguagem pode fornecer dicas, em seguida, o serviço de linguagem cria um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> objeto e chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> interface para notificar o IDE para exibir uma dica. Criar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> objeto usando `VSLocalCreateInstance` e especificando coclass `CLSID_VsMethodTipWindow`. `VsLocalCreateInstance` é uma função definida no vsdoc.h de arquivo de cabeçalho que chama `QueryService` para o registro local e chamadas `CreateInstance` nesse objeto para o `CLSID_VsMethodTipWindow`.  
  
## <a name="providing-a-method-tip"></a>Fornecer uma dica de método  
 Para fornecer uma dica de método, chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> método o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> interface, passando a implementação do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> interface.  
  
 Quando seu <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> classe é invocada, seus métodos são chamados na seguinte ordem:  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetContextStream%2A>  
  
     Retorna a posição e o comprimento dos dados relevantes no buffer de texto atual. Isso instrui o IDE não podem ocultar esses dados com a janela de dica de ferramenta.  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetCurMethod%2A>  
  
     Retorna o número de método (índice baseado em zero) a ser exibido inicialmente. Por exemplo, se você retornar zero, o primeiro método sobrecarregado inicialmente é apresentado.  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetOverloadCount%2A>  
  
     Retorna o número de métodos sobrecarregados que são aplicáveis no contexto atual. Se você retornar um valor maior que 1 para esse método, a exibição de texto exibe setas para cima e para você. Se você clicar na seta para baixo, o IDE chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.NextMethod%2A> método. Se você clicar na seta para cima, o IDE chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.PrevMethod%2A> método.  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A>  
  
     O texto da dica de ferramenta de informações do parâmetro é construído durante várias chamadas para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A> e <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A> métodos.  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterCount%2A>  
  
     Retorna o número de parâmetros para exibir no método.  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A>  
  
     Se você retornar um número de método correspondente com a sobrecarga que deseja exibir, este método é chamado, seguido por uma chamada para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A> método.  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A>  
  
     Informa o serviço de linguagem para atualizar o editor quando uma dica de método é exibida. No <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A> método, chame o seguinte:  
  
    ```  
    <pTxWin> ->UpdateTipWindow(<pTip>, UTW_CONTENTCHANGED | UTW_CONTEXTCHANGED).  
    ```  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>  
  
     Você receberá uma chamada para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> método quando você fechar a janela de dica de método.