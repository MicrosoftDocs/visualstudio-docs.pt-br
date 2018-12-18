---
title: Configuração para gerenciar a implantação de projeto | Microsoft Docs
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
- project configurations, managing deployment
- projects [Visual Studio SDK], configuration for managing deployment
ms.assetid: bd5940d9-d94d-4944-beda-4ec1ab2bbde5
caps.latest.revision: 9
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: a6ea732449c92b2dffb91c7e90ff738791b7c2f7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51721357"
---
# <a name="project-configuration-for-managing-deployment"></a>Configuração de projeto para gerenciar a implantação
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

A implantação é o ato de mover fisicamente os itens de saída de um processo de compilação para o local esperado para a instalação e a depuração. Por exemplo, um aplicativo Web pode criado em um computador local e, em seguida, colocado no servidor.  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] dá suporte a duas maneiras de projetos pode estar envolvida na implantação:  
  
- Como o assunto do processo de implantação.  
  
- Como o Gerenciador do processo de implantação.  
  
  Antes de soluções podem ser implantadas, você deve primeiro adicionar um projeto de implantação para configurar as opções de implantação. Se o projeto de implantação ainda não existir, será perguntado se deseja criá-lo quando você seleciona **implantar solução** da **Build** menu ou botão direito do mouse a solução. Clicando em **Sim** abre os **adicionar novo projeto** caixa de diálogo com o **Assistente de implantação remota** projeto selecionado.  
  
  O Assistente de implantação remota solicita o tipo de aplicativo (Windows ou Web), os grupos de saída do projeto para incluir, quaisquer arquivos adicionais que você deseja incluir e você deseja implantar no computador remoto. A última página do assistente exibe um resumo das opções selecionadas.  
  
  Projetos que são o assunto de um processo de implantação produzem os itens de saída devem ser movidos para um ambiente alternativo. Saída de esses itens são descritos como parâmetros para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> interface, cujo principal propósito if permitir que os projetos para o grupo de saídas. Para obter mais informações relacionadas à implementação de `IVsProjectCfg2`, consulte [configuração do projeto para saída](../../extensibility/internals/project-configuration-for-output.md).  
  
  Projetos de implantação, que gerenciem o processo de implantação, habilite o comando implantar e respondem quando esse comando é selecionado. Implementam projetos de implantação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> interface para realizar a implantação e fazer chamadas para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployStatusCallback> interface para o relatório implantar eventos de status.  
  
  As configurações podem especificar dependências que afetam as suas operações de compilação ou implantação. Compilar ou implantar as dependências são projetos que devem ser criados ou implantados antes ou depois que as configurações em si são criadas ou implantadas. Dependências de compilação entre os projetos são descritas com o <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency> da interface e implantar as dependências com o <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency> interface. Para obter mais informações, consulte [configuração do projeto para a construção](../../extensibility/internals/project-configuration-for-building.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar opções de configuração](../../extensibility/internals/managing-configuration-options.md)   
 [Configuração de projeto para criação](../../extensibility/internals/project-configuration-for-building.md)   
 [Configuração do projeto para saída](../../extensibility/internals/project-configuration-for-output.md)

