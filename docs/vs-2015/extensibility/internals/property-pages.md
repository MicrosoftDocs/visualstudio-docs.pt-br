---
title: Páginas de propriedades | Microsoft Docs
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
- configuration options, changing properties
- property pages
- property pages, changing configuration options
ms.assetid: b9b3e6e8-1e30-4c89-9862-330265dcf38c
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 74da0df2939b08615f3a659dfca70b1cea0e495d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51759854"
---
# <a name="property-pages"></a>Páginas de propriedade
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Os usuários podem exibir e alterar propriedades de configuração dependente de e - independentes de projeto usando páginas de propriedade. Um **páginas de propriedades** botão está habilitado na **propriedades** janela ou na barra de ferramentas do Gerenciador de soluções para objetos que fornecem um modo de exibição de página de propriedade do objeto selecionado. Páginas de propriedades são criadas pelo ambiente e estão disponíveis para soluções e projetos. Eles podem, no entanto, também ser disponibilizados para itens de projeto que fazem usam de propriedades de configuração dependente. Esse recurso pode ser usado quando os arquivos dentro de um projeto exigem as configurações do comutador de compilador diferente ser compilado corretamente.  
  
## <a name="using-property-pages"></a>Usando páginas de propriedade  
 Se uma página de propriedades já é exibida e a seleção é alterada (por exemplo, de uma solução para um projeto), as informações exibidas nas páginas de alterações para exibir as propriedades para a nova seleção. Se não houver nenhuma propriedade no objeto que dão suporte a páginas de propriedades, a página de propriedades está vazia.  
  
 Se forem selecionados vários objetos, a página de propriedades exibe a interseção de propriedades para todos os itens selecionados. Se o item selecionado não contém propriedades dependentes de configuração e o **páginas de propriedade** na barra de ferramentas do Gerenciador de soluções é clicada, o foco muda para a janela Propriedades. Para obter mais informações relativas à janela Propriedades e seleção, consulte [estendendo propriedades](../../extensibility/internals/extending-properties.md).  
  
 Se as propriedades são exibidas para vários objetos e você alterar um valor em uma página de propriedade, todos os valores para os objetos são definidos para o novo valor, mesmo se eles foram inicialmente diferentes e a página estava em branco quando as propriedades de um objeto individuais foram exibidas.  
  
 Há dois tipos gerais de **páginas ProjectProperty** caixas de diálogo disponíveis no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. No primeiro, para projetos do Visual Basic, por exemplo, as páginas de propriedade são exibidas usando um formato de campo, conforme mostrado na seguinte captura de tela. Na segunda, mostrado posteriormente nesta seção, a propriedade hosts página uma grade de propriedades semelhante àquela encontrada na janela Propriedades.  
  
 ![Páginas de propriedades do Visual Basic](../../extensibility/internals/media/vsvbproppages.gif "vsVBPropPages")  
Caixa de diálogo páginas de propriedades de projeto com a estrutura de árvore e o formato do campo  
  
 A estrutura de árvore na caixa de diálogo páginas de propriedade não é criada usando <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>. O ambiente, com base no nível nome passado para ele pela <xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages> e o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage> interfaces, compila-lo.  
  
 Há apenas duas categorias de nível superior disponíveis no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] páginas de propriedades:  
  
- Propriedades comuns, que exibe informações de configuração independente para o objeto ou objetos selecionados. Como resultado, quando uma das subcategorias de propriedades comuns é selecionada, as opções de configuração, plataforma e do Configuration Manager na parte superior da caixa de diálogo não estão disponíveis.  
  
- Propriedades de configuração, que contém informações de configuração dependente relacionadas aos parâmetros de compilação, otimização e depuração para a solução ou projeto.  
  
  Não é possível criar quaisquer categorias adicionais de nível superior, mas você pode optar por não exibir uma ou outra em sua implementação de `IVsPropertyPage`. Se, por exemplo, você não tiver todas as propriedades de configuração independente a ser exibida para um objeto, você pode optar por não exibir a categoria de propriedades comuns. Exibir propriedades comuns, se `ISpecifyPropertyPages` é implementado de objeto de procura do item e as propriedades de configuração quando você implementa `ISpecifyPropertyPages` no objeto de configuração (o objeto que implementa `IVsCfg`, `IVsProjectCfg`e relacionados interfaces).  
  
  Cada categoria exibida em uma categoria de alto nível representa uma página de propriedades separadas. Entradas de categoria e subcategoria disponíveis na caixa de diálogo são determinadas pela sua implementação de `ISpecifyPropertyPages` e `IVsPropertyPage`.  
  
  `IDispatch` objetos para itens no contêiner de seleção que têm propriedades a serem exibidas na implementação de páginas de propriedade `ISpecifyPropertyPages` para enumerar uma lista de IDs de classe. As IDs de classe são passadas como variáveis a serem `ISpecifyPropertyPages` e são usados para instanciar as páginas de propriedades. A lista de IDs de classe também é passada para `IVsPropertyPage` para criar a estrutura de árvore à esquerda da caixa de diálogo. As páginas de propriedades, em seguida, passe informações de volta para o `IDispatch` objeto que implementa `ISpecifyPropertyPages` e preenche as informações para cada página.  
  
  As propriedades do objeto de navegação são recuperadas usando `IDispatch` para cada objeto no contêiner de seleção.  
  
  Implementando `Help::DisplayTopicFromF1Keyword` no VSPackage oferece a funcionalidade para o botão Ajuda.  
  
  Para obter mais informações, consulte `IDispatch` e `ISpecifyPropertyPages`na biblioteca MSDN.  
  
  O segundo tipo de páginas de propriedades exibida nos hosts amostras uma forma de grade de propriedades, conforme mostrado na seguinte captura de tela.  
  
  ![Páginas de propriedade do VC](../../extensibility/internals/media/vsvcproppages.gif "vsVCPropPages")  
  Caixa de diálogo páginas de propriedades com a grade de propriedades  
  
  As interfaces `IVSMDPropertyBrowser` e `IVSMDPropertyGrid` (declarado em vsmanaged.h) são usados para criar e preencher a grade de propriedades dentro de uma caixa de diálogo ou janela.  
  
  A arquitetura de projetos foi alterado consideravelmente das versões anteriores do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Em particular, a noção de qual projeto está ativa foi alterado. No [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], não há nenhum conceito de um projeto ativo. Em ambientes de desenvolvimento anteriores, o projeto ativo foi padrão para o projeto que compile e implante comandos independentemente do contexto. Agora, a solução controla e arbitra que crie e implante comandos se aplicam a quais projetos.  
  
  O que era anteriormente um projeto ativo agora é capturada em um dos três maneiras diferentes:  
  
- O projeto de inicialização  
  
   Você pode especificar um projeto ou projetos da solução página de propriedades que será iniciado quando o usuário pressiona F5 ou seleciona a execução no menu Build. Isso funciona de maneira semelhante ao projeto ativo antigo no sentido de que seu nome é exibido no Gerenciador de soluções com fonte em negrito.  
  
   Você pode recuperar o projeto de inicialização como uma propriedade no modelo de automação chamando `DTE.Solution.SolutionBuild.StartupProjects`. Em um VSPackage, você chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> ou o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2.get_StartupProject%2A> métodos. `IVsSolutionBuildManager` está disponível como um serviço por `QueryService` em SID_SVsSolutionBuildManager. Para obter mais informações, consulte [objeto de configuração do projeto](../../extensibility/internals/project-configuration-object.md) e [configuração de solução](../../extensibility/internals/solution-configuration.md).  
  
- Configuração de compilação da solução ativa  
  
   [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] tem uma configuração de solução ativa, disponível no modelo de automação com a implementação de `DTE.Solution.SolutionBuild.ActiveConfiguration`. Uma configuração de solução é uma coleção que contém uma configuração de projeto para cada projeto na solução (cada projeto pode ter várias configurações, em várias plataformas, com nomes diferentes). Para obter mais informações relacionadas a páginas de propriedades da solução, consulte [configuração da solução](../../extensibility/internals/solution-configuration.md).  
  
- Projeto selecionado no momento  
  
   Implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCurrentSelection%2A> método para recuperar a hierarquia do projeto e item de projeto ou itens selecionados. De DTE, você usaria o `SelectedItems.SelectedItem.Project` e `SelectedItems.SelectedItem.ProjectItem` métodos. Não há código de exemplo sob esses títulos no núcleo do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] documentos.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPage>   
 [Gerenciar opções de configuração](../../extensibility/internals/managing-configuration-options.md)   
 [Objeto de configuração do projeto](../../extensibility/internals/project-configuration-object.md)   
 [Configuração da solução](../../extensibility/internals/solution-configuration.md)

