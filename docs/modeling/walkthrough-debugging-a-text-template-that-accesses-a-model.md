---
title: 'Instruções passo a passo: depurando um modelo (template) de texto que acessa um modelo'
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e33297bba899c1843b8601c031d7669531a1bd3f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546894"
---
# <a name="walkthrough-debugging-a-text-template-that-accesses-a-model"></a>Instruções passo a passo: depurando um modelo (template) de texto que acessa um modelo
Quando você modifica ou adiciona modelos de texto em uma solução de linguagem específica de domínio, você pode receber erros quando o mecanismo transforma o modelo no código-fonte ou quando compila o código gerado. A instrução a seguir demonstra algumas das coisas que você pode fazer para depurar um modelo de texto.

> [!NOTE]
> Para obter mais informações sobre modelos de texto em geral, consulte [geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md). Para obter mais informações sobre como depurar modelos de texto, consulte [Walkthrough: Depurando um modelo de texto](debugging-a-t4-text-template.md).

## <a name="creating-a-domain-specific-language-solution"></a>Criando uma solução de linguagem específica de domínio
 Neste procedimento, você cria uma solução de linguagem específica de domínio que tem as seguintes características:

- Nome: DebuggingTestLanguage

- Modelo de solução: linguagem mínima

- Extensão de arquivo:. DDD

- Nome da empresa: fabrikam

  Para obter mais informações sobre como criar uma solução de linguagem específica de domínio, consulte [como criar uma solução de linguagem específica de domínio](../modeling/how-to-create-a-domain-specific-language-solution.md).

## <a name="creating-a-text-template"></a>Criando um modelo de texto
 Adicione um modelo de texto à sua solução.

#### <a name="to-create-a-text-template"></a>Para criar um modelo de texto

1. Compile a solução e comece a executá-la no depurador. (No menu **Compilar** , clique em **Recompilar solução**e, em seguida, no menu **depurar** , clique em **Iniciar Depuração**.) Uma nova instância do Visual Studio abre o projeto de depuração.

2. Adicione um arquivo de texto chamado `DebugTest.tt` ao projeto de depuração.

3. Verifique se a propriedade da **ferramenta personalizada** de DebugTest.tt está definida como `TextTemplatingFileGenerator` .

## <a name="debugging-directives-that-access-a-model-from-a-text-template"></a>Diretivas de depuração que acessam um modelo de um modelo de texto
 Antes de poder acessar um modelo a partir das instruções e expressões em um modelo de texto, você deve primeiro chamar um processador de diretivas gerado. Chamar o processador de diretiva gerado torna as classes em seu modelo disponíveis para o código de modelo de texto como propriedades. Para obter mais informações, consulte [acessando modelos de modelos de texto](../modeling/accessing-models-from-text-templates.md).

 Nos procedimentos a seguir, você irá depurar um nome de diretiva incorreto e um nome de propriedade incorreto.

#### <a name="to-debug-an-incorrect-directive-name"></a>Para depurar um nome de diretiva incorreto

1. Substitua o código em DebugTest.tt pelo seguinte código:

    > [!NOTE]
    > O código contém um erro. Você está apresentando o erro para depurá-lo.

    ```csharp
    <#@ template language="C#" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ modelRoot processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>

    Model: <#= this.ExampleModel #>
    <#
    foreach (ExampleElement element in this.ExampleModel.Elements)
    {
    #>
        Element: <#= element.Name #>
    <#
    }
    #>
    ```

    ```vb
    <#@ template language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ modelRoot processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>

    Model: <#= Me.ExampleModel #>
    <#
    For Each element as ExampleElement in Me.ExampleModel.Elements
    #>
        Element: <#= element.Name #>
    <#
    Next
    #>
    ```

2. No **Gerenciador de soluções**, clique com o botão direito do mouse em DebugTest.tt e clique em **executar ferramenta personalizada**.

     A janela **lista de erros** exibe este erro:

     **O processador chamado ' DebuggingTestLanguageDirectiveProcessor ' não oferece suporte à diretiva chamada ' modelRoot '. A transformação não será executada.**

     Nesse caso, a chamada de diretiva contém um nome de diretiva incorreto. Você especificou `modelRoot` como o nome da diretiva, mas o nome de diretiva correto é `DebuggingTestLanguage` .

3. Clique duas vezes no erro na janela **lista de erros** para saltar para o código.

4. Para corrigir o código, altere o nome da diretiva para `DebuggingTestLanguage` .

     A alteração é realçada.

    ```csharp
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>
    ```

    ```vb
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>
    ```

5. No **Gerenciador de soluções**, clique com o botão direito do mouse em DebugTest.tt e clique em **executar ferramenta personalizada**.

     Agora o sistema transforma o modelo de texto e gera o arquivo de saída correspondente. Você não verá nenhum erro na janela de **lista de erros** .

#### <a name="to-debug-an-incorrect-property-name"></a>Para depurar um nome de propriedade incorreto

1. Substitua o código em DebugTest.tt pelo seguinte código:

    > [!NOTE]
    > O código contém um erro. Você está apresentando o erro para depurá-lo.

    ```csharp
    <#@ template language="C#" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= this.ExampleModel #>
    <#
    foreach (ExampleElement element in this.ExampleModel.Elements)
    {
    #>
        Element: <#= element.Name #>
    <#
    }
    #>
    ```

    ```vb
    <#@ template language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= Me.ExampleModel #>
    <#
    For Each element as ExampleElement in Me.ExampleModel.Elements
    #>
        Element: <#= element.Name #>
    <#
    Next
    #>
    ```

2. No **Gerenciador de soluções**, clique com o botão direito do mouse em DebugTest.tt e clique em **executar ferramenta personalizada**.

     A janela **lista de erros** é exibida e exibe um destes erros:

     (C#)

     **Compilando transformação: Microsoft. VisualStudio. TextTemplating \<GUID> . GeneratedTextTransformation ' não contém uma definição para ' ExampleModel '**

     (Visual Basic)

     **Compilando transformação: ' ExampleModel ' não é um membro de ' Microsoft. VisualStudio. TextTemplating \<GUID> . GeneratedTextTransformation'.**

     Nesse caso, o código do modelo de texto contém um nome de propriedade incorreto. Você especificou `ExampleModel` como o nome da propriedade, mas o nome correto da propriedade é `LibraryModel` . Você pode encontrar o nome de propriedade correto no parâmetro de forneceções, conforme mostrado no código a seguir:

    ```
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>
    ```

3. Clique duas vezes no erro na janela Lista de Erros para saltar para o código.

4. Para corrigir o código, altere o nome da propriedade para `LibraryModel` no código do modelo de texto.

     As alterações são realçadas.

    ```csharp
    <#@ template language="C#" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= this.LibraryModel #>
    <#
    foreach (ExampleElement element in this.LibraryModel.Elements)
    {
    #>
        Element: <#= element.Name #>
    <#
    }
    #>
    ```

    ```vb
    <#@ template language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= Me.LibraryModel #>
    <#
    For Each element as ExampleElement in Me.LibraryModel.Elements
    #>
        Element: <#= element.Name #>
    <#
    Next
    #>
    ```

5. No **Gerenciador de soluções**, clique com o botão direito do mouse em DebugTest.tt e clique em **executar ferramenta personalizada**.

     Agora o sistema transforma o modelo de texto e gera o arquivo de saída correspondente. Você não verá nenhum erro na janela de **lista de erros** .
