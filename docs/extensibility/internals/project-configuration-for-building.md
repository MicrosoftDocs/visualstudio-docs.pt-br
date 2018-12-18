---
title: Configuração de compilação de projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], configuration for building
- project configurations, building
ms.assetid: 2c83615d-fa4d-4b9f-b315-7a69b3000da0
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4d78ac1cabc356db162639d3eb19d0bff71e295e
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31133292"
---
# <a name="project-configuration-for-building"></a>Configuração de projeto para criação
A lista de configurações de solução para uma determinada solução é gerenciada pela caixa de diálogo Configurações da solução.  
  
 Um usuário pode criar configurações adicionais de solução, cada qual com seu próprio nome exclusivo. Quando o usuário cria uma nova configuração de solução, o IDE padrão é o nome de configuração correspondente em projetos ou depuração se nenhum nome correspondente existe. O usuário pode alterar a seleção para atender às necessidades específicas, se necessário. A única exceção a esse comportamento é quando o projeto dá suporte a uma configuração que corresponde ao nome da nova configuração de solução. Por exemplo, suponha que uma solução contiver Project1 e Project2. Project1 tem configurações de projeto MyConfig1, varejo e depuração. Project2 tem configurações de projeto MyConfig2, varejo e depuração.  
  
 Se o usuário cria uma nova configuração de solução chamada MyConfig2, Project1 associa sua configuração de depuração para a configuração da solução por padrão. Por padrão, Project2 também associa sua configuração MyConfig2 para a configuração da solução.  
  
> [!NOTE]
>  Associação diferencia maiusculas de minúsculas.  
  
 Quando o usuário seleciona o **seleção múltipla** item na lista suspensa de configuração, o ambiente exibe uma caixa de diálogo que fornece a lista de configurações disponíveis.  
  
 ![Várias configurações](../../extensibility/internals/media/vsmultiplecfgs.gif "vsMultipleCfgs")  
Várias configurações  
  
 Na caixa de diálogo, o usuário pode selecionar uma ou várias configurações. Quando selecionada, os valores de propriedade exibidos na caixa de diálogo páginas de propriedade refletem a interseção dos valores para as configurações selecionadas.  
  
 Consulte [configuração de solução](../../extensibility/internals/solution-configuration.md) para obter informações relacionadas ao adicionar e renomear as configurações para projetos e soluções.  
  
 Dependências do projeto e ordem de compilação são independentes da configuração de solução: ou seja, você só pode definir a árvore de uma dependência para todos os projetos na solução. Clicando duas vezes a solução ou projeto e selecionando o **dependências do projeto** ou **ordem de compilação de projeto** opção abre o **dependências do projeto** caixa de diálogo. Ela também pode ser aberta pelo **projeto** menu.  
  
 ![Dependências do projeto](../../extensibility/internals/media/vsprojdependencies.gif "vsProjDependencies")  
Dependências do projeto  
  
 Dependências do projeto determinam a ordem na qual criar projetos. Use a guia de ordem de compilação na caixa de diálogo para exibir a ordem exata em que projetos dentro de uma solução de compilação e use a guia dependências para modificar a ordem de compilação.  
  
> [!NOTE]
>  Foram adicionados projetos na lista que têm suas caixas de seleção marcadas, mas esmaecidos pelo ambiente de devido a dependências explícitas especificado pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency> ou <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency> interfaces e não pode ser alterado. Por exemplo, adicionando uma referência de projeto de um [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] projeto para outro projeto automaticamente adiciona uma dependência de compilação que só pode ser removida se você excluir a referência. Os projetos cujas caixas de seleção estão desmarcadas e esmaecidos não podem ser selecionados porque isso criaria um loop de dependência (por exemplo, Project1 seria dependente Project2 e Project2 seria dependente Project1), que deve parar a compilação.  
  
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] processos de compilação incluem a compilação típica e as operações de link que são invocadas com um único comando de compilação. Também haverá suporte para dois outros processos de compilação: uma operação de limpeza para excluir todos os itens de saída de uma compilação anterior e uma verificação de atualização para determinar se um item de saída em uma configuração foi alterada.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> objetos de retorno correspondente <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> (retornado de <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A>) para gerenciar seus processos de compilação. Para relatar o status de uma operação de compilação enquanto estiver ocorrendo, configurações de fazer chamadas para <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildStatusCallback>, uma interface implementada pelo ambiente e qualquer outro objeto interessado nos eventos de status de compilação.  
  
 Após a criação, as definições de configuração podem ser usadas para determinar se eles podem ser executados sob o controle do depurador. Implementam configurações <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> para oferecer suporte à depuração.  
  
 Depois de implementar as dependências do projeto, você pode manipular programaticamente as dependências por meio do modelo de automação. Você chama <xref:EnvDTE.SolutionBuild.BuildDependencies%2A> no modelo de automação. Não há nenhuma interface de nível de API do VSIP disponível que permitem a manipulação direta das configurações de Gerenciador de compilação de solução e suas propriedades.  
  
 Além disso, você pode fornecer uma grade na janela de dependências do projeto. Para obter mais informações, consulte [grade de exibição de propriedades](../../extensibility/internals/properties-display-grid.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar opções de configuração](../../extensibility/internals/managing-configuration-options.md)   
 [Configuração de projeto para gerenciar a implantação](../../extensibility/internals/project-configuration-for-managing-deployment.md)   
 [Configuração do projeto para saída](../../extensibility/internals/project-configuration-for-output.md)