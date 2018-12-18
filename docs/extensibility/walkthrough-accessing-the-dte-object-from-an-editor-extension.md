---
title: 'Passo a passo: Acessando o objeto DTE de uma extensão do Editor | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - getting the DTE object
ms.assetid: c1f40bab-c6ec-45b0-8333-ea5ceb02a39d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8ed4343139b3e59dfba7adc71b1c91cdf01c13db
ms.sourcegitcommit: 56ae5032d99d948aae0548ae318ca2bae97ea962
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2018
ms.locfileid: "39586242"
---
# <a name="walkthrough-accessing-the-dte-object-from-an-editor-extension"></a>Passo a passo: Acessando o objeto DTE de uma extensão do editor
Em VSPackages, você pode obter o objeto DTE chamando o <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> método com o tipo do objeto DTE. Nas extensões do Managed Extensibility Framework (MEF), você pode importar <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> e, em seguida, chamar o <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> método com um tipo de <xref:EnvDTE.DTE>.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para seguir este passo a passo, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
  
## <a name="getting-the-dte-object"></a>Obtendo o objeto DTE  
  
### <a name="to-get-the-dte-object-from-the-serviceprovider"></a>Para obter o objeto DTE do provedor de serviços  
  
1.  Crie um projeto de VSIX em C# chamado `DTETest`. Adicione um modelo de item de classificação do Editor e denomine- `DTETest`. Para obter mais informações, consulte [criar uma extensão com um modelo de item editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).  
  
2.  Adicione as seguintes referências de assembly ao projeto:  
  
    -   EnvDTE  
  
    -   EnvDTE80  
  
    -   Microsoft.VisualStudio.Shell.Immutable.10.0  
  
3.  Vá para o *DTETest.cs* do arquivo e adicione o seguinte `using` diretivas:  
  
    ```csharp  
    using EnvDTE;  
    using EnvDTE80;  
    using Microsoft.VisualStudio.Shell;  
  
    ```  
  
4.  No `GetDTEProvider` classe, importar um <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>.  
  
    ```csharp  
    [Import]  
    internal SVsServiceProvider ServiceProvider = null;  
  
    ```  
  
5.  No método `GetClassifier()`, adicione o seguinte código.  
  
    ```csharp  
    DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));  
  
    ```  
  
6.  Se você tiver que usar o <xref:EnvDTE80.DTE2> interface, você pode converter o objeto DTE para ele.  
  
## <a name="see-also"></a>Consulte também  
 [Pontos de extensão de editor e o serviço de linguagem](../extensibility/language-service-and-editor-extension-points.md)