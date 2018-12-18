---
title: Serviços de linguagem e o Editor de núcleo | Microsoft Docs
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
- editors [Visual Studio SDK], legacy - language services
ms.assetid: e03199a6-ad5f-4075-bfba-8d36865112b7
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 503924f435dda2d4432c915f9566846f0f4dd964
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51727297"
---
# <a name="language-services-and-the-core-editor"></a>Serviços de linguagem e o Editor de núcleo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Editores do Visual Studio são frequentemente associados um serviço de linguagem. Entre outras coisas, um serviço de linguagem fornece coloração de sintaxe, preenchimento de declaração, IntelliSense e formatação de texto.  
  
## <a name="core-editors-and-document-data-objects"></a>Editores de núcleo e objetos de dados de documento  
 Quando você acessa o editor de núcleo, você não criar dados de documentos e objetos de exibição de documento. O IDE cria e controla esses dois objetos, e você obter identificadores para eles, fazendo as chamadas apropriadas em seu editor de implementação de fábrica.  
  
 Para obter mais informações, consulte [determinar qual Editor abre um arquivo em um projeto](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md).  
  
## <a name="language-services-and-the-core-editor"></a>Serviços de linguagem e o Editor de núcleo  
 Implementando um serviço de linguagem, você pode controlar como os dados são exibidos no modo de exibição de documento. Um serviço de linguagem fornece informações e o comportamento é específico para um determinado idioma, como o Visual C++. Quando você cria um buffer de texto e determinar a extensão de nome de arquivo para o documento que você está abrindo, o buffer de texto determina o serviço de idioma associado a essa extensão de nome de uma chave do registro HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Editors \\\Extensions {YourLanguageService GUID}. O VSPackage padrão ao carregar o procedimento, em seguida, carrega o VSPackage e uma instância do seu serviço de linguagem é criada.  
  
 Um serviço de linguagem básico é mostrado na ilustração a seguir.  
  
 ![Gráfico de modelo de serviço de linguagem](../extensibility/media/vslanguageservicemodel.gif "vsLanguageServiceModel")  
Principais objetos de serviço de editor e linguagem  
  
 O objeto de dados de documento para o editor de núcleo é chamado um buffer de texto e é representado pelo <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> objeto. O objeto de exibição de documento é chamado de uma exibição de texto e é representado pelo <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> objeto. Esses dois objetos trabalham juntos por meio do serviço de linguagem para fornecer uma exibição unificada do editor de núcleo. Informações de buffer de texto e o modo de exibição do texto exibido em uma janela de documento chamado de uma janela de código. O documento da janela de código é gerenciado por um Gerenciador de janela de código.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>   
 [Fornecer um contexto de serviço de linguagem, usando a API herdada](../extensibility/providing-a-language-service-context-by-using-the-legacy-api.md)   
 [IntelliSense de hospedagem](../extensibility/intellisense-hosting.md)   
 [Idiomas independentes](../extensibility/contained-languages.md)   
 [Desenvolver um serviço de linguagem herdado](../extensibility/internals/developing-a-legacy-language-service.md)

