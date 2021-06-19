---
title: 'Passo a passo: depurar modelos de texto que acessam um modelo'
description: Fornece informações sobre como depurar um modelo de texto que acessa um modelo.
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: d39b1ac72210145cc1efa1c513b7f3b76d8c2e36
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388224"
---
# <a name="walkthrough-debugging-a-text-template-that-accesses-a-model"></a>Instruções passo a passo: depurando um modelo (template) de texto que acessa um modelo
Ao modificar ou adicionar modelos de texto em uma solução de linguagem específica ao domínio, você poderá receber erros quando o mecanismo transformar o modelo em código-fonte ou quando compilar o código gerado. O passo a passo a seguir demonstra algumas das coisas que você pode fazer para depurar um modelo de texto.

> [!NOTE]
> Para obter mais informações sobre modelos de texto em geral, consulte [Geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md). Para obter mais informações sobre como depurar modelos de texto, consulte [Passo a passo: depurando um modelo de texto.](debugging-a-t4-text-template.md)

## <a name="creating-a-domain-specific-language-solution"></a>Criando uma solução Domain-Specific linguagem
 Neste procedimento, você cria uma solução de linguagem específica ao domínio que tem as seguintes características:

- Nome: DepuraçãoTestLanguage

- Modelo de solução: linguagem mínima

- Extensão de arquivo: .ddd

- Nome da empresa: Fabrikam

  Para obter mais informações sobre como criar uma solução de linguagem específica do domínio, consulte [Como criar uma solução Domain-Specific linguagem .](../modeling/how-to-create-a-domain-specific-language-solution.md)

## <a name="creating-a-text-template"></a>Criando um modelo de texto
 Adicione um modelo de texto à sua solução.

#### <a name="to-create-a-text-template"></a>Para criar um modelo de texto

1. Crie a solução e comece a executa-la no depurador. (No menu **Build,** clique em **Recomperar** Solução e, em seguida, no menu **Depurar,** clique **em Iniciar Depuração**.) Uma nova instância do Visual Studio abre o projeto Depuração.

2. Adicione um arquivo de texto `DebugTest.tt` chamado ao projeto de Depuração.

3. Certifique-se de **que a propriedade Ferramenta** Personalizada DebugTest.tt está definida como `TextTemplatingFileGenerator` .

## <a name="debugging-directives-that-access-a-model-from-a-text-template"></a>Diretivas de depuração que acessam um modelo de um modelo de texto
 Antes de poder acessar um modelo das instruções e expressões em um modelo de texto, primeiro você deve chamar um processador de diretiva gerado. Chamar o processador de diretiva gerado disponibiliza as classes em seu modelo para o código do modelo de texto como propriedades. Para obter mais informações, [consulte Acessando modelos de modelos de texto](../modeling/accessing-models-from-text-templates.md).

 Nos procedimentos a seguir, você depurará um nome de diretiva incorreto e um nome de propriedade incorreto.

#### <a name="to-debug-an-incorrect-directive-name"></a>Para depurar um nome de diretiva incorreto

1. Substitua o código no DebugTest.tt pelo seguinte código:

    > [!NOTE]
    > O código contém um erro. Você está introduzindo o erro para depurá-lo.

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

2. No **Gerenciador de Soluções**, clique com o botão direito do DebugTest.tt e clique **em Executar Ferramenta Personalizada**.

     A **janela Lista** de Erros exibe este erro:

     **O processador chamado 'DebuggingTestLanguageDirectiveProcessor' não dá suporte à diretiva chamada 'modelRoot'. A transformação não será executado.**

     Nesse caso, a chamada de diretiva contém um nome de diretiva incorreto. Você especificou como `modelRoot` o nome da diretiva, mas o nome correto da diretiva é `DebuggingTestLanguage` .

3. Clique duas vezes no erro na janela **Lista de** Erros para ir para o código.

4. Para corrigir o código, altere o nome da diretiva para `DebuggingTestLanguage` .

     A alteração é realçada.

    ```csharp
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>
    ```

    ```vb
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>
    ```

5. No **Gerenciador de Soluções**, clique com o botão direito do DebugTest.tt e clique **em Executar Ferramenta Personalizada**.

     Agora, o sistema transforma o modelo de texto e gera o arquivo de saída correspondente. Você não verá nenhum erro na janela **Lista de** Erros.

#### <a name="to-debug-an-incorrect-property-name"></a>Para depurar um nome de propriedade incorreto

1. Substitua o código no DebugTest.tt pelo seguinte código:

    > [!NOTE]
    > O código contém um erro. Você está introduzindo o erro para depurá-lo.

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

2. No **Gerenciador de Soluções**, clique com o botão direito do DebugTest.tt e clique **em Executar Ferramenta Personalizada**.

     A **janela Lista** de Erros é exibida e exibe um destes erros:

     (C#)

     **Transformação de compilação: Microsoft.VisualStudio.TextTemplating. \<GUID> GeneratedTextTransformation' não contém uma definição para 'ExampleModel'**

     (Visual Basic)

     **Transformação de compilação: 'ExampleModel' não é membro de 'Microsoft.VisualStudio.TextTemplating. \<GUID> GeneratedTextTransformation'.**

     Nesse caso, o código do modelo de texto contém um nome de propriedade incorreto. Você especificou como `ExampleModel` o nome da propriedade, mas o nome correto da propriedade é `LibraryModel` . Você pode encontrar o nome correto da propriedade no parâmetro provides, conforme mostrado no código a seguir:

    ```
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>
    ```

3. Clique duas vezes no erro na janela Lista de Erros para ir para o código.

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

5. No **Gerenciador de Soluções**, clique com o botão direito do DebugTest.tt e clique **em Executar Ferramenta Personalizada**.

     Agora, o sistema transforma o modelo de texto e gera o arquivo de saída correspondente. Você não verá nenhum erro na janela **Lista de** Erros.
