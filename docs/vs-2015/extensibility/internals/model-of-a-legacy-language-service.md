---
title: Modelo de um serviço de linguagem herdado | Microsoft Docs
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
- language services, model
ms.assetid: d8ae1c0c-ee3d-4937-a581-ee78d0499793
caps.latest.revision: 21
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 76838d6beb5d24f7586ddd44f7bd5400dec4f355
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51795174"
---
# <a name="model-of-a-legacy-language-service"></a>Modelo de um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um serviço de linguagem define os elementos e recursos para um idioma específico e é usado para fornecer o editor com informações específicas para esse idioma. Por exemplo, o editor precisa saber os elementos e as palavras-chave da linguagem para dar suporte a coloração de sintaxe.  
  
 O serviço de linguagem trabalha junto com o buffer de texto gerenciado pelo editor e o modo de exibição que contém o editor. O Microsoft IntelliSense **informações rápidas** opção é um exemplo de um recurso fornecido por um serviço de linguagem.  
  
## <a name="a-minimal-language-service"></a>Um serviço de linguagem mínima  
 O serviço de linguagem mais básico contém os dois objetos a seguir:  
  
- O *serviço de linguagem* implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> interface. Um serviço de linguagem tem informações sobre a linguagem, incluindo seu nome, extensões de nome de arquivo, o Gerenciador de janela de código e colorizador.  
  
- O *colorizador* implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> interface.  
  
  O desenho conceitual a seguir mostra um modelo de um serviço de linguagem básica.  
  
  ![Gráfico de modelo de serviço de linguagem](../../extensibility/media/vslanguageservicemodel.gif "vsLanguageServiceModel")  
  Modelo de serviço de linguagem básica  
  
  Os hosts de janela de documento a *exibição de documento* do editor, neste caso, o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] editor de núcleo. O modo de exibição de documento e o buffer de texto são de propriedade pelo editor. Esses objetos funcionam com [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] por meio de uma janela de documento especializado chamado um *janela de código*. A janela de código está contida em um <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> objeto que é criado e controlado pelo IDE.  
  
  Quando um arquivo com uma determinada extensão é carregado, o editor localiza o serviço de idioma associado a essa extensão e passa para ele a janela de código chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> método. O serviço de linguagem retorna um *Gerenciador de janelas de código*, que implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> interface.  
  
  A tabela a seguir fornece uma visão geral dos objetos no modelo.  
  
|Componente|Objeto|Função|  
|---------------|------------|--------------|  
|Buffer de texto|<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>|Um fluxo de texto Unicode de leitura/gravação. É possível para usar outras codificações de texto.|  
|Janela de código|<xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>|Uma janela de documento que contém um ou mais modos de exibição de texto. Quando [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] está no modo de interface de documentos múltiplos (MDI), a janela de código é um filho MDI.|  
|Exibição de texto|<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>|Uma janela que permite que o usuário navegar e exibir o texto usando o teclado e mouse. Uma exibição de texto é exibida ao usuário como um editor. Você pode usar modos de exibição de texto em janelas do editor comum, a janela de saída e a janela imediata. Além disso, você pode configurar um ou mais modos de exibição de texto dentro de uma janela de código.|  
|Gerenciador de texto|Gerenciado pelo <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> de serviço, de que você obtenha um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager> ponteiro|Um componente que mantém informações comuns compartilhadas por todos os componentes descritos anteriormente.|  
|serviço de linguagem|Implementação dependente; implementa <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>|Um objeto que fornece o editor com informações específicas de linguagem, como realce de sintaxe, preenchimento de declaração e correspondência de chaves.|  
  
## <a name="see-also"></a>Consulte também  
 [Dados de documentos e exibição de documentos em editores personalizados](../../extensibility/document-data-and-document-view-in-custom-editors.md)

