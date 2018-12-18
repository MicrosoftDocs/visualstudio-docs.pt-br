---
title: Localizar chamadas para um método
ms.date: 05/18/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.CallHierarchy
helpviewer_keywords:
- Call Hierarchy
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0f386d3d73de45c539752207fb55200e8e8ee715
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49905943"
---
# <a name="view-call-hierarchy"></a>Exibir hierarquia de chamada

Ao exibir a hierarquia de chamadas para seu o código, você poderá navegar todas as chamadas de, a às vezes para, um método, propriedade ou construtor selecionado. Isso permite compreender melhor como o código flui, bem como avaliar os efeitos das alterações no código. Você pode examinar vários níveis de código para exibir cadeias complexas de chamadas de método e pontos de entrada adicionais para o código. Isso permite que você explore todos os possíveis caminhos de execução.

No Visual Studio, você pode exibir uma hierarquia de chamada em tempo de design. Isso significa que você não precisa definir um ponto de interrupção e iniciar o depurador para exibir a pilha de chamadas de tempo de execução.

## <a name="use-the-call-hierarchy-window"></a>Usar a janela Hierarquia de Chamada

Para exibir a janela **Hierarquia de Chamada**, clique com o botão direito no editor de código no nome de uma chamada de método, propriedade ou construtor e clique em **Exibir Hierarquia de Chamadas**.

O nome do membro é exibido em um painel de modo de exibição de árvore na janela **Hierarquia de Chamada**. Se você expandir o nó membro, os subnós **Chamadas para** *nome do membro* e para C++, **Chamadas de** *nome do membro* serão exibidos.

Para o código C++, você pode ver as chamadas de e para um membro:

![Hierarquia de chamadas do código C++ no Visual Studio](media/call-hierarchy-cpp.png)

Para código em C# e em Visual Basic, você pode ver as chamadas para um membro, mas não chamadas de:

![Hierarquia de chamadas do código C# no Visual Studio](media/call-hierarchy-csharp.png)

- Se você expandir o nó **Chamadas para**, todos os membros que chamam o membro selecionado serão exibidos.

- Para C++, se você expandir o nó **Chamadas de**, todos os membros que são chamados pelo membro selecionado serão exibidos.

Assim, você pode expandir cada membro que chama a fim de ver os nós **Chamadas para**, e para C++, **Chamadas de**. Isso permite navegar pela pilha de chamadores, conforme mostrado na imagem a seguir:

![Janela da Hierarquia de chamadas com vários níveis expandidos](media/call-hierarchy-csharp-expanded.png)

Para membros definidos como virtuais ou abstratos, um nó **Substitui o nome do método** é exibido. Para membros de interface, um nó **Implementa o nome do método** é exibido. Esses nós expansíveis aparecem no mesmo nível que os nós **Chamadas para** e **Chamadas de**.

A caixa **Escopo da Pesquisa** na barra de ferramentas contém opções para **Minha Solução**, **Projeto Atual** e **Documento Atual**.

Quando você seleciona um membro filho no painel do modo de exibição de árvore **Hierarquia de Chamada**:

- O painel de detalhes **Hierarquia de Chamada** exibe todas as linhas de código em que esse membro filho é chamado pelo membro pai.

- A janela de **Definição de Código**, se estiver aberta, exibe o código do membro selecionado (apenas C++). Para saber mais sobre essa janela, confira [Exibir a estrutura do código](../../ide/viewing-the-structure-of-code.md).

> [!NOTE]
> O recurso **Hierarquia de Chamadas** não encontra referências do grupo ao método, que incluem os locais a que um método é adicionado como manipulador de eventos ou é atribuído a um representante. Para localizar todas as referências a um método, você pode usar o comando **Localizar Todas as Referências**.

## <a name="shortcut-menu-items"></a>Itens do menu de atalho

A tabela a seguir descreve várias opções de menu de atalho que são disponibilizadas quando você clica com o botão direito do mouse em um nó no painel do modo de exibição de árvore.

|Item de menu de contexto|Descrição|
| - |-----------------|
|**Adicionar como Nova Raiz**|Adiciona o nó selecionado ao painel do modo de exibição de árvore como um novo nó raiz. Isso permite concentrar sua atenção em uma subárvore específica.|
|**Remover Raiz**|Remove o nó raiz selecionado do painel do modo de exibição de árvore. Esta opção está disponível somente de um nó raiz.<br /><br /> Você também pode usar o botão de barra de ferramentas **Remover Raiz** para remover o nó raiz selecionado.|
|**Ir para Definição**|Executa o comando Ir para Definição no nó selecionado. Isso leva até a definição original de uma chamada de membro ou definição de variável.<br /><br /> Para executar o comando Ir para Definição, você também pode clicar duas vezes no nó selecionado ou pressionar F12 no nó selecionado.|
|**Localizar Todas as Referências**|Executa o comando Localizar Todas as Referências no nó selecionado. Isso localiza todas as linhas de código em seu projeto que fazem referência a uma classe ou membro.<br /><br /> Também é possível usar SHIFT + F12 para executar o comando Localizar Todas as Referências no nó selecionado.|
|**Copiar**|Copia o conteúdo do nó selecionado (mas não de seus subnós).|
|**Atualizar**|Recolhe o nó selecionado de forma que expandi-lo novamente exibe informações atualizadas.|