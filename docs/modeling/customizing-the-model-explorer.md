---
title: Personalizando o Gerenciador de Modelos
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.dsldesigner.explorerbehavior
helpviewer_keywords:
- Domain-Specific Language Tools, Domain-Specific Language Explorer
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 625ba0d592d0dbdaa8cb910c366852fe32c5f220
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548363"
---
# <a name="customizing-the-model-explorer"></a>Personalizando o Gerenciador de Modelos
Você pode alterar a aparência e o comportamento do Gerenciador para o designer de linguagem específica do domínio da seguinte maneira:

- Alterar o título da janela.

- Altere o ícone de guia.

- Altere os ícones dos nós.

- Ocultar nós.

## <a name="changing-the-window-title"></a>Alterando o título da janela
 Para alterar o título da janela do Gerenciador gerado, selecione o **comportamento do Explorer** no Gerenciador de **DSL**e, em seguida, na janela **Propriedades** , defina a propriedade **título** como o título desejado.

## <a name="changing-the-tab-icon"></a>Alterando o ícone de guia
 Para alterar o ícone de guia do Gerenciador, use um ícone de 16x16 pixels em um arquivo. bmp. Coloque o arquivo de ícone na pasta \DslPackage\Resources\ e altere o nome do arquivo para **ModelExplorerToolWindowBitmaps.bmp**. Por exemplo, você pode alterar o arquivo de ícone Setup. ico do Visual Studio para o formato. bmp e renomeá-lo como **DSLLanguageName\DslPackage\Resources\ModelExplorerToolWindowBitmaps.bmp**. O designer gerado exibirá esse ícone na guia do seu Explorer quando ele estiver encaixado junto com **Gerenciador de soluções**.

## <a name="setting-custom-icons-on-explorer-nodes"></a>Configurando ícones personalizados em nós do Explorer
 Você pode personalizar os nós no seu Explorer usando as configurações de nó do Explorer. O procedimento a seguir mostra como adicionar um ícone a um nó.

#### <a name="to-add-an-icon-to-an-explorer-node"></a>Para adicionar um ícone a um nó do Explorer

1. Crie uma [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] solução usando o modelo de solução de fluxo de tarefas.

2. Coloque um arquivo. bmp que contenha um ícone de 16x16 pixels na pasta **Dsl\Resources** da solução.

3. No **Gerenciador de DSL**, clique com o botão direito do mouse em **comportamento do Explorer** e clique em **adicionar novas configurações de nó do Explorer**.

    Um nó **ExplorerNodeSettings** aparece sob o nó **configurações personalizadas do nó** .

4. Selecione **ExplorerNodeSettings**e, em seguida, na janela **Propriedades** , defina **classe** como **ator**.

5. Defina o **ícone para exibir** para o caminho do arquivo de ícone.

6. Transforme todos os modelos e, em seguida, compile e execute a solução.

7. No designer gerado, abra o diagrama de exemplo.

    O Explorer deve mostrar três nós de **ator** que têm seu ícone.

> [!NOTE]
> Se você tiver definido um ícone de nó para qualquer elemento exibido no explorador gerado, todos os nós do Explorer exibirão o ícone. Se nenhum ícone tiver sido definido, os nós exibirão o ícone padrão.

## <a name="changing-the-name-displayed-on-an-explorer-node"></a>Alterando o nome exibido em um nó do Gerenciador
 Você pode alterar como os nomes dos elementos do modelo são exibidos no seu Gerenciador. O procedimento a seguir mostra como exibir o nome da **tarefa** que é referenciada por um **Comentário** no nó de comentário.

#### <a name="to-display-a-property"></a>Para exibir uma propriedade

1. Abra a solução que você criou no procedimento anterior.

2. Certifique-se de que o **Comentário** referencie apenas uma única classe de domínio definindo a multiplicidade da função com o nome da propriedade **Subjects** como 0.. 1. O nome da propriedade deve se tornar **sujeito**e o nome da relação deve se tornar **CommentReferencesSubject**.

3. No **Gerenciador de DSL**, clique com o botão direito do mouse em **comportamento do Explorer** e clique em **adicionar novas configurações de nó do Explorer**.

     Um nó **ExplorerNodeSettings** aparece sob o nó **configurações personalizadas do nó** .

4. Selecione **ExplorerNodeSettings**e, em seguida, na janela **Propriedades** , defina **classe** como **Comentário**.

5. Clique com o botão direito do mouse no nó de **Comentário** e clique em **Adicionar novo caminho de propriedade**.

     Um novo nó aparece com a **propriedade nomeada exibida**.

6. Selecione a **propriedade exibida**e, em seguida, na janela **Propriedades** , clique no campo valor de **caminho para Propriedade**. Selecione **Comentário**, depois **CommentReferencesSubject**, **fluxoelement**. O caminho resultante deve ser semelhante a **CommentReferencesSubject. Subject/! Assunto**.

7. No campo valor da **Propriedade**, selecione **nome**.

8. Transforme todos os modelos e, em seguida, compile e execute sua solução.

9. No designer gerado, abra o diagrama de exemplo.

10. Desenhe um **conector de comentário** entre o elemento Comment e o elemento **Task1** no diagrama.

     O nó do Gerenciador deve exibir o comentário como **Task1**.

## <a name="hiding-nodes"></a>Ocultando nós
 Você pode ocultar um nó no seu Explorer adicionando seu caminho ao nó de **nós ocultos** do **Gerenciador de DSL**. O procedimento a seguir mostra como ocultar nós de **Comentário** .

#### <a name="to-hide-an-explorer-node"></a>Para ocultar um nó do Explorer

1. Abra a solução que você criou no procedimento anterior.

2. No **Gerenciador de DSL**, clique com o botão direito do mouse em **comportamento do Explorer** e clique em **Adicionar novo caminho de domínio**.

     Um nó de **caminho de domínio** aparece sob **nós ocultos**.

3. Selecione **caminho do domínio**e, na janela **Propriedades** , clique no campo valor da **definição do caminho**. Selecione **grafos**, em seguida, **FlowGraphHasComments**. O caminho resultante deve ser semelhante a **FlowGraphHasComments. Comments**

4. Transforme todos os modelos e, em seguida, compile e execute sua solução.

5. No designer gerado, abra o diagrama de exemplo.

     O Gerenciador deve mostrar apenas um nó **atores** e não deve mostrar o nó de **comentários** .

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
