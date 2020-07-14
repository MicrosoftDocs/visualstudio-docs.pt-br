---
title: Conectar host ao processador de diretivas gerado
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- walkthroughs [text templates], connecting host to processor
- text templates, custom directive hosts
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
dev_langs:
- CSharp
- VB
ms.openlocfilehash: c782b84f39419272c271f41d217442cc9e001b3f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535857"
---
# <a name="walkthrough-connect-a-host-to-a-generated-directive-processor"></a>Passo a passo: conectar um host a um processador de diretiva gerado

Você pode escrever seu próprio host que processa modelos de texto. Um host personalizado básico é demonstrado em [passo a passos: Criando um host de modelo de texto personalizado](../modeling/walkthrough-creating-a-custom-text-template-host.md). Você pode estender esse host para adicionar funções, como a geração de vários arquivos de saída.

Neste tutorial, você expande seu host personalizado para que ele dê suporte a modelos de texto que chamam processadores de diretiva. Quando você define uma linguagem específica de domínio, ela gera um *processador de diretiva* para o modelo de domínio. O processador de diretiva facilita para os usuários a gravação de modelos que acessam o modelo, reduzindo a necessidade de escrever diretivas de assembly e de importação nos modelos.

> [!NOTE]
> Este guia passo a passo baseia-se na [criação de um host de modelo de texto personalizado](../modeling/walkthrough-creating-a-custom-text-template-host.md). Execute esse passo a passos primeiro.

Esta explicação passo a passo inclui as seguintes tarefas:

- Usando [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] para gerar um processador de diretiva baseado em um modelo de domínio.

- Conectar um host de modelo de texto personalizado ao processador de diretiva gerado.

- Testando o host personalizado com o processador de diretiva gerado.

## <a name="prerequisites"></a>Pré-requisitos

Para definir uma DSL, é necessário ter instalados os seguintes componentes:

| | |
|-|-|
| Visual Studio | [http://go.microsoft.com/fwlink/?LinkId=185579](https://visualstudio.microsoft.com/) |
| [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)] | [http://go.microsoft.com/fwlink/?LinkId=185580](/azure/devops/integrate/index) |
| SDK de Visualização e Modelagem do Visual Studio | |

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

Além disso, você deve ter a transformação de modelo de texto personalizado criada em [passo a passo: Criando um host de modelo de texto personalizado](../modeling/walkthrough-creating-a-custom-text-template-host.md).

## <a name="use-domain-specific-language-tools-to-generate-a-directive-processor"></a>Usar Ferramentas de Linguagem Específica de Domínio para gerar um processador de diretiva

Neste tutorial, você usa o assistente de Designer de Linguagem Específica de Domínio para criar uma linguagem específica de domínio para a solução DSLMinimalTest.

1. Crie uma solução de linguagem específica de domínio que tenha as seguintes características:

   - Nome: DSLMinimalTest

   - Modelo de solução: linguagem mínima

   - Extensão de arquivo: mín.

   - Nome da empresa: fabrikam

   Para obter mais informações sobre como criar uma solução de linguagem específica de domínio, consulte [como criar uma solução de linguagem específica de domínio](../modeling/how-to-create-a-domain-specific-language-solution.md).

2. No menu **Compilar**, clique em **Compilar Solução**.

   > [!IMPORTANT]
   > Esta etapa gera o processador de diretiva e adiciona a chave para ele no registro.

3. No menu **depurar** , clique em **Iniciar Depuração**.

    Uma segunda instância do Visual Studio é aberta.

4. Na compilação experimental, em **Gerenciador de soluções**, clique duas vezes no arquivo **Sample. min**.

    O arquivo é aberto no designer. Observe que o modelo tem dois elementos, ExampleElement1 e ExampleElement2, e um link entre eles.

5. Feche a segunda instância do Visual Studio.

6. Salve a solução e, em seguida, feche a Designer de Linguagem Específica de Domínio.

## <a name="connect-a-custom-text-template-host-to-a-directive-processor"></a>Conectar um host de modelo de texto personalizado a um processador de diretiva

Depois de gerar o processador de diretiva, você conecta o processador de diretivas e o host de modelo de texto personalizado que você criou no [passo a passo: Criando um host de modelo de texto personalizado](../modeling/walkthrough-creating-a-custom-text-template-host.md).

1. Abra a solução CustomHost.

2. No menu **Projeto**, clique em **Adicionar Referência**.

     A caixa de diálogo **Adicionar referência** é aberta com a guia **.net** exibida.

3. Adicione as seguintes referências:

    - Microsoft. VisualStudio. Modeling. Sdk. 11.0

    - Microsoft. VisualStudio. Modeling. Sdk. Diagrams. 11.0

    - Microsoft. VisualStudio. TextTemplating. 11.0

    - Microsoft. VisualStudio. TextTemplating. interfaces. 11.0

    - Microsoft. VisualStudio. TextTemplating. Modeling. 11.0

    - Microsoft. VisualStudio. TextTemplating. VSHost. 11.0

4. Na parte superior de Program.cs ou Module1. vb, adicione a seguinte linha de código:

    ```csharp
    using Microsoft.Win32;
    ```

    ```vb
    Imports Microsoft.Win32
    ```

5. Localize o código da propriedade `StandardAssemblyReferences` e substitua-o pelo código a seguir:

    > [!NOTE]
    > Nesta etapa, você adiciona referências aos assemblies que são exigidos pelo processador de diretiva gerado ao qual seu host dará suporte.

    ```csharp
    //the host can provide standard assembly references
    //the engine will use these references when compiling and
    //executing the generated transformation class
    //--------------------------------------------------------------
    public IList<string> StandardAssemblyReferences
    {
        get
        {
            return new string[]
            {
                //if this host searches standard paths and the GAC
                //we can specify the assembly name like this:
                //"System"
                //since this host only resolves assemblies from the
                //fully qualified path and name of the assembly
                //this is a quick way to get the code to give us the
                //fully qualified path and name of the System assembly
                //---------------------------------------------------------
                typeof(System.Uri).Assembly.Location,
                            typeof(System.Uri).Assembly.Location,
                typeof(Microsoft.VisualStudio.Modeling.ModelElement).Assembly.Location,
                typeof(Microsoft.VisualStudio.Modeling.Diagrams.BinaryLinkShape).Assembly.Location,
                typeof(Microsoft.VisualStudio.TextTemplating.VSHost.ITextTemplating).Assembly.Location,
                typeof(Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation).Assembly.Location

            };
        }
    }
    ```

6. Localize o código para a função `ResolveDirectiveProcessor` e substitua-o pelo seguinte código:

    > [!IMPORTANT]
    > Esse código contém referências embutidas em código para o nome do processador de diretiva gerado ao qual você deseja se conectar. Você poderia facilmente tornar isso mais geral. nesse caso, ele procura todos os processadores de diretiva listados no registro e tenta encontrar uma correspondência. Nesse caso, o host funcionaria com qualquer processador de diretiva gerado.

    ```csharp
    //the engine calls this method based on the directives the user has
            //specified it in the text template
            //this method can be called 0, 1, or more times
            //---------------------------------------------------------------------
            public Type ResolveDirectiveProcessor(string processorName)
            {
                //check the processor name, and if it is the name of the processor the
                //host wants to support, return the type of the processor
                //---------------------------------------------------------------------
                if (string.Compare(processorName, "DSLMinimalTestDirectiveProcessor", StringComparison.InvariantCultureIgnoreCase) == 0)
                {
                    try
                    {
                        string keyName = @"Software\Microsoft\VisualStudio\10.0Exp_Config\TextTemplating\DirectiveProcessors\DSLMinimalTestDirectiveProcessor";
                        using (RegistryKey specificKey = Registry.CurrentUser.OpenSubKey(keyName))
                        {
                            if (specificKey != null)
                            {
                                List<string> names = new List<String>(specificKey.GetValueNames());
                                string classValue = specificKey.GetValue("Class") as string;
                                if (!string.IsNullOrEmpty(classValue))
                                {
                                    string loadValue = string.Empty;
                                    System.Reflection.Assembly processorAssembly = null;
                                    if (names.Contains("Assembly"))
                                    {
                                        loadValue = specificKey.GetValue("Assembly") as string;
                                        if (!string.IsNullOrEmpty(loadValue))
                                        {
                                            //the assembly must be installed in the GAC
                                            processorAssembly = System.Reflection.Assembly.Load(loadValue);
                                        }
                                    }
                                    else if (names.Contains("CodeBase"))
                                    {
                                        loadValue = specificKey.GetValue("CodeBase") as string;
                                        if (!string.IsNullOrEmpty(loadValue))
                                        {
                                            //loading local assembly
                                            processorAssembly = System.Reflection.Assembly.LoadFrom(loadValue);
                                        }
                                    }
                                    if (processorAssembly == null)
                                    {
                                        throw new Exception("Directive Processor not found");
                                    }
                                    Type processorType = processorAssembly.GetType(classValue);
                                    if (processorType == null)
                                    {
                                        throw new Exception("Directive Processor not found");
                                    }
                                    return processorType;
                                }
                            }
                        }
                    }
                    catch (Exception e)
                    {
                        //if the directive processor can not be found, throw an error
                        throw new Exception("Directive Processor not found");
                    }
                }

                //if the directive processor is not one this host wants to support
                throw new Exception("Directive Processor not supported");
            }
    ```

7. No menu **Arquivo** , clique em **Salvar Tudo**.

8. No menu **Compilar**, clique em **Compilar Solução**.

## <a name="test-the-custom-host-with-the-directive-processor"></a>Testar o host personalizado com o processador de diretiva

Para testar o host de modelo de texto personalizado, primeiro você deve escrever um modelo de texto que chame o processador de diretiva gerado. Em seguida, você executa o host personalizado, passa para ele o nome do modelo de texto e verifica se a diretiva é processada corretamente.

### <a name="create-a-text-template-to-test-the-custom-host"></a>Criar um modelo de texto para testar o host personalizado

1. Crie um arquivo de texto e nomeie-o `TestTemplateWithDP.tt` . Você pode usar qualquer editor de texto, como o bloco de notas, para criar o arquivo.

2. Adicione o seguinte ao arquivo de texto:

    > [!NOTE]
    > A linguagem de programação do modelo de texto não precisa corresponder à do host personalizado.

    ```csharp
    Text Template Host Test

    <#@ template debug="true" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>
    <# //this is the call to the examplemodel directive in the generated directive processor #>
    <#@ DSLMinimalTest processor="DSLMinimalTestDirectiveProcessor" requires="fileName='<Your Path>\Sample.min'" provides="ExampleModel=ExampleModel" #>
    <# //uncomment this line to test that the host allows the engine to set the extension #>
    <# //@ output extension=".htm" #>

    <# //uncomment this line if you want to see the generated transformation class #>
    <# //System.Diagnostics.Debugger.Break(); #>
    <# //this code uses the results of the examplemodel directive #>
    <#
        foreach ( ExampleElement box in this.ExampleModel.Elements )
        {
            WriteLine("Box: {0}", box.Name);

            foreach (ExampleElement linkedTo in box.Targets)
            {
                WriteLine("Linked to: {0}", linkedTo.Name);
            }

            foreach (ExampleElement linkedFrom in box.Sources)
            {
                WriteLine("Linked from: {0}", linkedFrom.Name);
            }

            WriteLine("");
        }
    #>
    ```

    ```vb
    Text Template Host Test

    <#@ template debug="true" language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>

    <# 'this is the call to the examplemodel directive in the generated directive processor #>
    <#@ DSLMinimalTest processor="DSLMinimalTestDirectiveProcessor" requires="fileName='<Your Path>\Sample.min'" provides="ExampleModel=ExampleModel" #>

    <# 'Uncomment this line to test that the host allows the engine to set the extension. #>
    <# '@ output extension=".htm" #>

    <# 'Uncomment this line if you want to see the generated transformation class. #>
    <# 'System.Diagnostics.Debugger.Break() #>

    <# 'this code uses the results of the examplemodel directive #>

    <#
       For Each box as ExampleElement In Me.ExampleModel.Elements

           WriteLine("Box: {0}", box.Name)

            For Each LinkedTo as ExampleElement In box.Targets
                WriteLine("Linked to: {0}", LinkedTo.Name)
            Next

            For Each LinkedFrom as ExampleElement In box.Sources
                WriteLine("Linked from: {0}", LinkedFrom.Name)
            Next

            WriteLine("")

       Next
    #>
    ```

3. No código, substitua \<YOUR PATH> pelo caminho do arquivo Sample. min da linguagem específica do design criada no primeiro procedimento.

4. Salve e feche o arquivo.

### <a name="test-the-custom-host"></a>Testar o host personalizado

1. Abra uma janela de Prompt de Comando.

2. Digite o caminho do arquivo executável para o host personalizado, mas não pressione ENTER ainda.

     Por exemplo, digite:

     `<YOUR PATH>CustomHost\bin\Debug\CustomHost.exe`

    > [!NOTE]
    > Em vez de digitar o endereço, você pode navegar até o arquivo CustomHost.exe no **Windows Explorer**e, em seguida, arrastar o arquivo para a janela de prompt de comando.

3. Digite um espaço.

4. Digite o caminho do arquivo de modelo de texto e pressione ENTER.

     Por exemplo, digite:

     `<YOUR PATH>TestTemplateWithDP.txt`

    > [!NOTE]
    > Em vez de digitar o endereço, você pode navegar até o arquivo TestTemplateWithDP.txt no **Windows Explorer**e, em seguida, arrastar o arquivo para a janela de prompt de comando.

     O aplicativo host personalizado é executado e inicia o processo de transformação do modelo de texto.

5. No **Windows Explorer**, navegue até a pasta que contém o arquivo TestTemplateWithDP.txt.

     A pasta também contém o arquivo TestTemplateWithDP1.txt.

6. Abra esse arquivo para ver os resultados da transformação do modelo de texto.

     Os resultados da saída de texto gerado são exibidos e devem ter a seguinte aparência:

    ```
    Text Template Host Test

    Box: ExampleElement1
    Linked to: ExampleElement2

    Box: ExampleElement2
    Linked from: ExampleElement1
    ```

## <a name="see-also"></a>Confira também

- [Instruções passo a passo: criando um host de modelo de texto personalizado](../modeling/walkthrough-creating-a-custom-text-template-host.md)
