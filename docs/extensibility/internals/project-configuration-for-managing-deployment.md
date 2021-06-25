---
title: Configuração de projeto para gerenciamento de implantação | Microsoft Docs
description: Saiba mais sobre a implantação no local esperado para depuração e instalação e as duas maneiras com que o Visual Studio dá suporte a projetos que dão suporte à implantação.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project configurations, managing deployment
- projects [Visual Studio SDK], configuration for managing deployment
ms.assetid: bd5940d9-d94d-4944-beda-4ec1ab2bbde5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3c6077665ccc3bbe5f87b91a1d2fc5636e08539d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899895"
---
# <a name="project-configuration-for-managing-deployment"></a>Configuração de projeto para gerenciar a implantação
A implantação é o ato de mover fisicamente os itens de saída de um processo de compilação para o local esperado para depuração e instalação. Por exemplo, um aplicativo Web pode ser criado em um computador local e, em seguida, colocado no servidor.

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o oferece suporte a duas maneiras em que os projetos podem estar envolvidos na implantação:

- Como o assunto do processo de implantação.

- Como o gerente do processo de implantação.

  Antes que as soluções possam ser implantadas, você deve primeiro adicionar um projeto de implantação para configurar as opções de implantação. Se o projeto de implantação ainda não existir, você será perguntado se deseja criar um ao selecionar **implantar solução** no menu **Compilar** ou clicar com o botão direito do mouse na solução. Clicar em **Sim** abre a caixa de diálogo **Adicionar novo projeto** com o projeto do **Assistente de implantação remota** selecionado.

  O assistente de implantação remota solicita o tipo de aplicativo (Windows ou Web), os grupos de saída do projeto a serem incluídos, os arquivos adicionais que você deseja incluir e o computador remoto no qual você deseja implantar. A última página do assistente exibe um resumo das opções selecionadas.

  Os projetos que são o assunto de um processo de implantação produzem itens de saída que devem ser movidos para um ambiente alternativo. Esses itens de saída são descritos como parâmetros para a <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> interface, cuja principal finalidade é permitir que os projetos agrupem saídas. Para obter mais informações relacionadas à implementação do `IVsProjectCfg2` , consulte [configuração de projeto para saída](../../extensibility/internals/project-configuration-for-output.md).

  Projetos de implantação, que gerenciam o processo de implantação, habilitam o comando implantar e respondem quando esse comando é selecionado. Projetos de implantação implementam a <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> interface para executar a implantação e fazer chamadas para a <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployStatusCallback> interface para relatar eventos de status de implantação.

  As configurações podem especificar dependências que afetam suas operações de compilação ou implantação. Compilar ou implantar dependências são projetos que devem ser compilados ou implantados antes ou depois que as próprias configurações são criadas ou implantadas. As dependências de compilação entre projetos são descritas com a <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency> interface e implantam dependências com a <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency> interface. Para obter mais informações, consulte [configuração de projeto para compilação](../../extensibility/internals/project-configuration-for-building.md).

## <a name="see-also"></a>Confira também
- [Gerenciando opções de configuração](../../extensibility/internals/managing-configuration-options.md)
- [Configuração de projeto para compilar](../../extensibility/internals/project-configuration-for-building.md)
- [Configuração de projeto para saída](../../extensibility/internals/project-configuration-for-output.md)
