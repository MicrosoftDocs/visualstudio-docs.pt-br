---
title: 'Lista de verificação: Criação de novos tipos de projeto | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], creating new types
- project types, checklist for creating
ms.assetid: 29eb9c3b-1933-4741-aa85-65a33f0825ba
caps.latest.revision: 24
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 02edc5925109a31eebfd98c90bd116fb86eef276
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697238"
---
# <a name="checklist-creating-new-project-types"></a>Lista de verificação: Criando tipos de projeto
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Você deve concluir várias tarefas para criar um novo tipo de projeto. A lista de verificação a seguir fornece um guia para essas tarefas.  
  
1. A funcionalidade para o novo tipo de projeto de design. Para obter mais informações, consulte [decisões de Design de tipo de projeto](../../extensibility/internals/project-type-design-decisions.md).  
  
2. Determine quais editores são usados para o código e outros elementos do projeto. Você pode usar o core ou editores padrão, ou você pode criar e usar os editores específicos do projeto. Para obter mais informações, consulte [criação personalizada editores e Designers](../../extensibility/creating-custom-editors-and-designers.md) e [como: Abrir editores específicos do projeto](../../extensibility/how-to-open-project-specific-editors.md).  
  
3. Determinar o nível de participação terão seus itens de projeto na **Class View** e o **Pesquisador de objetos**. Para obter mais informações, consulte [ferramentas de navegação de símbolo que dão suporte a](../../extensibility/internals/supporting-symbol-browsing-tools.md).  
  
4. Derive novas classes com base nas decisões de design que você fez anteriormente para seu projeto e itens de projeto.  
  
5. Escreva o código para os seguintes componentes do tipo de projeto:  
  
    - Fábrica de projeto, para gerenciar a criação de novos projetos e abrir projetos existentes. Para obter mais informações, consulte [criação de projeto instâncias por usando fábricas de projeto](../../extensibility/internals/creating-project-instances-by-using-project-factories.md).  
  
    - Hierarquia do projeto e manipulação de comandos. Para obter mais informações, consulte [não está em compilação: Usando Classes do projeto HierUtil7 para implementar um tipo de projeto (C++)](https://msdn.microsoft.com/a5c16a09-94a2-46ef-87b5-35b815e2f346), [elementos de um modelo de projeto](../../extensibility/internals/elements-of-a-project-model.md), [componentes principais do modelo de projeto](../../extensibility/internals/project-model-core-components.md) e [MenuCommands Vs. OleMenuCommands](../../misc/menucommands-vs-olemenucommands.md).  
  
    - Gerenciamento de itens de projeto, incluindo a adição de seu projeto para o **novo projeto** caixa de diálogo. Para obter mais informações, consulte [adicionando projeto e modelos de Item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md) e [registrar modelos de projeto e Item](../../extensibility/internals/registering-project-and-item-templates.md).  
  
    - Persistência de estado do projeto e itens individuais. Para obter mais informações, consulte [abrindo e salvando itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md). Para a persistência das informações de solução, consulte [soluções](../../extensibility/internals/solutions-overview.md).  
  
    - Propriedades de configuração independentes para exibir na janela Propriedades. Para obter mais informações, consulte [estendendo propriedades](../../extensibility/internals/extending-properties.md).  
  
    - Propriedades de configuração do projeto conforme implementado nas páginas de propriedades para mostrar propriedades dependentes de configuração. Para obter mais informações, consulte [opções de configuração de gerenciamento de](../../extensibility/internals/managing-configuration-options.md).  
  
    - Enumerando as saídas para a implantação. Para obter mais informações, consulte [configuração do projeto para saída](../../extensibility/internals/project-configuration-for-output.md).  
  
    - Serviços de inicialização do projeto. Para obter mais informações, consulte [elementos de um modelo de projeto](../../extensibility/internals/elements-of-a-project-model.md) e [componentes principais do projeto modelo](../../extensibility/internals/project-model-core-components.md).  
  
    - Objetos ou classes derivadas de `IDispatch`, disponível para a automação.  
  
    - Arquivos da tabela de comando de XML (. VSCT). Para obter mais informações, consulte [tabela de comando do Visual Studio (. VSCT) arquivos](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).  
  
6. Testar, depurar e iniciar o tipo de projeto.  
  
7. Exibir seu projeto na **Project** guia da **adicionar referência** caixa de diálogo, definindo `VARIANT_TRUE` como o valor para `VSHPROPID_ShowProjInSolutionPage`. Para obter mais informações, consulte <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>.  
  
8. Crie o arquivo do Microsoft Installer (. msi) para instalar seu VSPackages. Para obter mais informações, consulte [instalando VSPackages com o Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md), [registro de um tipo de projeto](../../extensibility/internals/registering-a-project-type.md), e [VSPackages](../../extensibility/internals/vspackages.md).  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquias no Visual Studio](../../extensibility/internals/hierarchies-in-visual-studio.md)   
 [Quando criar tipos de projeto](../../extensibility/internals/when-to-create-project-types.md)   
 [Criar tipos de projeto](../../extensibility/internals/creating-project-types.md)
