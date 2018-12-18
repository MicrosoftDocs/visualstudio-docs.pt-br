---
title: 'Passo a passo: Criar um trecho de código'
ms.date: 10/27/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- code snippets, creating
- code snippets, shortcut
- code snippets, template
- code snippets, replacements
- code snippets, references
- code snippets, imports
ms.assetid: 0dcaae11-39cf-4463-9c90-2494321251c2
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: 517eb98e7ca5b32d07a4501823ca092c366e4639
ms.sourcegitcommit: 0cf1e63b6e0e6a0130668278489b21a6e5038084
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39469146"
---
# <a name="walkthrough-create-a-code-snippet"></a>Passo a passo: Criar um trecho de código
Você pode criar um trecho de código com apenas algumas etapas. Tudo o que você precisa fazer é criar um arquivo XML, preencher os elementos apropriados e adicionar seu código. Você também pode adicionar referências e parâmetros de substituição ao seu código. Adicione o trecho à instalação do Visual Studio usando o botão **Importar** no **Gerenciador de Trechos de Código** (**Ferramentas** > **Gerenciador de Trechos de Código**).

## <a name="snippet-template"></a>Modelo de trecho
 A seguir está o modelo básico de trecho:

```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
    <CodeSnippet Format="1.0.0">
        <Header>
            <Title></Title>
        </Header>
        <Snippet>
            <Code Language="">
                <![CDATA[]]>
            </Code>
        </Snippet>
    </CodeSnippet>
</CodeSnippets>
```

### <a name="create-a-code-snippet"></a>Para criar um trecho de código

1.  Crie um novo arquivo XML no Visual Studio e adicione o modelo mostrado acima.

2.  Preencha o título do trecho, por exemplo, "Hello World VB", no elemento **Title**.

3.  Preencha a linguagem do trecho no atributo **Language** do elemento **Code**. Para este exemplo, use "VB".

4.  Adicione um código na seção **CDATA** dentro do elemento **Code**, por exemplo:

    ```xml
    <Code Language="VB">
        <![CDATA[Console.WriteLine("Hello, World!")]]>
    </Code>
    ```

5.  Salve o trecho como *VBCodeSnippet.snippet*.

### <a name="add-a-code-snippet-to-visual-studio"></a>Adicionar um trecho de código ao Visual Studio

1.  Você pode adicionar seus próprios trechos à instalação do Visual Studio usando o Gerenciador de Trechos de Código. Abra o **Gerenciador de Trechos de Código** (**Ferramentas** > **Gerenciador de Trechos de Código**).

2.  Clique no botão **Importar**.

3.  Vá para o local em que você salvou o trecho de código no procedimento anterior, selecione-o e clique em **Abrir**.

4.  A caixa de diálogo **Importar Trecho de Código** é aberta, solicitando que você escolha onde deseja adicionar o trecho entre as opções no painel à direita. Uma das opções deve ser **Trechos do Meu Código**. Selecione-a e clique em **Concluir** e, em seguida, em **OK**.

5.  O trecho é copiado para o seguinte local:

     *%USERPROFILE%\Documents\Visual Studio 2017\Code Snippets\Visual Basic\My Code Snippets*

6.  Teste seu trecho de código abrindo um projeto do Visual Basic e abrindo um arquivo de código. No arquivo, escolha **Trechos** > **Inserir Trecho** no menu de contexto e, em seguida, **Meus Trechos de Código**. Você deve ver um trecho chamado **Meu Trecho de Código do Visual Basic**. Clique duas vezes nesse item.

    `Console.WriteLine("Hello, World!")` é inserido no arquivo de código.

### <a name="add-description-and-shortcut-fields"></a>Adicionar campos de descrição e de atalho

1.  Campos de descrição fornecem mais informações sobre o trecho de código quando exibidos no Gerenciador de Trechos de Código. O atalho é uma marcação que os usuários podem digitar para inserir seu trecho. Edite o trecho adicionado abrindo o arquivo *%USERPROFILE%\Documents\Visual Studio 2017\Code Snippets\Visual Basic\My Code Snippet\VBCodeSnippet.snippet*.

2.  Adicione os elementos **Author** e **Description** ao elemento **Header** e preencha-os.

3.  O elemento **Header** deve ser parecido com este:

    ```xml
    <Header>
        <Title>Hello World VB</Title>
        <Author>Myself</Author>
        <Description>Says Hello to the world.</Description>
    </Header>
    ```

4.  Abra o **Gerenciador de Trechos de Código** e selecione o trecho de código. No painel direito, você deverá ver que os campos **Descrição** e **Autor** agora estão populados.

5.  Para adicionar um atalho, adicione um elemento **Shortcut** junto aos elementos **Author** e **Description**:

    ```xml
    <Header>
        <Title>Hello World VB</Title>
        <Author>Myself</Author>
        <Description>Says Hello to the world.</Description>
        <Shortcut>hello</Shortcut>
    </Header>
    ```

6.  Salve o arquivo de trecho novamente.

7.  Para testar o atalho, abra um projeto do Visual Basic e abra um arquivo de código. Digite `hello` no arquivo e pressione **TAB** duas vezes.

    O trecho de código é inserido.

### <a name="add-references-and-imports"></a>Adicionar referências e importações

1.  Adicione uma referência a um projeto usando o elemento **References** e adicione uma declaração Imports usando o elemento **Imports**. (Isso também funciona para C#). Por exemplo, se você alterar `Console.WriteLine` no exemplo de código para `MessageBox.Show`, talvez seja necessário adicionar o assembly *System.Windows.Forms.dll* ao projeto.

2.  Abra seu trecho.

3.  Adicione o elemento **References** sob o elemento **Snippet**:

    ```xml
    <References>
        <Reference>
            <Assembly>System.Windows.Forms.dll</Assembly>
        </Reference>
    </References>
    ```

4.  Adicione o elemento **Imports** sob o elemento **Snippet**:

    ```xml
    <Imports>
        <Import>
           <Namespace>System.Windows.Forms</Namespace>
        </Import>
    </Imports>
    ```

5.  Altere a seção **CDATA** para o seguinte:

    ```xml
    <![CDATA[MessageBox.Show("Hello, World!")]]>
    ```

6.  Salve o trecho.

7.  Abra um projeto do Visual Basic e adicione o trecho.

8.  Você verá uma instrução `Imports` na parte superior do arquivo de código:

    ```vb
    Imports System.Windows.Forms
    ```

9. Examine as propriedades do projeto. A guia **References** inclui uma referência à *System.Windows.Forms.dll*.

### <a name="add-replacements"></a>Adicionar substituições

1.  Você pode querer que partes dos trechos de código sejam substituídas pelo usuário, por exemplo, se você adicionar uma variável e quiser que o usuário a substitua por uma no projeto atual. Você pode fornecer dois tipos de substituições: literais e objetos. Literais são cadeias de caracteres de algum tipo (literais de cadeias de caracteres, nomes de variáveis ou representações de cadeia de caracteres de valores numéricos). Objetos são instâncias de um tipo que não cadeia de caracteres. Neste procedimento, você declarará uma substituição de literal e uma substituição de objeto e alterará o código para fazer referência a essas substituições.

2.  Abra seu trecho.

3.  Este exemplo usa uma cadeia de conexão SQL e, portanto, você precisa alterar os elementos **Imports** e **References** para adicionar as referências apropriadas:

    ```xml
    <References>
        <Reference>
            <Assembly>System.Data.dll</Assembly>
        </Reference>
        <Reference>
            <Assembly>System.Xml.dll</Assembly>
        </Reference>
    </References>
    <Imports>
        <Import>
            <Namespace>System.Data</Namespace>
        </Import>
        <Import>
            <Namespace>System.Data.SqlClient</Namespace>
        </Import>
    </Imports>
    ```

4.  Para declarar uma substituição de literal para a cadeia de conexão SQL, adicione um elemento **Declarations** no elemento **Snippet** e, a ele, adicione um elemento **Literal** com subelementos para a ID, a dica de ferramenta e o valor padrão para a substituição:

    ```xml
    <Declarations>
        <Literal>
            <ID>SqlConnString</ID>
            <ToolTip>Replace with a SQL connection string.</ToolTip>
            <Default>"SQL connection string"</Default>
        </Literal>
    </Declarations>
    ```

5.  Para declarar uma substituição de objeto para a conexão SQL, adicione um elemento **Object** dentro do elemento **Declarations** e adicione subelementos para a ID, o tipo de objeto, a dica de ferramenta e o valor padrão. O elemento **Declarations** resultante deve ter esta aparência:

    ```xml
    <Declarations>
        <Literal>
            <ID>SqlConnString</ID>
            <ToolTip>Replace with a SQL connection string.</ToolTip>
            <Default>"SQL connection string"</Default>
        </Literal>
        <Object>
            <ID>SqlConnection</ID>
            <Type>System.Data.SqlClient.SqlConnection</Type>
            <ToolTip>Replace with a connection object in your application.</ToolTip>
            <Default>dcConnection</Default>
        </Object>
    </Declarations>
    ```

6.  Na seção de código, você faz referência a substituições com sinais de $ ao redor, por exemplo, `$replacement$`:

    ```xml
    <Code Language="VB" Kind="method body">
        <![CDATA[Dim daCustomers As SqlDataAdapter
            Dim selectCommand As SqlCommand

            daCustomers = New SqlClient.SqlDataAdapter()
            selectCommand = new SqlClient.SqlCommand($SqlConnString$)
            daCustomers.SelectCommand = selectCommand
            daCustomers.SelectCommand.Connection = $SqlConnection$]]>
    </Code>
    ```

7.  Salve o trecho.

8.  Abra um projeto do Visual Basic e adicione o trecho.

9. O código deve se parecer com o seguinte, em que as substituições `SQL connection string` e `dcConnection` são realçadas em laranja claro. Escolha **TAB** para navegar de um para o outro.

    ```vb
    Dim daCustomers As SqlDataAdapter
    Dim selectCommand As SqlCommand

    daCustomers = New SqlClient.SqlDataAdapter()
    selectCommand = New SqlClient.SqlCommand("SQL connection string")
    daCustomers.SelectCommand = selectCommand
    daCustomers.SelectCommand.Connection = dcConnection
    ```

## <a name="see-also"></a>Consulte também

- [Referência de esquema dos trechos de código](../ide/code-snippets-schema-reference.md)