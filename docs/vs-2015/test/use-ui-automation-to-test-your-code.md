---
title: Usar Automação de Interface do Usuário para Testar Código | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.codedUITest
- vs.codedUITest.recorder
- vs.codedUITest.testbuilder
- vs.codedUITest.addAssertions
- vs.codedUITest.createdialog
helpviewer_keywords:
- automated tests, testing UI interface
- coded UI test
ms.assetid: ad9e3eaa-ab86-436e-95b8-dc20eb1f8b2a
caps.latest.revision: 87
ms.author: gewarren
manager: douge
ms.openlocfilehash: 251f6a99f64a191f1a5d957157c06c7e89147217
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49812667"
---
# <a name="use-ui-automation-to-test-your-code"></a>Usar automação de interface do usuário para testar código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os testes automatizados que orientam o aplicativo por meio da interface do usuário (UI) são conhecidos como *testes de IU codificados* (CUITs). Entre esses testes estão testes funcionais dos controles de interface de usuário. Eles permitem verificar se todo o aplicativo, inclusive sua interface do usuário, está funcionando corretamente. Os testes de IU codificados são especialmente úteis quando há validação ou outra lógica na interface do usuário, como em uma página da Web. Eles também costumam ser usados para automatizar um teste manual existente.  
  
 Conforme mostrado na ilustração a seguir, uma experiência de desenvolvimento típica pode ser uma em que, inicialmente, você só compila o aplicativo (F5) e clica nos controles de interface de usuário para verificar se as coisas estão funcionando corretamente. Em seguida, você pode optar por criar um teste codificado para não ser mais necessário testar o aplicativo manualmente. Dependendo da funcionalidade específica testada no aplicativo, você pode gravar código para um teste funcional ou para um teste de integração que pode ou não incluir testes no nível da interface do usuário. Se quiser apenas acessar diretamente uma lógica de negócios, você poderá codificar um teste de unidade. Porém, em determinadas circunstâncias, pode ser benéfico incluir testes dos diversos controles de interface de usuário no aplicativo. Um teste de IU codificado pode automatizar o cenário inicial (F5), verificando se a variação de código não afeta a funcionalidade do aplicativo.  
  
 ![Testes durante o desenvolvimento de aplicativos](../test/media/cuit-overview.png "CUIT_Overview")  
  
 É fácil criar um teste de IU codificado. Basta realizar o teste manualmente enquanto o CUIT Test Builder é executado em segundo plano. Também é possível especificar quais valores devem ser exibidos em campos específicos. O CUIT Test Builder registra as ações e gera códigos a partir delas. Depois que o teste for criado, será possível editá-lo em um editor especializado que permite modificar a sequência de ações.  
  
 Como alternativa, se tiver um caso de teste que tenha sido registrado no Microsoft Test Manager, será possível gerar código a partir dele. Para obter mais informações, consulte [Gravar e reproduzir testes manuais](http://msdn.microsoft.com/library/9792e72f-600e-441f-9d4e-6510e5965665).  
  
 O CUIT Test Builder especializado e o editor facilitam a criação e a edição de testes de IU codificados mesmo que suas habilidades principais estejam concentradas em testes, e não em codificação. Mas, se você for um desenvolvedor e quiser estender o teste de maneira mais avançada, o código será estruturado para simplificar a cópia e a adaptação. Por exemplo, convém registrar um teste para comprar algo em um site e editar o código gerado para adicionar um loop que compre muitos itens.  
  
 **Requisitos**  
  
- Visual Studio Enterprise  
  
  Para obter mais informações sobre quais plataformas e configurações têm suporte para testes de IU codificado, consulte [Configurações e Plataformas com Suporte para Testes de IU Codificados e Gravações de Ação](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md).  
  
  **Neste tópico**  
  
- [Criando testes de IU codificados](#VerifyingCodeUsingCUITCreate)  
  
  -   [Procedimento principal](#VerifyingCodeUsingCUITCreate)  
  
  -   [Iniciando e parando o aplicativo](#starting)  
  
  -   [Validando as propriedades de Controles de Interface do Usuário](#VerifyingCodeUsingCUITGenerateAssertions)  
  
- [Personalizando o teste de IU codificado](#VerifyingCodeCUITModify)  
  
  -   [O Código Gerado](#generatedCode)  
  
  -   [Codificando ações e propriedades de controle de interface do usuário](#actions)  
  
  -   [Depuração](#debugging)  
  
- [O que vem a seguir?](#VerifyCodeUsingCUITWhatsNext)  
  
##  <a name="VerifyingCodeUsingCUITCreate"></a> Criando Testes de IU Codificados  
  
1. **Crie um projeto de Teste de IU Codificado.**  
  
    Os testes de IU codificados devem estar contidos em um projeto de teste de IU codificado. Se você ainda não tiver um projeto de teste de IU codificado, crie um. No **Gerenciador de Soluções**, no menu de atalho da solução, escolha **Adicionar**, **Novo Projeto** e, em seguida, selecione **Visual Basic** ou **Visual C#**. Em seguida, escolha **Teste**, **Teste de IU Codificado**.  
  
   - <em>Não vejo os modelos de projeto do **Teste de IU Codificado</em>*.*  
  
      Você pode estar usando uma versão do Visual Studio que não oferece suporte a testes de IU codificados. Para criar testes de IU codificados, é necessário usar o Visual Studio Enterprise.  
  
2. **Adicione um arquivo de teste de IU codificado.**  
  
    Se tiver acabado de criar um projeto de IU codificado, o primeiro arquivo CUIT será adicionado automaticamente. Para adicionar outro arquivo de teste, abra o menu de atalho no projeto de teste de IU codificado, aponte para **Adicionar** e, em seguida, escolha **Teste de IU Codificado**.  
  
    ![Criar um Teste de IU Codificado](../test/media/codedui-create.png "CodedUI_Create")  
  
    Na caixa de diálogo **Gerar Código para Teste de IU Codificado**, escolha **Registrar ações, editar o mapa de interface do usuário ou adicionar asserções**.  
  
    ![Selecione registrar ações](../test/media/codedui-codegendialogb.png "CodedUI_CodeGenDialogB")  
  
    O Construtor de Teste de IU Codificado é exibido, e o Visual Studio é minimizado.  
  
    ![Construtor de Teste de IU Codificado](../test/media/codedui-testbuilder.png "CodedUI_TestBuilder")  
  
3. **Registre uma sequência de ações**.  
  
    **Para começar a registrar**, escolha o ícone **Registrar**. Realize as ações que você quer testar no aplicativo, inclusive iniciá-lo, se isso for necessário.  
  
    Por exemplo, se você estiver testando um aplicativo Web, convém iniciar um navegador, navegar até o site e fazer logon no aplicativo.  
  
    **Para pausar o registro**, por exemplo, se você precisar lidar com emails recebidos, escolha **Pausar**.  
  
   > [!WARNING]
   >  Todas as ações realizadas na área de trabalho serão registradas. Pause a gravação se estiver realizando ações que possam levar à exclusão de dados confidenciais na gravação.  
  
    **Para excluir ações** registradas por equívoco, escolha **Editar Ações**.  
  
    **Para gerar um código** que replicará as ações, escolha o ícone **Gerar Código** e digite um nome e uma descrição para o método de teste de IU codificado.  
  
4. **Verifique os valores nos campos de interface do usuário, como caixas de texto**.  
  
    Escolha **Adicionar Asserções** no Construtor de Teste de IU Codificado e escolha um controle de interface do usuário no aplicativo em execução. Na lista de propriedades exibida, selecione uma propriedade, por exemplo, **Texto** em uma caixa de texto. No menu de atalho, escolha **Adicionar Asserção**. Na caixa de diálogo, selecione o operador de comparação, o valor de comparação e a mensagem de erro.  
  
    Feche a janela de asserção e escolha **Gerar Código**.  
  
    ![Elemento de destino do teste de IU codificado](../test/media/codedui-1.png "CodedUI_1")  
  
   > [!TIP]
   >  Alterne entre o registro de ações e a verificação de valores. Gere códigos no final de cada sequência de ações ou verificações. Se quiser, você poderá inserir novas ações e verificações depois.  
  
    Para obter mais detalhes, consulte [Validando Propriedades de Controles](#VerifyingCodeUsingCUITGenerateAssertions).  
  
5. **Exiba o código de teste gerado**.  
  
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
  
6. **Adicione mais ações e asserções**.  
  
    Coloque o cursor no ponto apropriado no método de teste e, no menu de atalho, escolha **Gerar Código para Teste de IU Codificado**. O novo código será inserido nesse ponto.  
  
7. **Edite os detalhes das ações de teste e as asserções**.  
  
    Abra UIMap.uitest. Esse arquivo é aberto no Editor de testes de interface de usuário codificada, em que é possível editar qualquer sequência de ações registradas, além de editar as asserções.  
  
    ![Editor de Teste de IU Codificado](../test/media/cuit-editor-edit.png "CUIT_Editor_edit")  
  
    Para obter mais informações, consulte [Editing Coded UI Tests Using the Coded UI Test Editor](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md) (Editando testes de IU codificada usando o Editor de teste de IU codificado).  
  
8. **Execute o teste**.  
  
    Use o Gerenciador de Testes ou abra o menu de atalho no método de teste e, em seguida, escolha **Executar Testes**. Para obter mais informações sobre como executar testes, consulte [Executar testes de unidade com o Gerenciador de Testes](../test/run-unit-tests-with-test-explorer.md) e *Opções adicionais para executar testes de IU codificados* na seção [O que vem a seguir?](#VerifyCodeUsingCUITWhatsNext), no final deste tópico.  
  
   As seções restantes neste tópico fornecem mais detalhes sobre as etapas desse procedimento.  
  
   Para obter um exemplo mais detalhado, consulte [Passo a passo: criar, editar e manter um teste de IU codificado](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md). Neste passo a passo, você criará um aplicativo simples do Windows Presentation Foundation (WPF) para demonstrar como criar, editar e manter um teste de IU codificado. O passo a passo fornece soluções para corrigir os testes que foram interrompidos por vários problemas de timing e refatoração de controle.  
  
###  <a name="starting"></a> Iniciando e parando o aplicativo em teste  
 *Não desejo iniciar e parar meu aplicativo, navegador ou banco de dados separadamente para cada teste. Como evito isso?*  
  
-   ![Pré-requisito](../test/media/prereq.png "Prereq") Se não quiser registrar as ações para iniciar o aplicativo em teste, será necessário iniciá-lo antes de escolher o ícone **Registrar**.  
  
-   ![Pré-requisito](../test/media/prereq.png "Prereq")No final de um teste, o processo no qual o teste é executado será encerrado. Se tiver iniciado o aplicativo no teste, normalmente, o aplicativo é fechado.  Se não quiser que o teste feche o aplicativo quando terminar, você deverá adicionar um arquivo .runsettings à solução e usar a opção `KeepExecutorAliveAfterLegacyRun`. Para obter mais informações, consulte [Configurar testes de unidade usando um arquivo .runsettings](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md).  
  
-   ![Prerequsite](../test/media/prereq.png "Prereq") É possível adicionar um método de inicialização do teste, identificado por um atributo [TestInitialize], que executa o código no início de cada método de teste. Por exemplo, você poderia iniciar o aplicativo do método TestInitialize.  
  
-   ![Prerequsite](../test/media/prereq.png "Prereq") É possível adicionar um método de limpeza de teste, identificado por um atributo [TestCleanup], que executa o código no fim de cada método de teste. Por exemplo, o método para fechar o aplicativo poderia ser chamado do método TestCleanup.  
  
###  <a name="VerifyingCodeUsingCUITGenerateAssertions"></a> Validando as propriedades de controles de interface do usuário  
 É possível usar o **Construtor de Teste de IU Codificado** para adicionar um controle de interface do usuário ao <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap> para o teste ou gerar código para um método de validação que usa uma asserção para um controle de interface do usuário.  
  
 Para gerar asserções para os controles de interface do usuário, escolha a ferramenta **Adicionar Asserções** no Construtor de Teste de IU Codificado e arraste-a até o controle no aplicativo em teste que você deseja verificar se está correto. Quando a caixa contornar o controle, solte o mouse. O código da classe de controle é criado imediatamente no arquivo `UIMap.Designer.cs`.  
  
 ![Elemento de destino do teste de IU codificado](../test/media/codedui-1.png "CodedUI_1")  
  
 Agora, as propriedades desse controle serão listadas na caixa de diálogo **Adicionar Asserções**.  
  
 Outra maneira de navegar até um determinado controle é escolhendo a seta **(<<)** para expandir a exibição do **Mapa de Controles de interface do usuário**. Para encontrar um controle pai, irmão ou filho, é possível clicar em qualquer lugar no mapa e usar as telas de direção para navegar pela árvore.  
  
 ![Propriedades de teste de IU codificado](../test/media/codedui-2.png "CodedUI_2")  
  
- *Não vejo nenhuma propriedade quando seleciono um controle no aplicativo ou não vejo o controle no Mapa de Controles de interface do usuário.*  
  
   No código do aplicativo, o controle que você deseja verificar deve ter uma ID exclusiva, como um atributo de ID HTML ou WPF UId. Talvez seja necessário atualizar o código do aplicativo para adicionar essas IDs.  
  
  Depois, abra o menu de atalho na propriedade do controle de interface do usuário que você deseja verificar e aponte para **Adicionar Asserção**. Na caixa de diálogo **Adicionar Asserção**, selecione o **Comparador** da asserção, por exemplo, <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A> e digite o valor da asserção em **Valor de Comparação**.  
  
  ![Asserções do teste de IU codificado](../test/media/codedui-3.png "CodedUI_3")  
  
  Quando tiver adicionado todas as asserções do teste, escolha **OK**.  
  
  Para gerar o código das asserções e adicionar o controle ao mapa de interface do usuário, escolha o ícone **Gerar Código**. Digite um nome para o método de teste de IU codificado e uma descrição para o método, que serão adicionados como comentários para ele. Escolha **Adicionar e Gerar**. Em seguida, escolha o ícone **Fechar** para fechar o **Construtor de Teste de IU Codificado**. Isso gera um código semelhante ao código a seguir. Por exemplo, se o nome inserido for `AssertForAddTwoNumbers`, o código terá a aparência deste exemplo:  
  
- Adiciona uma chamada ao método de asserção AssertForAddTwoNumbers para o método de teste no arquivo de teste de IU codificado:  
  
  ```  
  [TestMethod]  
  public void CodedUITestMethod1()  
  {  
      this.UIMap.AddTwoNumbers();  
      this.UIMap.AssertForAddTwoNumbers();  
  }  
  ```  
  
   É possível editar esse arquivo para alterar a ordem das etapas e das asserções ou criar novos métodos de teste. Para adicionar mais código, coloque o cursor no método de teste e, no menu de atalho, escolha **Gerar Código para Teste de IU Codificado**.  
  
- Adiciona um método chamado `AssertForAddTwoNumbers` ao mapa de interface do usuário (UIMap.uitest). Esse arquivo é aberto no Editor de testes de interface de usuário codificada, em que é possível editar as asserções.  
  
   ![Editar asserção usando o Editor de Teste de IU Codificado](../test/media/cuit-editor-assert.png "CUIT_Editor_assert")  
  
   Para obter mais informações, consulte [Editing Coded UI Tests Using the Coded UI Test Editor](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md) (Editando testes de IU codificada usando o Editor de teste de IU codificado).  
  
   Também é possível exibir o código gerado do método de asserção em UIMap.Designer.cs. Porém, você não deve editar esse arquivo. Se quiser criar uma versão adaptada do código, copie os métodos em outro arquivo, como UIMap.cs, renomeie e edite os métodos lá.  
  
  ```  
  public void AssertForAddTwoNumbers()  
  {  
      ...  
  }  
  ```  
  
  *O controle que desejo selecionar perde o foco e desaparece quando tento selecionar a ferramenta Adicionar Asserções no Construtor de Teste de IU Codificado. Como seleciono o controle?*  
  **Selecionando um controle oculto usando o teclado**  
  
  Às vezes, ao [adicionar controles e validar suas propriedades](#VerifyingCodeUsingCUITGenerateAssertions), será necessário usar o teclado. Por exemplo, quando você tenta registrar um teste de IU codificado que usa um controle de menu de contexto, a lista de itens de menu no controle perderá o foco e desaparecerá quando você tentar selecionar a ferramenta Adicionar Asserções no Construtor de Teste de IU Codificado. Isso é demonstrado na ilustração a seguir, em que o menu de contexto no Internet Explorer perderá o foco e desaparecerá se você tentar selecioná-lo usando a ferramenta Adicionar Asserções.  
  
  ![CodedUITest&#95;SelectControlKeyboard](../test/media/codeduitest-selectcontrolkeyboard.png "CodedUITest_SelectControlKeyboard")  
  
  Para usar o teclado e selecionar um controle de interface de usuário, focalize o controle usando o mouse. Em seguida, mantenha as teclas **Ctrl** e **I** pressionadas simultaneamente. Solte as teclas. O controle é registrado pelo Construtor de Teste de IU Codificado.  
  
> [!WARNING]
>  Se usar o Microsoft Lync, feche o Lync antes de iniciar o Construtor de Teste de IU Codificado. O Microsoft Lync interfere no atalho de teclado **Ctrl+I**.  
  
 *Não consigo registrar uma passagem do mouse sobre um controle. Existe uma solução alternativa para isso?*  
 **Registrar manualmente passagens do mouse**  
  
 Em algumas circunstâncias, um determinado controle usado em um teste de IU codificado pode exigir que você use o teclado para registrar manualmente eventos de passagem do mouse. Por exemplo, quando você testa um aplicativo do Windows Form ou do Windows Presentation Foundation (WPF), talvez haja código personalizado. Ou talvez haja um comportamento especial definido para a passagem do mouse sobre um controle, como a expansão de um nó de árvore quando um usuário o focaliza. Para testar circunstâncias como essa, você precisa notificar manualmente o Construtor de Teste de IU Codificado que está focalizando o controle pressionando as teclas predefinidas do teclado.  
  
 Ao realizar o teste de IU codificado, focalize o controle. Em seguida, mantenha a tecla Ctrl pressionada, enquanto pressiona e solta as teclas Shift e R do teclado. Solte as teclas. Um evento de passagem do mouse é registrado pelo Construtor de Teste de IU Codificado.  
  
 ![CodedUI&#95;Hover](../test/media/codedui-hover.png "CodedUI_Hover")  
  
 Depois que você gerar o método de teste, um código semelhante ao exemplo a seguir será adicionado ao arquivo UIMap.Desinger.cs:  
  
```csharp  
// Mouse hover '1' label at (87, 9)  
Mouse.Hover(uIItem1Text, new Point(87, 9));  
  
```  
  
 *A atribuição de tecla para capturar eventos de passagem do mouse está sendo usada em outro lugar do ambiente. Posso alterar a atribuição de tecla padrão?*  
 **Configurando atribuições de teclado de passagem do mouse**  
  
 Se necessário, a atribuição de teclado padrão de Ctrl+Shift+R usada para aplicar eventos de passagem do mouse nos testes de IU codificados pode ser configurada para usar teclas diferentes.  
  
> [!WARNING]
>  Você não deve alterar as atribuições de teclado para eventos de passagem do mouse em circunstâncias comuns. Tenha cuidado ao definir a atribuição de teclado. A opção talvez já esteja em uso em outro lugar dentro do Visual Studio ou no aplicativo que está sendo testado.  
  
 Para alterar as atribuições de teclado, você deve modificar o seguinte arquivo de configuração:  
  
 `<drive letter:>\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\CodedUITestBuilder.exe.config`  
  
 No arquivo de configuração, altere os valores das teclas `HoverKeyModifier` e `HoverKey` para modificar as atribuições de teclado:  
  
```  
<!-- Begin : Background Recorder Settings -->  
<!-- HoverKey to use. -->  
<add key="HoverKeyModifier" value="Control, Shift"/>  
<add key="HoverKey" value="R"/>  
  
```  
  
 *Tenho problemas para registrar passagens do mouse em um site. Existe uma correção para isso também?*  
 **Definindo passagens do mouse implícitas para o navegador da Web**  
  
 Em muitos sites, quando você focaliza um determinado controle, ele expande para mostrar detalhes adicionais. Geralmente, eles parecem menus em aplicativos da área de trabalho. Como esse é um padrão comum, os testes de IU codificados permitem passagens do mouse implícitas na navegação na Web. Por exemplo, se você registrar passagens do mouse no Internet Explorer, será acionado um evento. Esses eventos podem acarretar o registro de passagens redundantes do mouse. Por isso, as passagens do mouse implícitas são registradas com `ContinueOnError` definido como `true` no arquivo de configuração de teste de interface do usuário. Isso permite que a reprodução continue em caso de falha em um evento de passagem do mouse.  
  
 Para permitir o registro de passagens do mouse implícitas em um navegador da Web, abra o arquivo de configuração:  
  
 `<drive letter:>\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\CodedUITestBuilder.exe.config`  
  
 Verifique se o arquivo de configuração está com a chave `RecordImplicitiHovers` definida com o valor `true`, como mostrado no exemplo a seguir:  
  
```  
<!--Use this to enable/disable recording of implicit hovers.-->  
<add key="RecordImplicitHover" value="true"/>  
  
```  
  
##  <a name="VerifyingCodeCUITModify"></a> Personalizando o teste de IU codificado  
 Depois de criar o teste de IU codificado, você poderá editá-lo usando qualquer uma destas ferramentas no Visual Studio:  
  
-   **Construtor de Teste de IU Codificado:** use o Construtor de Teste de IU Codificado para adicionar controles e validar testes. Consulte a seção [Adicionar controles e validar suas propriedades](#VerifyingCodeUsingCUITGenerateAssertions), neste tópico.  
  
-   **Editor de Teste de IU Codificado:** o Editor de Teste de IU Codificado permite modificar facilmente os testes de IU codificados. Com o Editor de testes de interface de usuário codificada, você pode localizar, exibir e editar os métodos de teste. Também é possível editar ações de interface do usuário e seus controles associados no mapa de controles de IU. Para obter mais informações, consulte [Editing Coded UI Tests Using the Coded UI Test Editor](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md) (Editando testes de IU codificada usando o Editor de teste de IU codificado).  
  
-   **Editor de Códigos:**  
  
    -   adicione manualmente códigos dos controles ao teste, como descrito na seção [Codificar ações e propriedades de controle de IU](#VerifyingCodeCUITActionsandProperties) deste tópico.  
  
    -   Depois de criar um teste de IU codificado, você poderá modificá-lo para ser controlado por dados. Para obter mais informações, consulte [Criar um Teste de IU Codificado Controlado por Dados](../test/creating-a-data-driven-coded-ui-test.md).  
  
    -   Na reprodução de um teste de IU codificado, é possível instruir o teste a aguardar a ocorrência de determinados eventos, como a exibição de uma janela, o desaparecimento da barra de progresso etc. Para isso, adicione o método UITestControl.WaitForControlXXX() apropriado. Para obter uma lista completa dos métodos disponíveis, consulte [Como fazer Testes de IU Codificados Aguardarem Eventos Específicos Durante a Reprodução](../test/making-coded-ui-tests-wait-for-specific-events-during-playback.md). Para obter um exemplo de um teste de IU codificado que aguarda um controle ser habilitado usando o método WaitForControlEnabled, consulte [Passo a Passo: Criar, Editar e Manter um Teste de IU Codificado](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md).  
  
    -   Os teste de IU codificados incluem suporte a alguns dos controles HTML5 incluídos no Internet Explorer 9 e no Internet Explorer 10. Para obter mais informações, consulte [Usar Controles HTML5 em Testes de IU Codificados](../test/using-html5-controls-in-coded-ui-tests.md).  
  
    -   **Diretrizes de codificação do teste de IU codificado:**  
  
        -   [Anatomia de um teste de IU codificado](../test/anatomy-of-a-coded-ui-test.md)  
  
        -   [Melhores práticas para testes de IU codificados](../test/best-practices-for-coded-ui-tests.md)  
  
        -   [Testando um aplicativo grande com vários mapas de interface do usuário](../test/testing-a-large-application-with-multiple-ui-maps.md)  
  
        -   [Configurações e plataformas com suporte para testes de IU codificados e gravações das ações](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)  
  
###  <a name="generatedCode"></a> O Código Gerado  
 Quando você escolhe **Gerar Código**, diversas partes do código são criadas:  
  
- **Uma linha no método de teste.**  
  
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
  
- **Um método em UIMap.uitest**  
  
   Esse método inclui os detalhes das ações registradas ou o valor verificado por você. Você pode editar esse código abrindo UIMap.uitest. Ele é aberto em um editor especializado, no qual é possível excluir ou refatorar as ações registradas.  
  
   Também é possível exibir o método gerado em UIMap.Designer.cs. Esse método realiza as ações registradas quando você executa o teste.  
  
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
  >  Você não deve editar esse arquivo, porque ele será registrado quando mais testes forem criados.  
  
   É possível criar versões adaptadas desses métodos copiando-os em UIMap.cs. Por exemplo, você poderia criar uma versão parametrizada que seria chamada a partir de um método de teste:  
  
  ```csharp  
  // File: UIMap.cs  
  public partial class UIMap // Same partial class  
  {  
    /// <summary>  
    /// Add two numbers – parameterized version  
    /// </summary>  
    public void AddTwoNumbers(int firstNumber, int secondNumber)  
    { ...   // Code modified to use parameters.  
    }  
  }  
  ```  
  
- **Declarações em UIMap.uitest**  
  
   Essas declarações representam os controles de interface de usuário do aplicativo usados pelo teste. Elas são usadas pelo código gerado para operar os controles e acessar suas propriedades.  
  
   Também será possível usá-las para gravar seu próprio código. Por exemplo, é possível fazer o método de teste escolher um hiperlink em um aplicativo Web, digitar um valor em uma caixa de texto ou ramificar e utilizar ações de testes diferentes com base no valor de um campo.  
  
   É possível adicionar vários testes de IU codificados e vários objetos e arquivos de mapa de IU para facilitar os testes de um aplicativo grande. Para obter mais informações, consulte [Testar um Aplicativo Grande com Vários Mapas de Interface do Usuário](../test/testing-a-large-application-with-multiple-ui-maps.md).  
  
  Para obter mais informações sobre o código gerado, consulte [Anatomia de um Teste de IU Codificado](../test/anatomy-of-a-coded-ui-test.md).  
  
###  <a name="actions"></a> Codificando ações e propriedades de controle de interface do usuário  
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
  
##### <a name="to-get-or-set-properties-from-ui-test-controls-directly"></a>Para obter ou definir propriedades de controles de teste de IU diretamente  
  
-   Com controles derivados de T:Microsoft.VisualStudio.TestTools.UITesting.UITestControl, como T:Microsoft.VisualStudio.TestTools.UITesting.HtmlControls.HtmlList ou T:Microsoft.VisualStudio.TestTools.UITesting.WinControls.WinComboBox, é possível obter ou definir os valores de propriedade diretamente da seguinte forma:  
  
    ```  
    int i = myHtmlList.ItemCount;  
    myWinCheckBox.Checked = true;  
    ```  
  
##### <a name="to-get-properties-from-ui-test-controls"></a>Para obter propriedades de controles de teste de IU  
  
-   Para obter um valor de propriedade de um controle, use <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A>.  
  
-   Para especificar a propriedade de controle a ser obtida, use a cadeia de caracteres apropriada da classe `PropertyNames` em cada controle como parâmetro para <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A>.  
  
-   <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.GetProperty%2A> retorna o tipo de dados apropriado, mas esse valor retornado é convertido como um <xref:System.Object>. Em seguida, o <xref:System.Object> de retorno deve ser convertido como tipo apropriado.  
  
     Exemplo:  
  
     `int i = (int)GetProperty(myHtmlList.PropertyNames.ItemCount);`  
  
##### <a name="to-set-properties-for-ui-test-controls"></a>Para definir propriedades para controles de teste de IU  
  
-   Para obter uma propriedade em um controle, use <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A>.  
  
-   Para especificar a propriedade do controle a ser definida, use a cadeia de caracteres apropriada da classe `PropertyNames` como primeiro parâmetro para <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.SetProperty%2A>, com o valor da propriedade como segundo parâmetro.  
  
     Exemplo:  
  
     `SetProperty(myWinCheckBox.PropertyNames.Checked, true);`  
  
###  <a name="debugging"></a> Depuração  
 Você pode analisar testes de IU codificados usando logs de teste de IU codificado. Os logs de teste de IU codificado filtram e registram informações importantes sobre as execuções de teste de IU codificado. O formato dos logs permite depurar rapidamente os problemas. Para obter mais informações, consulte [Analisando Testes de IU Codificado usando o Logs de Teste de IU Codificado](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md).  
  
##  <a name="VerifyCodeUsingCUITWhatsNext"></a> O que vem a seguir?  
 **Opções adicionais para executar testes de IU codificados:** é possível executar testes de IU codificados diretamente no Visual Studio, como descrito anteriormente neste tópico. Além disso, é possível executar testes de IU automatizados em [!INCLUDE[TCMext](../includes/tcmext-md.md)] ou [!INCLUDE[esprbuild](../includes/esprbuild-md.md)]. Quando são automatizados, os testes de IU codificados precisam interagir com a área de trabalho quando executados, diferentemente de outros testes automatizados.  
  
- [Como executar testes no Microsoft Visual Studio](http://msdn.microsoft.com/library/1a1207a9-2a33-4a1e-a1e3-ddf0181b1046)  
  
- [Executar Testes Automatizados no Microsoft Test Manager](http://msdn.microsoft.com/en-us/0632f265-63fe-4859-a413-9bb934c66835)  
  
- [Como Configurar e Executar Testes Programados Após o build do Aplicativo](http://msdn.microsoft.com/en-us/32acfeb1-b1aa-4afb-8cfe-cc209e6183fd)  
  
- [Executar Testes no Processo de build](http://msdn.microsoft.com/library/d05743a1-c5cf-447e-bed9-bed3cb595e38)  
  
- [Executando testes automatizados da linha de comando](http://msdn.microsoft.com/library/f18179c6-b688-4e41-9898-8aca130c4fc3)  
  
- [Como configurar o Test Agent para executar testes que interajam com a área de trabalho](~/E:/Repos/visualstudio-docs-pr/docs/test/how-to-set-up-your-test-agent-to-run-tests-that-interact-with-the-desktop.md)  
  
- [&#91;retired&#93; Usando Testes de IU Codificados em Testes de Carga](http://msdn.microsoft.com/library/704339ff-7da7-4d5f-acb3-c3b23f4acb43)  
  
  **Adicionar suporte para controles personalizados:** a estrutura de teste de IU codificado não oferece suporte para todas as interfaces do usuário possíveis e pode não oferecer suporte à interface do usuário que você deseja testar. Por exemplo, você não pode criar imediatamente um teste de IU codificado para a IU do [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)]. Porém, você pode criar uma extensão para o framework de teste de IU codificado que oferecerá suporte a um controle personalizado.  
  
- [Habilitar testes de IU codificados dos controles](../test/enable-coded-ui-testing-of-your-controls.md)  
  
- [Estendendo testes de IU codificados e gravações da ação para dar suporte ao Microsoft Excel](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)  
  
  Os testes de IU codificados costumam ser usados para automatizar testes manuais. Para obter diretrizes adicionais, consulte [Teste para Entrega Contínua com o Visual Studio 2012 – Capítulo 5: Automatizando os Testes de Sistema](http://go.microsoft.com/fwlink/?LinkID=255196). Para obter mais informações sobre testes manuais, consulte [&#91;retired&#93; Criar Casos de Testes Manuais por meio do Microsoft Test Manager](http://msdn.microsoft.com/library/9989e184-c8e4-444b-998d-a1a5ec94461e). Para obter mais informações sobre testes de sistemas automatizados, consulte [Criar Testes Automatizados por meio do Microsoft Test Manager](http://msdn.microsoft.com/en-us/7b5075ee-ddfe-411d-b1d4-94283550a5d0).  
  
## <a name="external-resources"></a>Recursos externos  
  
### <a name="guidance"></a>Diretrizes  
 [Testes de Entrega Contínua com o Visual Studio 2012 – Capítulo 2: Teste de Unidade: Testando o Interior](http://go.microsoft.com/fwlink/?LinkID=255188)  
  
 [Teste de Entrega Contínua com o Visual Studio 2012 – Capítulo 5: Automatizar Testes do Sistema](http://go.microsoft.com/fwlink/?LinkID=255196)  
  
### <a name="faq"></a>Perguntas Frequentes  
 [Perguntas frequentes sobre testes de IU codificados – 1](http://go.microsoft.com/fwlink/?LinkID=230576)  
  
 [Perguntas frequentes sobre testes de IU codificados – 2](http://go.microsoft.com/fwlink/?LinkID=230578)  
  
### <a name="forum"></a>Fórum  
 [Teste de Automação de interface do usuário do Visual Studio (inclui CodedUI)](http://go.microsoft.com/fwlink/?LinkID=224497)  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap>   
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert>   
 [Melhorar a Qualidade do Código](http://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)   
 [Instruções passo a passo: Criando, editando e mantendo um teste de IU codificado](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)   
 [Anatomia de um teste de IU codificado](../test/anatomy-of-a-coded-ui-test.md)   
 [Práticas recomendadas para testes de IU codificados](../test/best-practices-for-coded-ui-tests.md)   
 [Testando um aplicativo grande com vários mapas de interface do usuário](../test/testing-a-large-application-with-multiple-ui-maps.md)   
 [Editando testes de IU codificados usando o Editor de teste de IU codificados](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)   
 [Configurações e plataformas com suporte para testes de IU codificados e gravações das ações](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)   
 [Atualizando testes de IU codificados por meio do Visual Studio 2010](../test/upgrading-coded-ui-tests-from-visual-studio-2010.md)   
 [Gerenciando um Teste de IU Codificado de uma gravação da ação existente](http://msdn.microsoft.com/library/56736963-9027-493b-b5c4-2d4e86d1d497)



