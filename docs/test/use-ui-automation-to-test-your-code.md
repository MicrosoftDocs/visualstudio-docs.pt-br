---
title: Testes automatizados de IU
ms.date: 12/04/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
f1_keywords:
- vs.codedUITest
- vs.codedUITest.recorder
- vs.codedUITest.testbuilder
- vs.codedUITest.addAssertions
- vs.codedUITest.createdialog
helpviewer_keywords:
- automated tests, testing UI interface
- coded UI test
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ce10c81265ecfd95f43d62c73d69c902eda1a6c6
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896634"
---
# <a name="use-ui-automation-to-test-your-code"></a>Usar a automação da interface do usuário para testar o código

Os testes automatizados que orientam o aplicativo por meio da IU (interface do usuário) são conhecidos como *testes de IU codificados* (CUITs) no Visual Studio. Entre esses testes estão testes funcionais dos controles de interface de usuário. Eles permitem verificar se todo o aplicativo, inclusive sua interface do usuário, está funcionando corretamente. Os testes de IU codificados são especialmente úteis quando há validação ou outra lógica na interface do usuário, como em uma página da Web. Eles também costumam ser usados para automatizar um teste manual existente.

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

Conforme mostrado na ilustração a seguir, uma experiência de desenvolvimento típica pode ser uma em que, inicialmente, você só compila o aplicativo e clica nos controles de interface do usuário para verificar se as coisas estão funcionando corretamente. Em seguida, você pode optar por criar um teste automatizado para não precisar continuar testando o aplicativo manualmente. Dependendo da funcionalidade específica testada no aplicativo, é possível gravar código para um teste funcional ou para um teste de integração que pode ou não incluir testes no nível da interface do usuário. Se desejar acessar diretamente uma lógica de negócios, você poderá codificar um teste de unidade. Porém, em determinadas circunstâncias, pode ser benéfico incluir testes dos diversos controles de interface de usuário no aplicativo. Um teste de IU codificado pode verificar se a variação de código não afeta a funcionalidade do aplicativo.

![Testes durante o desenvolvimento de aplicativos](../test/media/cuit_overview.png)

É fácil criar um teste de IU codificado. Basta realizar o teste manualmente enquanto o **Construtor de Teste de IU Codificado** é executado em segundo plano. Também é possível especificar quais valores devem ser exibidos em campos específicos. O **Construtor de Teste de IU Codificado** registra suas ações e gera código com base nelas. Depois que o teste for criado, será possível editá-lo em um editor especializado que permite modificar a sequência de ações.

Como alternativa, se tiver um caso de teste que tenha sido registrado no Microsoft Test Manager, será possível gerar código a partir dele. Para obter mais informações, consulte [Gravar e reproduzir testes manuais](/azure/devops/test/mtm/record-play-back-manual-tests?view=vsts).

O **Construtor de Teste de IU Codificado** especializado e o editor facilitam a criação e a edição de testes de IU codificados mesmo que suas habilidades principais estejam concentradas em testes, e não em codificação. Mas, se você for um desenvolvedor e quiser estender o teste de maneira mais avançada, o código será estruturado para simplificar a cópia e a adaptação. Por exemplo, convém registrar um teste para comprar algo em um site e editar o código gerado para adicionar um loop que compre muitos itens.

**Requisitos**

- Visual Studio Enterprise
- Componente de teste de IU codificado

Para obter mais informações sobre quais plataformas e configurações são compatíveis com testes de IU codificados, confira [Plataformas com suporte](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md).

## <a name="install-the-coded-ui-test-component"></a>Instalar o componente de teste de IU codificado

Para acessar as ferramentas e os modelos do teste de IU codificado, instale o componente **Teste de IU Codificado** do Visual Studio 2017.

1. Inicie o **Instalador do Visual Studio** escolhendo **Ferramentas** > **Obter Ferramentas e Recursos**.

1. No **Instalador do Visual Studio**, escolha a guia **Componentes individuais** e, em seguida, role para baixo até a seção **Depuração e testes**. Selecione o componente **Teste de IU Codificado**.

   ![Componente de teste de IU codificado](media/coded-ui-test-component.png)

1. Selecione **Modificar**.

## <a name="create-a-coded-ui-test"></a>Criar um teste de IU codificado

1. Crie um projeto de teste de IU codificado.

   Os testes de IU codificados devem estar contidos em um projeto de teste de IU codificado. Se você ainda não tiver um projeto de teste de IU codificado, crie um. Escolha **Arquivo** > **Novo** > **Projeto** para abrir a caixa de diálogo **Novo Projeto**. No painel de categorias à esquerda, expanda **Instalado** > **Visual Basic** *ou* **Visual C#** > **Teste**. Selecione o modelo **Projeto de Teste de IU Codificado** e, em seguida, escolha **OK**.

   ![Modelo de projeto de teste de IU codificado na caixa de diálogo Novo Projeto](media/coded-ui-test-project-template.png)

   > [!NOTE]
   > Se o modelo **Projeto de Teste de IU Codificado** não for exibido, será necessário [instalar o componente Teste de IU Codificado](../test/use-ui-automation-to-test-your-code.md#install-the-coded-ui-test-component).

2. Adicione um arquivo de teste de IU codificado.

     Se tiver acabado de criar um projeto de IU codificado, o primeiro arquivo CUIT será adicionado automaticamente. Para adicionar outro arquivo de teste, abra o menu de atalho no projeto de teste de IU codificado em **Gerenciador de Soluções** e, em seguida, escolha **Adicionar** > **Teste de IU Codificado**.

     Na caixa de diálogo **Gerar Código para Teste de IU Codificado**, escolha **Registrar ações** > **Editar o mapa de interface do usuário ou adicionar declarações**.

     ![Caixa de diálogo Gerar Código para Teste de IU Codificado](media/generate-code-for-coded-ui-test.png)

     O **Construtor de Teste de IU Codificado** é exibido.

     ![Construtor de Teste de IU Codificado](../test/media/codedui_testbuilder.png)

3. Registre uma sequência de ações.

     **Para começar a registrar**, escolha o ícone **Registrar**. Realize as ações que você quer testar no aplicativo, inclusive iniciá-lo, se isso for necessário. Por exemplo, se você estiver testando um aplicativo Web, convém iniciar um navegador, navegar até o site e fazer logon no aplicativo.

     **Para pausar o registro**, por exemplo, se você precisar lidar com emails recebidos, escolha **Pausar**.

    > [!WARNING]
    > Todas as ações realizadas na área de trabalho serão registradas. Pause a gravação se estiver realizando ações que possam levar à exclusão de dados confidenciais na gravação.

     **Para excluir ações** registradas por equívoco, escolha **Editar Etapas**.

     **Para gerar um código** que replicará as ações, escolha o ícone **Gerar Código** e digite um nome e uma descrição para o método de teste de IU codificado.

4. Verifique os valores nos campos de interface do usuário, como caixas de texto.

     Escolha **Adicionar Declarações** no **Construtor de Teste de IU Codificado** e, em seguida, escolha um controle de interface do usuário no aplicativo em execução. Na lista de propriedades exibida, selecione uma propriedade, por exemplo, **Texto** em uma caixa de texto. No menu de atalho, escolha **Adicionar Asserção**. Na caixa de diálogo, selecione o operador de comparação, o valor de comparação e a mensagem de erro.

     Feche a janela de asserção e escolha **Gerar Código**.

     ![Elemento de destino do teste de IU codificado](../test/media/codedui_1.png)

    > [!TIP]
    > Alterne entre o registro de ações e a verificação de valores. Gere códigos no final de cada sequência de ações ou verificações. Se quiser, você poderá inserir novas ações e verificações depois.

     Para obter mais detalhes, confira [Validar as propriedades de controles](#validate-the-properties-of-ui-controls).

5. Exiba o código de teste gerado.

     Para exibir o código gerado, feche a janela Construtor de Teste de IU. No código, é possível ver os nomes que você deu a cada etapa. O código está no arquivo CUIT que você criou:

    ```csharp
    [CodedUITest]
    public class CodedUITest1
    { ...
      [TestMethod]
      public void CodedUITestMethod1()
      {
          this.UIMap.AddTwoNumbers();
          this.UIMap.VerifyResultValue();
          // To generate more code for this test, select
          // "Generate Code" from the shortcut menu.
      }
    }
    ```

6. Adicione mais ações e asserções.

   Coloque o cursor no ponto apropriado no método de teste e, no menu de atalho, escolha **Gerar Código para Teste de IU Codificado**. O novo código será inserido nesse ponto.

7. Edite os detalhes das ações de teste e as asserções.

     Abra *UIMap.uitest*. Esse arquivo é aberto no **Editor de Teste de IU Codificado**, em que é possível editar qualquer sequência de ações registradas, além de editar as declarações.

     ![Editor de Testes de Interface de Usuário Codificada](../test/media/cuit_editor_edit.png)

     Para obter mais informações, confira [Editar testes de IU codificados usando o editor de teste de IU codificado](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md).

8. Execute o teste.

   Use o Gerenciador de Testes ou abra o menu de atalho no método de teste e, em seguida, escolha **Executar Testes**. Para obter mais informações sobre como executar testes, consulte [Executar testes de unidade com o Gerenciador de Testes](../test/run-unit-tests-with-test-explorer.md) e *Opções adicionais para executar testes de IU codificados* na seção [O que vem a seguir?](#what's-next?), no final deste tópico.

As seções restantes neste tópico fornecem mais detalhes sobre as etapas desse procedimento.

Para obter um exemplo mais detalhado, confira [Passo a passo: Criando, editando e mantendo um teste de IU codificado](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md). Neste passo a passo, você criará um aplicativo simples do Windows Presentation Foundation (WPF) para demonstrar como criar, editar e manter um teste de IU codificado. O passo a passo fornece soluções para corrigir os testes que foram interrompidos por vários problemas de timing e refatoração de controle.

## <a name="start-and-stop-the-application-under-test"></a>Iniciar e parar o aplicativo em teste

Se não quiser iniciar e parar o aplicativo, o navegador ou o banco de dados separadamente para cada teste, faça um dos seguintes:

- Se não quiser registrar as ações para iniciar o aplicativo em teste, será necessário iniciá-lo antes de escolher o ícone **Registrar**.

- No final de um teste, o processo no qual o teste é executado é encerrado. Se tiver iniciado o aplicativo no teste, normalmente, o aplicativo é fechado.  Se não quiser que o teste feche o aplicativo quando terminar, adicione um arquivo *.runsettings* à solução e usar a opção `KeepExecutorAliveAfterLegacyRun`. Para obter mais informações, consulte [Configurar testes de unidade usando um arquivo .runsettings](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md).

- Adicione um método de inicialização do teste, identificado por um atributo `[TestInitialize]`, que executa o código no início de cada método de teste. Por exemplo, você poderia iniciar o aplicativo do método TestInitialize.

- Adicione um método de limpeza do teste, identificado por um atributo `[TestCleanup]`, que executa o código no final de cada método de teste. Por exemplo, o método para fechar o aplicativo poderia ser chamado do método TestCleanup.

## <a name="validate-the-properties-of-ui-controls"></a>Validar as propriedades de controles de IU

É possível usar o **Construtor de Teste de IU Codificado** para adicionar um controle de interface do usuário ao <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap> para o teste ou gerar código para um método de validação que usa uma asserção para um controle de interface do usuário.

Para gerar declarações para os controles de interface do usuário, escolha a ferramenta **Adicionar Declarações** no **Construtor de Teste de IU Codificado** e arraste-a até o controle no aplicativo em teste que você deseja verificar se está correto. Quando a caixa contornar o controle, solte o mouse. O código da classe de controle é criado imediatamente no arquivo *UIMap.Designer.cs*.

![Elemento de destino do teste de IU codificado](../test/media/codedui_1.png)

Agora, as propriedades desse controle serão listadas na caixa de diálogo **Adicionar Asserções**.

Outra maneira de navegar até um determinado controle é escolhendo a seta **(<<)** para expandir a exibição do **Mapa de Controles de interface do usuário**. Para encontrar um controle pai, irmão ou filho, é possível clicar em qualquer lugar no mapa e usar as telas de direção para navegar pela árvore.

![Propriedades de teste de IU codificado](../test/media/codedui_2.png)

> [!TIP]
> Se você não vir nenhuma propriedade quando selecionar um controle em seu aplicativo ou não vir o controle no mapa de controle de interface do usuário, verifique se o controle tem uma ID exclusiva no código do aplicativo. A ID exclusiva pode ser um atributo de ID HTML ou um UId do WPF.

Depois, abra o menu de atalho na propriedade do controle de interface do usuário que você deseja verificar e aponte para **Adicionar Asserção**. Na caixa de diálogo **Adicionar Asserção**, selecione o **Comparador** da asserção, por exemplo, <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A> e digite o valor da asserção em **Valor de Comparação**.

![Asserções do teste de IU codificado](../test/media/codedui_3.png)

Quando tiver adicionado todas as asserções do teste, escolha **OK**.

Para gerar o código das asserções e adicionar o controle ao mapa de interface do usuário, escolha o ícone **Gerar Código**. Digite um nome para o método de teste de IU codificado e uma descrição para o método, que serão adicionados como comentários para ele. Escolha **Adicionar e Gerar**. Em seguida, escolha o ícone **Fechar** para fechar o **Construtor de Teste de IU Codificado**. Isso gera um código semelhante ao código a seguir. Por exemplo, se o nome inserido for `AssertForAddTwoNumbers`, o código terá a aparência deste exemplo:

- Adiciona uma chamada ao método de asserção AssertForAddTwoNumbers para o método de teste no arquivo de teste de IU codificado:

    ```csharp
    [TestMethod]
    public void CodedUITestMethod1()
    {
        this.UIMap.AddTwoNumbers();
        this.UIMap.AssertForAddTwoNumbers();
    }
    ```

     É possível editar esse arquivo para alterar a ordem das etapas e das asserções ou criar novos métodos de teste. Para adicionar mais código, coloque o cursor no método de teste e, no menu de atalho, escolha **Gerar Código para Teste de IU Codificado**.

- Adiciona um método chamado `AssertForAddTwoNumbers` ao mapa de interface do usuário (*UIMap.uitest*). Esse arquivo é aberto no **Editor de Teste de IU Codificado**, em que é possível editar as declarações.

     ![Editar asserção usando o Editor do Teste de IU Codificado](../test/media/cuit_editor_assert.png)

     Para obter mais informações, confira [Editar testes de IU codificados usando o editor de teste de IU codificado](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md).

     Exiba também o código gerado do método de declaração em *UIMap.Designer.cs*. Porém, você não deve editar esse arquivo. Caso deseje criar uma versão adaptada do código, copie os métodos para outro arquivo, como *UIMap.cs*, renomeie os métodos e edite-os nesse arquivo.

    ```csharp
    public void AssertForAddTwoNumbers()
    {
        ...
    }
    ```

### <a name="select-a-hidden-control-using-the-keyboard"></a>Selecionar um controle oculto usando o teclado

Se o controle que você deseja selecionar perder o foco e desaparecer quando você tentar selecionar a ferramenta **Adicionar Declarações** no **Construtor de Teste de IU Codificado**:

Às vezes, ao adicionar controles e validar suas propriedades, talvez você precise usar o teclado. Por exemplo, quando você tentar gravar um teste de IU codificado que usa um controle de menu de contexto, a lista de itens de menu no controle perderá o foco e desaparecerá quando você tentar selecionar a ferramenta **Adicionar Declarações** no **Construtor de Teste de IU Codificado**. Isso é demonstrado na ilustração a seguir, em que o menu de contexto no Internet Explorer perderá o foco e desaparecerá se você tentar selecioná-lo com a ferramenta **Adicionar Declarações**.

![CodedUITest&#95;SelectControlKeyboard](../test/media/codeduitest_selectcontrolkeyboard.png)

Para usar o teclado e selecionar um controle de interface de usuário, focalize o controle usando o mouse. Em seguida, mantenha as teclas **Ctrl** e **I** pressionadas simultaneamente. Solte as teclas. O controle é registrado pelo **Construtor de Teste de IU Codificado**.

#### <a name="manually-record-mouse-hovers"></a>Registrar manualmente passagens do mouse

Se não conseguir registrar uma passagem do mouse sobre um controle:

Em algumas circunstâncias, um determinado controle usado em um teste de IU codificado pode exigir que você use o teclado para registrar manualmente os eventos de passagem do mouse. Por exemplo, quando você testa um aplicativo do Windows Form ou do Windows Presentation Foundation (WPF), talvez haja código personalizado. Ou talvez haja um comportamento especial definido para a passagem do mouse sobre um controle, como a expansão de um nó de árvore quando um usuário o focaliza. Para testar circunstâncias como essa, você precisa notificar manualmente o **Construtor de Teste de IU Codificado** que está focalizando o controle pressionando as teclas predefinidas do teclado.

Ao realizar o teste de IU codificado, focalize o controle. Em seguida, mantenha a tecla **Ctrl** pressionada, enquanto pressiona e mantém pressionadas as teclas **Shift** e **R** do teclado. Solte as teclas. Um evento de passagem do mouse é gravado pelo **Construtor de Teste de IU Codificado**.

![CodedUI&#95;Hover](../test/media/codedui_hover.png)

Depois que você gerar o método de teste, um código semelhante ao seguinte exemplo será adicionado ao arquivo *UIMap.Designer.cs*:

```csharp
// Mouse hover '1' label at (87, 9)
Mouse.Hover(uIItem1Text, new Point(87, 9));
```

### <a name="configure-mouse-hover-keyboard-assignments"></a>Configurar atribuições de teclado de passagem do mouse

Se a atribuição de tecla para capturar eventos de passagem do mouse estiver sendo usada em outro lugar do ambiente:

Se necessário, a atribuição de teclado padrão de **Ctrl**+**Shift**+**R** usada para aplicar eventos de passagem do mouse nos testes de IU codificados pode ser configurada para usar teclas diferentes.

> [!WARNING]
> Você não deve alterar as atribuições de teclado para eventos de passagem do mouse em circunstâncias comuns. Tenha cuidado ao definir a atribuição de teclado. A opção talvez já esteja em uso em outro lugar dentro do Visual Studio ou no aplicativo que está sendo testado.

Para alterar as atribuições de teclado, modifique o seguinte arquivo de configuração:

*%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CodedUITestBuilder.exe.config*

No arquivo de configuração, altere os valores das teclas `HoverKeyModifier` e `HoverKey` para modificar as atribuições de teclado:

```xml
<!-- Begin : Background Recorder Settings -->
<!-- HoverKey to use. -->
<add key="HoverKeyModifier" value="Control, Shift"/>
<add key="HoverKey" value="R"/>
```

### <a name="set-implicit-mouse-hovers-for-the-web-browser"></a>Definir passagens do mouse implícitas para o navegador da Web

Se tiver problemas para registrar passagens do mouse em um site:

Em muitos sites, quando você focaliza um determinado controle, ele expande para mostrar detalhes adicionais. Geralmente, eles parecem menus em aplicativos da área de trabalho. Como esse é um padrão comum, os testes de IU codificados permitem passagens do mouse implícitas na navegação na Web. Por exemplo, se você registrar passagens do mouse no Internet Explorer, será acionado um evento. Esses eventos podem acarretar o registro de passagens redundantes do mouse. Por isso, as passagens do mouse implícitas são registradas com `ContinueOnError` definido como `true` no arquivo de configuração de teste de interface do usuário. Isso permite que a reprodução continue em caso de falha em um evento de passagem do mouse.

Para permitir o registro de passagens do mouse implícitas em um navegador da Web, abra o arquivo de configuração:

*%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CodedUITestBuilder.exe.config*

Verifique se o arquivo de configuração está com a chave `RecordImplicitiHovers` definida com o valor `true`, como mostrado no exemplo a seguir:

```xml
<!--Use this to enable/disable recording of implicit hovers.-->
<add key="RecordImplicitHover" value="true"/>
```

## <a name="customize-the-coded-ui-test"></a>Personalizar o teste de IU codificado

Depois de criar o teste de IU codificado, você poderá editá-lo usando qualquer uma destas ferramentas no Visual Studio:

- Use o **Construtor de Teste de IU Codificado** para adicionar controles e validação a seus testes. Confira a seção [Adicionar controles e validar suas propriedades](#validate-the-properties-of-ui-controls) neste tópico.

- O **Editor do Construtor de Teste de IU Codificado** permite modificar facilmente seus testes de IU codificados. Com o **Editor de Teste de IU Codificado**, é possível localizar, exibir e editar seus métodos de teste. Também é possível editar ações de interface do usuário e seus controles associados no mapa de controles de IU. Para obter mais informações, confira [Editar testes de IU codificados usando o editor de teste de IU codificado](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md).

- **Editor de Códigos:**

    - Adicione manualmente o código dos controles ao teste, conforme descrito na seção [Ações e propriedades do controle de IU codificado](#coded-ui-control-actions-and-properties) deste tópico.

    - Depois de criar um teste de IU codificado, você poderá modificá-lo para ser controlado por dados. Para obter mais informações, confira [Criar um teste de IU codificado controlado por dados](../test/creating-a-data-driven-coded-ui-test.md).

    - Na reprodução de um teste de IU codificado, é possível instruir o teste a aguardar a ocorrência de determinados eventos, como a exibição de uma janela, o desaparecimento da barra de progresso etc. Para isso, adicione o método UITestControl.WaitForControlXXX() apropriado. Para obter uma lista completa dos métodos disponíveis, confira [Fazer os testes de IU codificados aguardarem eventos específicos durante a reprodução](../test/making-coded-ui-tests-wait-for-specific-events-during-playback.md). Para obter um exemplo de um teste de IU codificado que aguarda a habilitação de um controle usando o método WaitForControlEnabled, confira [Passo a passo: Criando, editando e mantendo um teste de IU codificado](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md).

    - Os teste de IU codificados incluem suporte a alguns dos controles HTML5 incluídos no Internet Explorer 9 e no Internet Explorer 10. Para obter mais informações, confira [Usar controles HTML5 em testes de IU codificados](../test/using-html5-controls-in-coded-ui-tests.md).

    - Diretrizes de codificação do teste de IU codificado:

       - [Anatomia de um teste de IU codificado](../test/anatomy-of-a-coded-ui-test.md)

       - [Práticas recomendadas para testes de IU codificados](../test/best-practices-for-coded-ui-tests.md)

       - [Testar um aplicativo grande com vários Mapas de Interface do Usuário](../test/testing-a-large-application-with-multiple-ui-maps.md)

       - [Configurações e plataformas compatíveis para testes de IU codificados e gravações de ação](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)

### <a name="the-generated-code"></a>O código gerado

Quando você escolhe **Gerar Código**, diversas partes do código são criadas:

- Uma linha no método de teste.

    ```csharp
    [CodedUITest]
    public class CodedUITest1
    { ...
      [TestMethod]
      public void CodedUITestMethod1()
      {
          this.UIMap.AddTwoNumbers();
          // To generate more code for this test, select
          // "Generate Code" from the shortcut menu.      }
    }
    ```

     É possível clicar com o botão direito do mouse nesse método para adicionar mais ações registradas e verificações. Também é possível editá-lo para estender ou modificar o código. Por exemplo, você poderia embutir parte do código em um loop.

     Também é possível adicionar novos métodos de teste e adicionar código a eles da mesma forma. Cada método de teste deve ter o atributo `[TestMethod]`.

- Um método em *UIMap.uitest*.

     Esse método inclui os detalhes das ações registradas ou o valor verificado por você. Edite esse código abrindo *UIMap.uitest*. Ele é aberto em um editor especializado, no qual é possível excluir ou refatorar as ações registradas.

     Exiba também o método gerado em *UIMap.Designer.cs*. Esse método realiza as ações registradas quando você executa o teste.

    ```csharp
    // File: UIMap.Designer.cs
    public partial class UIMap
    {
      /// <summary>
      /// Add two numbers
      /// </summary>
      public void AddTwoNumbers()
      { ...   }
    }
    ```

    > [!WARNING]
    > Você não deve editar esse arquivo, porque ele será registrado quando mais testes forem criados.

     É possível criar versões adaptadas desses métodos copiando-os em *UIMap.cs*. Por exemplo, você poderia criar uma versão parametrizada que seria chamada a partir de um método de teste:

    ```csharp
    // File: UIMap.cs
    public partial class UIMap // Same partial class
    {
      /// <summary>
      /// Add two numbers - parameterized version
      /// </summary>
      public void AddTwoNumbers(int firstNumber, int secondNumber)
      { ...   // Code modified to use parameters.
      }
    }
    ```

- Declarações em *UIMap.uitest*.

    Essas declarações representam os controles de interface de usuário do aplicativo usados pelo teste. Elas são usadas pelo código gerado para operar os controles e acessar suas propriedades.

    Também será possível usá-las para gravar seu próprio código. Por exemplo, é possível fazer o método de teste escolher um hiperlink em um aplicativo Web, digitar um valor em uma caixa de texto ou ramificar e utilizar ações de testes diferentes com base no valor de um campo.

    É possível adicionar vários testes de IU codificados e vários objetos e arquivos de mapa de IU para facilitar os testes de um aplicativo grande. Para obter mais informações, confira [Testar um aplicativo grande com vários Mapas de Interface do Usuário](../test/testing-a-large-application-with-multiple-ui-maps.md).

Para obter mais informações sobre o código gerado, confira [Anatomia de um teste de IU codificado](../test/anatomy-of-a-coded-ui-test.md).

## <a name="coded-ui-control-actions-and-properties"></a>Propriedades e ações de controle de IU codificado

Quando você trabalha com controles de teste de IU em testes de IU codificados, eles são separados em duas partes: ações e propriedades.

- A primeira parte consiste em ações, que é possível realizar em controles de teste de IU. Por exemplo, os testes de IU codificados podem simular cliques do mouse em um controle de teste de IU ou simular teclas pressionadas no teclado para afetar um controle de teste de IU.

- A segunda parte consiste em permitir que você obtenha e defina as propriedades em um controle de teste de IU. Por exemplo, os testes de IU codificados podem obter a contagem de itens em um `ListBox` ou definir um `CheckBox` no estado selecionado.

**Acessando Ações do Controle de Teste de IU**

Para realizar ações em controles de teste de IU, como cliques do mouse ou ações de teclado, use os métodos nas classes <xref:Microsoft.VisualStudio.TestTools.UITesting.Mouse> e <xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard>:

- Para realizar uma ação orientada pelo mouse, como um clique do mouse em um controle de teste de IU, use <xref:Microsoft.VisualStudio.TestTools.UITesting.Mouse.Click%2A>.

     `Mouse.Click(buttonCancel);`

- Para realizar uma ação orientada pelo teclado, como digitar em um controle de edição, use <xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard.SendKeys%2A>.

     `Keyboard.SendKeys(textBoxDestination, @"C:\Temp\Output.txt");`

**Acessando Propriedades do Controle de Teste de IU**

Para obter e definir valores de propriedade específicas de controle de interface de usuário, é possível obter e definir diretamente os valores como as propriedades de um controle ou usar os métodos <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A?displayProperty=fullName> e <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A?displayProperty=fullName> com o nome da propriedade específica que você deseja obter ou definir.

<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A> retorna um objeto, que pode ser convertido no <xref:System.Type> apropriado. <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A> aceita um objeto para o valor da propriedade.

### <a name="to-get-or-set-properties-from-ui-test-controls-directly"></a>Para obter ou definir propriedades de controles de teste de IU diretamente

Com controles que derivam de <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl>, como [HtmlList](xref:Microsoft.VisualStudio.TestTools.UITesting.HtmlControls.HtmlList) ou [WinComboBox](xref:Microsoft.VisualStudio.TestTools.UITesting.WinControls.WinComboBox), você pode obter ou definir os valores de propriedade diretamente. O código a seguir mostra alguns exemplos:

 ```csharp
 int i = myHtmlList.ItemCount;
 myWinCheckBox.Checked = true;
 ```

### <a name="to-get-properties-from-ui-test-controls"></a>Para obter propriedades de controles de teste de IU

- Para obter um valor de propriedade de um controle, use <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A>.

- Para especificar a propriedade de controle a ser obtida, use a cadeia de caracteres apropriada da classe `PropertyNames` em cada controle como parâmetro para <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A>.

- <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A> retorna o tipo de dados apropriado, mas esse valor retornado é convertido como um <xref:System.Object>. Em seguida, o <xref:System.Object> de retorno deve ser convertido como tipo apropriado.

     Exemplo:

     `int i = (int)GetProperty(myHtmlList.PropertyNames.ItemCount);`

### <a name="to-set-properties-for-ui-test-controls"></a>Para definir propriedades para controles de teste de IU

- Para obter uma propriedade em um controle, use <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A>.

- Para especificar a propriedade do controle a ser definida, use a cadeia de caracteres apropriada da classe `PropertyNames` como primeiro parâmetro para <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A>, com o valor da propriedade como segundo parâmetro.

     Exemplo:

     `SetProperty(myWinCheckBox.PropertyNames.Checked, true);`

## <a name="debug"></a>Depurar

Você pode analisar testes de IU codificados usando logs de teste de IU codificado. Os logs de teste de IU codificado filtram e registram informações importantes sobre as execuções de teste de IU codificado. O formato dos logs permite depurar rapidamente os problemas. Para obter mais informações, confira [Analisar testes de IU codificados usando logs de teste de IU codificado](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md).

## <a name="whats-next"></a>O que vem a seguir?

**Opções adicionais para executar testes de IU codificados:** é possível executar testes de IU codificados diretamente no Visual Studio, como descrito anteriormente neste tópico. Além disso, você pode executar testes automatizados de interface do usuário no Microsoft Test Manager ou usando o Azure Pipelines. Quando são automatizados, os testes de IU codificados precisam interagir com a área de trabalho quando executados, diferentemente de outros testes automatizados.

- [Executar testes de unidade com o Gerenciador de Testes](../test/run-unit-tests-with-test-explorer.md)

- [Executar Testes no Processo de build](/azure/devops/pipelines/test/getting-started-with-continuous-testing?view=vsts)

- [Como configurar o agente de teste para executar testes que interagem com a área de trabalho](https://msdn.microsoft.com/Library/3a94dd07-6d17-402c-ae8f-7947143755c9)

**Adicionar suporte para controles personalizados:** a estrutura de teste de IU codificado não oferece suporte para todas as interfaces do usuário possíveis e pode não oferecer suporte à interface do usuário que você deseja testar. Por exemplo, você não pode criar imediatamente um teste de IU codificado para a IU do Microsoft Excel. Porém, você pode criar uma extensão para o framework de teste de IU codificado que oferecerá suporte a um controle personalizado.

- [Habilitar testes de IU codificados dos controles](../test/enable-coded-ui-testing-of-your-controls.md)

- [Estender testes de IU codificados e gravações de ação](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)

Os testes de IU codificados costumam ser usados para automatizar testes manuais. Para obter mais informações sobre testes manuais, consulte [Run manual tests with Microsoft Test Manager](/azure/devops/test/mtm/run-manual-tests-with-microsoft-test-manager?view=vsts) (Executar testes manuais com o Microsoft Test Manager). Para obter mais informações sobre testes automatizados, confira [Ferramentas de teste no Visual Studio](../test/improve-code-quality.md).

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap>
- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert>
- [Passo a passo: Criar, editar e manter um teste de IU codificado](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)
- [Criar um teste de IU codificado para testar um aplicativo UWP](test-uwp-app-with-coded-ui-test.md)
- [Anatomia de um teste de IU codificado](../test/anatomy-of-a-coded-ui-test.md)
- [Práticas recomendadas para testes de IU codificados](../test/best-practices-for-coded-ui-tests.md)
- [Testar um aplicativo grande com vários Mapas de Interface do Usuário](../test/testing-a-large-application-with-multiple-ui-maps.md)
