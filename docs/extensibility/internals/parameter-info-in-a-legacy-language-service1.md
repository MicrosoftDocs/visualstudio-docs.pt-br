---
title: Informações de parâmetro em um Service1 de linguagem herdada | Microsoft Docs
description: Saiba como implementar a dica de ferramenta de informações de parâmetro do IntelliSense, que fornece aos usuários dicas, em um serviço de linguagem herdado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, method tips
- method tips
- language services, parameter info tooltip
- IVsMethodData interface
- Parameter Info (IntelliSense)
ms.assetid: f367295e-45b6-45d2-9ec8-77481743beef
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4dade924ef89be22161c598ba0ae64084c0697ea
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061141"
---
# <a name="parameter-info-in-a-legacy-language-service-1"></a>Informações de parâmetro em um serviço de idioma herdado 1
A dica de ferramenta de informações de parâmetro do IntelliSense fornece aos usuários dicas sobre onde eles estão em uma construção de linguagem.

 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente de implementar recursos de serviço de linguagem é usar extensões de MEF. Para obter mais informações, consulte [estendendo o editor e os serviços de linguagem](../../extensibility/extending-the-editor-and-language-services.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor o mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

## <a name="how-parameter-info-tooltips-work"></a>Como funcionam as dicas de ferramentas de informações do parâmetro
 Quando você digita uma instrução no editor, o VSPackage exibe uma pequena janela de dica de ferramenta que contém a definição da instrução que está sendo digitada. Por exemplo, se você digitar uma instrução MFC (MFC) (como `pMainFrame ->UpdateWindow` ) e pressionar a tecla de parênteses de abertura para iniciar a listagem de parâmetros, uma dica de método será exibida exibindo a definição do `UpdateWindow` método.

 As dicas de ferramentas de informações de parâmetros geralmente são usadas em conjunto com a conclusão de instrução. Elas são mais úteis para idiomas que têm parâmetros ou outras informações formatadas após o nome do método ou palavra-chave.

 As dicas de ferramentas de informações de parâmetro são iniciadas pelo serviço de linguagem por meio da interceptação de comando. Para interceptar caracteres de usuário, o objeto de serviço de idioma deve implementar a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface e passar a exibição de texto de um ponteiro para sua <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> implementação, chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> método na <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> interface. O filtro de comando intercepta os comandos que você digita na janela de código. Monitore as informações do comando para saber quando exibir informações de parâmetro para o usuário. Você pode usar o mesmo filtro de comando para conclusão de instrução, marcadores de erro e assim por diante.

 Quando você digita uma palavra-chave para a qual o serviço de linguagem pode fornecer dicas, o serviço de linguagem cria um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> objeto e chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> método na <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> interface para notificar o IDE para exibir uma dica. Crie o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> objeto usando `VSLocalCreateInstance` e especificando a coclass `CLSID_VsMethodTipWindow` . `VsLocalCreateInstance` é uma função definida no arquivo de cabeçalho vsdoc. h que chama `QueryService` o registro local e chama `CreateInstance` esse objeto para o `CLSID_VsMethodTipWindow` .

## <a name="providing-a-method-tip"></a>Fornecendo uma dica de método
 Para fornecer uma dica de método, chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> método na <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> interface, passando-a sua implementação da <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> interface.

 Quando sua <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> classe é invocada, seus métodos são chamados na seguinte ordem:

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetContextStream%2A>

     Retorna a posição e o comprimento dos dados relevantes no buffer de texto atual. Isso instrui o IDE a não obscurecer esses dados com a janela de dica de ferramenta.

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetCurMethod%2A>

     Retorna o número do método (índice de base zero) que você deseja exibir inicialmente. Por exemplo, se você retornar zero, o primeiro método sobrecarregado será apresentado inicialmente.

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetOverloadCount%2A>

     Retorna o número de métodos sobrecarregados que são aplicáveis no contexto atual. Se você retornar um valor maior que 1 para esse método, a exibição de texto exibirá as setas para cima e para baixo. Se você clicar na seta para baixo, o IDE chamará o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.NextMethod%2A> método. Se você clicar na seta para cima, o IDE chamará o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.PrevMethod%2A> método.

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A>

     O texto da dica de ferramenta informações do parâmetro é construído durante várias chamadas para os <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetMethodText%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A> métodos e.

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterCount%2A>

     Retorna o número de parâmetros a serem exibidos no método.

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.GetParameterText%2A>

     Se você retornar um número de método correspondente à sobrecarga que deseja exibir, esse método será chamado, seguido por uma chamada para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A> método.

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A>

     Informa o serviço de linguagem para atualizar o editor quando uma dica de método é exibida. No <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.UpdateView%2A> método, chame o seguinte:

    ```
    <pTxWin> ->UpdateTipWindow(<pTip>, UTW_CONTENTCHANGED | UTW_CONTEXTCHANGED).
    ```

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A>

     Você recebe uma chamada para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> método quando fecha a janela de dica do método.
