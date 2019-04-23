---
title: 'Passo a passo: Depurando um modelo de texto que acessa um modelo | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: af46a7fe-6b98-4d3d-b816-0bbf8e81e220
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: eb5a9e6806c76cbb072090c35444d936ce50bb79
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60087112"
---
# <a name="walkthrough-debugging-a-text-template-that-accesses-a-model"></a>Passo a passo: Depurando um modelo de texto que acessa um modelo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você modificar ou adicionar modelos de texto em uma solução de linguagem específica de domínio, você pode receber erros quando o mecanismo transforma o modelo de código-fonte ou quando ele compila o código gerado. A instrução a seguir demonstra algumas das coisas que você pode fazer para depurar um modelo de texto.  
  
> [!NOTE]
>  Para obter mais informações sobre o texto modelos em geral, consulte [geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md). Para obter mais informações sobre a depuração de modelos de texto, consulte [passo a passo: Depurando um modelo de texto](http://msdn.microsoft.com/library/5c3fd3b7-c110-4e86-a22f-d5756be6b94f).  
  
## <a name="creating-a-domain-specific-language-solution"></a>Criando uma solução de linguagem específica do domínio  
 Neste procedimento, você deve criar uma solução de linguagem específica de domínio que tem as seguintes características:  
  
- Nome: DebuggingTestLanguage  
  
- Modelo de solução: Linguagem mínima  
  
- Extensão de arquivo: .ddd  
  
- Nome da empresa: Fabrikam  
  
  Para obter mais informações sobre como criar uma solução de linguagem específica de domínio, consulte [como: criar uma solução de linguagem específica de domínio](../modeling/how-to-create-a-domain-specific-language-solution.md).  
  
## <a name="creating-a-text-template"></a>Criando um modelo de texto  
 Adicione um modelo de texto à sua solução.  
  
#### <a name="to-create-a-text-template"></a>Para criar um modelo de texto  
  
1. Compile a solução e iniciar a execução no depurador. (Na **construir** menu, clique em **recompilar solução**e, em seguida, no **depurar** menu, clique em **iniciar depuração**.) Uma nova instância do Visual Studio abre o projeto de depuração.  
  
2. Adicione um arquivo de texto chamado `DebugTest.tt` para depuração de projeto.  
  
3. Certifique-se de que o **Custom Tool** de DebugTest.tt estiver definida como `TextTemplatingFileGenerator`.  
  
## <a name="debugging-directives-that-access-a-model-from-a-text-template"></a>Diretivas de depuração que acessar um modelo de um modelo de texto  
 Antes de poder acessar um modelo de instruções e expressões em um modelo de texto, você deve primeiro chamar um processador de diretriz gerado. Chamar o processador de diretriz gerado disponibiliza as classes em seu modelo para o código de modelo de texto como propriedades. Para obter mais informações, consulte [acessando modelos a partir de modelos de texto](../modeling/accessing-models-from-text-templates.md).  
  
 Os procedimentos a seguir, você depurará um nome de diretiva incorreto e um nome de propriedade incorreta.  
  
#### <a name="to-debug-an-incorrect-directive-name"></a>Para depurar um nome incorreto de diretiva  
  
1. Substitua o código no DebugTest.tt com o código a seguir:  
  
    > [!NOTE]
    >  O código contém um erro. Apresentando o erro para depurá-lo.  
  
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
  
2. Na **Gerenciador de soluções**DebugTest.tt com o botão direito e, em seguida, clique em **executar ferramenta personalizada**.  
  
     O **Error List** janela exibirá este erro:  
  
     **O processador chamado 'DebuggingTestLanguageDirectiveProcessor' não dá suporte a diretiva chamada 'modelRoot'. A transformação não será executada.**  
  
     Nesse caso, a diretiva chamada contém um nome de diretiva incorreto. Você especificou `modelRoot` como o nome de diretiva, mas o nome correto a diretiva é `DebuggingTestLanguage`.  
  
3. Clique duas vezes no erro na **Error List** janela para ir para o código.  
  
4. Para corrigir o código, altere o nome de diretiva para `DebuggingTestLanguage`.  
  
     A alteração é realçada.  
  
    ```csharp  
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>  
    ```  
  
    ```vb  
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>  
    ```  
  
5. Na **Gerenciador de soluções**DebugTest.tt com o botão direito e, em seguida, clique em **executar ferramenta personalizada**.  
  
     Agora, o sistema transforma o modelo de texto e gera o arquivo de saída correspondente. Você não verá quaisquer erros na **Error List** janela.  
  
#### <a name="to-debug-an-incorrect-property-name"></a>Para depurar um nome de propriedade incorreto  
  
1. Substitua o código no DebugTest.tt com o código a seguir:  
  
    > [!NOTE]
    >  O código contém um erro. Apresentando o erro para depurá-lo.  
  
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
  
2. No **Gerenciador de soluções**DebugTest.tt com o botão direito e, em seguida, clique em **executar ferramenta personalizada**.  
  
     O **Error List** janela aparece e exibe um desses erros:  
  
     (C#)  
  
     **Compilando transformação: Microsoft.VisualStudio.TextTemplating\<GUID>. GeneratedTextTransformation' não contém uma definição para 'ExampleModel'**  
  
     (Visual Basic)  
  
     **Compilando transformação: 'ExampleModel' não é um membro de ' Microsoft.VisualStudio.TextTemplating\<GUID >. GeneratedTextTransformation'.**  
  
     Nesse caso, o código de modelo de texto contém um nome de propriedade incorreta. Você especificou `ExampleModel` como o nome da propriedade, mas a propriedade correta é nome `LibraryModel`. Você pode encontrar o nome da propriedade correto no fornece o parâmetro, conforme mostrado no código a seguir:  
  
    ```  
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>  
    ```  
  
3. Clique duas vezes o erro na janela lista de erros para ir para o código.  
  
4. Para corrigir o código, altere o nome de propriedade para `LibraryModel` no código do modelo de texto.  
  
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
  
5. Na **Gerenciador de soluções**DebugTest.tt com o botão direito e, em seguida, clique em **executar ferramenta personalizada**.  
  
     Agora, o sistema transforma o modelo de texto e gera o arquivo de saída correspondente. Você não verá quaisquer erros na **Error List** janela.
