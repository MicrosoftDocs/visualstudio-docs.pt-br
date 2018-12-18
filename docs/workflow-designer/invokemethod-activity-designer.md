---
title: Designer de fluxo de trabalho - Designer de atividade de InvokeMethod
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Statements.InvokeMethod.UI
ms.assetid: 15e6efdc-52ca-46d8-9c5e-063f7c8265a6
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7ac82e36d3abc942e0c5492cc4d7acf347eba36c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49839564"
---
# <a name="invokemethod-activity-designer"></a>Designer de atividade de InvokeMethod

**InvokeMethod** designer é usado para criar e configurar um <xref:System.Activities.Statements.InvokeMethod> atividade.

## <a name="the-invokemethod-activity"></a>A atividade de InvokeMethod

<xref:System.Activities.Statements.InvokeMethod> chama um método público de um objeto ou tipo especificado.

### <a name="use-the-invokemethod-activity-designer"></a>Use o Designer de atividade de InvokeMethod

Acesso a **InvokeMethod** designer de atividade na **primitivos** categoria dos **caixa de ferramentas**. O **InvokeMethod** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Soltar o designer de atividade cria uma <xref:System.Activities.Statements.InvokeMethod> atividade com um padrão <xref:System.Activities.Activity.DisplayName%2A> de InvokeMethod. O <xref:System.Activities.Activity.DisplayName%2A> pode ser editado no cabeçalho do **InvokeMethod** designer de atividade ou nos **DisplayName** caixa da grade de propriedade.

### <a name="the-invokemethod-properties"></a>As propriedades de InvokeMethod

A tabela a seguir mostra o <xref:System.Activities.Statements.InvokeMethod> propriedades e descreve como eles são usados no designer. Essas propriedades podem ser editadas na grade de propriedade e alguns podem ser editados na superfície do Designer de fluxo de trabalho.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.Activities.Statements.InvokeMethod> . O valor padrão é InvokeMethod.<br /><br /> Embora o <xref:System.Activities.Activity.DisplayName%2A> não é estritamente necessária, é melhor usar um.|
|<xref:System.Activities.Statements.InvokeMethod.MethodName%2A>|verdadeiro|O nome do método a ser chamado quando a atividade executar. O método chamado deve ser declarado como **público**. Essa propriedade pode ser editada na superfície do designer e é obrigatória.|
|<xref:System.Activities.Statements.InvokeMethod.Parameters%2A>|False|A coleção de parâmetros do método chamado. Os parâmetros devem ser adicionados à coleção na mesma ordem que eles aparecem na assinatura de método. Para exibir o **parâmetros** caixa de diálogo onde é possível definir essa propriedade, clique no botão de reticências na **parâmetros** campo da grade de propriedade. Clique o **criar argumento** botão para adicionar os parâmetros.|
|<xref:System.Activities.Statements.InvokeMethod.Result%2A>|False|O valor de retorno de chamada de método.|
|<xref:System.Activities.Statements.InvokeMethod.RunAsynchronously%2A>|verdadeiro|Especifica se o método é chamado de forma assíncrona. O valor padrão é **falsos**.|
|<xref:System.Activities.Statements.InvokeMethod.TargetObject%2A>|False|O objeto que contém o método para chamar. Esta propriedade pode ser editada na superfície de designer.<br /><br /> <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> ou <xref:System.Activities.Statements.InvokeMethod.TargetType%2A> são necessários para ser definidos.|
|<xref:System.Activities.Statements.InvokeMethod.TargetType%2A>|False|O tipo de <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A>. Esta propriedade pode ser editada na superfície de designer. Esta propriedade deve ser definida somente se o método é chamado estático.|

Passar parâmetros como uma linguagem c# **horizontalmente** parâmetro (por exemplo, `Method1(out myParam))`, use **OutArgument** em vez de **InOutArgument**

Métodos com argumentos chamados **TargetObject** ou **resultado** não pode ser invocado usando o <xref:System.Activities.Statements.InvokeMethod> atividade. A razão para isso é que registros de atividade de <xref:System.Activities.Statements.InvokeMethod><xref:System.Activities.Statements.InvokeMethod.GenericTypeArguments%2A>, <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> e <xref:System.Activities.Statements.InvokeMethod.Result%2A> em <xref:System.Activities.Activity.CacheMetadata%2A>.

O algoritmo para registrar os parâmetros em <xref:System.Activities.Activity.CacheMetadata%2A> é mostrado na lista a seguir:

1.  Argumento de <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> do registro.

2.  Argumento de <xref:System.Activities.Statements.InvokeMethod.Result%2A> do registro.

3.  Iterar através da coleção de <xref:System.Activities.Statements.InvokeMethod.Parameters%2A> e registrar cada argumento.

A exceção resultante é do tipo <xref:System.Activities.InvalidWorkflowException> com a seguinte mensagem: “InvokeMethod”: Uma variável, RuntimeArgument ou um DelegateArgument já existem com o nome “TargetObject”. Nomes devem ser exclusivos dentro do escopo de ambiente.

Essa restrição não se aplica aos <xref:System.Activities.Statements.InvokeMethod.TargetType%2A> e <xref:System.Activities.Statements.InvokeMethod.RunAsynchronously%2A>. Eles não são argumentos de fluxo de trabalho e, portanto, não estão registrados na <xref:System.Activities.Statements.InvokeMethod.GenericTypeArguments%2A> coleção do <xref:System.Activities.Statements.InvokeMethod> atividade no <xref:System.Activities.Activity.CacheMetadata%2A> método.

## <a name="see-also"></a>Consulte também

- [Primitives](../workflow-designer/primitives-activity-designers.md)
- [Atribuir](../workflow-designer/assign-activity-designer.md)
- [Atrasar](../workflow-designer/delay-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)