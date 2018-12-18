---
title: Designer de fluxo de trabalho - atalhos de teclado no Designer de fluxo de trabalho
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- WFDKeyboardShortcuts.UI
ms.assetid: 9be75438-a4a3-4781-94e5-45b7ec082358
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e4040a5b370674e7794b09e4d1cae68f424c7792
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49887365"
---
# <a name="keyboard-shortcuts-in-the-workflow-designer"></a>Atalhos de teclado no Designer de Fluxo de Trabalho

Toda a funcionalidade de núcleo do Designer de fluxo de trabalho pode ser acessada pelo teclado.

## <a name="navigating-the-workflow-designer-using-the-keyboard"></a>Navegando em Designer de Fluxo de Trabalho usando o teclado

Dentro do Visual Studio, os atalhos globais e os atalhos de depuração se aplicam ao Designer de fluxo de trabalho. Além disso, um número de atalhos de teclado específicos do Designer de fluxo de trabalho ter sido criado. No Visual Studio, todos os atalhos de teclado podem ser remapeados. No entanto, em um aplicativo rehosted, esses atalhos de teclado são embutidas em código.

### <a name="workflow-designer-keyboard-shortcuts"></a>Atalhos de teclado Designer de Fluxo de Trabalho

A tabela a seguir resume os atalhos de teclado padrão atribuídos aos comandos de Designer de fluxo de trabalho.

|Atalho|Finalidade|
|-|-------------|
|CTRL+E, A|Mostra ou oculta o designer do argumento.|
|CTRL+E, C 2.0|Recolhe a atividade selecionada no lugar.|
|CTRL+E, E|Expandir a atividade selecionada no lugar.|
|CTRL+E, F- 2.0|Conecta as atividades selecionadas em um fluxograma.|
|CTRL+E, I|Mostra ou oculta o designer imports.|
|CTRL+E, M|Move o foco do teclado para o próximo item na ordem de tabulação.|
|CTRL+E, N|Cria uma nova variável no escopo da atividade selecionada (ou o mais próximo.)|
|CTRL+E, O|Mostra ou oculta o mapa da revisão.|
|CTRL+E, P|Navega para o pai da atividade selecionada. Isso vai a um nível em navegação de rastreamento e altera a atividade raiz na superfície de designer.|
|CTRL+E, S|Adiciona o item com foco do teclado a seleção atual.|
|CTRL+E, V|Mostra ou oculta o designer variável.|
|CTRL+E, X|Expande todas as atividades no fluxo de trabalho.|
|CTRL+ALT+F6|Foco do teclado dos movimentos da área atual do usuário para a área seguir na sequência. A ordem é a seguinte:<br /><br /> 1.  Barra de navegação de rastreamento.<br />2.  A superfície do designer<br />3.  Designer dos argumentos/variáveis/imports se aberto<br />4.  Shell|

### <a name="flowchart"></a>Fluxograma

A lista a seguir mostra os gestos usados para construir um fluxograma pelo teclado. Como no restante do Designer de fluxo de trabalho, as atividades são adicionadas à superfície do designer usando os atalhos globais da caixa de ferramentas fornecidos com o Visual Studio.

- Para mover uma atividade, selecione a atividade e use as teclas de seta para reposicioná-la.

- Para redimensionar um fluxograma, mover uma atividade após a borda atual do fluxograma usando as teclas de direção. O fluxograma é redimensionado automaticamente.

- Para definir uma atividade como o nó inicial, use o **DataSet como StartNode** comando no menu de contexto.

- Para conectar atividades:

    1.  Selecione a atividade de origem alternar a atividade.

    2.  Pressione CTRL+E, M quantas vezes forem necessárias mover o foco do teclado a atividade de destino.

    3.  Pressione CTRL+E, S para adicionar a atividade de destino a seleção.

    4.  Pressione CTRL+E, F- 2.0 para adicionar o conector de origem para o destino.

Notas sobre como conectar atividades pelo teclado:

- Você pode fazer várias conexões ao mesmo tempo, adicionando mais atividades a seleção antes de pressionar CTRL + E, F. As conexões são feitas na ordem em que as atividades foram adicionadas à seleção.

- Se um par de atividades não pode ser conectado, por exemplo se a atividade de origem já tiver uma conexão de saída, conexões entre outras atividades na seleção é feito ainda sempre que possível.

- Quando um **FlowDecision** está incluído na seleção e o **FlowDecision** não tem nenhum conector de saída, o conector é colocado no **verdadeiro** branch.

### <a name="expression-editing"></a>Edição de expressão

Por padrão, os atalhos de teclado padrão para edição de texto do Visual Basic se aplicam no editor de expressão no Designer de fluxo de trabalho, com as seguintes limitações:

- O remapeamento atalhos de teclado para os seguintes comandos não tem efeito. Você pode usar os atalhos de teclado padrão para acessar esses comandos para editar uma expressão.

   - Recortar
   - Copiar
   - Colar
   - Selecionar Tudo
   - Desfazer
   - Refazer

- Para remapear atalhos de teclado para comandos de edição de expressão dentro do Designer de fluxo de trabalho no Visual Studio, edite os atalhos no escopo do Designer de fluxo de trabalho. As alterações feitas no escopo do Editor de texto não são aplicadas automaticamente ao Designer de fluxo de trabalho. Se você deseja remapear atalhos nos dois lugares, você deve aplicar as alterações duas vezes (uma vez para cada escopo).