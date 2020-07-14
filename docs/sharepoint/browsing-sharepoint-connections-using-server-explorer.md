---
title: Procurando conexões do SharePoint usando Gerenciador de Servidores | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
f1_keywords:
- VS.SharePointTools.SharePointExplorer.SharePointConnection
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, browsing SharePoint sites
- SharePoint development in Visual Studio, SharePoint Connections
- SharePoint Connections [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: baf580ace98ab14032de1e9a3edf18af2b2cfee8
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016348"
---
# <a name="browse-sharepoint-connections-by-using-server-explorer"></a>Procurar conexões do SharePoint usando Gerenciador de Servidores
  Agora você pode procurar conexões locais do SharePoint em **Gerenciador de servidores**. Usando essa técnica, você pode navegar pelos componentes de um site do SharePoint em seu sistema. Os componentes do site do SharePoint, como definições de lista e tipos de conteúdo, aparecem em um nó chamado **conexões do SharePoint** no modo de exibição de árvore de **Gerenciador de servidores**. Para exibir **Gerenciador de servidores**, na barra de menus, escolha **Exibir**  >  **Gerenciador de servidores**. Além de exibir os componentes do site do SharePoint, você pode remover itens, exibir suas propriedades ou atualizar o modo de exibição de árvore usando comandos no menu de atalho.

> [!IMPORTANT]
> Para procurar um site do SharePoint, você deve ser um administrador do conjunto de sites do SharePoint e deve estar executando o Visual Studio como administrador do computador local. Caso contrário, o site aparecerá em **Gerenciador de servidores**, mas você não poderá expandir seu nó. Para verificar se você é um administrador do conjunto de sites, abra o site em um navegador da Web, abra o menu **ações do site** , escolha **permissões do site**e, na página **permissões: site da equipe** , escolha o comando administradores do conjunto de **sites** no grupo **gerenciar** na faixa de seleção. Seu nome aparecerá na caixa de texto se você for um administrador do conjunto de sites. Se o comando **Administradores do conjunto de sites** não aparecer no grupo Gerenciar na faixa de, você não é um administrador do conjunto de sites e deve obter as permissões apropriadas do administrador do site.

## <a name="server-explorer-nodes"></a>Nós de Gerenciador de Servidores
 Cada componente de um site do SharePoint é representado por um nó no modo de exibição de árvore de **Gerenciador de servidores** em **conexões do SharePoint**. Por exemplo, sites padrão do SharePoint incluem um tipo de conteúdo chamado Discussion, que representa um tipo de discussão que é exibido na página **discussões** do site do SharePoint. O tipo de conteúdo de discussão contém vários campos. Para exibir esses campos em **Gerenciador de servidores**, expanda o nó **ContentTypes** e, em seguida, o nó **discussão** . Sob ele, há vários nós de campo, como corpo, assunto da discussão e título.

## <a name="node-shortcut-menu-commands"></a>Comandos do menu de atalho do nó
 Cada nó tem um menu de atalho que você acessa clicando com o botão direito do mouse no nó ou escolhendo-o e escolhendo as teclas **Shift** + **F10** . Os comandos de nó podem incluir o seguinte:

|Nome do comando|Descrição|
|------------------|-----------------|
|Atualizar|Atualiza o modo de exibição de árvore para refletir as alterações que possam ter ocorrido desde a última vez em que o nó foi exibido.|
|Excluir|Remove o nó selecionado da exibição de árvore. **Observação:**  Esse comando é habilitado somente em conexões do SharePoint listadas no nó **conexões do SharePoint** .|
|Propriedades|Exibe as propriedades disponíveis para o nó selecionado na janela **Propriedades** . As propriedades são somente leitura e nem cada nó tem propriedades associadas a ela.|
|Adicionar Conexão|Permite especificar um site do SharePoint que você deseja procurar. Disponível no nó **conexões do SharePoint** e nós de subsite.|
|Exibir no navegador|Exibe a lista selecionada no navegador da Web. Esse comando está disponível em algumas listas no nó **listas** , que está contido em **listas e bibliotecas**.|

## <a name="related-topics"></a>Tópicos relacionados

|Title|Descrição|
|-----------|-----------------|
|[Como: Adicionar ou remover conexões do SharePoint](../sharepoint/how-to-add-or-remove-sharepoint-connections.md)|Descreve as etapas necessárias para adicionar um novo site do SharePoint ao nó **conexões do SharePoint** no **Gerenciador de servidores**.|

## <a name="see-also"></a>Consulte também
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)
