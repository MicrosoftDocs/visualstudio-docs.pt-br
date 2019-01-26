---
title: Fundamentos do tipo de projeto | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types [Visual Studio SDK]
ms.assetid: 09991589-2300-430e-b6a4-7f2b95fe676f
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f0b6b3509af981a07fce76be69f16d767ec0c246
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55017923"
---
# <a name="project-type-essentials"></a>Conceitos básicos do tipo de projeto
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] inclui vários tipos de projeto para linguagens, como [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] ou [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] também permite que você crie seus próprios tipos de projeto.  
  
 Se você quiser apenas adicionar comandos personalizados, editores ou janelas de ferramentas para [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], você pode fazer isso sem criar um novo tipo de projeto. Para mais informações, consulte os seguintes tópicos:  
  
- [Comandos, menus e barras de ferramentas](../../extensibility/internals/commands-menus-and-toolbars.md)  
  
- [Editor e extensões do serviço de linguagem](../../extensibility/editor-and-language-service-extensions.md)  
  
- [Ampliar e personalizar janelas de ferramentas](../../extensibility/extending-and-customizing-tool-windows.md)  
  
  Da mesma forma, se você deseja personalizar o comportamento de fornecido [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] e [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] tipos de projeto, você pode fazer isso usando subtipos do projeto. Para obter mais informações, consulte [subtipos do projeto](../../extensibility/internals/project-subtypes.md).  
  
  Você deve criar um novo tipo de projeto para projetos com base em uma linguagem diferente de [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] e [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] se você quiser dar suporte a uma ou mais das seguintes opções:  
  
- Build  
  
- Implantação  
  
- Várias configurações  
  
- Controle do código-fonte  
  
- Depuração  
  
- Itens de projeto no Gerenciador de soluções  
  
- O **Abrir projeto** ou **novo projeto** caixas de diálogo  
  
- Aninhamento de projeto  
  
- Para obter mais informações sobre os recursos de tipos de projeto, consulte o seguinte:  
  
- Tipos de projeto são objetos em um VSPackage que implementam o conjunto de interfaces [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] espera. Se você estiver usando c# para desenvolver um tipo de projeto, as classes do projeto de estrutura de pacote gerenciado implementam as interfaces necessárias para você e permitem que você herdar dessa implementação. Para obter mais informações, consulte [usando a estrutura de pacote gerenciado para implementar um tipo de projeto (c#)](../../extensibility/internals/using-the-managed-package-framework-to-implement-a-project-type-csharp.md).  
  
- Para desenvolvedores de C++, as classes na biblioteca HierUtil funcionam de maneira semelhante. Para obter mais informações, consulte [não está em compilação: Usando Classes do projeto HierUtil7 para implementar um tipo de projeto (C++)](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346).  
  
- Tipos de projeto podem dar suporte a dados que não sejam arquivos código-fonte típico que se baseiam em um assembly .exe ou. dll. Por exemplo, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] projetos de banco de dados contêm referências a arquivos de script e de consulta armazenados em disco e adicionar comandos ao **Gerenciador de soluções** para executar os scripts e consultas em um banco de dados, mas os projetos não dão suporte a Crie o comportamento. Para obter mais informações, consulte [abrindo e salvando itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md).  
  
- Não tem um tipo de projeto usar os arquivos em todos os. Por exemplo, um tipo de projeto pode armazenar todos os seus dados em um banco de dados. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] fornece tipos de projeto com controle completo sobre como eles persistirem dados para projetos e itens de projeto. Para obter mais informações, consulte [decisões de Design de tipo de projeto](../../extensibility/internals/project-type-design-decisions.md).  
  
- Tipos de projeto devem fornecer um *fábrica de projeto*, que é um objeto que cria uma instância do projeto digite sempre que [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] é instruído a abrir ou criar um projeto com base nesse tipo de projeto. Para obter mais informações, consulte [criação de projeto instâncias por usando fábricas de projeto](../../extensibility/internals/creating-project-instances-by-using-project-factories.md).  
  
- Tipos de projeto devem fornecer modelos para projetos e itens de projeto. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] usa os modelos quando os usuários criar novos projetos e adicionar novos itens a projetos existentes. Para obter mais informações, consulte [adicionando projeto e modelos de Item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md).  
  
- Tipos de projeto podem dar suporte a várias configurações, como Debug e Release. Os usuários podem alterar as diferentes configurações de um projeto por meio de páginas de propriedade fornecidos por você. Para obter mais informações, consulte [opções de configuração de gerenciamento de](../../extensibility/internals/managing-configuration-options.md).  
  
## <a name="see-also"></a>Consulte também  
 [Implantar tipos de projeto](../../extensibility/internals/deploying-project-types.md)