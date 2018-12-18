---
title: Comandos, Menus e barras de ferramentas | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- menus [Visual Studio SDK], commands
- commands [Visual Studio]
- toolbars [Visual Studio], commands
ms.assetid: 07b4ed90-dbbd-40df-b6c9-8395fd6f2ab6
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8a8bd6716b40816ae625dcdb32fb62237aa543fd
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49928419"
---
# <a name="commands-menus-and-toolbars"></a>Comandos, menus e barras de ferramentas
Menus e barras de ferramentas são que os maneira como os usuários acessam comandos no VSPackage. Comandos são funções que realizam tarefas, como imprimir um documento, a atualização de uma exibição ou criando um novo arquivo. Menus e barras de ferramentas são maneiras gráficas convenientes para apresentar seus comandos aos usuários. Normalmente, comandos relacionados são agrupados juntos no mesmo menu ou barra de ferramentas.  
  
- Menus normalmente são exibidos como cadeias de caracteres de uma palavra em cluster em uma linha na parte superior do ambiente de desenvolvimento integrado (IDE) ou uma janela de ferramentas. Menus também podem ser exibidos como o resultado de um evento de mouse e são conhecidos como menus de atalho nesse contexto. Quando clicado, menus expanda para exibir um ou mais comandos. Comandos, quando clicado, podem realizar tarefas ou iniciar submenus que contêm comandos adicionais. Alguns nomes de menu bem conhecidos são **arquivo**, **editar**, **exibição**, e **janela**. Para obter mais informações, consulte [estendem os menus e comandos](../../extensibility/extending-menus-and-commands.md).  
  
- Normalmente, as barras de ferramentas são linhas de botões e outros controles, como caixas de combinação, caixas de listagem, caixas de texto e controladores de menu. Todos os controles de barra de ferramentas são associados a comandos. Quando você clica em um botão de barra de ferramentas, o comando associado está ativado. Botões da barra de ferramentas geralmente têm ícones que sugerem os comandos subjacentes, como uma impressora para um comando de impressão. Em um controle de lista suspensa, cada item na lista está associado um comando diferente. Um controlador de menu é um híbrido no qual um dos lados do controle é um botão de barra de ferramentas e o outro lado é uma seta para baixo que exibe comandos adicionais quando clicado. Para obter mais informações, consulte [adicionar um controlador de menu a uma barra de ferramentas](../../extensibility/adding-a-menu-controller-to-a-toolbar.md).  
  
- Quando você cria um comando, você também deve criar um manipulador de eventos para ele. O manipulador de eventos determina quando o comando é visível ou habilitada, permite que você modifique seu texto e garante que o comando responde apropriadamente ("rotas") quando ativado. Na maioria dos casos, o IDE manipula os comandos que usam o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface. Os comandos no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] rota de forma hierárquica, começando com o contexto do comando interno, com base na seleção de local e continuando para o contexto mais externo, com base na seleção global. Comandos adicionados ao menu principal estão imediatamente disponíveis para execução de scripts. Para obter mais informações, consulte [MenuCommands vs. OleMenuCommands](../../extensibility/menucommands-vs-olemenucommands.md) e [objetos de contexto de seleção](../../extensibility/internals/selection-context-objects.md).  
  
  Para definir novos menus e barras de ferramentas, você deve descrevê-los em uma tabela de comando do Visual Studio (*VSCT*) arquivos. O modelo de pacote do Visual Studio cria esse arquivo para você, juntamente com os elementos necessários para dar suporte a quaisquer comandos, barras de ferramentas e editores que você selecionou no modelo. Como alternativa, você pode escrever seus próprios *VSCT* do arquivo, usando o esquema XML descrito aqui: [referência de esquema XML do VSCT](../../extensibility/vsct-xml-schema-reference.md).  
  
  Para obter mais informações sobre como trabalhar com *VSCT* arquivos, consulte [arquivos de tabela (. VSCT) de comando do Visual Studio](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).  
  
  Os tópicos nesta seção explicam como comandos, menus e barras de ferramentas funcionam em VSPackages.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)  
 Uma descrição detalhada da especificação de formato de tabela do comando.  
  
 [Arquivos de tabela (. VSCT) de comando do Visual Studio](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)  
 Descreve uma sintaxe baseada em XML e o compilador para tabelas de comando.  
  
 [Posicionamento de comando, grupo e barra de ferramentas padrão](../../extensibility/internals/default-command-group-and-toolbar-placement.md)  
 Descreve os comandos predefinidos, grupos, menus e barras de ferramentas.  
  
 [Grupos, menus e comandos definidos pelo IDE](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)  
 Especifica o predefinidos de menus, comandos e grupos de comando disponíveis para uso pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE.  
  
 [Design de comando](../../extensibility/internals/command-design.md)  
 Explica como criar comandos.  
  
 [Otimizar os comandos de menu e barra de ferramentas](../../extensibility/internals/optimizing-menu-and-toolbar-commands.md)  
 Fornece diretrizes para comandos.  
  
 [Tornar os comandos disponíveis](../../extensibility/internals/making-commands-available.md)  
 Explica como tornar os comandos disponíveis para o Visual Studio.  
  
 [Comandos e menus que usam assemblies de interoperabilidade](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)  
 Explica como implementar comandos que usam assemblies de interoperabilidade.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Roteamento de comando em VSPackages](../../extensibility/internals/command-routing-in-vspackages.md)  
 Explica o roteamento de comando em VSPackages.