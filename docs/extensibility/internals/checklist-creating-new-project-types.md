---
title: 'Lista de verificação: criando novos tipos de projeto | Microsoft Docs'
description: Saiba mais sobre as tarefas que devem ser concluídas para criar e exibir um novo tipo de projeto no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], creating new types
- project types, checklist for creating
ms.assetid: 29eb9c3b-1933-4741-aa85-65a33f0825ba
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ac6495a6c2d5edcde00a3eb002f2fc41211a27e3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074763"
---
# <a name="checklist-create-new-project-types"></a>Lista de verificação: criar novos tipos de projeto
Você deve concluir várias tarefas para criar um novo tipo de projeto. A lista de verificação a seguir fornece um guia para essas tarefas:

1. Projete a funcionalidade para o novo tipo de projeto. Para obter mais informações, consulte [Project Type design decisions](../../extensibility/internals/project-type-design-decisions.md).

2. Determine quais editores são usados para código e outros elementos do projeto. Você pode usar os editores principais ou padrão, ou pode criar e usar editores específicos do projeto. Para obter mais informações, consulte [criar editores e designers personalizados](../../extensibility/creating-custom-editors-and-designers.md) e [como: abrir editores específicos do projeto](../../extensibility/how-to-open-project-specific-editors.md).

3. Determine o nível de participação que seus itens de projeto terão no **modo de exibição de classe** e no **pesquisador de objetos**. Para obter mais informações, consulte [ferramentas de navegação de símbolo de suporte](../../extensibility/internals/supporting-symbol-browsing-tools.md).

4. Derive novas classes com base nas decisões de design feitas anteriormente para o projeto e os itens do projeto.

5. Escreva o código para os seguintes componentes de tipo de projeto:

    - Fábrica de projetos, para gerenciar a criação de novos projetos e a abertura de projetos existentes. Para obter mais informações, consulte [criar instâncias de projeto usando fábricas de projeto](../../extensibility/internals/creating-project-instances-by-using-project-factories.md).

    - Hierarquia de projeto e manipulação de comandos. Para obter mais informações, consulte [usar classes de projeto HierUtil7 para implementar um tipo de projeto (C++)](/previous-versions/bb166212(v=vs.100)), [elementos de um modelo de projeto](../../extensibility/internals/elements-of-a-project-model.md), [componentes principais do Project Model](../../extensibility/internals/project-model-core-components.md)e [MenuCommands vs. OleMenuCommands](/previous-versions/visualstudio/visual-studio-2015/misc/menucommands-vs-olemenucommands?preserve-view=true&view=vs-2015).

    - Gerenciamento de itens de projeto, incluindo a adição de seu projeto à caixa de diálogo **novo projeto** . Para obter mais informações, consulte [Add Project and Project item templates](../../extensibility/internals/adding-project-and-project-item-templates.md) e [Register Project and item templates](../../extensibility/internals/registering-project-and-item-templates.md).

    - Persistência do estado do projeto e de itens individuais. Para obter mais informações, consulte [abrir e salvar itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md). Para persistência das informações da solução, consulte [soluções](../../extensibility/internals/solutions-overview.md).

    - Propriedades independentes de configuração para exibir no janela Propriedades. Para obter mais informações, consulte [estender Propriedades](../../extensibility/internals/extending-properties.md).

    - Propriedades de configuração de projeto conforme implementadas em páginas de propriedades para mostrar propriedades dependentes de configuração. Para obter mais informações, consulte [Gerenciar opções de configuração](../../extensibility/internals/managing-configuration-options.md).

    - Enumerando saídas para implantação. Para obter mais informações, consulte [configuração de projeto para saída](../../extensibility/internals/project-configuration-for-output.md).

    - Serviços de inicialização do projeto. Para obter mais informações, consulte [elementos de um modelo de projeto](../../extensibility/internals/elements-of-a-project-model.md) e [componentes principais do modelo de projeto](../../extensibility/internals/project-model-core-components.md).

    - Objetos ou classes derivadas de `IDispatch` , disponíveis para automação.

    - Arquivos de tabela de comando XML (*. vsct*). Para obter mais informações, consulte [arquivos de tabela de comando do Visual Studio (. vsct)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).

6. Teste, depure e inicie o tipo de projeto.

7. Exiba o projeto na guia **projeto** da caixa de diálogo **Adicionar referência** definindo `VARIANT_TRUE` como o valor de `VSHPROPID_ShowProjInSolutionPage` . Para obter mais informações, consulte <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>.

8. Crie o arquivo do Microsoft Installer (*. msi*) para instalar seu VSPackages. Para obter mais informações, consulte [instalar o VSPackages com Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md), [registrar um tipo de projeto](../../extensibility/internals/registering-a-project-type.md)e [VSPackages](../../extensibility/internals/vspackages.md).

## <a name="see-also"></a>Confira também
- [Hierarquias no Visual Studio](../../extensibility/internals/hierarchies-in-visual-studio.md)
- [Quando criar tipos de projeto](../../extensibility/internals/when-to-create-project-types.md)
- [Criar tipos de projeto](../../extensibility/internals/creating-project-types.md)