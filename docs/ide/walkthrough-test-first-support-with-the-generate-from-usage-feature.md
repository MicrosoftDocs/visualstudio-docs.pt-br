---
title: Desenvolvimento de teste antes da codificação com recurso gerar com base no uso
ms.date: 10/09/2017
dev_langs:
- VB
- CSharp
ms.topic: how-to
helpviewer_keywords:
- Generate From Usage
- Test-First Development
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ceed19ab052584ea47629244372af4402835beb5
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770796"
---
# <a name="walkthrough-test-first-development-with-the-generate-from-usage-feature"></a>Instruções passo a passo: desenvolvimento de teste antes da codificação com o recurso gerar com base no uso

Este tópico demonstra como usar o recurso [Gerar do Uso](../ide/visual-csharp-intellisense.md#generate-from-usage), que oferece suporte ao desenvolvimento de test-first.

 O *desenvolvimento test-first* é uma abordagem para design de software em que você primeiro escreve testes de unidade baseados nas especificações do produto e, em seguida, escreve o código-fonte que é necessário para tornar os testes bem-sucedidos. O Visual Studio é compatível com o desenvolvimento teste antes da codificação (test-first) através da geração de novos tipos e membros no código-fonte ao referenciá-los pela primeira vez em seus casos de teste antes de serem definidos.

O Visual Studio gera os novos tipos e membros com uma interrupção mínima no seu fluxo de trabalho. Você pode criar stubs para tipos, métodos, propriedades, campos ou construtores sem sair do seu local atual no código. Quando você abre uma caixa de diálogo para especificar as opções para a geração de tipo, o foco retorna imediatamente para o arquivo aberto no momento quando a caixa de diálogo é fechada.

O recurso **gerar de uso** pode ser usado com estruturas de teste que se integram ao Visual Studio. A Estrutura de Teste de unidade da Microsoft é demonstrada neste tópico.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="create-a-windows-class-library-project-and-a-test-project"></a>Criar um projeto de Biblioteca de Classes do Windows e um projeto de Teste

1. Em C# ou no Visual Basic, crie um projeto da **Biblioteca de classes do Windows**. Nomeie-o `GFUDemo_VB` ou `GFUDemo_CS`, dependendo de qual linguagem você está usando.

2. No **Gerenciador de Soluções**, clique com o botão direito do mouse no ícone da solução na parte superior, escolha **Adicionar** > **Novo Projeto**.

3. Crie um **projeto de Teste de Unidade (.NET Framework)**.

   ::: moniker range="vs-2017"

   A ilustração a seguir mostra a caixa de diálogo **Novo Projeto** para modelos C#.

   ![Modelo de projeto de teste de unidade](../ide/media/newproject_test.png)

   ::: moniker-end

### <a name="add-a-reference-to-the-class-library-project"></a>Adicionar uma referência ao projeto de Biblioteca de Classes

1. No **Gerenciador de Soluções**, em seu projeto de teste de unidade, clique com o botão direito do mouse na entrada **Referências** e escolha **Adicionar Referência**.

2. Na caixa de diálogo **Gerenciador de Referências**, selecione **Projetos** e, em seguida, selecione o projeto da biblioteca de classes.

3. Escolha **OK** para fechar a caixa de diálogo **Gerenciador de Referências**.

4. Salvar sua solução. Agora você está pronto para começar a escrever testes.

### <a name="generate-a-new-class-from-a-unit-test"></a>Gerar uma nova classe com base em um teste de unidade

1. O projeto de teste contém um arquivo chamado *UnitTest1*. Clique duas vezes nesse arquivo em **Gerenciador de soluções** para abri-lo no editor de códigos. Uma classe de teste e um método de teste foram gerados.

2. Localize a declaração da classe `UnitTest1` e renomeie para `AutomobileTest`.

   > [!NOTE]
   > O IntelliSense agora fornece duas alternativas para o preenchimento de declaração do IntelliSense: *modo de preenchimento* e *modo de sugestão*. Use o modo de sugestão para situações nas quais classes e membros são usados antes de serem definidos. Quando uma janela do **IntelliSense** é aberta, pressione **Ctrl**+**Alt**+**Espaço** para alternar entre o modo de conclusão e o modo de sugestão. Consulte [Usar o IntelliSense](../ide/using-intellisense.md) para obter mais informações. O modo de sugestão ajudará quando você estiver digitando `Automobile` na próxima etapa.

3. Localize o método `TestMethod1()` e renomeie-o para `DefaultAutomobileIsInitializedCorrectly()`. Dentro desse método, crie uma nova instância de uma classe chamada `Automobile`, conforme mostrado nas capturas de tela a seguir. Um sublinhado ondulado é exibido, indicando um erro em tempo de compilação e uma lâmpada de erro de [Ações Rápidas](../ide/quick-actions.md) aparece na margem esquerda ou diretamente abaixo do rabisco, se você passa o mouse sobre ele.

    ![Ações rápidas no Visual Basic](../ide/media/genclass_underlinevb.png)

    ![Ações rápidas em C&#35;](../ide/media/genclass_underline.png)

4. Escolha ou clique na lâmpada de **ações rápidas** . Você verá uma mensagem de erro afirmando que o tipo `Automobile` não está definido. Você também verá algumas possíveis soluções.

5. Clique em **gerar novo tipo** para abrir a caixa de diálogo **gerar tipo** . Essa caixa de diálogo fornece opções que incluem a geração de tipo em um projeto diferente.

6. Na lista **Projetos**, clique em **GFUDemo\_VB** ou **GFUDemo_CS** para instruir o Visual Studio a adicionar o arquivo no projeto de biblioteca de classes em vez do projeto de teste. Se ainda não estiver selecionado, escolha **Criar novo arquivo** e nomeie-o *Automobile.cs* ou *Automobile.vb*.

     ![Caixa de diálogo Gerar Novo Tipo](../ide/media/genotherdialog.png)

7. Clique em **OK** para fechar a caixa de diálogo e criar o novo arquivo.

8. Em **Gerenciador de soluções**, examine o **GFUDemo_VB** ou **GFUDemo_CS** nó do projeto para verificar se o novo arquivo *automóvel. vb* ou *Automobile.cs* está lá. No editor de código, o foco ainda estará em `AutomobileTest.DefaultAutomobileIsInitializedCorrectly`, o que permite que você continue a escrever o teste com um mínimo de interrupção.

### <a name="generate-a-property-stub"></a>Gerar um stub de propriedade
Suponha que a especificação de produto afirma que a classe `Automobile` tem duas propriedades públicas chamadas `Model` e `TopSpeed`. Essas propriedades devem ser inicializadas com valores padrão de `"Not specified"` e `-1` pelo construtor padrão. O seguinte teste de unidade verificará para que o construtor padrão defina as propriedades para seus valores padrão corretos.

1. Adicione a seguinte linha de código no método de teste `DefaultAutomobileIsInitializedCorrectly`.

     [!code-csharp[VbTDDWalkthrough#1](../ide/codesnippet/CSharp/walkthrough-test-first-support-with-the-generate-from-usage-feature_1.cs)]
     [!code-vb[VbTDDWalkthrough#1](../ide/codesnippet/VisualBasic/walkthrough-test-first-support-with-the-generate-from-usage-feature_1.vb)]

2. Com o código faz referência a duas propriedades indefinidas em `Automobile`, um sublinhado ondulado aparecerá sob `Model` e `TopSpeed`. Passe o mouse sobre `Model`, escolha a lâmpada de erro **Ações Rápidas** e, em seguida, escolha **Gerar propriedade 'Automobile.Model'**.

3. Gere um stub de propriedade para a propriedade `TopSpeed` da mesma maneira.

     Na classe `Automobile`, os tipos das novas propriedades são inferidos corretamente do contexto.

### <a name="generate-a-stub-for-a-new-constructor"></a>Gerar um stub para um novo construtor
Agora vamos criar um método de teste que gerará um stub de construtor para inicializar as propriedades `Model` e `TopSpeed`. Depois, você adicionará mais código para concluir o teste.

1. Adicione também o seguinte método de teste à sua classe `AutomobileTest`.

     [!code-csharp[VbTDDWalkthrough#2](../ide/codesnippet/CSharp/walkthrough-test-first-support-with-the-generate-from-usage-feature_2.cs)]
     [!code-vb[VbTDDWalkthrough#2](../ide/codesnippet/VisualBasic/walkthrough-test-first-support-with-the-generate-from-usage-feature_2.vb)]

2. Clique na lâmpada de erro **Ações Rápidas** sob a linha ondulada vermelha e, em seguida, clique em **Gerar construtor em 'Automobile'**.

     No arquivo de classe `Automobile`, observe que o novo construtor examinou os nomes das variáveis locais que são usadas na chamada do construtor, encontrou propriedades que têm os mesmos nomes na classe `Automobile` e forneceu código no corpo do construtor para armazenar os valores de argumento nas propriedades `Model` e `TopSpeed`.

3. Depois de gerar o novo construtor, um sublinhado ondulado aparece sob a chamada para o construtor padrão em `DefaultAutomobileIsInitializedCorrectly`. A mensagem de erro informa que a classe `Automobile` não tem nenhum construtor que assuma zero argumentos. Para gerar um construtor padrão explícito que não tem parâmetros, clique na lâmpada de erro **Ações Rápidas** e, em seguida, clique em **Gerar construtor em 'Automobile'**.

### <a name="generate-a-stub-for-a-method"></a>Gerar um stub para um método
Suponha que a especificação afirme que um novo `Automobile` poderá ser colocado em um estado `IsRunning` se suas propriedades `Model` e `TopSpeed` forem definidas como algo diferente dos valores padrão.

1. Adicione as seguintes linhas ao método `AutomobileWithModelNameCanStart`.

     [!code-csharp[VbTDDWalkthrough#3](../ide/codesnippet/CSharp/walkthrough-test-first-support-with-the-generate-from-usage-feature_3.cs)]
     [!code-vb[VbTDDWalkthrough#3](../ide/codesnippet/VisualBasic/walkthrough-test-first-support-with-the-generate-from-usage-feature_3.vb)]

2. Clique na lâmpada de erro **Ações Rápidas** para a chamada de método `myAuto.Start` e, em seguida, clique em **Gerar método 'Automobile.Start'**.

3. Clique na lâmpada de **ações rápidas** para a `IsRunning` propriedade e, em seguida, clique em **gerar Propriedade ' automóvel. IsRunning '**.

     Agora a classe `Automobile` contém um método chamado `Start()` e uma propriedade chamada `IsRunning`.

### <a name="run-the-tests"></a>Executar os testes

1. No menu **Teste**, escolha **Executar** > **Todos os Testes**.

     O comando **executar**  >  **todos os testes** executa todos os testes em todas as estruturas de teste que são gravadas para a solução atual. Nesse caso, há dois testes e ambos falham conforme o esperado. O teste `DefaultAutomobileIsInitializedCorrectly` falha porque a condição `Assert.IsTrue` retorna `False`. O teste `AutomobileWithModelNameCanStart` falha porque o método `Start` na classe `Automobile` lança uma exceção.

     A janela **Resultados do Teste** é mostrada na ilustração a seguir.

     ![Resultados de teste que falharam](../ide/media/testsfailed.png)

2. Na janela **Resultados de Teste**, clique duas vezes em cada linha de resultado do teste para ir até o local de cada teste.

### <a name="implement-the-source-code"></a>Implementar o código-fonte

1. Adicione o seguinte código ao construtor padrão, de maneira que as propriedades `Model`, `TopSpeed` e `IsRunning` sejam inicializadas com seus valores padrão corretos, `"Not specified"`, `-1` e `False` (ou `false` para o C#).

     [!code-csharp[VbTDDWalkthrough#5](../ide/codesnippet/CSharp/walkthrough-test-first-support-with-the-generate-from-usage-feature_5.cs)]
     [!code-vb[VbTDDWalkthrough#5](../ide/codesnippet/VisualBasic/walkthrough-test-first-support-with-the-generate-from-usage-feature_5.vb)]

2. Quando o método `Start` é chamado, ele deve definir o sinalizador `IsRunning` como true apenas se as propriedades `Model` ou `TopSpeed` estiverem definidas com valor diferente de seu valor padrão. Remova o `NotImplementedException` do corpo do método e adicione o código a seguir.

     [!code-csharp[VbTDDWalkthrough#6](../ide/codesnippet/CSharp/walkthrough-test-first-support-with-the-generate-from-usage-feature_6.cs)]
     [!code-vb[VbTDDWalkthrough#6](../ide/codesnippet/VisualBasic/walkthrough-test-first-support-with-the-generate-from-usage-feature_6.vb)]

### <a name="run-the-tests-again"></a>Executar os testes novamente

- No menu **Testar**, aponte para **Executar** e, em seguida, clique em **Todos os Testes**.

     Dessa vez os testes são aprovados. A janela **Resultados do Teste** é mostrada na ilustração a seguir.

     ![Resultados de teste que foram aprovados](../ide/media/testspassed.png)

## <a name="see-also"></a>Confira também

- [Gerar com base no uso](../ide/visual-csharp-intellisense.md#generate-from-usage)
- [Recursos do editor de código](../ide/writing-code-in-the-code-and-text-editor.md)
- [Usar o IntelliSense](../ide/using-intellisense.md)
- [Teste de unidade em seu código](../test/unit-test-your-code.md)
- [Ações Rápidas](../ide/quick-actions.md)
