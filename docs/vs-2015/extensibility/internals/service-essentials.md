---
title: Conceitos básicos do serviço | Microsoft Docs
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
- services, essentials
ms.assetid: fbe84ad9-efe1-48b1-aba3-b50b90424d47
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 90cec13c403194c70b9d44cff349b53495a0e160
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51776454"
---
# <a name="service-essentials"></a>Conceitos básicos do serviço
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um serviço é um contrato entre dois VSPackages. Um VSPackage fornece um conjunto específico de interfaces para outro VSPackage consumir. [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] é uma coleção de VSPackages que fornece serviços a outros VSPackages.  
  
 Por exemplo, você pode usar o serviço de SVsActivityLog para obter uma interface IVsActivityLog, que pode ser usado para gravar no log de atividades. Para obter mais informações, consulte [como: usar o Log de atividades](../../extensibility/how-to-use-the-activity-log.md).  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] também fornece alguns serviços internos que não estão registrados. Os VSPackages pode substituir internos ou outros serviços, fornecendo uma substituição de serviço. Somente um serviço de substituição é permitida para qualquer serviço.  
  
 Os serviços não têm nenhuma capacidade de descoberta. Portanto, você deve saber o identificador de serviço (SID) de um serviço que você deseja consumir, e você deve saber quais interfaces que ele fornece. A documentação de referência para o serviço fornece essas informações.  
  
-   Os VSPackages que fornecem serviços são chamados de provedores de serviço.  
  
-   Serviços que são fornecidos a outros VSPackages são chamados de serviços globais.  
  
-   Serviços que estão disponíveis somente para o VSPackage que implementa-los, ou qualquer objeto que ele cria, são chamados de serviços locais.  
  
-   Serviços que substituir serviços internos ou serviços fornecidos por outros pacotes, são chamados de substituições de serviço.  
  
-   Serviços ou substituições de serviço, são carregadas sob demanda, ou seja, o provedor de serviço é carregado quando o serviço que fornece, é solicitado por outro VSPackage.  
  
-   Para dar suporte a carregamento sob demanda, um provedor de serviço registra seus serviços globais com [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Para obter mais informações, consulte [Registrando serviços](../../misc/registering-services.md).  
  
-   Depois de obter um serviço, use [QueryInterface](http://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) (código não gerenciado) ou conversão (código gerenciado) para obter a interface desejada, por exemplo:  
  
    ```vb  
    TryCast(GetService(GetType(SVsActivityLog)), IVsActivityLog)  
    ```  
  
    ```csharp  
    GetService(typeof(SVsActivityLog)) as IVsActivityLog;  
  
    ```  
  
-   Código gerenciado se refere a um serviço por seu tipo, enquanto que o código não gerenciado se refere a um serviço pelo seu GUID.  
  
-   Quando [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] carrega um VSPackage, ele passa um provedor de serviços para o VSPackage para fornecer o acesso de VSPackage aos serviços globais. Isso é chamado de "localização" VSPackage.  
  
-   Os VSPackages pode ser provedores de serviço para os objetos que eles criam. Por exemplo, um formulário pode enviar uma solicitação para um serviço de cor ao seu quadro, que pode passar a solicitação [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
-   Objetos gerenciados que estão profundamente aninhados ou não foi localizados, podem chamar <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> para acesso direto aos serviços globais. Para obter mais informações, consulte [como: usar GetGlobalService](../../misc/how-to-use-getglobalservice.md).  
  
## <a name="see-also"></a>Consulte também  
 [Lista de serviços disponíveis](../../extensibility/internals/list-of-available-services.md)   
 [Usar e fornecer serviços](../../extensibility/using-and-providing-services.md)   
 [Conversões cast e conversões de tipo](http://msdn.microsoft.com/library/568df58a-d292-4b55-93ba-601578722878)   
 [Conversão](http://msdn.microsoft.com/library/3dbeb06e-2f4b-4693-832d-624bc8ec95de)

