---
title: 'Designer de fluxo de trabalho - como: usar a navegação estrutural'
ms.date: 11/04/2016
ms.topic: conceptual
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
ms.assetid: 4a688056-37dc-406a-9071-be2141e192fe
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 59d1012a3a291c2f49cf5fd5e447ce46909c0cdd
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39512272"
---
# <a name="how-to-use-breadcrumb-navigation"></a>Como: Use a navegação de rastreamento

Há três maneiras principais de alterar o conjunto de atividades que são exibidos no Designer de fluxo de trabalho:

1.  Clique duas vezes para furar na uma atividade filho.

2.  Clique em um botão na barra de rastreamento para navegar em uma atividade de ancestral.

3.  Expandir ou recolher atividades no lugar.

## <a name="using-breadcrumb-navigation"></a>Usando a navegação de rastreamento

1.  Clique duas vezes em uma atividade do Designer de fluxo de trabalho para alterar a atividade raiz para a atividade clicado. A atividade clicado, em seguida, é totalmente expandida na raiz e seus ancestrais são mostrados na barra de navegação estrutural. Isso é às vezes chamado perfuração ou de uma atividade.

2.  Para navegar a um predecessor de atividade atual da raiz, clique na atividade na barra de rastreamento.

## <a name="expanding-or-collapsing-an-activity-in-place"></a>Expandindo ou recolhendo uma atividade no lugar

1.  Clique nas vigas em uma atividade expande ou recolhe a atividade no lugar.

2.  Quando o estado do estado de expansão é alterado clicando no botão, o novo estado de expansão é salvo em XAML.

    > [!WARNING]
    > Nem todas as atividades podem ser expandidos no lugar. Há dois casos quando uma atividade não pode ser expandida no local: ou o pai da atividade não permite seus filhos sejam expandidos no lugar, (por exemplo, as atividades em um fluxograma não podem ser expandidos no local), ou o designer de atividade não se permite que é expandido no lugar. Embora nenhum Designer de atividade incluído no Designer de fluxo de trabalho tem o último comportamento, algumas atividades personalizadas podem exibir esse comportamento.

## <a name="expanding-all-or-collapsing-all-activities"></a>Tudo expandir ou recolher todas as atividades

1.  Use o **Expandir tudo** e **Recolher tudo** botões na interface do usuário para expandir ou recolher todas as atividades na raiz atual de rastreamento. Observe que expande todas e recolhe todo é estados globais. Isso significa que quando você altera a atividade raiz usando a navegação de trilha, expandir ou recolhe qualquer estado persiste até que você clique em **restaurar**.

2.  Depois que você aplicou qualquer expandir ou recolhe qualquer estado, você pode clicar na **restaurar** botão que aparece para voltar para examinar o estado anteriormente aplicado a cada atividade.

    > [!WARNING]
    > Se uma atividade, como <xref:System.Activities.Statements.Flowchart>, optou fora de expanda local, a funcionalidade associada com o **Expandir tudo** e **Recolher tudo** botões está desabilitado no **fluxograma**  designer. Para obter mais informações sobre o **fluxograma** designer, consulte o [fluxograma](../workflow-designer/flowchart-activity-designer.md) tópico.

    > [!WARNING]
    > Expandir tudo também tem um efeito especial **comutador** e **TryCatch** designers de atividade. Quando você clica em **Expandir tudo**, todos os casos de comutador e todos os blocos try/catch/finally são exibidos. Clicando em **restaurar** ou **Recolher tudo** retorna esses designers para seu estado padrão, no qual você pode clicar em um casos/bloco individuais para exibir seu conteúdo.