---
title: Parâmetros de contexto | Microsoft Docs
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
- wizards, context parameters
- context parameters
ms.assetid: 1a062dcb-8a8f-40dd-bea9-3d10f9448966
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: f9d9c1d6c78bb026fe0e26c99bbf712d4412ebd5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51773204"
---
# <a name="context-parameters"></a>Parâmetros de contexto
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

No [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ambiente de desenvolvimento integrado (IDE), você pode adicionar assistentes para a **novo projeto**, **Adicionar Novo Item**, ou **adicionar Sub projeto** caixas de diálogo. Os assistentes adicionados estão disponíveis na **arquivo** menus ou clicando em um projeto no **Gerenciador de soluções**. O IDE passa parâmetros de contexto para a implementação do assistente. Os parâmetros de contexto definem o estado do projeto quando o IDE chama o assistente.  
  
 O IDE inicia assistentes, definindo o <xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION> sinalizador na chamada do IDE para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A> método para o projeto. Quando definido, o projeto deve fazer com que o `IVsExtensibility::RunWizardFile` método a ser executado usando o nome registrado do assistente ou o GUID e outros parâmetros de contexto que o IDE passa para ele.  
  
## <a name="context-parameters-for-new-project"></a>Parâmetros de contexto para o novo projeto  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`WizardType`|Tipo de assistente registrado (<xref:EnvDTE.Constants.vsWizardNewProject>) ou o GUID que indica o tipo de assistente. No [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] implementação, o GUID para o assistente é {0F90E1D0-4999-11D1-B6D1-00A0C90F2744}.|  
|`ProjectName`|Uma cadeia de caracteres que é a única [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] nome do projeto.|  
|`LocalDirectory`|Localização local de trabalho de arquivos de projeto.|  
|`InstallationDirectory`|Caminho do diretório a [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] é a instalação.|  
|`FExclusive`|Sinalizador booliano que indica que o projeto deve feche soluções abertas.|  
|`SolutionName`|Nome do arquivo de solução sem a parte do diretório ou a extensão. sln. O nome do arquivo. suo também é criado usando `SolutionName`. Quando esse argumento não for uma cadeia de caracteres vazia, o assistente usa <xref:EnvDTE._Solution.Create%2A> antes de adicionar o projeto com <xref:EnvDTE._Solution.AddFromTemplate%2A>. Se esse nome é uma cadeia de caracteres vazia, use <xref:EnvDTE._Solution.AddFromTemplate%2A> sem chamar <xref:EnvDTE._Solution.Create%2A>.|  
|`Silent`|Valor booliano que indica se o assistente deve ser executado silenciosamente como se **terminar** foram clicados (`TRUE`).|  
  
## <a name="context-parameters-for-add-new-item"></a>Parâmetros de contexto para adicionar novo Item  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`WizardType`|Tipo de assistente registrado (<xref:EnvDTE.Constants.vsWizardAddItem>) ou o GUID que indica o tipo de assistente. No [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] implementação, o GUID para o assistente é {0F90E1D1-4999-11D1-B6D1-00A0C90F2744}.|  
|`ProjectName`|Uma cadeia de caracteres que é a única [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] nome do projeto.|  
|`ProjectItems`|Localização local que contém os arquivos de projeto de trabalho.|  
|`ItemName`|Nome do item a ser adicionado. Esse nome é o nome de arquivo ou o nome do arquivo que o usuário digita a partir de **adicionar itens** caixa de diálogo. O nome baseia-se os sinalizadores definidos no arquivo. vsdir. O nome pode ser um valor nulo.|  
|`InstallationDirectory`|Caminho do diretório a [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] é a instalação.|  
|`Silent`|Valor booliano que indica se o assistente deve ser executado silenciosamente como se **terminar** foram clicados (`TRUE`).|  
  
## <a name="context-parameters-for-add-sub-project"></a>Parâmetros de contexto para adicionar Sub projeto  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`WizardType`|Tipo de assistente registrado (<xref:EnvDTE.Constants.vsWizardAddSubProject>) ou o GUID que indica o tipo de assistente. No [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] implementação, o GUID para o assistente é {0F90E1D2-4999-11D1-B6D1-00A0C90F2744}.|  
|`ProjectName`|Uma cadeia de caracteres que é a única [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] nome do projeto.|  
|`ProjectItems`|Ponteiro para o `ProjectItems` coleção em que o assistente opera. Esse ponteiro é passado para o assistente com base na seleção de hierarquia do projeto. Um usuário normalmente seleciona uma pasta na qual colocar o item e, em seguida, chama o projeto **Adicionar Item** caixa de diálogo.|  
|`LocalDirectory`|Localização local de trabalho de arquivos de projeto.|  
|`ItemName`|Nome do item a ser adicionado. Esse nome é o nome de arquivo ou o nome do arquivo que o usuário digita a partir de **adicionar itens** caixa de diálogo. O nome baseia-se os sinalizadores definidos no arquivo. vsdir. O nome pode ser um valor nulo.|  
|`InstallationDirectory`|Caminho do diretório a [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] é a instalação.|  
|`Silent`|Valor booliano que indica se o assistente deve ser executado silenciosamente como se **terminar** foram clicados (`TRUE`).|  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2>   
 [Parâmetros personalizados](../../extensibility/internals/custom-parameters.md)   
 [Assistentes](../../extensibility/internals/wizards.md)   
 [Assistente (. Arquivo vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)   
 [Parâmetros de contexto para iniciar assistentes](http://msdn.microsoft.com/library/051a10f4-9e45-4604-b344-123044f33a24)

