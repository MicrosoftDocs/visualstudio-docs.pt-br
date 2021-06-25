---
title: Configuração do projeto para criação de | Microsoft Docs
description: Saiba como uma lista de configurações de solução para uma solução específica é gerenciada pela caixa de diálogo Configurações da Solução em um novo tipo de projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- projects [Visual Studio SDK], configuration for building
- project configurations, building
ms.assetid: 2c83615d-fa4d-4b9f-b315-7a69b3000da0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bf98698d3527220c4bc25cdf36132f0088ae4ea7
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899921"
---
# <a name="project-configuration-for-building"></a>Configuração de projeto para compilar
A lista de configurações de solução para uma determinada solução é gerenciada pela caixa de diálogo Configurações da Solução .

 Um usuário pode criar configurações de solução adicionais, cada uma com seu próprio nome exclusivo. Quando o usuário cria uma nova configuração de solução, o IDE assume como padrão o nome de configuração correspondente nos projetos ou Depurar se não houver nenhum nome correspondente. O usuário pode alterar a seleção para atender a requisitos específicos, se necessário. A única exceção a esse comportamento é quando o projeto dá suporte a uma configuração que corresponde ao nome da nova configuração da solução. Por exemplo, suponha que uma solução contenha Project1 e Project2. O Project1 tem configurações de projeto Depuração, Varejo e MyConfig1. O Project2 tem configurações de projeto Depuração, Varejo e MyConfig2.

 Se o usuário criar uma nova configuração de solução chamada MyConfig2, o Project1 vinculará sua configuração de Depuração à configuração da solução por padrão. O Project2 também vincula sua configuração myConfig2 à configuração da solução por padrão.

> [!NOTE]
> A associação não faz maiúsculas de minúsculas.

 Quando o usuário seleciona o **item** Seleção Múltipla na lista de opções de configuração, o ambiente exibe uma caixa de diálogo que fornece a lista de configurações disponíveis.

 ![Várias configurações](../../extensibility/internals/media/vsmultiplecfgs.gif "vsMultipleCfgs") Várias configurações

 Dentro dessa caixa de diálogo, o usuário pode selecionar uma ou várias configurações. Depois de selecionados, os valores de propriedade exibidos na caixa de diálogo páginas de propriedades refletem a interseção de valores para as configurações selecionadas.

 Consulte [Configuração da](../../extensibility/internals/solution-configuration.md) Solução para obter informações relacionadas à adição e renomeação de configurações para soluções e projetos.

 As dependências do projeto e a ordem de build são independentes de configuração de solução: ou seja, você só pode configurar uma árvore de dependência para todos os projetos na solução. Clicar com o botão direito do  mouse na solução ou projeto e selecionar a opção Dependências do Projeto ou Ordem de **Build** do Projeto abre a caixa de diálogo **Dependências** do Projeto. Ele também pode ser aberto **no** menu Projeto.

 ![Dependências do projeto](../../extensibility/internals/media/vsprojdependencies.gif "vsProjDependencies") Dependências do projeto

 As dependências do projeto determinam a ordem na qual os projetos são build. Use a guia Ordem de Build na caixa de diálogo para exibir a ordem exata na qual os projetos dentro de uma solução serão construídos e use a guia Dependências para modificar a ordem de build.

> [!NOTE]
> Projetos na lista que têm suas caixas de seleção selecionadas, mas aparecem esmaecidas, foram adicionados pelo ambiente devido a dependências explícitas especificadas pelas interfaces ou e não podem <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency> ser alterados. Por exemplo, adicionar uma referência de projeto de um projeto a outro projeto adiciona automaticamente uma dependência de build que só pode ser removida [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] excluindo a referência. Projetos cujas caixas de seleção estão claras e aparecem esmaecidas não podem ser selecionados porque isso criaria um loop de dependência (por exemplo, Project1 seria dependente de Project2 e Project2 seria dependente de Project1), o que pararia o build.

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Os processos de build incluem as operações típicas de compilação e link que são invocadas com um único comando Build. Dois outros processos de build também podem ser suportados: uma operação limpa para excluir todos os itens de saída de um build anterior e uma verificação atualizada para determinar se um item de saída em uma configuração foi alterado.

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> os objetos retornam um <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> correspondente (retornado de <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A> ) para gerenciar seus processos de build. Para relatar o status de uma operação de build enquanto ela está ocorrendo, as configurações fazem chamadas para , uma interface implementada pelo ambiente e qualquer outro objeto interessado em eventos de <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildStatusCallback> status de build.

 Depois de criadas, as definições de configuração podem ser usadas para determinar se elas podem ou não ser executados sob o controle do depurador. As configurações são <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> implementadas para dar suporte à depuração.

 Depois de implementar as dependências do projeto, você pode manipular programaticamente as dependências por meio do modelo de automação. Você chama <xref:EnvDTE.SolutionBuild.BuildDependencies%2A> no modelo de automação. Não há interfaces disponíveis no nível da API do VSIP que permitam a manipulação direta das configurações do gerenciador de build da solução e suas propriedades.

 Além disso, você pode fornecer uma grade na janela dependências do projeto. Para obter mais informações, consulte [Grade de Exibição de Propriedades](../../extensibility/internals/properties-display-grid.md).

## <a name="see-also"></a>Confira também
- [Gerenciando opções de configuração](../../extensibility/internals/managing-configuration-options.md)
- [Configuração de projeto para gerenciar a implantação](../../extensibility/internals/project-configuration-for-managing-deployment.md)
- [Configuração de projeto para saída](../../extensibility/internals/project-configuration-for-output.md)
