---
title: Designer de fluxo de trabalho - Designer de atividade de interoperabilidade
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Statements.Interop.UI
ms.assetid: 800a3403-ba86-41c4-8de1-c4fee9703eb1
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7f3b5fd2674d63fad6398eeaee082862c4cf6476
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51809123"
---
# <a name="interop-activity-designer"></a>Designer de atividade de Interoperabilidade

O **Interop** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.Interop> atividade.

## <a name="the-interop-activity"></a>A atividade de Interoperabilidade

A atividade de <xref:System.Activities.Statements.Interop> gerencia a execução de tipos que derivam de <xref:System.Workflow.ComponentModel.Activity?displayProperty=fullName> em um fluxo de trabalho.

### <a name="use-the-interop-activity-designer"></a>Use o Designer de atividade de interoperabilidade

O **Interop** designer de atividade pode ser encontrado na **migração** categoria da **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas**guia. Como alternativa, selecione **caixa de ferramentas** da **exibição** menus ou pressione **Ctrl**+**Alt** + **X**.

O [migração](../workflow-designer/migration-activity-designers.md) categoria que contém o <xref:System.Activities.Statements.Interop> atividade aparece somente na **caixa de ferramentas** se seu projeto tiver como alvo o .NET Framework 4 completo.

Para projetos c#, você pode redirecionar o projeto para usar o .NET Framework 4 completo clicando com o projeto no **Gerenciador de soluções** e selecionando **propriedades**. Sobre o **aplicativo** guia, selecione o **NET Framework 4** opção no **estrutura de destino**. Selecione **Sim** confirme essa alteração.

Para projetos do Visual Basic, você pode redirecionar o projeto para usar o .NET Framework 4 completo pelo botão direito do mouse no projeto no **Gerenciador de soluções** e selecionando **propriedades**. Sobre o **Compile** , clique no **opções avançadas de compilação** botão. Selecione **.Net Framework 4** da **lista do framework de destino**e, em seguida, clique em **Okey**. Selecione **Sim** confirme essa alteração.

O **Interop** designer de atividade pode ser arrastado de **caixa de ferramentas** e solto sobre a superfície do Designer de fluxo de trabalho onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Descartando o **Interop** designer de atividade cria uma <xref:System.Activities.Statements.Interop> atividade com um padrão **DisplayName** de interoperabilidade. Você pode editar a <xref:System.Activities.Activity.DisplayName%2A> no cabeçalho do **interoperabilidade** designer de atividade, ou nos **DisplayName** caixa da grade de propriedade.

Clique o **clique para procurar** texto na **ActivityType** caixa, no **interoperabilidade** atividade designer ou na grade de propriedade para abrir o **procurar e Selecione um .net tipo** caixa de diálogo. Somente tipos para os trabalhos 3,0 ou o trabalho 3,5 atividades são mostrados. Ou seja, somente os tipos derivados de <xref:System.Workflow.ComponentModel.Activity> são mostrados. Para obter mais informações sobre como usar essa caixa para especificar um tipo, consulte [navegue e selecione uma caixa de diálogo do tipo .NET](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box.md).

### <a name="the-interop-properties"></a>As propriedades de Interoperabilidade

A tabela a seguir mostra o <xref:System.Activities.Statements.Interop> propriedades e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade ou na superfície de Designer de fluxo de trabalho.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.Activities.Statements.Interop> . O valor padrão é **interoperabilidade**. Embora o nome de exibição não é necessário, é recomendável fornecer um.|
|<xref:System.Activities.Statements.Interop.ActivityType%2A>|verdadeiro|Especifica o tipo de atividade contida pela atividade de <xref:System.Activities.Statements.Interop> . Este tipo especificado deve derivar de <xref:System.Workflow.ComponentModel.Activity>.|

## <a name="see-also"></a>Consulte também

- [Migração](../workflow-designer/migration-activity-designers.md)