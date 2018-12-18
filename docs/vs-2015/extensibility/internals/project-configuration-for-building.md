---
title: Configuração para a criação de projeto | Microsoft Docs
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
- projects [Visual Studio SDK], configuration for building
- project configurations, building
ms.assetid: 2c83615d-fa4d-4b9f-b315-7a69b3000da0
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: ef43fe505e859cb32f7c0fbe407bcc73c4f4e0e8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51725526"
---
# <a name="project-configuration-for-building"></a>Configuração de projeto para compilar
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

A lista de configurações da solução para uma determinada solução é gerenciada pela caixa de diálogo Configurações da solução.  
  
 Um usuário pode criar configurações adicionais da solução, cada um com seu próprio nome exclusivo. Quando o usuário cria uma nova configuração de solução, o IDE assume como padrão o nome de configuração correspondente em projetos ou depuração se nenhum nome correspondente existe. O usuário pode alterar a seleção para atender aos requisitos específicos, se necessário. A única exceção a esse comportamento é quando o projeto dá suporte a uma configuração que corresponde ao nome da nova configuração de solução. Por exemplo, suponha que uma solução contém Projeto1 e Projeto2. Project1 tem configurações de projeto MyConfig1, varejo e depuração. Projeto2 tem configurações de projeto MyConfig2, varejo e depuração.  
  
 Se o usuário cria uma nova configuração de solução chamada MyConfig2, Projeto1 associa sua configuração de depuração para a configuração da solução, por padrão. Por padrão, Projeto2 também associa sua configuração MyConfig2 para a configuração da solução.  
  
> [!NOTE]
>  Associação diferencia maiusculas de minúsculas.  
  
 Quando o usuário seleciona o **seleção múltipla** item na lista suspensa de configuração, o ambiente exibe uma caixa de diálogo que fornece a lista de configurações disponíveis.  
  
 ![Configurações com várias](../../extensibility/internals/media/vsmultiplecfgs.gif "vsMultipleCfgs")  
Várias configurações  
  
 Na caixa de diálogo, o usuário pode selecionar uma ou várias configurações. Depois de selecionado, os valores de propriedade exibidos na caixa de diálogo páginas de propriedade refletem a interseção dos valores para as configurações selecionadas.  
  
 Ver [configuração da solução](../../extensibility/internals/solution-configuration.md) para obter informações relativas a adicionar e renomear as configurações para soluções e projetos.  
  
 Dependências do projeto e a ordem de compilação são independentes da configuração de solução: ou seja, você só pode definir a árvore de uma dependência para todos os projetos na solução. Clicando duas vezes a solução ou projeto e selecionando o **dependências do projeto** ou **ordem de Build do projeto** opção abre o **dependências do projeto** caixa de diálogo. Ele também pode ser aberto na **projeto** menu.  
  
 ![Dependências do projeto](../../extensibility/internals/media/vsprojdependencies.gif "vsProjDependencies")  
Dependências do projeto  
  
 Dependências do projeto determinam a ordem na qual os projetos são compilados. Use a guia de ordem de Build na caixa de diálogo para exibir a ordem exata em que projetos dentro de uma solução de build e use a guia dependências para modificar a ordem de compilação.  
  
> [!NOTE]
>  Projetos na lista que têm suas caixas de seleção marcadas, mas esmaecidos foram adicionados pelo ambiente devido a dependências explícitas especificadas pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency> ou o <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency> interfaces e não pode ser alterado. Por exemplo, adicionando uma referência de projeto de um [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] projeto a outro projeto automaticamente adiciona uma dependência de compilação que só pode ser removida, excluindo a referência. Não não possível selecionar projetos cujas caixas de seleção estão desmarcadas e aparecem esmaecidas porque isso geraria um loop de dependência (por exemplo, Projeto1 seria dependente Projeto2 e Projeto2 seria dependente Projeto1), que teria de paralisações da compilação.  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] processos de compilação incluem as operações de link que são invocadas com um único comando de compilação e a compilação típica. Também haverá suporte para dois outros processos de compilação: uma operação de limpeza para excluir todos os itens de saída de uma compilação anterior e uma verificação de atualização para determinar se um item de saída em uma configuração foi alterada.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> objetos de retorno correspondente <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> (retornado do <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A>) para gerenciar seus processos de compilação. Para relatar o status de uma operação de compilação enquanto ele está em execução, as configurações de fazem chamadas para <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildStatusCallback>, uma interface implementada pelo ambiente e qualquer outro objeto está interessado em eventos de status de compilação.  
  
 Depois de criado, as definições de configuração podem ser usadas para determinar se eles podem ser executados sob o controle do depurador. Implementam configurações <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> para dar suporte à depuração.  
  
 Depois de implementar as dependências do projeto, você pode manipular programaticamente as dependências por meio do modelo de automação. Você chama <xref:EnvDTE.SolutionBuild.BuildDependencies%2A> no modelo de automação. Não há nenhuma interface de nível de API do VSIP disponível que permitem a manipulação direta das configurações de Gerenciador de build da solução e suas propriedades.  
  
 Além disso, você pode fornecer uma grade na janela de dependências do projeto. Para obter mais informações, consulte [grade de exibição de propriedades](../../extensibility/internals/properties-display-grid.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar opções de configuração](../../extensibility/internals/managing-configuration-options.md)   
 [Configuração de projeto para gerenciar a implantação](../../extensibility/internals/project-configuration-for-managing-deployment.md)   
 [Configuração do projeto para saída](../../extensibility/internals/project-configuration-for-output.md)

