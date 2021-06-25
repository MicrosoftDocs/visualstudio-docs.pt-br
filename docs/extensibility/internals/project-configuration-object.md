---
title: Objeto de configuração do projeto | Microsoft Docs
description: Saiba como o objeto de configuração do projeto gerencia a exibição de informações de configuração para a interface do usuário.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project configurations, object
- objects, project configuration
ms.assetid: 877756c9-4261-43d9-9f32-51bf06b4219f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 15a999f78d017c76ee021f86d81cb611310d079d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899856"
---
# <a name="project-configuration-object"></a>Objeto de configuração de projeto
O objeto de configuração do projeto gerencia a exibição de informações de configuração para a interface do usuário.

 ![Configuração de projeto do Visual Studio](../../extensibility/internals/media/vsprojectcfg.gif "vsProjectCfg") Páginas de propriedades de configuração do projeto

 O provedor de configuração do projeto gerencia as configurações do projeto. O ambiente e outros pacotes, para obter acesso e recuperar informações sobre as configurações de um projeto, chame as interfaces anexadas ao objeto de provedor de configuração de projeto.

> [!NOTE]
> Você não pode criar ou editar arquivos de configuração de solução programaticamente. É necessário usar `DTE.SolutionBuilder`. Consulte [configuração da solução](../../extensibility/internals/solution-configuration.md) para obter mais informações.

 Para publicar um nome de exibição a ser usado na interface do usuário de configuração, seu projeto deve implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_DisplayName%2A> . O ambiente chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A> , que retorna uma lista de `IVsCfg` ponteiros que você pode usar para obter os nomes de exibição para as informações de configuração e plataforma a serem listadas na interface do usuário do ambiente. A configuração e a plataforma ativas são determinadas pela configuração do projeto armazenada na configuração da solução ativa. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager.FindActiveProjectCfg%2A> método pode ser usado para recuperar a configuração do projeto ativo.

 O <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> objeto pode, opcionalmente, ser implementado no <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> objeto com o <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProviderEventsHelper> objeto para permitir que você recupere um `IVsProjectCfg2` objeto com base no nome de configuração do projeto canônico.

 Outra maneira de fornecer o ambiente e outros projetos com acesso às configurações do projeto é que os projetos forneçam uma implementação do `IVsCfgProvider2::GetCfgs` método para retornar um ou mais objetos de configuração. Os projetos também podem implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> , que herda de `IVsProjectCfg` e, dessa forma `IVsCfg` , fornecer informações específicas de configuração. <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> oferece suporte a plataformas e funcionalidade para adicionar, excluir e renomear configurações de projeto.

> [!NOTE]
> Como o Visual Studio não está mais limitado a dois tipos de configuração, o código que processa as configurações não deve ser escrito com suposições sobre o número de configurações, nem deve ser escrito com a suposição de que um projeto que tenha apenas uma configuração seja necessariamente a depuração ou o varejo. Isso torna o uso de <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsReleaseOnly%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg.get_IsDebugOnly%2A> obsoleto.

 Chamando `QueryInterface` no objeto retornado de `IVsGetCfgProvider::GetCfgProvider` recuperações `IVsCfgProvider2` . Se `IVsGetCfgProvider` não for encontrado chamando `QueryInterface` no `IVsProject3` objeto Project, você poderá acessar o objeto do provedor de configuração chamando `QueryInterface` no objeto de navegador raiz da hierarquia para o objeto retornado para `IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_BrowseObject)` , ou através de um ponteiro para o provedor de configuração retornado para `IVsHierarchy::GetProperty(VSITEM_ROOT, VSHPROPID_ConfigurationProvider)` .

 `IVsProjectCfg2` fornece principalmente acesso a objetos de gerenciamento de compilação, depuração e implantação e permite aos projetos a liberdade de agrupar saídas. Os métodos de `IVsProjectCfg` e `IVsProjectCfg2` podem ser usados para implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> o para gerenciar o processo de compilação e os <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup> ponteiros para os grupos de saída de uma configuração.

 O projeto deve retornar o mesmo número de grupos para cada configuração que ele suporta, embora o número de saídas contidas em um grupo possa variar de configuração para configuração. Os grupos também devem ter as mesmas informações de identificador (nome canônico, nome de exibição e informações de grupo) da configuração para a configuração em um projeto. Para obter mais informações, consulte [configuração de projeto para saída](../../extensibility/internals/project-configuration-for-output.md).

 Para habilitar a depuração, suas configurações devem implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> . `IVsDebuggableProjectCfg` é uma interface opcional implementada por projetos para permitir que o depurador inicie uma configuração e seja implementado no objeto de configuração com `IVsCfg` e `IVsProjectCfg` . O ambiente o chama quando o usuário opta por iniciar o depurador pressionando F5.

 `ISpecifyPropertyPages` e `IDispatch` são usados em conjunto com páginas de propriedades para recuperar e exibir informações dependentes de configuração para o usuário. Para obter mais informações, consulte [páginas de propriedades](../../extensibility/internals/property-pages.md).

## <a name="see-also"></a>Confira também
- [Gerenciando opções de configuração](../../extensibility/internals/managing-configuration-options.md)
- [Configuração de projeto para compilar](../../extensibility/internals/project-configuration-for-building.md)
- [Configuração de projeto para saída](../../extensibility/internals/project-configuration-for-output.md)
- [Páginas de propriedade](../../extensibility/internals/property-pages.md)
- [Configuração da solução](../../extensibility/internals/solution-configuration.md)
