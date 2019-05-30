---
title: Design de comando | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands
- commands, implementation
ms.assetid: 097108c3-f758-4b87-89d6-b32d12d9041a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e1644cfa71296c4233cf17b6b225933aeeb3d477
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66342169"
---
# <a name="command-design"></a>Design de comando
Quando você adiciona um comando a um VSPackage, você deve especificar onde ele deve ser exibido quando ele está disponível e como ele deve ser tratada.

## <a name="define-commands"></a>Definir comandos
 Para definir novos comandos, incluir uma tabela de comando do Visual Studio (*VSCT*) o arquivo em seu projeto de VSPackage. Se você tiver criado um VSPackage usando o modelo de pacote do Visual Studio, o projeto inclui um desses arquivos. Para obter mais informações, consulte [arquivos de tabela (. VSCT) de comando do Visual Studio](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).

 Visual Studio mescla todos os *VSCT* arquivos localiza para que ele possa exibir os comandos. Como esses arquivos são distintos de VSPackage binário, o Visual Studio não tem ao carregar o pacote para localizar os comandos. Para obter mais informações, consulte [VSPackages como adicionar elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md).

 O Visual Studio usa o <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> atributo de registro para definir recursos do menu e comandos. Para obter mais informações, consulte [implementação do comando](../../extensibility/internals/command-implementation.md).

 Comandos podem ser alterados em tempo de execução de várias maneiras diferentes. Eles podem ser exibidos ou ocultos, habilitados ou desabilitados. Eles podem exibir texto diferente ou ícones ou contêm valores diferentes. Uma grande quantidade de personalização pode ser executada antes que o Visual Studio carregará o VSPackage. Para obter mais informações, consulte [VSPackages como adicionar elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md).

## <a name="command-handlers"></a>Manipuladores de comandos
 Quando você cria um comando, você deve fornecer um manipulador de eventos para executar o comando. Se o usuário seleciona o comando, ele deve ser adequadamente roteado. Roteamento de um comando significa enviá-la para o VSPackage correto para habilitar ou desabilitá-lo, ocultar ou exibi-lo e executá-lo se o usuário optar por fazê-lo. Para obter mais informações, consulte [algoritmo de roteamento do comando](../../extensibility/internals/command-routing-algorithm.md).

## <a name="visual-studio-command-environment"></a>Ambiente de comando do Visual Studio
 Visual Studio pode hospedar qualquer número de VSPackages e cada um pode contribuir com seu próprio conjunto de comandos. O ambiente exibe somente os comandos que são apropriados para a tarefa atual. Para obter mais informações, consulte [disponibilidade de comando](../../extensibility/internals/command-availability.md) e [objetos de contexto de seleção](../../extensibility/internals/selection-context-objects.md).

 Um VSPackage que define novos comandos, menus, barras de ferramentas ou menus de atalho fornece suas informações de comando do Visual Studio no momento da instalação por meio de entradas do registro que fazem referência a recursos em assemblies nativos ou gerenciados. Cada recurso, em seguida, faz referência a um recurso de dados binários (*CTO já*) o arquivo, que é gerado quando você compila uma tabela de comando do Visual Studio (*VSCT*) arquivos. Isso permite que o Visual Studio fornecer conjuntos de comandos mesclado, menus e barras de ferramentas sem ter que carregar cada VSPackage instalado.

### <a name="command-organization"></a>Organização de comando
 O ambiente posiciona comandos por grupo, prioridade e menu.

- Grupos são coleções lógicas de comandos relacionados, por exemplo, o **Recortar**, **cópia**, e **colar** grupo de comandos. Grupos são os comandos que aparecem nos menus.

- Prioridade determina a ordem na qual os comandos individuais em um grupo aparecem no menu.

- Menus atuam como contêineres para grupos.

  O ambiente predefine alguns comandos, grupos e menus. Para obter mais informações, consulte [posicionamento de comando, grupo e barra de ferramentas padrão](../../extensibility/internals/default-command-group-and-toolbar-placement.md).

  Um comando pode ser atribuído a um grupo primário. O grupo primário controla a posição do comando na estrutura do menu principal e além de **personalizar** caixa de diálogo. Um comando pode aparecer em vários grupos; Por exemplo, um comando pode ser, no menu principal, um menu de atalho e uma barra de ferramentas. Para obter mais informações, consulte [VSPackages como adicionar elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md).

### <a name="command-routing"></a>Roteamento de comando
 O processo de invocação e roteamento de comandos para VSPackages difere do processo de chamada de métodos em instâncias de objeto.

 O ambiente roteia comandos em sequência do contexto interno de comando (local), que se baseia na seleção atual, para o contexto mais externo (global). O primeiro contexto que é capaz de executar o comando é aquela que lida com isso. Para obter mais informações, consulte [algoritmo de roteamento do comando](../../extensibility/internals/command-routing-algorithm.md).

 Na maioria dos casos, o ambiente manipula os comandos usando o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface. Porque o esquema de roteamento de comando permite que vários objetos diferentes lidar com comandos, <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> pode ser implementada por qualquer número de objetos; eles incluem controles Microsoft ActiveX, implementações de modo de exibição da janela, objetos de documento, hierarquias de projeto e objetos de VSPackage (para comandos globais). Em alguns casos especializados, por exemplo, rotear comandos em uma hierarquia, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> interface deve ser implementada.

## <a name="related-topics"></a>Tópicos relacionados

|Título|Descrição|
|-----------|-----------------|
|[Implementação do comando](../../extensibility/internals/command-implementation.md)|Descreve como implementar comandos em um VSPackage.|
|[Disponibilidade do comando](../../extensibility/internals/command-availability.md)|Descreve como o contexto do Visual Studio determina quais comandos estão disponíveis.|
|[Algoritmo de roteamento de comando](../../extensibility/internals/command-routing-algorithm.md)|Descreve como a arquitetura de roteamento de comando do Visual Studio permite que os comandos a serem manipuladas por diferentes VSPackages.|
|[Diretrizes de posicionamento do comando](../../extensibility/internals/command-placement-guidelines.md)|Sugere como posicionar os comandos no ambiente do Visual Studio.|
|[Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)|Descreve como os VSPackages pode utilizar melhor a arquitetura de comando do Visual Studio.|
|[Posicionamento de comando, grupo e barra de ferramentas padrão](../../extensibility/internals/default-command-group-and-toolbar-placement.md)|Descreve como os VSPackages melhor pode usar os comandos que estão incluídos no Visual Studio.|
|[Gerenciar VSPackages](../../extensibility/managing-vspackages.md)|Descreve como o Visual Studio carrega os VSPackages.|
|[Arquivos de tabela (. VSCT) de comando do Visual Studio](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)|Fornece informações sobre baseado em XML *VSCT* arquivos, que são usados para descrever o layout e aparência de comandos em VSPackages.|