---
title: 'Passo a passo: Para criar um snippet de código'
ms.date: 03/31/2020
ms.topic: how-to
helpviewer_keywords:
- code snippets, creating
- code snippets, shortcut
- code snippets, template
- code snippets, replacements
- code snippets, references
- code snippets, imports
ms.assetid: 0dcaae11-39cf-4463-9c90-2494321251c2
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: 8f46dc6a1871b6d44c37c1931bf65f1b4a11c9ae
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770787"
---
# <a name="walkthrough-create-a-code-snippet"></a>Passo a passo: Para criar um snippet de código

Você pode criar um snippet de código com apenas algumas etapas. Tudo o que você precisa fazer é criar um arquivo XML, preencher os elementos apropriados e adicionar seu código. Opcionalmente, você pode fazer uso de parâmetros de substituição e referências de projeto. Importe o snippet à instalação do Visual Studio usando o botão **Importar** no **Gerenciador de Snippets de Código** (**Ferramentas** > **Gerenciador de Snippets de Código**).

## <a name="snippet-template"></a>Modelo de snippet

O seguinte XML é o modelo básico de snippet:

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

## <a name="create-a-code-snippet"></a>Para criar um snippet de código

1. Crie um novo arquivo XML no Visual Studio e adicione o modelo mostrado acima.

2. Preencha o título do snippet no elemento **Título**. Use o título **Raiz Quadrada**.

3. Preencha a linguagem do snippet no atributo **Language** do elemento **Code**. Para o C#, use **Csharp**, por Visual Basic, use o **VB**e, para C++, use **cpp**.

   > [!TIP]
   > Para ver todos os valores de linguagem disponíveis, procure a [seção Atributos de elemento de código](code-snippets-schema-reference.md#attributes) na página [Referência de esquema de snippets de código](code-snippets-schema-reference.md).

4. Adicione o snippet de código na seção **CDATA** dentro do elemento **Code**.

   Para o C#:

   ```xml
   <Code Language="CSharp">
       <![CDATA[double root = Math.Sqrt(16);]]>
   </Code>
   ```

   Ou para o Visual Basic:

   ```xml
   <Code Language="VB">
       <![CDATA[Dim root = Math.Sqrt(16)]]>
   </Code>
   ```

   > [!NOTE]
   > Não é possível especificar como as linhas de código na seção **CDATA** de um snippet de código devem ser recuadas ou formatadas. Após a inserção, o serviço de linguagem formata automaticamente o código inserido.

5. Salve o snippet como *SquareRoot.snippet* (salve-o em qualquer lugar).

## <a name="import-a-code-snippet"></a>Importar um snippet de código

1. Importe um snippet para a instalação do Visual Studio usando o **Gerenciador de Snippets de Código**. Abra-o escolhendo **ferramentas**  >  **códigos trechos de código Gerenciador**.

2. Clique no botão **Importar**.

3. Vá para o local em que você salvou o snippet de código no procedimento anterior, selecione-o e clique em **Abrir**.

4. A caixa de diálogo **Importar Snippet de Código** é aberta, solicitando que você escolha onde deseja adicionar o snippet entre as opções no painel à direita. Uma das opções deve ser **Meus Snippets de Código**. Selecione-a e clique em **Concluir** e, em seguida, em **OK**.

5. O snippet é copiado para uma das seguintes localizações, dependendo da linguagem de código:

   ::: moniker range="vs-2017"

   *%USERPROFILE%\Documents\Visual Studio 2017 \ código Snippets\Visual C# \Meus trechos* 
    de código *%USERPROFILE%\Documents\Visual Studio 2017 \ código Snippets\Visual Basic\My trechos de código*

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   *%USERPROFILE%\Documents\Visual Studio 2019 \ Code Snippets\Visual C# \Meus trechos* 
    de código *%USERPROFILE%\Documents\Visual Studio 2019 \ Code Snippets\Visual Basic\My trechos de código*

   ::: moniker-end

6. Teste o snippet abrindo um projeto C# ou Visual Basic. Com um arquivo de código aberto no editor, escolha **trechos**  >  **Inserir trecho** no menu do botão direito do mouse, em seguida, **meus trechos de código**. Você deverá ver um snippet chamado **Raiz Quadrada**. Clique duas vezes nesse item.

   O snippet de código é inserido no arquivo de código.

## <a name="description-and-shortcut-fields"></a>Campos de descrição e de atalho

::: moniker range="vs-2017"

1. Campos de descrição fornecem mais informações sobre o snippet de código quando exibidos no Gerenciador de Snippets de Código. O atalho é uma marcação que os usuários podem digitar para inserir seu snippet. Edite o snippet adicionado abrindo o arquivo *%USERPROFILE%\Documents\Visual Studio 2017\Code Snippets\\[Visual C# ou Visual Basic]\My Code Snippet\SquareRoot.snippet*.

::: moniker-end

::: moniker range=">=vs-2019"

1. Campos de descrição fornecem mais informações sobre o snippet de código quando exibidos no Gerenciador de Snippets de Código. O atalho é uma marcação que os usuários podem digitar para inserir seu snippet. Edite o snippet adicionado abrindo o arquivo *%USERPROFILE%\Documents\Visual Studio 2019\Code Snippets\\[Visual C# ou Visual Basic]\My Code Snippet\SquareRoot.snippet*.

::: moniker-end

   > [!TIP]
   > Como você está editando o arquivo no diretório em que o Visual Studio o colocou, você não precisa importá-lo novamente para o Visual Studio.

2. Adicione os elementos **Author** e **Description** ao elemento **Header** e preencha-os.

3. O elemento **Header** deve ser parecido com este:

   ```xml
   <Header>
       <Title>Square Root</Title>
       <Author>Myself</Author>
       <Description>Calculates the square root of 16.</Description>
   </Header>
   ```

4. Abra o **Gerenciador de Snippets de Código** e selecione o snippet de código. No painel direito, observe que os campos **Descrição** e **Autor** agora estão populados.

   ![Descrição do snippet de código no Gerenciador de Snippets de Código](media/code-snippet-description-author.png)

5. Para adicionar um atalho, adicione um elemento **Shortcut** dentro do elemento **Header**:

   ```xml
   <Header>
      <Title>Square Root</Title>
      <Author>Myself</Author>
      <Description>Calculates the square root of 16.</Description>
      <Shortcut>sqrt</Shortcut>
    </Header>
   ```

6. Salve o arquivo de snippet novamente.

7. Para testar o atalho, abra o projeto que você usou anteriormente, digite **sqrt** no editor e pressione **Tab** (uma vez para o Visual Basic, duas vezes para o C#).

   O snippet de código é inserido.

## <a name="replacement-parameters"></a>Parâmetros de substituição

Você pode desejar que algumas partes de um snippet de código sejam substituídas pelo usuário. Por exemplo, o ideal é que o usuário substitua um nome de variável por um no projeto atual. Você pode fornecer dois tipos de substituições: literais e objetos. Use o [elemento Literal](code-snippets-schema-reference.md#literal-element) para identificar um substituto para uma parte de código totalmente contido no snippet, mas que provavelmente será personalizado depois de inserido no código (por exemplo, uma cadeia de caracteres ou um valor numérico). Use o [elemento Object](code-snippets-schema-reference.md#object-element) para identificar um item exigido pelo snippet de código, mas que provavelmente será definido fora do snippet em si (por exemplo, uma instância de objeto ou um controle).

1. Para permitir que o usuário substitua o número com facilidade para calcular a raiz quadrada dele, modifique o elemento **Snippet** do arquivo *SquareRoot.snippet* da seguinte maneira:

   ```xml
   <Snippet>
     <Code Language="CSharp">
       <![CDATA[double root = Math.Sqrt($Number$);]]>
     </Code>
     <Declarations>
       <Literal>
         <ID>Number</ID>
         <ToolTip>Choose the number you want the square root of.</ToolTip>
         <Default>16</Default>
       </Literal>
     </Declarations>
   </Snippet>
   ```

   Observe que a substituição de literal recebe uma ID (`Number`). Essa ID é referenciada no snippet de código colocando-a entre os caracteres `$`:

   ```xml
   <![CDATA[double root = Math.Sqrt($Number$);]]>
   ```

2. Salve o arquivo de snippet.

3. Abra um projeto e insira o snippet.

   O snippet de código é inserido e o literal editável é realçado para substituição. Focalize o parâmetro de substituição para ver a dica de ferramenta para o valor.

   ![Dica de ferramenta do parâmetro de substituição de snippet de código no Visual Studio](media/snippet-replacement-parameter-tooltip.png)

   > [!TIP]
   > Se houver mais de um parâmetro substituível em um snippet, pressione **Tab** para ir de um para o outro e alterar os valores.

## <a name="import-a-namespace"></a>Importar um namespace

Você pode usar um snippet de código para adicionar uma diretiva `using` (C#) ou uma instrução `Imports` (Visual Basic) incluindo o [elemento Imports](code-snippets-schema-reference.md#imports-element). Para projetos .NET Framework, você também pode adicionar uma referência ao projeto usando o [elemento References](code-snippets-schema-reference.md#references-element).

O XML a seguir mostra um snippet de código que usa o método `File.Exists` no namespace System.IO e, portanto, define o elemento **Imports** para importar o namespace System.IO.

```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
  <CodeSnippet Format="1.0.0">
    <Header>
      <Title>File Exists</Title>
      <Shortcut>exists</Shortcut>
    </Header>
    <Snippet>
      <Code Language="CSharp">
        <![CDATA[var exists = File.Exists("C:\\Temp\\Notes.txt");]]>
      </Code>
      <Imports>
        <Import>
          <Namespace>System.IO</Namespace>
        </Import>
      </Imports>
    </Snippet>
  </CodeSnippet>
</CodeSnippets>
```

## <a name="see-also"></a>Confira também

- [Referência de esquema dos snippets de código](../ide/code-snippets-schema-reference.md)
