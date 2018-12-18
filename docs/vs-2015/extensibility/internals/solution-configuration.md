---
title: Configuração da solução | Microsoft Docs
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
- solution configurations
ms.assetid: f22cfc75-3e31-4e0d-88a9-3ca99539203b
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 53d8e3d33a81e20d553e6a5c97eb6e6f33339079
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51801596"
---
# <a name="solution-configuration"></a>Configuração da solução
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Configurações da solução armazenam propriedades de nível de solução. Eles direcionam o comportamento do **inicie** chave (F5) e **Build** comandos. Por padrão, esses comandos criaram e iniciar a configuração de depuração. Ambos os comandos são executados no contexto de uma configuração de solução. Isso significa que o usuário pode esperar F5 para iniciar e seja qual for a solução ativa é configurada por meio das configurações de compilação. O ambiente foi projetado para otimizar para soluções em vez de projetos, quando se trata de criação e execução.  
  
 A barra de ferramentas padrão do Visual Studio contém um botão de início e uma lista suspensa à direita do botão Iniciar configuração da solução. Essa lista permite aos usuários escolher a configuração a ser iniciado quando F5 é pressionado, criar suas próprias configurações de solução ou editar uma configuração existente.  
  
> [!NOTE]
>  Não há nenhuma interface de extensibilidade para criar ou editar as configurações da solução. Você deve usar `DTE.SolutionBuilder`. No entanto, há APIs de extensibilidade para gerenciar a compilação da solução. Para obter mais informações, consulte <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2>.  
  
 Aqui está como você pode implementar as configurações de solução com suporte pelo seu tipo de projeto:  
  
- Projeto  
  
   Exibe os nomes dos projetos encontrados na solução atual.  
  
- Configuração  
  
   Para fornecer a lista de configurações com suporte pelo seu tipo de projeto e exibidos nas páginas de propriedades, implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>.  
  
   A coluna de configuração exibe o nome da configuração de projeto para compilar nesta configuração de solução e lista todas as configurações de projeto quando você clica no botão de seta. O ambiente chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgNames%2A> método para preencher essa lista. Se o <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A> método indica que o projeto dá suporte à edição de configuração, novo ou editar seleções também são exibidas sob o título de configuração. Cada uma dessas seleções iniciar caixas de diálogo que chamam métodos do `IVsCfgProvider2` interface para editar as configurações do projeto.  
  
   Se um projeto não oferece suporte a configurações, a coluna de configuração exibe nenhum e está desabilitada.  
  
- Plataforma  
  
   Exibe a plataforma de builds para a configuração de projeto selecionado e lista todas as plataformas disponíveis para o projeto quando você clica no botão de seta. O ambiente chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetPlatformNames%2A> método para preencher essa lista. Se o <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A> método indica que o projeto dá suporte à plataforma de edição, novo ou editar seleções também são exibidas sob o título de plataforma. Cada uma dessas seleções iniciar caixas de diálogo que chamam `IVsCfgProvider2` métodos para editar as plataformas disponíveis do projeto.  
  
   Se um projeto não der suporte a plataformas, a coluna de plataforma para o projeto exibe nenhum e está desabilitada.  
  
- Build  
  
   Especifica se o projeto é compilado pela configuração da solução atual. Projetos não selecionados não são criados quando os comandos de compilação de nível de solução são invocados, apesar de todas as dependências de projeto que eles contêm. Projetos não selecionados para ser compilado ainda são incluídos na depuração, execução, empacotamento e implantação da solução.  
  
- Implantar  
  
   Especifica se o projeto será implantado quando os comandos Start ou implantar são usados com a configuração de build da solução selecionada. A caixa de seleção para esse campo estará disponível se o projeto dá suporte à implantação com a implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> interface no seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> objeto.  
  
  Depois que uma nova configuração de solução é adicionada, o usuário pode selecioná-lo na caixa de lista suspensa de configuração da solução na barra de ferramentas padrão para criar e/ou iniciar essa configuração de.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar opções de configuração](../../extensibility/internals/managing-configuration-options.md)   
 [Configuração de projeto para criação](../../extensibility/internals/project-configuration-for-building.md)   
 [Objeto de configuração do projeto](../../extensibility/internals/project-configuration-object.md)

