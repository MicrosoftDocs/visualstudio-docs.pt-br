---
title: Comandos, menus e barras de ferramentas | Microsoft Docs
description: Saiba mais sobre comandos, menus e barras de ferramentas no Visual Studio, incluindo o que eles são e como eles funcionam no VSPackages.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus [Visual Studio SDK], commands
- commands [Visual Studio]
- toolbars [Visual Studio], commands
ms.assetid: 07b4ed90-dbbd-40df-b6c9-8395fd6f2ab6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2a1b4cdb95fa5b053bc75efb559ea77b84ae56dd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057150"
---
# <a name="commands-menus-and-toolbars"></a>Comandos, menus e barras de ferramentas
Menus e barras de ferramentas são a maneira como os usuários acessam comandos em seu VSPackage. Os comandos são funções que realizam tarefas, como imprimir um documento, atualizar uma exibição ou criar um novo arquivo. Menus e barras de ferramentas são maneiras gráficas convenientes de apresentar seus comandos aos usuários. Normalmente, os comandos relacionados são agrupados no mesmo menu ou barra de ferramentas.

- Os menus normalmente são exibidos como cadeias de caracteres de uma palavra agrupadas em uma linha na parte superior do ambiente de desenvolvimento integrado (IDE) ou de uma janela de ferramentas. Os menus também podem ser exibidos como resultado de um evento de clique com o botão direito do mouse e são chamados de menus de atalho nesse contexto. Quando clicado, os menus expandem para exibir um ou mais comandos. Os comandos, quando clicados, podem executar tarefas ou iniciar submenus que contêm comandos adicionais. Alguns nomes de menu bem conhecidos são **arquivo**, **edição**, **exibição** e **janela**. Para obter mais informações, consulte [estender menus e comandos](../../extensibility/extending-menus-and-commands.md).

- Normalmente, as barras de ferramentas são linhas de botões e outros controles, como caixas de combinação, caixas de listagem, caixas de texto e controladores de menu. Todos os controles da barra de ferramentas estão associados a comandos. Quando você clica em um botão da barra de ferramentas, seu comando associado é ativado. Os botões da barra de ferramentas geralmente têm ícones que sugerem os comandos subjacentes, como uma impressora para um comando Print. Em um controle de lista suspensa, cada item da lista é associado a um comando diferente. Um controlador de menu é um híbrido no qual um lado do controle é um botão da barra de ferramentas e o outro lado é uma seta para baixo que exibe comandos adicionais quando clicado. Para obter mais informações, consulte [Adicionar um controlador de menu a uma barra de ferramentas](../../extensibility/adding-a-menu-controller-to-a-toolbar.md).

- Ao criar um comando, você também deve criar um manipulador de eventos para ele. O manipulador de eventos determina quando o comando é visível ou habilitado, permite que você modifique seu texto e garante que o comando responda adequadamente ("rotas") quando ativado. Na maioria dos casos, o IDE manipula comandos usando a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface. Comandos em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] rota de maneira hierárquica, começando com o contexto de comando mais interno, com base na seleção local, e prosseguindo para o contexto mais externo, com base na seleção global. Os comandos adicionados ao menu principal estão imediatamente disponíveis para scripts. Para obter mais informações, consulte [MenuCommands vs. OleMenuCommands](/previous-versions/visualstudio/visual-studio-2015/misc/menucommands-vs-olemenucommands?preserve-view=true&view=vs-2015) e [objetos de contexto de seleção](../../extensibility/internals/selection-context-objects.md).

  Para definir novos menus e barras de ferramentas, você deve descrevê-los em um arquivo de tabela de comando do Visual Studio (*. vsct*). O modelo de pacote do Visual Studio cria esse arquivo para você, juntamente com os elementos necessários para dar suporte a quaisquer comandos, barras de ferramentas e editores selecionados no modelo. Como alternativa, você pode escrever seu próprio arquivo *. vsct* , usando o esquema XML descrito aqui: [referência de esquema XML vsct](../../extensibility/vsct-xml-schema-reference.md).

  Para obter mais informações sobre como trabalhar com arquivos *. vsct* , consulte [arquivos de tabela de comando (. vsct) do Visual Studio](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).

  Os tópicos nesta seção explicam como os comandos, menus e barras de ferramentas funcionam no VSPackages.

## <a name="in-this-section"></a>Nesta seção
- [Como VSPackages adicionar elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 Uma descrição detalhada da especificação de formato de tabela de comando.

- [Arquivos de tabela de comando do Visual Studio (. vsct)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)

 Descreve uma sintaxe baseada em XML e um compilador para tabelas de comando.

- [Posicionamento do comando, grupo e barra de ferramentas padrão](../../extensibility/internals/default-command-group-and-toolbar-placement.md)

 Descreve comandos, grupos, menus e barras de ferramentas predefinidos.

- [Comandos, menus e grupos definidos pelo IDE](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)

 Especifica os menus, comandos e grupos de comandos predefinidos disponíveis para uso pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE.

- [Design de comando](../../extensibility/internals/command-design.md)

 Explica como criar comandos.

- [Otimizar menus e comandos da barra de ferramentas](../../extensibility/internals/optimizing-menu-and-toolbar-commands.md)

 Fornece diretrizes para comandos.

- [Tornar os comandos disponíveis](../../extensibility/internals/making-commands-available.md)

 Explica como disponibilizar comandos para o Visual Studio.

- [Comandos e menus que usam assemblies de interoperabilidade](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)

 Explica como implementar comandos que usam assemblies de interoperabilidade.

## <a name="related-sections"></a>Seções relacionadas
- [Roteamento de comandos em VSPackages](../../extensibility/internals/command-routing-in-vspackages.md)

 Explica o roteamento de comandos em VSPackages.