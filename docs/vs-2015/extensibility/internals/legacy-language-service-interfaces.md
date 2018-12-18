---
title: Interfaces de serviço de linguagem herdado | Microsoft Docs
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
- IVsLanguageInfo interface
- language services, objects
ms.assetid: 03b2d507-f463-417e-bc22-bdac68eeda52
caps.latest.revision: 25
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: a5e574267ac83d145c5f3fb44117534127e3f1fd
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51785840"
---
# <a name="legacy-language-service-interfaces"></a>Interfaces de serviço de linguagem herdada
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Para qualquer linguagem de programação específica, pode haver apenas uma instância de um serviço de linguagem por vez. Entretanto, um serviço de linguagem única pode atender mais de um editor.  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] não associa um serviço de linguagem com qualquer editor específico. Portanto, quando você solicita uma operação de serviço de linguagem, você deve identificar o editor apropriado como um parâmetro.  
  
## <a name="common-interfaces-associated-with-language-services"></a>Interfaces comuns associadas aos serviços de linguagem  
 O editor obtém o serviço de linguagem chamando <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> em VSPackage apropriado. O SID (ID) passado na chamada de serviço identifica o serviço de linguagem que está sendo solicitado.  
  
 Você pode implementar as interfaces de serviço de linguagem principal em qualquer número de classes separadas. No entanto, uma abordagem comum é implementar as interfaces a seguir em uma única classe:  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageBlock> (opcional)  
  
  O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> interface deve ser implementada em todos os serviços de linguagem. Ele fornece informações sobre seu serviço de linguagem, como o nome localizado da linguagem, as extensões de nome de arquivo associadas com o serviço de linguagem e como recuperar um colorizador.  
  
## <a name="additional-language-service-interfaces"></a>Interfaces de serviço de idioma adicionais  
 Outras interfaces podem ser fornecidos com o serviço de linguagem. [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] solicita uma instância separada dessas interfaces para cada instância do buffer de texto. Portanto, você deve implementar cada uma dessas interfaces em seu próprio objeto. A tabela a seguir mostra as interfaces que exigem uma instância por instância do buffer de texto.  
  
|Interface|Descrição|  
|---------------|-----------------|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|Gerencia os adornos da janela de código, como a barra de menu suspenso. Você pode obter essa interface usando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> método. Há um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> por janela de código.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>|Colore delimitadores e palavras-chave. Você pode obter essa interface usando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> método. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> é chamado em tempo de pintura. Evitar o trabalho de computação intensiva dentro <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> ou poderão afetar o desempenho.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>|Fornece dicas de ferramenta do IntelliSense parâmetro. Quando o serviço de linguagem reconhece um caractere que indica que os dados método deve ser exibido como um parêntese de abertura, ele chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> view de método para notificar o texto que o serviço de linguagem está pronto para exibir uma dica de ferramenta de informações do parâmetro. A exibição de texto, em seguida, chama de volta para o serviço de linguagem, usando os métodos do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> a interface para obter as informações necessárias para exibir a dica de ferramenta.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>|Fornece preenchimento de declaração do IntelliSense. Quando o serviço de linguagem está pronto para exibir uma lista de conclusão, ele chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> método no modo de texto. A exibição de texto, em seguida, chama de volta para o serviço de linguagem por usando métodos do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> objeto.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>|Permite a modificação do modo de exibição de texto usando o manipulador de comandos. A classe em que você implemente a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> também deve implementar a interface a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface. Recupera a exibição de texto a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> objeto consultando a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> objeto é passado para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> método. Deve haver um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> objeto para cada modo de exibição.|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|Intercepta comandos que o usuário digita na janela de código. Monitorar a saída do seu <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> implementação para fornecer informações de conclusão personalizados e exibir modificação<br /><br /> Para passar seus <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> objeto para o modo de exibição de texto, chamada <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>.|  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolver um serviço de linguagem herdado](../../extensibility/internals/developing-a-legacy-language-service.md)   
 [Lista de verificação: Criar um serviço de linguagem herdado](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)

