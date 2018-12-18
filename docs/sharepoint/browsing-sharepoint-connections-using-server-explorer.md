---
title: Navegando em conexões do SharePoint usando o Gerenciador de servidores | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.SharePointExplorer.SharePointConnection
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, browsing SharePoint sites
- SharePoint development in Visual Studio, SharePoint Connections
- SharePoint Connections [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: e897469eee33a1e4ee48b9096714b4213c099a8f
ms.sourcegitcommit: e6b13898cfbd89449f786c2e8f3e3e7377afcf25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/22/2018
ms.locfileid: "36325989"
---
# <a name="browse-sharepoint-connections-by-using-server-explorer"></a>Procurar conexões do SharePoint usando o Gerenciador de servidores
  Agora você pode procurar conexões locais do SharePoint no **Gerenciador de servidores**. Ao usar essa técnica, você pode navegar através dos componentes de um site do SharePoint em seu sistema. Componentes do site do SharePoint, como definições de listas e tipos de conteúdo, são exibidos em um nó que é denominado **conexões do SharePoint** na exibição de árvore da **Gerenciador de servidores**. Para exibir **Gerenciador de servidores**, na barra de menus, escolha **exibição** > **Server Explorer**. Além de exibir os componentes do site do SharePoint, você pode remover itens, exibir suas propriedades ou atualizar a exibição de árvore usando comandos no menu de atalho.  
  
> [!IMPORTANT]  
>  Para procurar um site do SharePoint, você deve ser um administrador do conjunto de sites do SharePoint, e você deve estar executando o Visual Studio como administrador do computador local. Caso contrário, o site será exibido na **Gerenciador de servidores**, mas você não pode expandir o nó. Para verificar se você for um administrador do conjunto de sites, abra o site em um navegador da web, abra o **ações do Site** menu, escolha **permissões de Site**e, em seguida, no **permissões: equipe Site** , escolha o **os administradores de coleção de sites** comando da **gerenciar** grupo na faixa de opções. Seu nome será exibido na caixa de texto, se você for um administrador de conjunto de sites. Se o **administradores de coleção de sites** comando não aparece no grupo Gerenciar da faixa de opções, você não for um administrador para o conjunto de sites e você deve obter as permissões adequadas de administrador do site.  
  
## <a name="server-explorer-nodes"></a>Nós do Gerenciador de servidor
 Todos os componentes de um site do SharePoint é representado por um nó na **Gerenciador de servidores** em modo de exibição de árvore **conexões do SharePoint**. Por exemplo, sites do SharePoint padrão incluem um tipo de conteúdo chamado discussão, que representa um tipo de discussão que exibe a **discussões** página do site do SharePoint. O tipo de conteúdo de discussão contém vários campos. Para exibir esses campos em **Gerenciador de servidores**, expanda o **ContentTypes** nó e, em seguida, o **discussão** nó. Em que ele são vários nós de campo, como título, assunto da discussão e corpo.  
  
## <a name="node-shortcut-menu-commands"></a>Comandos de menu de atalho do nó
 Cada nó tem um menu de atalho que você pode acessar clicando com botão direito no nó ou selecioná-la e, em seguida, escolhendo a **Shift**+**F10** chaves. Comandos de nó podem incluir o seguinte:  
  
|Nome do comando|Descrição|  
|------------------|-----------------|  
|Atualizar|Atualiza a exibição de árvore para refletir quaisquer alterações que possam ter ocorrido desde a última vez em que o nó foi exibido.|  
|Excluir|Remove o nó selecionado da exibição de árvore. **Observação:** esse comando é habilitado somente em conexões do SharePoint listadas sob o **conexões do SharePoint** nó.|  
|Propriedades|Exibe as propriedades disponíveis para o nó selecionado na **propriedades** janela. As propriedades são somente leitura e não todos os nós têm propriedades associadas a ele.|  
|Adicionar Conexão|Permite que você especifique um site do SharePoint que você deseja procurar. Disponível na **conexões do SharePoint** nó e nós subsite.|  
|Exibir no navegador|Exibe a lista selecionada no navegador da Web. Esse comando está disponível em algumas listas sob o **lista** nó que está contida no **listas e bibliotecas**.|  
  
## <a name="related-topics"></a>Tópicos relacionados
  
|Título|Descrição|  
|-----------|-----------------|  
|[Como: Adicionar ou remover conexões do SharePoint](../sharepoint/how-to-add-or-remove-sharepoint-connections.md)|Descreve as etapas necessárias para adicionar um novo site do SharePoint para o **conexões do SharePoint** nó no **Gerenciador de servidores**.|  
  
## <a name="see-also"></a>Consulte também
 [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)  
  
 
