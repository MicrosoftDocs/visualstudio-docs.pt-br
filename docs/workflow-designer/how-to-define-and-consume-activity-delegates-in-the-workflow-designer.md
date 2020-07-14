---
title: 'Designer de Fluxo de Trabalho: definir e consumir delegados de atividade'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: c68e42ad-3ec0-4c2d-b104-fe36c6d83b5e
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: 41271266793927f6029f50c0411bb9a150f5a64a
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817496"
---
# <a name="how-to-define-and-consume-activity-delegates-in-the-workflow-designer"></a>Como: Defina e consumir representantes de atividade em Designer de Fluxo de Trabalho

O .NET Framework 4,5 inclui um designer pronto para a <xref:System.Activities.Statements.InvokeDelegate> atividade. Este criador pode ser usado para atribuir os representantes para a atividade que derivam de <xref:System.Activities.ActivityDelegate>, como <xref:System.Activities.ActivityAction> ou <xref:System.Activities.ActivityFunc%601>.

## <a name="define-an-activity-delegate"></a>Defina um representante de atividades

1. Crie um novo projeto de **aplicativo do console de fluxo de trabalho** .

   > [!NOTE]
   > Se você não vir os modelos de projeto de **fluxo de trabalho** , primeiro instale o componente **Windows Workflow Foundation** do Visual Studio. Para obter instruções detalhadas, consulte [instalar Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation).

3. Clique com o botão direito do mouse no projeto no **Gerenciador de soluções** e selecione **Adicionar**  >  **novo item**. Selecione a categoria **fluxo de trabalho** e, em seguida, selecione o modelo item de **atividade** . Nomeie a nova atividade **myforeach. XAML** e, em seguida, selecione **OK**.

   A atividade é aberta no designer de fluxo de trabalho.

4. Na Designer de Fluxo de Trabalho, clique na guia **argumentos** .

5. Clique em **Criar Argumento**. Nomeie os novos **itens**de argumento.

6. Na coluna **tipo de argumento** , selecione **matriz de [T]**.

7. No navegador de tipos, selecione **objeto** e, em seguida, selecione **OK**.

8. Clique em **criar argumento** novamente. Nomeie o novo **corpo**do argumento. Na coluna **direção** do novo argumento, selecione **Propriedade**.

9. Na coluna tipo de argumento, selecione **procurar tipos**

10. No navegador de tipos, insira **ActivityAction** no campo **nome do tipo** . Selecione **ActivityAction \<T> ** no modo de exibição de árvore. Selecione **objeto** na lista suspensa que aparece para atribuir o tipo ** \<Object> ActivityAction** ao argumento.

11. Arraste uma <xref:System.Activities.Statements.While> atividade da seção **fluxo de controle** da caixa de ferramentas para a superfície do designer.

12. Selecione a <xref:System.Activities.Statements.While> atividade e selecione a guia **variáveis** .

13. Selecione **criar variável**. Nomeie o novo **índice**de variável.

14. Na coluna **tipo de variável** , selecione **Int32**. Deixe o **escopo** como **while**e a coluna **padrão** em branco.

15. Defina a propriedade **condição** da <xref:System.Activities.Statements.While> atividade para **indexar < itens. Length;**.

16. Arraste uma <xref:System.Activities.Statements.InvokeDelegate> atividade da seção **primitivas** da caixa de ferramentas para o **corpo** da <xref:System.Activities.Statements.While> atividade.

17. Selecione **corpo** na lista suspensa delegar.

18. Na grade de **Propriedades** da <xref:System.Activities.Statements.InvokeDelegate> atividade, clique no botão **...** na propriedade de **argumentos de representante** .

19. Na coluna **valor** do argumento chamado **argumento**, insira **itens [índice]**. Clique em **OK** para fechar a caixa de diálogo **DelegateArguments** .

20. Arraste uma atividade de <xref:System.Activities.Statements.Assign> na linha horizontal abaixo de atividade de <xref:System.Activities.Statements.InvokeDelegate> . A <xref:System.Activities.Statements.Assign> atividade é criada e uma <xref:System.Activities.Statements.Sequence> atividade é criada automaticamente para conter as duas atividades na seção **corpo** da atividade **myforeach** . A sequência é necessária, pois a seção **Body** só pode conter uma única atividade. A criação automática de uma nova <xref:System.Activities.Statements.Sequence> atividade é um novo recurso do .NET Framework 4,5.

21. Defina a propriedade **to** da <xref:System.Activities.Statements.Assign> atividade como **index**. Defina a propriedade **valor** da atividade **atribuir** como **índice + 1**.

    A atividade personalizada **myforeach** invoca uma atividade arbitrária uma vez para cada valor passado por meio da coleção **Items** , com os valores na coleção como entradas para a atividade.

## <a name="use-the-custom-activity-in-a-workflow"></a>Use a atividade personalizado em um fluxo de trabalho

1. Crie o projeto pressionando **Ctrl** + **Shift** + **B**.

2. No **Gerenciador de soluções**, abra **Workflow1. XAML** no designer.

3. Arraste uma atividade **myforeach** da caixa de ferramentas para a superfície do designer. A atividade está em uma seção da caixa de ferramentas com o mesmo nome que o projeto.

4. Defina a propriedade **Items** da atividade **myforeach** como **New Object [] {1, "ABC"}**.

5. Arraste uma <xref:System.Activities.Statements.WriteLine> atividade da seção **primitivas** da caixa de ferramentas para a seção **delegar: corpo** da atividade **myforeach** .

6. Defina a propriedade **Text** da <xref:System.Activities.Statements.WriteLine> atividade como **Argument. ToString ()**.

Quando o fluxo de trabalho é executado, o console mostra a seguinte saída:

**1** 
 **ABC**
