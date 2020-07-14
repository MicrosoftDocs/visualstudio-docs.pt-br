---
title: 'Designer de Fluxo de Trabalho-como: usar a navegação por trilha'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 4a688056-37dc-406a-9071-be2141e192fe
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2a432d7cfc40ad6116f570d0e7beb4bfc5b40493
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817457"
---
# <a name="how-to-use-breadcrumb-navigation"></a>Como: Use a navegação de rastreamento

Há três maneiras principais de alterar o conjunto de atividades que são exibidas no Designer de Fluxo de Trabalho:

1. Clique duas vezes para furar na uma atividade filho.

2. Clique em um botão na barra de rastreamento para navegar em uma atividade de ancestral.

3. Expandir ou recolher atividades no lugar.

## <a name="using-breadcrumb-navigation"></a>Usando a navegação de rastreamento

1. Clique duas vezes em uma atividade de Designer de Fluxo de Trabalho para alterar a atividade raiz para a atividade clicada. A atividade clicada é, então, totalmente expandida na raiz e seus ancestrais são mostrados na barra de navegação estrutural. Isso é às vezes chamado perfuração ou de uma atividade.

2. Para navegar a um predecessor de atividade atual da raiz, clique na atividade na barra de rastreamento.

## <a name="expanding-or-collapsing-an-activity-in-place"></a>Expandindo ou recolhendo uma atividade no lugar

1. Clique nas vigas em uma atividade expande ou recolhe a atividade no lugar.

2. Quando o estado do estado de expansão é alterado clicando no botão, o novo estado de expansão é salvo em XAML.

    > [!WARNING]
    > Nem todas as atividades podem ser expandidos no lugar. Há dois casos quando uma atividade não pode ser expandida no local: ou o pai da atividade não permite seus filhos sejam expandidos no lugar, (por exemplo, as atividades em um fluxograma não podem ser expandidos no local), ou o designer de atividade não se permite que é expandido no lugar. Embora nenhum dos designers de atividade incluídos no Designer de Fluxo de Trabalho tenha o último comportamento, algumas atividades personalizadas podem apresentar esse comportamento.

## <a name="expanding-all-or-collapsing-all-activities"></a>Tudo expandir ou recolher todas as atividades

1. Use os botões **expandir tudo** e **recolher tudo** na interface do usuário para expandir ou recolher todas as atividades na raiz de navegação estrutural atual. Observe que expande todas e recolhe todo é estados globais. Isso significa que, quando você altera a atividade raiz usando a navegação estrutural, o estado expandir tudo ou recolher tudo persiste até que você clique em **restaurar**.

2. Depois de aplicar um estado expandir tudo ou recolher tudo, você pode clicar no botão **restaurar** que aparece para voltar ao exame do estado aplicado anteriormente a cada atividade.

    > [!WARNING]
    > Se uma atividade, como <xref:System.Activities.Statements.Flowchart> , tiver optado por uma expansão em vigor, a funcionalidade associada aos botões **expandir tudo** e **recolher tudo** estará desabilitada no designer de **fluxograma** . Para obter mais informações sobre o designer de **fluxograma** , consulte o tópico [fluxograma](../workflow-designer/flowchart-activity-designer.md) .

    > [!WARNING]
    > Expandir tudo também tem um efeito especial nos designers de atividade **switch** e **TryCatch** . Quando você clica em **expandir tudo**, todos os casos de comutador e todos os blocos try/catch/finally são exibidos. Clicar em **restaurar** ou **recolher todos** retorna esses designers ao seu estado padrão, no qual você pode clicar em um caso/bloco individual para exibir seu conteúdo.
