---
title: Configuração de projeto para compilação | Microsoft Docs
description: Saiba como uma lista de configurações de solução para uma solução específica é gerenciada pela caixa de diálogo Configurações de solução em um novo tipo de projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], configuration for building
- project configurations, building
ms.assetid: 2c83615d-fa4d-4b9f-b315-7a69b3000da0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b817607f765626a6b63693e681306309512fdb7d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074438"
---
# <a name="project-configuration-for-building"></a>Configuração de projeto para compilar
A lista de configurações de solução para uma determinada solução é gerenciada pela caixa de diálogo Configurações de solução.

 Um usuário pode criar configurações de solução adicionais, cada uma com seu próprio nome exclusivo. Quando o usuário cria uma nova configuração de solução, o IDE usa como padrão o nome de configuração correspondente nos projetos ou depurar se não existir nenhum nome correspondente. O usuário pode alterar a seleção para atender a requisitos específicos, se necessário. A única exceção a esse comportamento é quando o projeto dá suporte a uma configuração que corresponde ao nome da nova configuração de solução. Por exemplo, suponha que uma solução contenha Projeto1 e Projeto2. O Projeto1 tem configurações de projeto Debug, Retail e MyConfig1. O Projeto2 tem configurações de projeto Debug, Retail e MyConfig2.

 Se o usuário criar uma nova configuração de solução chamada MyConfig2, Projeto1 associará sua configuração de depuração à configuração da solução por padrão. O Projeto2 também associa sua configuração MyConfig2 à configuração da solução por padrão.

> [!NOTE]
> A associação não diferencia maiúsculas de minúsculas.

 Quando o usuário seleciona o item **seleção múltipla** na lista suspensa configuração, o ambiente exibe uma caixa de diálogo que fornece a lista de configurações disponíveis.

 ![Várias configurações](../../extensibility/internals/media/vsmultiplecfgs.gif "vsMultipleCfgs") Várias configurações

 Nessa caixa de diálogo, o usuário pode selecionar uma ou várias configurações. Depois de selecionado, os valores de propriedade exibidos na caixa de diálogo páginas de propriedades refletem a interseção de valores para as configurações selecionadas.

 Consulte [configuração da solução](../../extensibility/internals/solution-configuration.md) para obter informações relacionadas à adição e renomeação de configurações para soluções e projetos.

 As dependências de projeto e a ordem de compilação são independentes de configuração de solução: ou seja, você só pode configurar uma árvore de dependência para todos os projetos na solução. Clicar com o botão direito do mouse na solução ou no projeto e selecionar a opção **dependências do projeto** ou **ordem de compilação do projeto** abre a caixa de diálogo **dependências do projeto** . Ele também pode ser aberto no menu **projeto** .

 ![Dependências do projeto](../../extensibility/internals/media/vsprojdependencies.gif "vsProjDependencies") Dependências do projeto

 As dependências do projeto determinam a ordem na qual os projetos são criados. Use a guia ordem de compilação na caixa de diálogo para exibir a ordem exata na qual os projetos dentro de uma solução serão compilados e use a guia dependências para modificar a ordem de compilação.

> [!NOTE]
> Os projetos na lista que têm suas caixas de seleção selecionadas, mas aparecem esmaecidos foram adicionados pelo ambiente devido a dependências explícitas especificadas pelas <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency> interfaces do ou do <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency> , e não podem ser alterados. Por exemplo, a adição de uma referência de projeto de um [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] projeto a outro projeto adiciona automaticamente uma dependência de compilação que só pode ser removida com a exclusão da referência. Os projetos cujas caixas de seleção são claras e aparecem esmaecidos não podem ser selecionados, pois isso criaria um loop de dependência (por exemplo, Projeto1 seria dependente de Projeto2, e Projeto2 seria dependente de Projeto1), o que paralisaria a compilação.

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] os processos de compilação incluem as operações típicas de compilação e vinculação que são invocadas com um único comando de compilação. Dois outros processos de compilação também podem ter suporte: uma operação de limpeza para excluir todos os itens de saída de uma compilação anterior e uma verificação atualizada para determinar se um item de saída em uma configuração foi alterado.

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> os objetos retornam um correspondente <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> (retornado de <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A> ) para gerenciar seus processos de compilação. Para relatar o status de uma operação de compilação enquanto ela está ocorrendo, as configurações fazem chamadas para <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildStatusCallback> o, uma interface implementada pelo ambiente e qualquer outro objeto interessado em eventos de status de compilação.

 Uma vez criadas, as definições de configuração podem ser usadas para determinar se elas podem ou não ser executadas sob o controle do depurador. As configurações implementam <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> para dar suporte à depuração.

 Depois de implementar as dependências do projeto, você pode manipular programaticamente as dependências por meio do modelo de automação. Você chama <xref:EnvDTE.SolutionBuild.BuildDependencies%2A> o modelo de automação. Não há nenhuma interface de nível de API do VSIP disponível que permita a manipulação direta das configurações do Gerenciador de compilação de solução e suas propriedades.

 Além disso, você pode fornecer uma grade na janela dependências do projeto. Para obter mais informações, consulte [grade de exibição de propriedades](../../extensibility/internals/properties-display-grid.md).

## <a name="see-also"></a>Confira também
- [Gerenciando opções de configuração](../../extensibility/internals/managing-configuration-options.md)
- [Configuração de projeto para gerenciar a implantação](../../extensibility/internals/project-configuration-for-managing-deployment.md)
- [Configuração de projeto para saída](../../extensibility/internals/project-configuration-for-output.md)
