---
title: Designer de fluxo de trabalho - Designer de atividade PickBranch
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Statements.PickBranch.UI
ms.assetid: f523ad47-bbc0-4cda-a35c-41e67c4ba081
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e45c8ec2d7af5f1bfde5e145607728d3ff0bc85d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49831777"
---
# <a name="pickbranch-activity-designer"></a>Designer de atividade de PickBranch

<xref:System.Activities.Statements.PickBranch> fornece um caminho de execução baseado em uma atividade de <xref:System.Activities.Statements.Pick> que pode ser acionada por um evento de entrada.

## <a name="pickbranch"></a>PickBranch

os objetos de<xref:System.Activities.Statements.PickBranch> estão contidos na coleção de <xref:System.Activities.Statements.Pick.Branches%2A> de uma atividade de <xref:System.Activities.Statements.Pick> . Cada <xref:System.Activities.Statements.PickBranch> está contido em uma ramificação de atividade de <xref:System.Activities.Statements.Pick> e pode ser executado devido a qualquer evento de entrada que serve como um disparador. Dessa forma o Designer de fluxo de trabalho fornece a modelagem de fluxo de controle baseado em evento. Cada <xref:System.Activities.Statements.PickBranch> contém <xref:System.Activities.Statements.PickBranch.Trigger%2A> e <xref:System.Activities.Statements.PickBranch.Action%2A>.

### <a name="how-to-use-the-pick-activity-designer"></a>Como usar o designer de atividade de picareta

Acesso a **PickBranch** designer na **fluxo de controle** categoria dos **caixa de ferramentas**.

Dois vazio <xref:System.Activities.Statements.PickBranch> objetos com nomes para exibição de **Branch1** e **Branch2** são criados por padrão como elementos de um <xref:System.Activities.Statements.Pick> atividade quando o **escolher** designer de atividade é solto inicialmente para o Designer de fluxo de trabalho. Esses respectivos <xref:System.Activities.Statements.PickBranch.DisplayName%2A> valores de propriedade podem ser editados na **PickBranch** cabeçalho do designer ou dentro de **propriedades** janela para cada ramificação.

Há duas maneiras de adicionar <xref:System.Activities.Statements.PickBranch> objetos à coleção de um <xref:System.Activities.Statements.Pick> objeto: arrastando e soltando o **PickBranch** designer dos **caixa de ferramentas**, ou usando o menu de contexto do dentro de **escolher** superfície de design:

- O **PickBranch** designer cria um <xref:System.Activities.Statements.PickBranch> quando ele é arrastado dos **caixa de ferramentas** e solto em um dos ramificações de um **escolher** designer de atividade no Superfície do Designer de fluxo de trabalho. Novos objetos de <xref:System.Activities.Statements.PickBranch> podem ser colocados dentro do designer de <xref:System.Activities.Statements.Pick> para a esquerda ou direita de todos os elementos existentes de <xref:System.Activities.Statements.PickBranch> já contidos na coleção. Ao arrastar uma **PickBranch** designer para o **escolher** designer com o mouse, o **escolher** designer usa uma faixa azul cinza vertical para indicar onde o <xref:System.Activities.Statements.PickBranch> é adicionado para um determinada posicionamento do mouse.

- Clique com botão direito **escolher** designer de atividade (mas não estão dentro **PickBranch** designer) para obter um menu de contexto e selecione **criar ramificação** para adicionar um novo <xref:System.Activities.Statements.PickBranch>. Observe que o novo <xref:System.Activities.Statements.PickBranch> é adicionada à direita da existente <xref:System.Activities.Statements.PickBranch> objetos na **escolher** designer.

O **PickBranch** designer pode ser expandido para revelar as **gatilho** e **ação** caixas ou recolhidos clicando-se os sinais de interpolação duplas no lado direito dos cabeçalhos. Editar o <xref:System.Activities.Statements.PickBranch.Trigger%2A> e <xref:System.Activities.Statements.PickBranch.Action%2A> de cada <xref:System.Activities.Statements.PickBranch> soltando atividades na **gatilho** e **ação** caixas de seus designers.

O <xref:System.Activities.Statements.PickBranch> objetos na <xref:System.Activities.Statements.Pick.Branches%2A> coleção de uma <xref:System.Activities.Statements.Pick> de objeto, podem ser reordenadas arrastando e soltando-os para um novo local dentro de **escolher** designer. O **escolher** designer usa uma faixa azul cinza vertical para indicar onde o <xref:System.Activities.Statements.PickBranch> é adicionado para um determinada posicionamento do mouse.

Há duas maneiras para excluir <xref:System.Activities.Statements.PickBranch>:

- Selecione o **PickBranch** designer e excluí-lo.
- Selecione o **PickBranch** designer, clique com botão direito para obter o menu de contexto e selecione **excluir**.

Certifique-se de selecionar o **PickBranch** designer, como selecionar uma das atividades dentro de seu **gatilho** ou **ação** encaixota exclui por engano uma dessas atividades e não o <xref:System.Activities.Statements.PickBranch> objeto.

### <a name="pickbranch-properties-in-the-workflow-designer"></a>Propriedades de PickBranch em Designer de Fluxo de Trabalho

A tabela a seguir mostra os mais úteis <xref:System.Activities.Statements.PickBranch> propriedades e descreve como usá-los no Designer de fluxo de trabalho.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Statements.PickBranch.DisplayName%2A>|False|O nome amigável exibido no cabeçalho do **PickBranch** designer. O valor padrão é ramificação.<br /><br /> Embora não seja necessário <xref:System.Activities.Activity.DisplayName%2A> restrita, é uma prática recomendada usar um.|
|<xref:System.Activities.Statements.PickBranch.Trigger%2A>|verdadeiro|Cada <xref:System.Activities.Statements.PickBranch> contém uma ação de <xref:System.Activities.Statements.PickBranch.Trigger%2A> que pode chamar <xref:System.Activities.Statements.PickBranch.Action%2A>.|
|<xref:System.Activities.Statements.PickBranch.Action%2A>|False|Cada <xref:System.Activities.Statements.PickBranch> contém <xref:System.Activities.Statements.PickBranch.Action%2A> que é executado se disparado.|

## <a name="see-also"></a>Consulte também

- [Fluxo de Controle](../workflow-designer/control-flow-activity-designers.md)
- [Escolher atividade](/dotnet/framework/windows-workflow-foundation/pick-activity)
- [Usando a atividade de Pick](/dotnet/framework/windows-workflow-foundation/samples/using-the-pick-activity)