---
title: 'Lista de verificação: Criar novos tipos de projeto | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], creating new types
- project types, checklist for creating
ms.assetid: 29eb9c3b-1933-4741-aa85-65a33f0825ba
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3da952e22515b48f06fdc50b34b2eb49f5709cc2
ms.sourcegitcommit: 3dd15e019cba7d35dbabc1aa3bf55842a59f5278
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/19/2018
ms.locfileid: "46370569"
---
# <a name="checklist-create-new-project-types"></a>Lista de verificação: Criar novos tipos de projeto
Você deve concluir várias tarefas para criar um novo tipo de projeto. A lista de verificação a seguir fornece um guia para essas tarefas:  
  
1.  A funcionalidade para o novo tipo de projeto de design. Para obter mais informações, consulte [decisões de design de tipo de projeto](../../extensibility/internals/project-type-design-decisions.md).  
  
2.  Determine quais editores são usados para o código e outros elementos do projeto. Você pode usar o core ou editores padrão, ou você pode criar e usar os editores específicos do projeto. Para obter mais informações, consulte [criar designers e editores personalizados](../../extensibility/creating-custom-editors-and-designers.md) e [como: abrir editores específicos do projeto](../../extensibility/how-to-open-project-specific-editors.md).  
  
3.  Determinar o nível de participação terão seus itens de projeto na **Class View** e o **Pesquisador de objetos**. Para obter mais informações, consulte [dar suporte a ferramentas de navegação de símbolo](../../extensibility/internals/supporting-symbol-browsing-tools.md).  
  
4.  Derive novas classes com base nas decisões de design que você fez anteriormente para seu projeto e itens de projeto.  
  
5.  Escreva o código para os seguintes componentes do tipo de projeto:  
  
    -   Fábrica de projeto, para gerenciar a criação de novos projetos e abrir projetos existentes. Para obter mais informações, consulte [criar instâncias de projetos usando fábricas de projeto](../../extensibility/internals/creating-project-instances-by-using-project-factories.md).  
  
    -   Hierarquia do projeto e manipulação de comandos. Para obter mais informações, consulte [HierUtil7 Use classes do projeto para implementar um tipo de projeto (C++)](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346), [elementos de um modelo de projeto](../../extensibility/internals/elements-of-a-project-model.md), [componentes principais do modelo de projeto](../../extensibility/internals/project-model-core-components.md)e [ MenuCommands vs. OleMenuCommands](../../extensibility/menucommands-vs-olemenucommands.md).  
  
    -   Gerenciamento de itens de projeto, incluindo a adição de seu projeto para o **novo projeto** caixa de diálogo. Para obter mais informações, consulte [adicionar o projeto e modelos de item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md) e [registrar modelos de projeto e item](../../extensibility/internals/registering-project-and-item-templates.md).  
  
    -   Persistência de estado do projeto e itens individuais. Para obter mais informações, consulte [abrir e salvar itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md). Para a persistência das informações de solução, consulte [soluções](../../extensibility/internals/solutions.md).  
  
    -   Propriedades de configuração independente para exibir na janela Propriedades. Para obter mais informações, consulte [estender propriedades](../../extensibility/internals/extending-properties.md).  
  
    -   Propriedades de configuração do projeto conforme implementado nas páginas de propriedades para mostrar propriedades dependentes de configuração. Para obter mais informações, consulte [gerenciar opções de configuração](../../extensibility/internals/managing-configuration-options.md).  
  
    -   Enumerando as saídas para a implantação. Para obter mais informações, consulte [configuração do projeto para saída](../../extensibility/internals/project-configuration-for-output.md).  
  
    -   Serviços de inicialização do projeto. Para obter mais informações, consulte [elementos de um modelo de projeto](../../extensibility/internals/elements-of-a-project-model.md) e [componentes principais do modelo de projeto](../../extensibility/internals/project-model-core-components.md).  
  
    -   Objetos ou classes derivadas de `IDispatch`, disponível para a automação.  
  
    -   Tabela de comando XML (*VSCT*) arquivos. Para obter mais informações, consulte [arquivos de tabela (. VSCT) de comando do Visual Studio](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).  
  
6.  Testar, depurar e iniciar o tipo de projeto.  
  
7.  Exibir seu projeto na **Project** guia da **adicionar referência** caixa de diálogo, definindo `VARIANT_TRUE` como o valor para `VSHPROPID_ShowProjInSolutionPage`. Para obter mais informações, consulte <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>.  
  
8.  Criar o Microsoft Installer (*. msi*) o arquivo para instalar seu VSPackages. Para obter mais informações, consulte [instalar VSPackages com o Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md), [registrar um tipo de projeto](../../extensibility/internals/registering-a-project-type.md), e [VSPackages](../../extensibility/internals/vspackages.md).  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquias no Visual Studio](../../extensibility/internals/hierarchies-in-visual-studio.md)   
 [Quando criar tipos de projeto](../../extensibility/internals/when-to-create-project-types.md)   
 [Criar tipos de projeto](../../extensibility/internals/creating-project-types.md)