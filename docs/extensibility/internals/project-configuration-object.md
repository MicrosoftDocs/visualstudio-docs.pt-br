---
title: Objeto de configuração do projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project configurations, object
- objects, project configuration
ms.assetid: 877756c9-4261-43d9-9f32-51bf06b4219f
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 7385a5f7768a57fd1a3d9688df152fd60a1ea130
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31136023"
---
# <a name="project-configuration-object"></a>Objeto de configuração de projeto
O objeto de configuração de projeto gerencia a exibição de informações de configuração para a interface do usuário.  
  
 ![Configuração de projeto do Visual Studio](../../extensibility/internals/media/vsprojectcfg.gif "vsProjectCfg")  
Páginas de propriedades de configuração de projeto  
  
 O provedor de configuração de projeto gerencia as configurações do projeto. O ambiente e outros pacotes, para acessar e recuperar informações sobre configurações do projeto, chame as interfaces anexadas ao objeto de provedor de configuração de projeto.  
  
> [!NOTE]
>  Você não pode criar ou editar arquivos de configuração de solução programaticamente. Você deve usar `DTE.SolutionBuilder`. Consulte [configuração de solução](../../extensibility/internals/solution-configuration.md) para obter mais informações.  
  
 Para publicar um nome para exibição a ser usado na configuração de interface do usuário, o projeto deve implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_DisplayName%2A>. O ambiente chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A>, que retorna uma lista de `IVsCfg` ponteiros que você pode usar para obter os nomes de exibição para as informações de configuração e plataforma seja listado na interface de usuário do ambiente. A plataforma e a configuração ativa são determinados pela configuração do projeto armazenada na configuração de solução ativa. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager.FindActiveProjectCfg%2A> método pode ser usado para recuperar a configuração do projeto ativo.  
  
 O <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> objeto opcionalmente pode ser implementado no <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> do objeto com o <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProviderEventsHelper> objeto para permitir que você recupere um `IVsProjectCfg2` objeto com base no nome de configuração do projeto canônico.  
  
 É outra maneira de fornecer o ambiente e outros projetos acesso às configurações de projeto para projetos fornecer uma implementação de `IVsCfgProvider2::GetCfgs` método para retornar um ou mais objetos de configuração. Os projetos também podem implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>, que herda de `IVsProjectCfg` e, portanto, de `IVsCfg`, para fornecer informações específicas de configuração. <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> dá suporte a plataformas e funcionalidade para adicionar, excluir e renomear as configurações do projeto.  
  
> [!NOTE]
>  Desde que o Visual Studio não está mais limitado a dois tipos de configuração, o código que processa as configurações não deve ser escrito com suposições sobre o número de configurações, nem deve ser escrito com a suposição de que um projeto que tem apenas um configuração é necessariamente depuração ou varejo. Isso torna o uso de <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsReleaseOnly%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsDebugOnly%2A> obsoleto.  
  
 Chamando `QueryInterface` no objeto retornado de`IVsGetCfgProvider::GetCfgProvider` recupera `IVsCfgProvider2`. Se `IVsGetCfgProvider` não foi encontrado chamando `QueryInterface` no `IVsProject3` objeto de projeto, você pode acessar o objeto de provedor de configuração chamando `QueryInterface` no objeto de navegador de raiz de hierarquia para o objeto retornado para `IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_BrowseObject)`, ou por meio um ponteiro para o provedor de configuração retornado para `IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_ConfigurationProvider)`.  
  
 `IVsProjectCfg2` principalmente fornece acesso para compilar, depurar e objetos de gerenciamento de implantação e permite que os projetos a liberdade de grupo de saídas. Os métodos de `IVsProjectCfg` e `IVsProjectCfg2` podem ser usados para implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> para gerenciar o processo de compilação e <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup> ponteiros para os grupos de saída de uma configuração.  
  
 O projeto deve retornar o mesmo número de grupos para cada configuração que ele oferece suporte, embora o número de saídas contido dentro de um grupo pode variar para cada configuração. Os grupos também devem ter as mesmas informações de identificador (nome canônico, nome de exibição e informações de grupo) de configuração em um projeto. Para obter mais informações, consulte [configuração do projeto para a saída](../../extensibility/internals/project-configuration-for-output.md).  
  
 Para habilitar a depuração, as configurações devem implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>. `IVsDebuggableProjectCfg` é uma interface opcional implementada por projetos para permitir que o depurador a iniciar uma configuração e é implementado no objeto de configuração com `IVsCfg` e `IVsProjectCfg`. O ambiente chama quando o usuário opta por iniciar o depurador pressionando F5.  
  
 `ISpecifyPropertyPages` e `IDispatch` são usados em conjunto com as páginas de propriedade para recuperar e exibir as informações de configuração dependente para o usuário. Para obter mais informações, consulte [páginas de propriedade](../../extensibility/internals/property-pages.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar opções de configuração](../../extensibility/internals/managing-configuration-options.md)   
 [Configuração de projeto para criação](../../extensibility/internals/project-configuration-for-building.md)   
 [Configuração de projeto para saída](../../extensibility/internals/project-configuration-for-output.md)   
 [Páginas de propriedade](../../extensibility/internals/property-pages.md)   
 [Configuração da solução](../../extensibility/internals/solution-configuration.md)