---
title: Designer de fluxo de trabalho - Designer de atividade de TryCatch
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
f1_keywords:
- System.Activities.Statements.TryCatch.UI
- System.Activities.Statements.Catch`1.UI
ms.assetid: 02a326c2-4009-442f-b7cb-e42121fd2992
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a4a62b660f2deb2b3ab3a092cdfd586a56b2bcb8
ms.sourcegitcommit: 38db86369af19e174b0aba59ba1918a5c4fe4a61
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54269807"
---
# <a name="trycatch-activity-designer"></a>Designer de atividade de TryCatch

O **TryCatch** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.TryCatch> atividade.

## <a name="the-trycatch-activity"></a>A atividade de TryCatch
 O <xref:System.Activities.Statements.TryCatch> atividade contém uma <xref:System.Activities.Statements.TryCatch.Try%2A> atividade, uma coleção de **Catch\<TException >** e um <xref:System.Activities.Statements.TryCatch.Finally%2A> atividade. Um <xref:System.Activities.Statements.Catch%601> do tipo **TException** contém um <xref:System.Activities.Statements.Catch%601.ExceptionType%2A> e um <xref:System.Activities.Statements.Catch%601.Action%2A>. São usados juntos para implementar um mecanismo exceção baseado típico de manipulação de erro. Uma atividade de <xref:System.Activities.Statements.TryCatch> tentar executar a atividade de <xref:System.Activities.Statements.TryCatch.Try%2A> . Se o <xref:System.Activities.Statements.TryCatch.Try%2A> atividade lança uma exceção, o <xref:System.Activities.Statements.TryCatch> atividade usa seus **Catch < TException\>**  coleção para coincidir com a exceção. Se houver uma correspondência, o <xref:System.Activities.Statements.Catch%601.Action%2A> de correspondente **Catch\<TException >** é executado, servindo como o lógica de manipulação de exceção de erro. Se as atividades na seção de <xref:System.Activities.Statements.TryCatch.Try%2A> completa com êxito ou as atividades em <xref:System.Activities.Statements.TryCatch.Catches%2A> completa com êxito, a atividade de <xref:System.Activities.Statements.TryCatch> executa sua atividade de <xref:System.Activities.Statements.TryCatch.Finally%2A> . Para obter mais informações, consulte [exceções de fluxo de trabalho do Windows](/dotnet/framework/windows-workflow-foundation/exceptions).

### <a name="using-the-trycatch-activity-designer"></a>Usando o designer de atividade de TryCatch

Acesso a **TryCatch** designer de atividade na **tratamento de erros** categoria dos **caixa de ferramentas**.

O **TryCatch** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Isso cria uma atividade de <xref:System.Activities.Statements.TryCatch> com <xref:System.Activities.Activity.DisplayName%2A> padrão de TryCatch. O <xref:System.Activities.Activity.DisplayName%2A> valor pode ser editado no cabeçalho do **TryCatch** designer de atividade ou nos **DisplayName** caixa da grade de propriedade. As outras propriedades devem ser editadas na superfície do **TryCatch** designer de atividade.

Clique no botão expandir no canto superior direito das **TryCatch** designer para ver os **tente**, **captura**, e **finalmente** nas caixas a exibição expandida. Para adicionar uma captura, clique o **adicionar novo catch** botão **TryCatch** designer. O botão muda para uma caixa de combinação de tipo. Selecione um tipo de exceção e pressione ENTER para adicionar a captura. Depois de adicionar um **Catch**, a área de captura expande e uma atividade pode ser levada na captura para definir a lógica de execução para a captura. Observe que há uma caixa de texto no lado direito da área expandida catch. Você pode nomear a variável de exceções usando esta caixa de texto. A variável de exceção só pode ser usada para atividades dentro do mesmo **Catch**.

O **TryCatch** designer não oferece suporte à edição **Catch**. Se você quiser alterar o tipo de exceção, você precisa excluir o **Catch** e adicione um novo. Um **Catch** pode ser excluído selecionando-lo e excluí-lo ou selecionando **excluir** no menu de contexto que é acessado clicando com o.

### <a name="the-trycatch-properties"></a>As propriedades de TryCatch

A tabela a seguir mostra o <xref:System.Activities.Statements.TryCatch>propriedades e descreve como elas são usadas no designer.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|Especifica o nome amigável opcional de atividade de <xref:System.Activities.Statements.TryCatch> . O padrão é TryCatch.|
|<xref:System.Activities.Statements.TryCatch.Try%2A>|False|A atividade executada primeiro quando <xref:System.Activities.Statements.TryCatch> executar.|
|<xref:System.Activities.Statements.TryCatch.Catches%2A>|False|A coleção de **Catch** elementos a ser verificado quando o <xref:System.Activities.Statements.TryCatch.Try%2A> atividade lançará uma exceção.<br /><br /> Você precisa pelo menos de adicionar uma atividade em <xref:System.Activities.Statements.TryCatch.Catches%2A> ou uma atividade no bloco de <xref:System.Activities.Statements.TryCatch.Finally%2A> .|
|<xref:System.Activities.Statements.TryCatch.Finally%2A>|False|A atividade a ser executada quando <xref:System.Activities.Statements.TryCatch.Try%2A> e todas as atividades necessárias na coleção de <xref:System.Activities.Statements.TryCatch.Catches%2A> tiver terminado a execução.<br /><br /> Você precisa pelo menos de adicionar uma atividade em <xref:System.Activities.Statements.TryCatch.Catches%2A> ou uma atividade no bloco de <xref:System.Activities.Statements.TryCatch.Finally%2A> .|

## <a name="see-also"></a>Consulte também

- [Coleção](../workflow-designer/collection-activity-designers.md)
- [Relançar](../workflow-designer/rethrow-activity-designer.md)
- [Throw](../workflow-designer/throw-activity-designer.md)