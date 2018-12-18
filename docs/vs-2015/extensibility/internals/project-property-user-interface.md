---
title: Interface de usuário de propriedades do projeto | Microsoft Docs
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
- project properties [Visual Studio], user interface
- projects [Visual Studio SDK], properties UI
- project properties UI
ms.assetid: b6aec634-8533-476c-9ebd-36536a2288e2
caps.latest.revision: 17
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e295bff2f8398765f90c3fd537ca4f546208ce4b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51768288"
---
# <a name="project-property-user-interface"></a>Interface do usuário de propriedades do projeto
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um subtipo de projeto pode usar os itens no projeto **páginas de propriedade** caixa de diálogo como eles são fornecidos pelo projeto base, ocultar ou tornar somente leitura de controles e páginas inteiras como fornecidos ou adicionar páginas de subtipo específico de projeto para o **Páginas de propriedade** caixa de diálogo.  
  
## <a name="extending-the-project-property-dialog-box"></a>Estendendo a caixa de diálogo de propriedades do projeto  
 Um subtipo de projeto implementa extensores de automação e procurar objetos de configuração do projeto. Implementam esses extensores o <xref:EnvDTE.IFilterProperties> interface para tornar as propriedades específicas ocultos ou somente leitura. O **páginas de propriedade** honra de caixa de diálogo do projeto base, implementado pelo projeto base, a filtragem executada pelos extensores de automação.  
  
 O processo de estender uma **propriedade do projeto** caixa de diálogo é descrita a seguir:  
  
- O projeto base recupera os Extensores do subtipo de projeto, Implementando o <xref:EnvDTE80.IInternalExtenderProvider> interface. A procura, automação de projeto e objetos de procura de configuração de projeto do projeto base todos os implementam essa interface.  
  
- A implementação de <xref:EnvDTE80.IInternalExtenderProvider> para o objeto de navegação do projeto e o objeto de automação de projeto representante para o <xref:EnvDTE80.IInternalExtenderProvider> implementação do agregador de subtipo de projeto (ou seja, eles `QueryInterface` para <xref:EnvDTE80.IInternalExtenderProvider> sobre o <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> objeto de projeto).  
  
- O objeto de procura de configuração do projeto base também implementa <xref:EnvDTE80.IInternalExtenderProvider> ligar diretamente no extensor de automação do objeto de configuração do subtipo de projeto. Sua implementação delega para o <xref:EnvDTE80.IInternalExtenderProvider> interface implementada pelo agregador do subtipo de projeto.  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetProjectItem%2A>, implementadas pelo objeto de procura de configuração de projeto, retorna o <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> objeto.  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject.GetCfg%2A>, também é implementado pelo objeto de procura de configuração de projeto, retorna o <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg> objeto.  
  
- Um subtipo de projeto pode determinar as CATIDs apropriados para os diversos objetos extensíveis do projeto base no tempo de execução, recuperando o seguinte <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> valores:  
  
  -   <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>  
  
  -   <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>  
  
  -   <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>  
  
  Para determinar as CATIDs do escopo do projeto, o subtipo de projeto recupera as propriedades acima para <xref:Microsoft.VisualStudio.VSConstants.VSITEMID> do `VSITEMID``typedef`. Um subtipo de projeto talvez também queira controlar quais **páginas de propriedade** páginas da caixa de diálogo são exibidas para o projeto, configuração dependente e independentes da configuração. Alguns subtipos de projeto, talvez seja necessário remover páginas internas e adicionar a páginas específicas do subtipo de projeto. Para habilitar isso, as chamadas de projeto de cliente gerenciado a <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> método para as seguintes propriedades:  
  
- `VSHPROPID_PropertyPagesCLSIDList` — uma lista delimitada por ponto e vírgula de CLSIDs de páginas de propriedades de configuração independente.  
  
- `VSHPROPID_CfgPropertyPagesCLSIDList —` uma lista delimitada por ponto e vírgula de CLSIDs de páginas de propriedades de configuração dependente.  
  
  Porque o projeto de agregações de subtipo de <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> do objeto, ele pode substituir a definição dessas propriedades para controlar quais **páginas de propriedade** caixas de diálogo são exibidas. O subtipo de projeto pode recuperar essas propriedades do projeto base interno e, em seguida, adicionar ou remover CLSIDs conforme necessário.  
  
  Novas páginas de propriedades adicionadas por um subtipo de projeto são entregues a um objeto de procura de configuração de projeto da implementação do projeto base. Esse objeto de procura de configuração de projeto dá suporte a extensores de automação. Para obter mais informações sobre AutomationExtenders, consulte [implementando e usando extensores de automação](http://msdn.microsoft.com/library/0d5c218c-f412-4b28-ab0c-33a611f62356). As páginas de propriedades implementadas pela chamada de subtipo de projeto <xref:EnvDTE.Project.Extender%2A> para recuperar seu próprio objeto de procura de configuração de subtipo de projeto que estende o objeto de configuração de navegação do projeto base.  
  
## <a name="see-also"></a>Consulte também  
 <xref:EnvDTE.IFilterProperties>   
 [Caixa de diálogo páginas de propriedades](http://msdn.microsoft.com/en-us/4a3d34ac-ed03-45e8-ae60-a0e1aad300e4)

