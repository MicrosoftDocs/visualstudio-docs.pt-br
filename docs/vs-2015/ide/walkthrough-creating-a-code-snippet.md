---
title: 'Passo a passo: criando um snippet de código | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- code snippets, creating
- code snippets, shortcut
- code snippets, template
- code snippets, replacements
- code snippets, references
- code snippets, imports
ms.assetid: 0dcaae11-39cf-4463-9c90-2494321251c2
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 038635db92d08837cc6519670053c9619ebe3c9b
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49267727"
---
# <a name="walkthrough-creating-a-code-snippet"></a>Instruções passo a passo: criando um snippet de código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode criar um snippet de código com apenas algumas etapas. Tudo o que você precisa fazer é criar um arquivo XML, preencher os elementos apropriados e adicionar seu código. Você também pode adicionar referências e parâmetros de substituição ao seu código. Você pode adicionar o snippet à instalação do Visual Studio usando o botão Importar no Gerenciador de Snippets de Código (**Ferramentas/Gerenciador de Snippets de Código**).  
  
> [!TIP]
>  Para obter informações sobre como escrever snippets de código mais facilmente, pesquise o site da CodePlex para ferramentas da comunidade, como [Editor de Snippet](http://go.microsoft.com/fwlink/?LinkId=251033).  
  
## <a name="snippet-template"></a>Modelo de Snippet  
 A seguir está o modelo básico de snippet:  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<CodeSnippets  
    xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">  
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
  
### <a name="to-create-a-code-snippet"></a>Para criar um snippet de código  
  
1.  Crie um novo arquivo XML no Visual Studio e adicione o modelo mostrado acima.  
  
2.  Preencha o título do snippet, por exemplo, "Hello World VB", no elemento Title.  
  
3.  Preencha a linguagem do snippet no atributo Linguagens do elemento Código. Para este exemplo, use "VB".  
  
4.  Adicione algum código na seção CDATA dentro do elemento de Código, por exemplo:  
  
    ```  
    <Code Language="VB">  
        <![CDATA[Console.WriteLine("Hello, World!")]]>  
    </Code>  
  
    ```  
  
5.  Salve o trecho como VBCodeSnippet.snippet.  
  
### <a name="to-add-a-code-snippet-to-visual-studio"></a>Para adicionar um snippet de código ao Visual Studio  
  
1.  Você pode adicionar seus próprios snippets à instalação do Visual Studio usando o Gerenciador de Snippets de Código. Abra o Gerenciador de Snippets de Código (**Ferramentas/Gerenciador de Snippets de Código**).  
  
2.  Clique no botão **Importar**.  
  
3.  Vá para o local em que você salvou o snippet de código no procedimento anterior, selecione-o e clique em **Abrir**.  
  
4.  A caixa de diálogo **Importar Snippet de Código** é aberta, solicitando que você escolha onde deseja adicionar o snippet entre as opções no painel à direita. Uma das opções deve ser **Meus Snippets de Código**. Selecione-a e clique em **Concluir** e, em seguida, em **OK**.  
  
5.  O snippet é copiado para o seguinte local:  
  
     `%USERPROFILE%\Documents\Visual Studio 2013\Code Snippets\Visual Basic\My Code Snippets`  
  
6.  Teste seu snippet abrindo um projeto do Visual Basic e abrindo um arquivo de código. No arquivo, clique em **Inserir Snippet** no menu de contexto e, em seguida, **Snippets do Meu Código**. Você deve ver um snippet chamado **Meu Snippet de Código do Visual Basic**. Clique duas vezes nesse item.  
  
7.  Você deve ver `Console.WriteLine("Hello, World!")` inserido no código.  
  
### <a name="adding-description-and-shortcut-fields"></a>Adicionando campos de atalho e descrição  
  
1.  Campos de descrição fornecem mais informações sobre o snippet de código quando exibidos no Gerenciador de Snippets de Código. O atalho é uma marcação que os usuários podem digitar para inserir seu snippet. Edite o snippet adicionado abrindo o arquivo `%USERPROFILE%\Documents\Visual Studio 2013\Code Snippets\Visual Basic\My Code Snippet\VBCodeSnippet.snippet`.  
  
2.  Adicione os elementos Autor e Descrição ao elemento de Cabeçalho e preencha-os.  
  
3.  O elemento Cabeçalho deve ser semelhante a isto:  
  
    ```  
    <Header>  
        <Title>Hello World VB</Title>  
        <Author>Myself</Author>  
        <Description>Says Hello to the world.</Description>  
    </Header>  
  
    ```  
  
4.  Abra o Gerenciador de Snippets de Código e selecione seu snippet de código. No painel à direita, você deverá ver os campos Descrição e Autor agora preenchidos.  
  
5.  Para adicionar um atalho, adicione um elemento Atalho junto dos elementos Autor e Descrição:  
  
    ```  
    <Header>  
        <Title>Hello World VB</Title>  
        <Author>Myself</Author>  
        <Description>Says Hello to the world.</Description>  
        <Shortcut>hello</Shortcut>  
    </Header>  
  
    ```  
  
6.  Salve o arquivo de snippet novamente.  
  
7.  Para testar o atalho, abra um projeto do Visual Basic e abra um arquivo de código. Digite `hello` no arquivo e pressione TAB. O snippet de código deve ser inserido.  
  
### <a name="to-add-references-and-imports"></a>Para adicionar referências e importações  
  
1.  Com snippets do Visual Basic, você pode adicionar uma referência a um projeto usando o elemento Referências e adicionar uma declaração Importações usando o elemento Importações. (Snippets em outras linguagens não têm esse recurso.) Por exemplo, se você alterar `Console.WriteLine` no código de exemplo para `MessageBox.Show`, talvez seja necessário adicionar o assembly System.Windows.Forms.dll ao projeto.  
  
2.  Abra seu snippet.  
  
3.  Adicione o elemento Referências sob o elemento Snippet:  
  
    ```  
    <References>  
        <Reference>  
            <Assembly>System.Windows.Forms.dll</Assembly>  
        </Reference>  
    </References>  
  
    ```  
  
4.  Adicione o elemento Importações sob o elemento Snippet:  
  
    ```  
    <Imports>  
        <Import>  
           <Namespace>System.Windows.Forms</Namespace>  
        </Import>  
    </Imports>  
  
    ```  
  
5.  Altere a seção CDATA para o seguinte:  
  
    ```  
    <![CDATA[MessageBox.Show("Hello, World!")]]>  
    ```  
  
6.  Salve o snippet.  
  
7.  Abra um projeto do Visual Basic e adicione o snippet.  
  
8.  Você verá uma instrução Importações no alto do arquivo de código:  
  
    ```  
    Imports System.Windows.Forms  
  
    ```  
  
9. Examine as propriedades do projeto. A guia Referências inclui uma referência para a System.Windows.Forms.dll.  
  
### <a name="adding-replacements"></a>Adicionando substituições  
  
1.  Você pode querer que partes dos snippets de código sejam substituídas pelo usuário, por exemplo, se você adicionar uma variável e quiser que o usuário a substitua por uma no projeto atual. Você pode fornecer dois tipos de substituições: literais e objetos. Literais são cadeias de caracteres de algum tipo (literais de cadeias de caracteres, nomes de variáveis ou representações de cadeia de caracteres de valores numéricos). Objetos são instâncias de um tipo que não cadeia de caracteres. Neste procedimento, você declarará uma substituição de literal e uma substituição de objeto e alterará o código para fazer referência a essas substituições.  
  
2.  Abra seu snippet.  
  
3.  Este exemplo usa uma cadeia de conexão do SQL, então você precisa alterar os elementos Importações e Referências para adicionar as referências apropriadas:  
  
    ```  
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
  
4.  Para declarar uma substituição de literal para a cadeia de conexão SQL, adicione um elemento de Declarações sob o elemento de Snippet e, nele, adicione um elemento Literal com subelementos para a ID, a dica de ferramenta e o valor padrão para a substituição:  
  
    ```  
    <Declarations>  
        <Literal>  
            <ID>SqlConnString</ID>  
            <ToolTip>Replace with a SQL connection string.</ToolTip>  
            <Default>"SQL connection string"</Default>  
        </Literal>  
    </Declarations>  
  
    ```  
  
5.  Para declarar uma substituição de objeto para a conexão SQL, adicione um elemento de Objeto dentro do elemento de Declarações e adicione subelementos para a ID, o tipo de objeto, a dica de ferramenta e o valor padrão. O elemento Declarações resultante deve ter esta aparência:  
  
    ```  
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
  
    ```  
    <Code Language="VB" Kind="method body">  
        <![CDATA[Dim daCustomers As SqlDataAdapter  
            Dim selectCommand As SqlCommand  
  
            daCustomers = New SqlClient.SqlDataAdapter()  
            selectCommand = new SqlClient.SqlCommand($SqlConnString$)  
            daCustomers.SelectCommand = selectCommand  
            daCustomers.SelectCommand.Connection = $SqlConnection$]]>  
    </Code>  
    ```  
  
7.  Salve o snippet.  
  
8.  Abra um projeto do Visual Basic e adicione o snippet.  
  
9. O código deve se parecer com o seguinte, em que as substituições `SQL connection string` e `dcConnection` são realçadas em laranja claro. Pressione TAB para navegar de um para o outro.  
  
    ```  
    Dim daCustomers As SqlDataAdapter  
    Dim selectCommand As SqlCommand  
  
    daCustomers = New SqlClient.SqlDataAdapter()  
    selectCommand = New SqlClient.SqlCommand("SQL connection string")  
    daCustomers.SelectCommand = selectCommand  
    daCustomers.SelectCommand.Connection = dcConnection  
  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema dos snippets de código](../ide/code-snippets-schema-reference.md)



