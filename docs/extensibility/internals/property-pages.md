---
title: Páginas de propriedades | Microsoft Docs
description: Saiba mais sobre como trabalhar com Páginas de Propriedades para o novo tipo de projeto no SDK do Visual Studio, que permite aos usuários exibir e alterar as propriedades do projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
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
ms.openlocfilehash: 88ebf99ef2361a232c4a5c4c02b9a140155d66e9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903405"
---
# <a name="property-pages"></a>Páginas de propriedade
Os usuários podem exibir e alterar propriedades independentes e dependentes de configuração do projeto usando páginas de propriedades. Um **botão Páginas de** Propriedades  é habilitado na janela Propriedades ou na Gerenciador de Soluções de ferramentas para objetos que fornecem uma exibição de página de propriedades do objeto selecionado. As páginas de propriedades são criadas pelo ambiente e estão disponíveis para soluções e projetos. No entanto, eles também podem ser disponibilizados para itens de projeto que usam propriedades dependentes de configuração. Essa funcionalidade pode ser usada quando os arquivos dentro de um projeto exigem configurações diferentes de opção do compilador para serem compilados corretamente.

## <a name="using-property-pages"></a>Usando páginas de propriedades
 Se uma página de propriedades já estiver exibida e a seleção for mudada (por exemplo, de uma solução para um projeto), as informações exibidas nas páginas serão mudadas para exibir as propriedades da nova seleção. Se não houver propriedades no objeto que suportam páginas de propriedades, a página de propriedades será vazia.

 Se vários objetos forem selecionados, a página de propriedades exibirá a interseção de propriedades para todos os itens selecionados. Se o item selecionado não tiver propriedades  dependentes de configuração e o botão Páginas de Propriedades na barra de ferramentas Gerenciador de Soluções for clicado, o foco será janela Propriedades. Para obter mais informações relacionadas à janela Propriedades e à seleção, consulte [Estendendo propriedades](../../extensibility/internals/extending-properties.md).

 Se as propriedades são exibidas para vários objetos e você altera um valor em uma página de propriedades, todos os valores dos objetos são definidos como o novo valor, mesmo que eles fossem inicialmente diferentes e a página estivesse em branco quando as propriedades de um objeto individual eram exibidas.

 Há dois tipos gerais de caixas **de diálogo ProjectProperty Pages** disponíveis em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Na primeira, para Visual Basic, por exemplo, as páginas de propriedades são exibidas usando um formato de campo, conforme mostrado na captura de tela a seguir. Na segunda, mostrada posteriormente nesta seção, a página de propriedades hospeda uma grade de propriedades semelhante à encontrada na Janela Propriedades.

 ![Visual Basic de propriedades](../../extensibility/internals/media/vsvbproppages.gif "vsVBPropPages") Caixa de diálogo Páginas de Propriedades do Projeto com estrutura de árvore e formato de campo

 A estrutura de árvore na caixa de diálogo Páginas de Propriedades não é criada usando <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> . O ambiente, com base no nome de nível passado para ele pelas interfaces e <xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages> <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage> , o cria.

 Há apenas duas categorias de nível superior disponíveis em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Páginas de propriedades:

- Propriedades Comuns, que exibe informações independentes de configuração para o objeto ou objetos selecionados. Como resultado, quando uma das subcategorias Propriedades Comuns é selecionada, as opções Configuração, Plataforma e Gerenciador de Configurações na parte superior da caixa de diálogo não estão disponíveis.

- Propriedades de configuração, que contém informações dependentes de configuração relacionadas aos parâmetros Depuração, Otimização e Build para a solução ou o projeto.

  Não é possível criar nenhuma categoria de nível superior adicional, mas você pode optar por não exibir uma ou outra na implementação do `IVsPropertyPage` . Se, por exemplo, você não tiver nenhuma propriedade independente de configuração a ser exibida para um objeto, poderá optar por não exibir a categoria Propriedades Comuns. Você exibirá Propriedades comuns se for implementado do objeto browse do item e propriedades de Configuração quando implementar no objeto de configuração (o objeto que implementa `ISpecifyPropertyPages` `ISpecifyPropertyPages` , e `IVsCfg` `IVsProjectCfg` interfaces relacionadas).

  Cada categoria exibida em uma categoria de nível superior representa uma página de propriedades separada. As entradas de categoria e subcategoria disponíveis na caixa de diálogo são determinadas pela implementação de `ISpecifyPropertyPages` e `IVsPropertyPage` .

  `IDispatch` objetos para itens no contêiner de seleção que têm propriedades a serem exibidas nas páginas de propriedades implementam para enumerar uma `ISpecifyPropertyPages` lista de IDs de classe. As IDs de classe são passadas como variáveis `ISpecifyPropertyPages` para e são usadas para insinciar as páginas de propriedades. A lista de IDs de classe também é passada para para criar a `IVsPropertyPage` estrutura de árvore à esquerda da caixa de diálogo. Em seguida, as páginas de propriedades passam informações de volta para o objeto que implementa e preenche `IDispatch` as informações de cada `ISpecifyPropertyPages` página.

  As propriedades do objeto browse são recuperadas usando `IDispatch` para cada objeto no contêiner de seleção.

  Implementar em `Help::DisplayTopicFromF1Keyword` seu VSPackage fornece a funcionalidade para o botão Ajuda.

  Para obter mais informações, `IDispatch` consulte e na biblioteca `ISpecifyPropertyPages` MSDN.

  O segundo tipo de páginas de propriedade exibido nos exemplos hospeda um formulário da grade de propriedades, conforme mostrado na captura de tela a seguir.

  ![Páginas de propriedades do VC](../../extensibility/internals/media/vsvcproppages.gif "vsVCPropPages") Caixa de diálogo Páginas de Propriedades com grade de propriedades

  As interfaces `IVSMDPropertyBrowser` e (declaradas em vsmanaged.h) são usadas para criar e preencher a grade de propriedades em uma caixa de `IVSMDPropertyGrid` diálogo ou janela.

  A arquitetura de projetos mudou consideravelmente em versões anteriores do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Em particular, a noção de qual projeto está ativo foi alterada. No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , não há nenhum conceito de um projeto ativo. Em ambientes de desenvolvimento anteriores, o projeto ativo era o projeto que criava e implantava comandos padrão, independentemente do contexto. Agora, a solução controla e desmoraliza quais comandos de build e implantação se aplicam a quais projetos.

  O que era anteriormente um projeto ativo agora é capturado de uma das três maneiras diferentes:

- O projeto de inicialização

   Você pode especificar um projeto ou projetos na página de propriedades da solução que será iniciada quando o usuário pressionar F5 ou selecionar Executar no menu Build. Isso funciona de maneira semelhante ao projeto ativo antigo, no sentido de que seu nome é exibido Gerenciador de Soluções fonte em negrito.

   Você pode recuperar o projeto de inicialização como uma propriedade no modelo de automação chamando `DTE.Solution.SolutionBuild.StartupProjects` . Em um VSPackage, você chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> os <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> métodos ou . `IVsSolutionBuildManager` está disponível como um serviço pelo `QueryService` SID_SVsSolutionBuildManager. Para obter mais informações, consulte [Project Configuration Object and](../../extensibility/internals/project-configuration-object.md) Solution [Configuration](../../extensibility/internals/solution-configuration.md).

- Configuração de build de solução ativa

   [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] tem uma configuração de solução ativa, disponível no modelo de automação implementando `DTE.Solution.SolutionBuild.ActiveConfiguration` . Uma configuração de solução é uma coleção que contém uma configuração de projeto para cada projeto na solução (cada projeto pode ter várias configurações, em várias plataformas, com nomes diferentes). Para obter mais informações relacionadas às páginas de propriedades da solução, consulte [Configuração da solução](../../extensibility/internals/solution-configuration.md).

- Projeto selecionado no momento

   Implemente <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCurrentSelection%2A> o método para recuperar a hierarquia do projeto e o item de projeto ou itens selecionados. Na DTE, você usaria os `SelectedItems.SelectedItem.Project` `SelectedItems.SelectedItem.ProjectItem` métodos e . Há um código de exemplo sob esses títulos nos documentos [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] principais.

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage>
- [Gerenciando opções de configuração](../../extensibility/internals/managing-configuration-options.md)
- [Objeto de configuração de projeto](../../extensibility/internals/project-configuration-object.md)
- [Configuração da solução](../../extensibility/internals/solution-configuration.md)
