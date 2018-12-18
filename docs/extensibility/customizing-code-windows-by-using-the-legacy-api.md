---
title: Personalizando o Windows do código usando a API herdada | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - code windows
ms.assetid: 5328ab2f-55cb-4680-9744-ec79f55acd1b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 454d58a48abafe9b23f8a812e5d40b9fc6477b50
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39499348"
---
# <a name="customize-code-windows-by-using-the-legacy-api"></a>Personalizar janelas de código usando a API herdada
Uma janela de código é um objeto de janela de documento que dá suporte a um ou mais modos de exibição de texto. Os recursos exatos de uma janela de código dependem do serviço de idioma associado. No modo de interface de documentos múltiplos (MDI), a janela de código é o quadro filho MDI.  
  
 Janelas de código são controladas pelos serviços de linguagem, e cada serviço de linguagem pode fornecer seu próprio Gerenciador de janela de código. Isso permite que o serviço de linguagem adicionar seus próprio adornos a janela de código, como linhas onduladas, colorização e muito mais. Para obter mais informações sobre como criar uma janela de core, consulte [instanciar o editor principal usando a API herdada](../extensibility/instantiating-the-core-editor-by-using-the-legacy-api.md).  
  
 Uma janela de código é um <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> objeto que tem uma exibição de texto e quaisquer adornos localizados no objeto. Quando você cria a janela de código durante a instanciação do núcleo do editor, o serviço de linguagem pode anexar um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> para a janela de código, como é mostrado na ilustração a seguir.  
  
 ![Gráfico de CodeWindow](../extensibility/media/vscodewindow.gif "vscodewindow")  
Janela de código  
  
 O serviço de linguagem implementa o Gerenciador de janelas de código e é responsável por gerenciar adornos, como uma barra de menu suspenso. O janela de código chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A> método durante a inicialização da janela de código. Quando essa chamada é feita, o serviço de linguagem pode adicionar uma barra de menu ou uma barra de botões (<xref:Microsoft.VisualStudio.TextManager.Interop.IVsButtonBarClient>) para a janela de código.  
  
## <a name="in-this-section"></a>Nesta seção  
 `Customizing Code Windows by Using the Legacy API`  
 Explica como personalizar o windows de código usando a API herdada.  
  
 [Como: hospedar um editor em outro editor](../extensibility/how-to-host-an-editor-in-another-editor.md)  
 Explica como hospedar um segundo editor dentro de uma janela do editor.  
  
 [Como: disparar eventos quando o editor perde o foco](../extensibility/how-to-fire-events-when-the-editor-loses-focus.md)  
 Explica como anexar um modo de exibição de documento para um objeto de dados do documento.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>   
 [Criar uma instância o editor principal usando a API herdada](../extensibility/instantiating-the-core-editor-by-using-the-legacy-api.md)   
 [Exibição de theText de acesso usando a API herdada](../extensibility/accessing-thetext-view-by-using-the-legacy-api.md)