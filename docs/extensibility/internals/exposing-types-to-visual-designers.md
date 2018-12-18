---
title: Expor tipos aos Designers visuais | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- types [Visual Studio SDK], exposing to visual designers
- designers [Visual Studio SDK], exposing types
- custom tools, exposing types to visual designers
ms.assetid: a7a32ad4-3a0a-4eb8-a6ac-491c42885639
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 9f1820b3df61dd8029ac9404eb7f4a09e44707ac
ms.sourcegitcommit: 3dd15e019cba7d35dbabc1aa3bf55842a59f5278
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/19/2018
ms.locfileid: "46370621"
---
# <a name="expose-types-to-visual-designers"></a>Expor tipos aos designers visuais
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] deve ter acesso a definições de classe e tipo em tempo de design para exibir um designer visual. As classes são carregadas de um conjunto predefinido de assemblies que incluem o conjunto completo de dependência do projeto atual (referências além de suas dependências). Ele também pode ser necessário para designers visuais classes de acesso e tipos que são definidos nos arquivos gerados por ferramentas personalizadas.  
  
 O [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] e [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] sistemas de projeto fornecem suporte para acessar tipos e classes geradas por meio de portáteis temporários arquivos executáveis (PEs temporária). Qualquer arquivo gerado por uma ferramenta personalizada pode ser compilado em um assembly temporário para que os tipos podem ser carregados a partir desses assemblies e expostos aos designers. A saída de cada ferramenta personalizada é compilada em um PE temporário separado, e o sucesso ou fracasso desta compilação temporário depende somente ou não o arquivo gerado pode ser compilado. Mesmo que um projeto pode não ser compilado como um todo, os PEs temporário individuais ainda podem estar disponíveis para designers.  
  
 O sistema de projeto fornece suporte completo para o controle de alterações ao arquivo de saída de uma ferramenta personalizada, desde que essas alterações são o resultado da execução da ferramenta personalizada. Cada vez que a ferramenta personalizada é executada, um novo PE temporário é gerado e são enviadas notificações apropriadas para designers.  
  
> [!NOTE]
>  Porque o arquivo de geração de executáveis de programas temporários ocorre em segundo plano, sem erros são relatados para o usuário se a compilação falhará.  
  
 Ferramentas personalizadas que tiram proveito do suporte de PE temporário devem seguir as regras a seguir:  
  
-   **GeneratesDesignTimeSource** deve ser definido como 1 no registro.  
  
     Nenhuma compilação do arquivo executável de programa ocorre sem essa configuração.  
  
-   O código gerado deve estar no mesmo idioma em que a configuração do projeto global.  
  
     O PE temporário é compilado, independentemente do que a ferramenta personalizada informa como a extensão solicitada na <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A> desde que **GeneratesDesignTimeSource** é definido como 1 no registro. A extensão não precisa ser *. vb*, *. CS*, ou *. jsl*; pode ser qualquer extensão.  
  
-   O código gerado pela ferramenta personalizada deve ser válido, e ele deve compilar em seu próprio usando apenas o conjunto de referências presentes no projeto no momento <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> termina a execução.  
  
     Quando um PE temporário é compilado, o único arquivo de origem fornecido ao compilador é a saída da ferramenta personalizada. Portanto, uma ferramenta personalizada que usa um PE temporário deve gerar arquivos de saída que podem ser compilados independentemente dos outros arquivos no projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Introdução ao objeto BuildManager](https://msdn.microsoft.com/library/50080ec2-c1c9-412c-98ef-18d7f895e7fa)   
 [Implementar geradores de arquivo único](../../extensibility/internals/implementing-single-file-generators.md)   
 [Registrar geradores de arquivo único](../../extensibility/internals/registering-single-file-generators.md)