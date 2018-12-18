---
title: Propriedades e métodos estendidos por projeto subtipos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, extended methods
- project subtypes, extended properties
ms.assetid: 2b9833bf-8551-4ae1-93db-197ba645c65e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 23510ffbb42e0c0c37c07e0ee80ae15f99e5df00
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31132081"
---
# <a name="properties-and-methods-extended-by-project-subtypes"></a>Propriedades e métodos estendidos por subtipos de projeto
Um subtipo de projeto tem uma grande quantidade de energia para influenciar o comportamento do projeto porque ele é criado como um agregador de um projeto de base. Esta seção resume alguns dos recursos que podem ser aprimorados ou modificados por subtipos de projeto.  
  
## <a name="features-gained-by-aggregation"></a>Recursos obtidos pela agregação  
 A tabela a seguir resume a muitos dos métodos de agregação permite que os subtipos de projeto substituir em projetos de base.  
  
|Métodos substituídos pela agregação|Subtipo de projeto|  
|---------------------------------------|---------------------|  
|De <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>:<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetGuidProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetGuidProperty%2A>|Permite que um subtipo de projeto para<br /><br /> -Altere a legenda e o ícone do nó do projeto.<br />-Substituir o projeto completamente `Browse` objeto.<br />-Controle se o projeto pode ser renomeado.<br />-Ordem de classificação control.<br />-Contexto de usuário de controle para obter ajuda dinâmica.|  
|De <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>:<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetItemContext%2A>|Permite que um subtipo de projeto controlar quais serviços contextuais são fornecidos para designers e editores.|  
|De <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>:<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A><br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>|Permite que um subtipo de projeto para<br /><br /> -Participe de roteamento de comando para comandos do projeto.<br />-Adicionar, remover ou desabilitar comandos de ambiente de projeto e comandos ativos do Gerenciador de soluções.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>|Habilita o subtipo de projeto filtrar o que o usuário vê no **Adicionar Novo Item** caixa de diálogo.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGeneratorFactory>|Permite que um subtipo de projeto para<br /><br /> -Determine o gerador de padrão fornecido a uma extensão de arquivo.<br />-Mapear um nome de gerador legível humana para um objeto COM.|  
  
## <a name="properties-used-by-project-subtypes"></a>Propriedades usadas pelo projeto subtipos  
 O sistema de projeto base e o ambiente pode usar as propriedades de <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID> e <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2> enumerações detalhadas na tabela a seguir para habilitar um subtipo de projeto controlar vários recursos do sistema de projeto.  
  
|Propriedade VSHPROPID|Subtipo de projeto|  
|------------------------|---------------------|  
|`AddItemTemplatesGuid`|Permite que um subtipo de projeto controlar o conteúdo do **Adicionar Item** caixa de diálogo. O subtipo de projeto pode fornecer uma nova especificação de pastas de modelo, adicionar novos tipos de itens, remover itens existentes e reorganizar um subconjunto de itens do projeto base **Adicionar Item** caixa de diálogo.|  
|`PropertyPagesCLSIDList`|Permite que um subtipo de projeto Adicionar ou remover páginas de propriedades de configuração independente.|  
|`CfgPropertyPagesCLSIDList`|Permite que um subtipo de projeto Adicionar ou remover páginas de propriedades de configuração dependente.|  
|`ExtObjectCATID`|Permite que um subtipo de projeto fornecer um extensor de automação para o projeto ou item objetos Conhecendo o CATID de extensor. Por exemplo, um subtipo de projeto pode fornecer um personalizado `Project.Extender("<subtype>")` objeto.|  
|`BrowseObjectCATID`|Permite que um subtipo de projeto fornecer um extensor de automação para o `Browse` objeto Conhecendo o CATID de extensor. Por exemplo, um subtipo de projeto pode adicionar propriedades adicionais para o <xref:EnvDTE.Project.Properties%2A> coleção.|  
|`CfgBrowseObjectCATID`|Permite que um subtipo de projeto fornecer um extensor de automação para o objeto de procura de configuração de projeto. Por exemplo, um subtipo de projeto pode adicionar propriedades adicionais para o <xref:EnvDTE.Configuration.Properties%2A> coleção.|  
|`CfgExtObjectCATID`|Permite que um subtipo de projeto fornecer um extensor de automação para o objeto de configuração.|  
|`DefaultPlatformName`|Permite que um subtipo de projeto determinar o nome da plataforma para objetos de configuração do projeto.|  
  
 O projeto base fornece uma implementação padrão das propriedades acima. O projeto base obtém essas chamando `QueryInterface` para <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> no subtipo de projeto mais externo, permitindo o subtipo de projeto substituir a implementação das propriedades.  
  
## <a name="see-also"></a>Consulte também  
 [Design de subtipos de projeto](../../extensibility/internals/project-subtypes-design.md)