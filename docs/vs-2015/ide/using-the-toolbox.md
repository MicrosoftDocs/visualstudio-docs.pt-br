---
title: Usando a Caixa de Ferramentas | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.chooseitems
- vs.toolboxpages.activexcontrols
- VS.CHOOSEITEMS.windowsuixamlcomponents
- VS.chooseitems.silverlightcomponents
- VC.EDITORS.RIBBON
- vs.customizetoolbox
- VS.chooseitems.System.Workflow_Components
- vs.chooseitems.frameworkcomponents
- VS.ToolboxPages..NET_Framework_Components
- VS.chooseitems.Microsoft.VisualStudio.Toolbox.VsToolboxPage
- vs.chooseitems.comcomponents
- vs.toolboxpages.NGWS_components
helpviewer_keywords:
- toolbox, adding items
- Visual Studio, toolbox
- toolbox, tabs
- toolbox
ms.assetid: 82e7cb43-4d0b-4e17-b7b0-43f96c22c3c2
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 207beb085046748a4eaabdff025cd461c5ddba26
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68179301"
---
# <a name="using-the-toolbox"></a>Usando a caixa de ferramentas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar a caixa de ferramentas para adicionar controles e outros itens ao seu projeto. Você pode arrastar e soltar diferentes controles na superfície do designer que você está usando, redimensionar e posicionar os controles.  
  
 A caixa de ferramentas aparece com as exibições de designer, como a exibição de designer de um arquivo XAML. A caixa de ferramentas exibe apenas os controles que podem ser usados ​​no designer atual.  
  
 A versão .NET Framework de destino do seu projeto também afeta o conjunto de controles visíveis na caixa de ferramentas. Por padrão, os projetos [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] têm como destino o .NET Framework 4.5.1. Você pode configurar seu projeto para ter como destino uma versão diferente do .NET Framework selecionando o nó do projeto no **Gerenciador de Soluções** e navegando até **Propriedades/Aplicativo/Estrutura de Destino**.  
  
## <a name="managing-the-toolbox-and-its-controls"></a>Gerenciando a caixa de ferramentas e seus controles  
 Por padrão, a caixa de ferramentas fica recolhida no lado esquerdo do IDE do Visual Studio e aparece quando o cursor é movido sobre ela. É possível fixar a caixa de ferramentas (clicando no ícone **Fixar** na barra de ferramentas da caixa de ferramentas) para que ela permaneça aberta quando você move o cursor. Você também pode desencaixar a janela da caixa de ferramentas e arrastá-la para qualquer lugar na tela. Você pode encaixar, desencaixar e ocultar a caixa de ferramentas, clicando com o botão direito na barra de ferramentas da caixa de ferramentas e selecionando uma das opções.  
  
 Você pode reorganizar os itens em uma guia de caixa de ferramentas ou adicionar guias e itens personalizados usando os seguintes comandos no menu de contexto:  
  
- **Renomear Item** – renomeia o item selecionado.  
  
- **Mostrar Todos** – mostra todos os controles possíveis (e não apenas os que se aplicam ao designer atual).  
  
- **Exibição de Lista** – mostra os controles em uma lista vertical. Se todas as opções estiverem desmarcadas, os controles aparecem na horizontal.  
  
- **Escolher Itens** – abre a caixa de diálogo **Escolher Itens da Caixa de Ferramentas** para que você possa especificar os itens que aparecem na **Caixa de Ferramentas**. Você pode mostrar ou ocultar um item, marcando ou desmarcando a caixa de seleção.  
  
- **Classificar itens em ordem alfabética** – classifica os itens por nome.  
  
- **Redefinir barra de ferramentas** – restaura as configurações e itens padrão da caixa de ferramentas.  
  
- **Adicionar Guia** – adiciona uma nova guia da caixa de ferramentas.  
  
- **Mover para Cima** – move o item selecionado para cima.  
  
- **Mover para Baixo** – move o item selecionado para baixo.  
  
## <a name="creating-and-distributing-custom-toolbox-controls"></a>Criando e distribuindo controles da caixa de ferramentas  
 Você pode criar um controle de caixa de ferramentas personalizado no Visual Basic ou Visual C#, e pode começar com um modelo de projeto baseado no [Windows Presentation Foundation](../extensibility/creating-a-wpf-toolbox-control.md) ou no [Windows Forms](../misc/how-to-create-a-toolbox-control-that-uses-windows-forms.md). Você pode distribuir o controle para seus colegas de equipe ou publicá-lo na Web usando o [Instalador de Controles da Caixa de Ferramentas](http://download.microsoft.com/download/8/3/6/836657BD-9CCB-4ED4-B9D2-FB769473B284/TCI_whitepaper.docx).
