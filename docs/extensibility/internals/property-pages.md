---
title: Páginas de propriedades | Microsoft Docs
description: Saiba mais sobre como trabalhar com páginas de propriedades para o novo tipo de projeto no SDK do Visual Studio, que permite que os usuários exibam e alterem as propriedades do projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- configuration options, changing properties
- property pages
- property pages, changing configuration options
ms.assetid: b9b3e6e8-1e30-4c89-9862-330265dcf38c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f3e36960b35119434e56f075f622ae2513454dd6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061011"
---
# <a name="property-pages"></a>Páginas de propriedade
Os usuários podem exibir e alterar propriedades dependentes de configuração de projeto e independentes usando páginas de propriedades. Um botão **páginas de propriedades** é habilitado na janela **Propriedades** ou na barra de ferramentas Gerenciador de soluções para objetos que fornecem uma exibição de página de propriedades do objeto selecionado. As páginas de propriedades são criadas pelo ambiente e estão disponíveis para soluções e projetos. No entanto, eles também podem ser disponibilizados para itens de projeto que fazem uso de propriedades dependentes de configuração. Esse recurso pode ser usado quando arquivos dentro de um projeto exigem configurações de comutador de compilador diferentes para serem compilados corretamente.

## <a name="using-property-pages"></a>Usando páginas de propriedades
 Se uma página de propriedades já estiver sendo exibida e a seleção for alterada (por exemplo, de uma solução para um projeto), as informações exibidas nas páginas serão alteradas para exibir as propriedades da nova seleção. Se não houver nenhuma propriedade no objeto que ofereça suporte a páginas de propriedades, a página de propriedades estará vazia.

 Se vários objetos forem selecionados, a página de Propriedades exibirá a interseção de propriedades de todos os itens selecionados. Se o item selecionado não contiver propriedades dependentes de configuração e o botão **páginas de propriedades** na barra de ferramentas Gerenciador de soluções for clicado, o foco será alterado para o janela Propriedades. Para obter mais informações relacionadas ao janela Propriedades e à seleção, consulte [estendendo propriedades](../../extensibility/internals/extending-properties.md).

 Se as propriedades forem exibidas para vários objetos e você alterar um valor em uma página de propriedades, todos os valores dos objetos serão definidos para o novo valor, mesmo se forem inicialmente diferentes e a página ficar em branco quando as propriedades de um objeto individual forem exibidas.

 Há dois tipos gerais de caixas de diálogo de **páginas ProjectProperty** disponíveis no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Na primeira, para projetos Visual Basic, por exemplo, as páginas de propriedades são exibidas usando um formato de campo, conforme mostrado na captura de tela a seguir. No segundo, mostrado mais adiante nesta seção, a página de propriedades hospeda uma grade de propriedades semelhante àquela encontrada na janela Propriedades.

 ![Visual Basic páginas de propriedades](../../extensibility/internals/media/vsvbproppages.gif "vsVBPropPages") Caixa de diálogo páginas de propriedades do projeto com formato de campo e estrutura de árvore

 A estrutura de árvore na caixa de diálogo páginas de propriedades não é criada usando <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> . O ambiente, com base no nome de nível passado para ele pelo <xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages> e pelas <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage> interfaces, compila-o.

 Há apenas duas categorias de nível superior disponíveis em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] páginas de propriedades:

- Propriedades comuns, que exibe informações independentes de configuração para o objeto ou objetos selecionados. Como resultado, quando uma das subcategorias de propriedades comuns estiver selecionada, as opções configuração, plataforma e Configuration Manager na parte superior da caixa de diálogo não estarão disponíveis.

- Propriedades de configuração, que contêm informações dependentes de configuração relacionadas aos parâmetros de depuração, otimização e compilação para a solução ou o projeto.

  Não é possível criar nenhuma categoria adicional de nível superior, mas você pode optar por não exibir um ou outro na sua implementação do `IVsPropertyPage` . Se, por exemplo, você não tiver nenhuma propriedade independente de configuração para exibir um objeto, poderá optar por não exibir a categoria de propriedades comuns. Você exibirá Propriedades comuns se `ISpecifyPropertyPages` o for implementado no objeto de procura e nas propriedades de configuração do item quando você implementar `ISpecifyPropertyPages` no objeto de configuração (o objeto que implementa o `IVsCfg` , o e as `IVsProjectCfg` interfaces relacionadas).

  Cada categoria exibida em uma categoria de nível superior representa uma página de propriedades separada. As entradas de categoria e subcategoria disponíveis na caixa de diálogo são determinadas pela implementação do `ISpecifyPropertyPages` e do `IVsPropertyPage` .

  `IDispatch` objetos para itens no contêiner de seleção que têm propriedades a serem exibidas em páginas de propriedades implementam `ISpecifyPropertyPages` para enumerar uma lista de IDs de classe. As IDs de classe são passadas como variáveis para `ISpecifyPropertyPages` e são usadas para instanciar as páginas de propriedades. A lista de IDs de classe também é passada para `IVsPropertyPage` para criar a estrutura de árvore à esquerda da caixa de diálogo. As páginas de propriedades passam informações de volta para o `IDispatch` objeto que implementa `ISpecifyPropertyPages` e preenche as informações de cada página.

  As propriedades do objeto de procura são recuperadas usando `IDispatch` para cada objeto no contêiner de seleção.

  Implementar `Help::DisplayTopicFromF1Keyword` em seu VSPackage fornece a funcionalidade para o botão ajuda.

  Para obter mais informações, consulte `IDispatch` e `ISpecifyPropertyPages` na biblioteca MSDN.

  O segundo tipo de páginas de propriedades exibido nos exemplos hospeda uma forma da grade de propriedades, conforme mostrado na captura de tela a seguir.

  ![Páginas de propriedades do vc](../../extensibility/internals/media/vsvcproppages.gif "vsVCPropPages") Caixa de diálogo páginas de propriedade com grade de propriedades

  As interfaces `IVSMDPropertyBrowser` e `IVSMDPropertyGrid` (declaradas em vsmanaged. h) são usadas para criar e preencher a grade de propriedades dentro de uma caixa de diálogo ou janela.

  A arquitetura dos projetos mudou consideravelmente das versões anteriores do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Em particular, a noção de qual projeto está ativo foi alterada. No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , não há nenhum conceito de projeto ativo. Em ambientes de desenvolvimento anteriores, o projeto ativo era o projeto que cria e implanta comandos por padrão, independentemente do contexto. Agora, a solução controla e arbitra os comandos de compilação e implantação que se aplicam a quais projetos.

  O que antes era um projeto ativo agora é capturado de uma das três maneiras diferentes:

- O projeto de inicialização

   Você pode especificar um projeto ou projetos da página de propriedades da solução que será iniciada quando o usuário pressionar F5 ou selecionar executar no menu Compilar. Isso funciona de maneira semelhante ao antigo projeto ativo, no sentido de que seu nome é exibido em Gerenciador de Soluções com fonte em negrito.

   Você pode recuperar o projeto de inicialização como uma propriedade no modelo de automação chamando `DTE.Solution.SolutionBuild.StartupProjects` . Em um VSPackage, você chama os <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> métodos ou <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> . `IVsSolutionBuildManager` está disponível como um serviço por `QueryService` SID_SVsSolutionBuildManager. Para obter mais informações, consulte configuração do [objeto de configuração do projeto](../../extensibility/internals/project-configuration-object.md) e [solução](../../extensibility/internals/solution-configuration.md).

- Configuração de Build de solução ativa

   [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] tem uma configuração de solução ativa, disponível no modelo de automação implementando `DTE.Solution.SolutionBuild.ActiveConfiguration` . Uma configuração de solução é uma coleção que contém uma configuração de projeto para cada projeto na solução (cada projeto pode ter várias configurações, em várias plataformas, com nomes diferentes). Para obter mais informações relacionadas às páginas de propriedades da solução, consulte [configuração da solução](../../extensibility/internals/solution-configuration.md).

- Projeto selecionado no momento

   Implemente o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCurrentSelection%2A> método para recuperar a hierarquia do projeto e o item do projeto ou itens selecionados. No DTE, você usaria os `SelectedItems.SelectedItem.Project` métodos e `SelectedItems.SelectedItem.ProjectItem` . Há um código de exemplo sob esses cabeçalhos nos documentos principais [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage>
- [Gerenciando opções de configuração](../../extensibility/internals/managing-configuration-options.md)
- [Objeto de configuração de projeto](../../extensibility/internals/project-configuration-object.md)
- [Configuração da solução](../../extensibility/internals/solution-configuration.md)
