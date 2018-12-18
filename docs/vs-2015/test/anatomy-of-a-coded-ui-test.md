---
title: Anatomia de um teste de IU codificado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- coded UI tests
ms.assetid: 9c5d82fc-3fb7-4bb1-a9ac-ac1fa3a4b500
caps.latest.revision: 25
ms.author: gewarren
manager: douge
ms.openlocfilehash: 7595a967a6dae091da6c5a7613a27c602cc1381e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49202742"
---
# <a name="anatomy-of-a-coded-ui-test"></a>Anatomia de um teste de IU codificado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você cria um teste de IU codificado em um projeto de teste de IU codificado, vários arquivos são adicionados a sua solução. Neste tópico, usaremos um exemplo de teste de IU codificado para explorar esses arquivos.  
  
 **Requisitos**  
  
-   Visual Studio Enterprise  
  
## <a name="contents-of-a-coded-ui-test"></a>Conteúdo do teste de IU codificado  
 Quando você cria um teste de IU codificado, o **Construtor de Teste de IU Codificado** cria um mapa da interface do usuário em teste e também dos métodos de teste, parâmetros e asserções para todos os testes. Ele também cria um arquivo de classe para cada teste.  
  
|Arquivo|Conteúdo|Editável?|  
|----------|--------------|---------------|  
|[UIMap.Designer.cs](#UIMapDesignerFile)|[Seção Declarações](#UIMapDesignerFile)<br /><br /> [Classe UIMap](#UIMapClass) (parcial, gerada automaticamente)<br /><br /> [Métodos](#UIMapMethods)<br /><br /> [Propriedades](#UIMapProperties)|Não|  
|[UIMap.cs](#UIMapCS)|[Classe UIMap](#UIMapCS) (parcial)|Sim|  
|[CodedUITest1.cs](#CodedUITestCS)|[Classe CodedUITest1](#CodedUITestCS)<br /><br /> [Métodos](#CodedUITestMethods)<br /><br /> [Propriedades](#CodedUITestProperties)|Sim|  
|[UIMap.uitest](#UIMapuitest)|O mapa XML da interface do usuário para o teste.|Não|  
  
###  <a name="UIMapDesignerFile"></a> UIMap.Designer.cs  
 Esse arquivo contém o código que é criado automaticamente com o **Construtor de Teste de IU Codificado** quando um teste é criado. Esse arquivo é recriado cada vez que um teste for alterado para que ele não seja um arquivo no qual você pode adicionar ou modificar o código.  
  
#### <a name="declarations-section"></a>Seção Declarações  
 Esta seção inclui as seguintes declarações para uma interface do usuário do Windows.  
  
```csharp  
using System;  
using System.CodeDom.Compiler;  
using System.Collections.Generic;  
using System.Drawing;  
using System.Text.RegularExpressions;  
using System.Windows.Input;  
using Microsoft.VisualStudio.TestTools.UITest.Extension;  
using Microsoft.VisualStudio.TestTools.UITesting;  
using Microsoft.VisualStudio.TestTools.UITesting.WinControls;  
using Microsoft.VisualStudio.TestTools.UnitTesting;  
using Keyboard = Microsoft.VisualStudio.TestTools.UITesting.Keyboard;  
using Mouse = Microsoft.VisualStudio.TestTools.UITesting.Mouse;  
using MouseButtons = System.Windows.Forms.MouseButtons;  
```  
  
 O namespace <xref:Microsoft.VisualStudio.TestTools.UITesting.WinControls> é incluído para uma interface do usuário do Windows. Para uma interface do usuário de página da Web, o namespace seria <xref:Microsoft.VisualStudio.TestTools.UITesting.HtmlControls>; para uma interface do usuário do Windows Presentation Foundation, o namespace seria <xref:Microsoft.VisualStudio.TestTools.UITesting.WpfControls>.  
  
####  <a name="UIMapClass"></a> Classe UIMap  
 A próxima seção do arquivo é a classe <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap>.  
  
```  
[GeneratedCode("Coded UITest Builder", "10.0.21221.0")]  
public partial class UIMap  
```  
  
 O código de classe é iniciado com um <xref:System.CodeDom.Compiler.GeneratedCodeAttribute> que é aplicado à classe, que é declarada como uma classe parcial. Você observará que o atributo também é aplicado a todas as classes nesse arquivo. O outro arquivo que pode conter mais códigos para essa classe é `UIMap.cs`, que será discutido mais tarde.  
  
 A classe `UIMap` gerada inclui o código para cada método que foi especificado quando o teste foi gravado.  
  
```  
public void LaunchCalculator()  
public void AddItems()  
public void VerifyTotal()  
public void CleanUp()  
```  
  
 Esta parte da classe <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap> também inclui o código gerado para cada propriedade que é exigido pelos métodos.  
  
```  
public virtual LaunchCalculatorParams LaunchCalculatorParams  
public virtual AddItemsParams AddItemsParams  
public virtual VerifyTotalExpectedValues VerifyTotalExpectedValues  
public virtual CalculateItemsParams CalculateItemsParams  
public virtual VerifyMathAppTotalExpectedValues   
    VerifyMathAppTotalExpectedValues  
public UIStartMenuWindow UIStartMenuWindow  
public UIRunWindow UIRunWindow  
public UICalculatorWindow UICalculatorWindow  
public UIStartWindow UIStartWindow  
public UIMathApplicationWindow UIMathApplicationWindow  
```  
  
#####  <a name="UIMapMethods"></a> Métodos UIMap  
 Cada método tem uma estrutura semelhante ao método `AddItems()`. Isso é explicado com mais detalhes no código, que é apresentado com quebras de linha para dar maior clareza.  
  
```  
/// <summary>  
/// AddItems - Use 'AddItemsParams' to pass parameters into this method.  
/// </summary>  
public void AddItems()  
{  
    #region Variable Declarations  
    WinControl uICalculatorDialog =   
        this.UICalculatorWindow.UICalculatorDialog;  
    WinEdit uIItemEdit =   
        this.UICalculatorWindow.UIItemWindow.UIItemEdit;  
    #endregion  
  
    // Type '{NumPad7}' in 'Calculator' Dialog  
    Keyboard.SendKeys(uICalculatorDialog,   
        this.AddItemsParams.UICalculatorDialogSendKeys,   
        ModifierKeys.None);  
  
    // Type '{Add}{NumPad2}{Enter}' in 'Unknown Name' text box  
    Keyboard.SendKeys(uIItemEdit,   
        this.AddItemsParams.UIItemEditSendKeys,   
        ModifierKeys.None);  
}  
```  
  
 O comentário de resumo para cada definição do método informa qual classe usar para valores de parâmetro para o método. Nesse caso, é a classe `AddItemsParams`, que é definida posteriormente no arquivo `UIMap.cs` e que também é o tipo de valor que é retornado pela propriedade `AddItemsParams`.  
  
 Na parte superior do método de código está uma região `Variable Declarations` que define as variáveis locais para os objetos da interface do usuário que será usada pelo método.  
  
 Nesse método, `UIItemWindow` e `UIItemEdit` são propriedades que são acessadas por meio da classe `UICalculatorWindow`, que é definida posteriormente no arquivo `UIMap.cs`.  
  
 Em seguida estão as linhas que enviam texto do teclado para o aplicativo Calculadora usando propriedades do objeto `AddItemsParams`.  
  
 O método `VerifyTotal()` tem uma estrutura muito semelhante e inclui o seguinte código de declaração.  
  
```  
// Verify that 'Unknown Name' text box's property 'Text' equals '9. '  
Assert.AreEqual(  
    this.VerifyTotalExpectedValues.UIItemEditText,   
    uIItemEdit.Text);  
```  
  
 O nome da caixa de texto é listado como desconhecido porque o desenvolvedor do aplicativo Calculadora do Windows não forneceu um nome publicamente disponível para o controle. O método <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A?displayProperty=fullName> falha quando o valor real não é igual ao valor esperado, o que faz com que o teste falhe. Observe também que o valor esperado inclui um ponto decimal seguido por um espaço. Se você alguma vez precisar modificar a funcionalidade desse teste específico, será necessário permitir esse ponto decimal e o espaço.  
  
#####  <a name="UIMapProperties"></a> Propriedades UIMap  
 O código para cada propriedade também é muito padrão na classe. O código a seguir para a propriedade `AddItemsParams` é usado no método `AddItems()`.  
  
```  
public virtual AddItemsParams AddItemsParams  
{  
    get  
    {  
        if ((this.mAddItemsParams == null))  
        {  
            this.mAddItemsParams = new AddItemsParams();  
        }  
        return this.mAddItemsParams;  
    }  
}  
```  
  
 Observe que a propriedade usa uma variável local privada denominada `mAddItemsParams` para armazenar o valor antes de retornar a ele. O nome da propriedade e o nome de classe do objeto que ela retorna são os mesmos. A classe é definida posteriormente no arquivo `UIMap.cs`.  
  
 Cada classe retornada por uma propriedade é estruturada de maneira semelhante. A seguir está a classe `AddItemsParams`.  
  
```  
/// <summary>  
/// Parameters to be passed into 'AddItems'  
/// </summary>  
[GeneratedCode("Coded UITest Builder", "10.0.21221.0")]  
public class AddItemsParams  
{  
    #region Fields  
    /// <summary>  
    /// Type '{NumPad7}' in 'Calculator' Dialog  
    /// </summary>  
    public string UICalculatorDialogSendKeys = "{NumPad7}";  
  
    /// <summary>  
    /// Type '{Add}{NumPad2}{Enter}' in 'Unknown Name' text box  
    /// </summary>  
    public string UIItemEditSendKeys = "{Add}{NumPad2}{Enter}";  
    #endregion  
}  
```  
  
 Assim como acontece com todas as classes no arquivo `UIMap.cs`, essa classe é iniciada com <xref:System.CodeDom.Compiler.GeneratedCodeAttribute>. Nessa pequena classe há uma região `Fields` que define as cadeias de caracteres a serem usadas como parâmetros para o método <xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard.SendKeys%2A?displayProperty=fullName> que é usado no método `UIMap.AddItems()` que foi discutido anteriormente. Você pode escrever o código para substituir os valores nesses campos de cadeia de caracteres antes de o método no qual esses parâmetros são usados ser chamado.  
  
###  <a name="UIMapCS"></a> UIMap.cs  
 Por padrão, esse arquivo contém uma classe `UIMap` parcial que não tem métodos ou propriedades.  
  
#### <a name="uimap-class"></a>Classe UIMap  
 É nesta classe que você pode criar código personalizado para estender a funcionalidade da classe <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap>. O código que você cria neste arquivo não será regenerado pelo **Construtor de Teste de IU Codificado** toda vez que um teste for modificado.  
  
 Todas as partes do <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap> podem usar os métodos e as propriedades de qualquer outra parte da classe <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap>.  
  
###  <a name="CodedUITestCS"></a> CodedUITest1.cs  
 Esse arquivo é gerado pelo **Construtor de Teste de IU Codificado**, mas não será recriado sempre que o teste for modificado, de modo que você pode modificar o código nesse arquivo. O nome do arquivo é gerado do nome que você especificou para o teste quando você o criou.  
  
#### <a name="codeduitest1-class"></a>Classe CodedUITest1  
 Por padrão, esse arquivo contém a definição para apenas uma classe.  
  
```  
[CodedUITest]  
public class CodedUITest1  
```  
  
 O T:Microsoft.VisualStudio.TestTools.UITesting.CodedUITestAttribute é aplicado automaticamente à classe, o que permite que a estrutura de teste o reconheça como uma extensão de teste. Observe também que não se trata de uma classe parcial. Todo o código de classe está contido nesse arquivo.  
  
#####  <a name="CodedUITestProperties"></a> Propriedades CodedUITest1  
 A classe contém duas propriedades padrão que estão localizadas na parte inferior do arquivo. Elas não devem ser modificadas.  
  
```  
/// <summary>  
/// Gets or sets the test context which provides  
/// information about and functionality for the current test run.  
///</summary>  
public TestContext TestContext  
public UIMap UIMap  
```  
  
#####  <a name="CodedUITestMethods"></a> Métodos CodedUITest1  
 Por padrão, a classe contém apenas um método.  
  
```  
public void CodedUITestMethod1()  
```  
  
 Esse método chama cada método `UIMap` especificado quando você registrou o seu teste, que é descrito na seção na [Classe UIMap](#UIMapClass).  
  
 Uma região que é intitulada `Additional test attributes`, se as marcas de comentário forem removidas, contém dois métodos opcionais.  
  
```  
// Use TestInitialize to run code before running each test   
[TestInitialize()]  
public void MyTestInitialize()  
{  
    // To generate code for this test, select "Generate Code for Coded   
    // UI Test" from the shortcut menu and select one of the menu items.  
    // For more information on generated code, see   
    // http://go.microsoft.com/fwlink/?LinkId=179463  
  
    // You could move this line from the CodedUITestMethod1() method  
    this.UIMap.LaunchCalculator();  
}  
  
// Use TestCleanup to run code after each test has run  
[TestCleanup()]  
public void MyTestCleanup()  
{  
    // To generate code for this test, select "Generate Code for Coded   
    // UI Test" from the shortcut menu and select one of the menu items.  
    // For more information on generated code, see   
    // http://go.microsoft.com/fwlink/?LinkId=179463  
  
    // You could move this line from the CodedUITestMethod1() method  
    this.UIMap.CloseCalculator();  
}  
```  
  
 O método `MyTestInitialize()` tem o <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestInitializeAttribute> aplicado a ele, que solicita que a estrutura de teste chame esse método antes de quaisquer outros métodos de teste. Da mesma forma, o método `MyTestCleanup()` tem o <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestCleanupAttribute> aplicado a ele, que solicita que a estrutura de teste chame esse método depois que todos os outros métodos de teste forem chamados. O uso desses métodos é opcional. Para este teste, o método `UIMap.LaunchCalculator()` poderia ser chamado de `MyTestInitialize()` e o método `UIMap.CloseCalculator()` poderia ser chamado de `MyTestCleanup()` em vez do `CodedUITest1Method1()`.  
  
 Se você adicionar mais métodos a essa classe usando o <xref:Microsoft.VisualStudio.TestTools.UITesting.CodedUITestAttribute>, a estrutura de teste chamará cada método como parte do teste.  
  
###  <a name="UIMapuitest"></a> UIMap.uitest  
 Este é um arquivo XML que representa a estrutura do registro do teste de IU codificado e todas as suas partes. Isso inclui as ações e as classes além dos métodos e das propriedades dessas classes. O arquivo [UIMap.Designer.cs](#UIMapDesignerFile) contém o código que é gerado pelo Construtor de IU Codificado para reproduzir a estrutura do teste e fornecer a conexão à estrutura de teste.  
  
 O arquivo `UIMap.uitest` não é editável diretamente. No entanto, você pode usar o Construtor de IU Codificado para modificar o teste, que modifica automaticamente o arquivo `UIMap.uitest` e o arquivo [UIMap.Designer.cs](#UIMapDesignerFile).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap>   
 <xref:Microsoft.VisualStudio.TestTools.UITesting.WinControls>   
 <xref:Microsoft.VisualStudio.TestTools.UITesting.HtmlControls>   
 <xref:Microsoft.VisualStudio.TestTools.UITesting.WpfControls>   
 <xref:System.CodeDom.Compiler.GeneratedCodeAttribute>   
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A?displayProperty=fullName>   
 <xref:Microsoft.VisualStudio.TestTools.UITesting.Keyboard.SendKeys%2A?displayProperty=fullName>   
 <xref:Microsoft.VisualStudio.TestTools.UITesting.CodedUITestAttribute>   
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestInitializeAttribute>   
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestCleanupAttribute>   
 [Usar a automação de interface do usuário para testar o código](../test/use-ui-automation-to-test-your-code.md)   
 [Criando testes de IU codificados](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate)   
 [Práticas recomendadas para testes de IU codificados](../test/best-practices-for-coded-ui-tests.md)   
 [Testando um aplicativo grande com vários mapas de interface do usuário](../test/testing-a-large-application-with-multiple-ui-maps.md)   
 [Configurações e plataformas com suporte para testes de IU codificados e gravações das ações](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)



