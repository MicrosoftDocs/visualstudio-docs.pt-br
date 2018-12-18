---
title: Designer de atividade de InvokeMethod | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.InvokeMethod.UI
ms.assetid: 15e6efdc-52ca-46d8-9c5e-063f7c8265a6
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: a3fa1c07bbb32bc1da963a0d2f0a91ae6c193a30
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49863679"
---
# <a name="invokemethod-activity-designer"></a>Designer de atividade de InvokeMethod
**InvokeMethod** designer é usado para criar e configurar um <xref:System.Activities.Statements.InvokeMethod> atividade.  
  
## <a name="the-invokemethod-activity"></a>A atividade de InvokeMethod  
 <xref:System.Activities.Statements.InvokeMethod> chama um método público de um objeto ou tipo especificado.  
  
### <a name="using-the-invokemethod-activity-designer"></a>Usando o designer de atividade de InvokeMethod  
 O **InvokeMethod** designer de atividade pode ser encontrado na **primitivos** categoria da **caixa de ferramentas**, que é acessado clicando o **dacaixadeferramentas** guia [!INCLUDE[wfd2](../includes/wfd2-md.md)] (como alternativa, selecione **barra de ferramentas** do **exibição** menu, ou CRTL + ALT + X.)  
  
 O **InvokeMethod** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície em que nunca atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Isso cria uma atividade de <xref:System.Activities.Statements.InvokeMethod> com <xref:System.Activities.Activity.DisplayName%2A> padrão de InvokeMethod. O <xref:System.Activities.Activity.DisplayName%2A> pode ser editado no cabeçalho do **InvokeMethod** designer de atividade ou nos **DisplayName** caixa da grade de propriedade.  
  
### <a name="the-invokemethod-properties"></a>As propriedades de InvokeMethod  
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.InvokeMethod> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade e alguns podem ser editados na superfície do designer de [!INCLUDE[wfd2](../includes/wfd2-md.md)].  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.Activities.Statements.InvokeMethod> . O valor padrão é InvokeMethod.<br /><br /> Embora não seja necessário <xref:System.Activities.Activity.DisplayName%2A> restrita, é uma prática recomendada usar um.|  
|<xref:System.Activities.Statements.InvokeMethod.MethodName%2A>|verdadeiro|O nome do método a ser chamado quando a atividade executar. O método chamado deve ser declarado como **público**. Esta propriedade pode ser editada na superfície de designer. Esta é uma propriedade imperativa.|  
|<xref:System.Activities.Statements.InvokeMethod.Parameters%2A>|False|A coleção de parâmetros do método chamado. Os parâmetros devem ser adicionados à coleção na mesma ordem que eles aparecem na assinatura de método. Na grade de propriedade, clique no botão de reticências na **parâmetros** campo, ele exibe a **parâmetros** caixa de diálogo para permitir que você definir essa propriedade. Clique o **criar argumento** botão para adicionar os parâmetros.|  
|<xref:System.Activities.Statements.InvokeMethod.Result%2A>|False|O valor de retorno de chamada de método.|  
|<xref:System.Activities.Statements.InvokeMethod.RunAsynchronously%2A>|verdadeiro|Especifica se o método é chamado de forma assíncrona. O valor padrão é **falsos**.|  
|<xref:System.Activities.Statements.InvokeMethod.TargetObject%2A>|False|O objeto que contém o método para chamar. Esta propriedade pode ser editada na superfície de designer.<br /><br /> <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> ou <xref:System.Activities.Statements.InvokeMethod.TargetType%2A> são necessários para ser definidos.|  
|<xref:System.Activities.Statements.InvokeMethod.TargetType%2A>|False|O tipo de <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A>. Esta propriedade pode ser editada na superfície de designer. Esta propriedade deve ser definida somente se o método é chamado estático.|  
  
 Passar parâmetros como uma linguagem c# **horizontalmente** parâmetro (por exemplo, `Method1(out myParam)),` você deve usar **OutArgument** em vez de **InOutArgument**  
  
 Métodos com argumentos chamados **TargetObject** ou **resultado** não pode ser invocado usando o <xref:System.Activities.Statements.InvokeMethod> atividade. A razão para isso é que registros de atividade de <xref:System.Activities.Statements.InvokeMethod><xref:System.Activities.Statements.InvokeMethod.GenericTypeArguments%2A>, <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> e <xref:System.Activities.Statements.InvokeMethod.Result%2A> em <xref:System.Activities.Activity.CacheMetadata%2A>.  
  
 O algoritmo para registrar os parâmetros em <xref:System.Activities.Activity.CacheMetadata%2A> é mostrado na lista a seguir:  
  
1. Argumento de <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> do registro.  
  
2. Argumento de <xref:System.Activities.Statements.InvokeMethod.Result%2A> do registro.  
  
3. Iterar através da coleção de <xref:System.Activities.Statements.InvokeMethod.Parameters%2A> e registrar cada argumento.  
  
   A exceção resultante é do tipo <xref:System.Activities.InvalidWorkflowException> com a seguinte mensagem: “InvokeMethod”: Uma variável, RuntimeArgument ou um DelegateArgument já existem com o nome “TargetObject”. Nomes devem ser exclusivos dentro do escopo de ambiente.  
  
   Essa limitação não se aplica a <xref:System.Activities.Statements.InvokeMethod.TargetType%2A> e a <xref:System.Activities.Statements.InvokeMethod.RunAsynchronously%2A> porque não são argumentos de fluxo de trabalho e portanto não são registrados na coleção de <xref:System.Activities.Statements.InvokeMethod.GenericTypeArguments%2A> de atividade de <xref:System.Activities.Statements.InvokeMethod> no método de <xref:System.Activities.Activity.CacheMetadata%2A> .  
  
## <a name="see-also"></a>Consulte também  
 [Primitivos](../workflow-designer/primitives-activity-designers.md)   
 [Atribuir](../workflow-designer/assign-activity-designer.md)   
 [Atraso](../workflow-designer/delay-activity-designer.md)   
 [WriteLine](../workflow-designer/writeline-activity-designer.md)