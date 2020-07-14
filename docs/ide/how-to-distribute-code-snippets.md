---
title: Distribuir snippets de código como uma extensão
ms.date: 03/21/2019
ms.topic: how-to
helpviewer_keywords:
- code snippets, distributing
ms.assetid: 5f717abd-e167-47ae-818c-6b0bae100ceb
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: c283d5ca29b67e772df2a0bb2e25dee70cd63fd3
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284367"
---
# <a name="how-to-distribute-code-snippets"></a>Como distribuir snippets de código

Você pode fornecer os snippets de código a seus amigos e solicitar a eles que instalem os snippets em seus próprios computadores usando o **Gerenciador de Snippets de Código**. No entanto, se tiver vários snippets para distribuir ou desejar distribuí-los mais amplamente, você poderá incluir os arquivos de snippet em uma extensão do Visual Studio. Em seguida, os usuários do Visual Studio podem instalar a extensão para obter os snippets.

## <a name="prerequisites"></a>Pré-requisitos

Instale a carga de trabalho do **desenvolvimento de extensões do Visual Studio** para obter acesso aos modelos do **Projeto do VSIX**.

![Carga de trabalho de desenvolvimento de extensão do Visual Studio](media/vs-2019/extension-development-workload.png)

## <a name="set-up-the-extension"></a>Configurar a extensão

Neste procedimento, você usará o mesmo trecho de código de Olá, Mundo que é criado em [Walkthrough: criar um trecho de código](../ide/walkthrough-creating-a-code-snippet.md). Este artigo fornece o snippet XML, portanto, você não precisa voltar e criar um snippet.

1. Crie um projeto por meio do modelo **Projeto Vazio do VSIX** e dê a ele o nome **TestSnippet**.

2. No projeto **TestSnippet**, adicione um novo arquivo XML e chame-o de *VBCodeSnippet.snippet*. Substitua o conteúdo pelo seguinte XML:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <CodeSnippets
        xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
      <CodeSnippet Format="1.0.0">
        <Header>
          <Title>Hello World VB</Title>
          <Shortcut>HelloWorld</Shortcut>
          <Description>Inserts code</Description>
          <Author>MSIT</Author>
          <SnippetTypes>
            <SnippetType>Expansion</SnippetType>
            <SnippetType>SurroundsWith</SnippetType>
          </SnippetTypes>
        </Header>
        <Snippet>
          <Code Language="VB">
            <![CDATA[Console.WriteLine("Hello, World!")]]>
          </Code>
        </Snippet>
      </CodeSnippet>
    </CodeSnippets>
    ```

### <a name="set-up-the-directory-structure"></a>Configurar a estrutura de diretório

1. No **Gerenciador de Soluções**, selecione o nó do projeto e adicione uma pasta que tenha o nome que deseja que o snippet tenha no **Gerenciador de Snippets de Código**. Neste caso, deve ser **HelloWorldVB**.

2. Mova o arquivo *.snippet* para a pasta *HelloWorldVB*.

3. Selecione o arquivo *.snippet* no **Gerenciador de Soluções** e, na janela **Propriedades**, garanta que **Ação de Build** esteja definida como **Conteúdo**, **Copiar para Diretório de Saída** esteja definido como **Copiar sempre** e **Incluir no VSIX** esteja definido como **true**.

### <a name="add-the-pkgdef-file"></a>Adicionar o arquivo .pkgdef

::: moniker range="vs-2017"

1. Adicione um arquivo de texto à pasta *HelloWorldVB* e dê a ele o nome de *HelloWorldVB.pkgdef*. Esse arquivo é usado para adicionar determinadas chaves ao Registro. Nesse caso, ele adiciona uma nova subchave à chave **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\15.0\Languages\CodeExpansions\Basic**.

::: moniker-end

::: moniker range=">=vs-2019"

1. Adicione um arquivo de texto à pasta *HelloWorldVB* e dê a ele o nome de *HelloWorldVB.pkgdef*. Esse arquivo é usado para adicionar determinadas chaves ao Registro. Nesse caso, ele adiciona uma nova subchave à chave **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\16.0\Languages\CodeExpansions\Basic**.

::: moniker-end

2. Adicione as seguintes linhas ao arquivo.

    ```txt
    // Visual Basic
    [$RootKey$\Languages\CodeExpansions\Basic\Paths]
    "HelloWorldVB"="$PackageFolder$"
    ```

    Se você examinar essa chave, poderá ver como especificar diferentes idiomas.

3. Selecione o arquivo *.pkgdef* no **Gerenciador de Soluções** e, na janela **Propriedades**, garanta que:

   - A opção **Ação de Build** esteja definida como **Conteúdo**
   - A opção **Copiar para Diretório de Saída** esteja definida como **Sempre copiar**
   - A opção **Incluir no VSIX** esteja definida como **true**

4. Adicione o arquivo *.pkgdef* como um ativo no manifesto VSIX. No arquivo *source.extension.vsixmanifest*, vá para a guia **Ativos** e clique em **Novo**.

5. Na caixa de diálogo **Adicionar Novo Ativo**, defina o **Tipo** como **Microsoft.VisualStudio.VsPackage**, a **Origem** como **Arquivo no sistema de arquivos** e o **Caminho** como **HelloWorldVB.pkgdef** (que deve aparecer na lista suspensa).

### <a name="test-the-snippet"></a>Teste o snippet

1. Agora você pode verificar se o snippet de código funciona na instância experimental do Visual Studio. A instância experimental é uma segunda cópia do Visual Studio, que é separada daquela que você usa para escrever código. Ela permite que você trabalhe em uma extensão sem afetar seu ambiente de desenvolvimento.

2. Compile o projeto e comece a depuração.

   Uma segunda instância do Visual Studio é exibida.

3. Na instância experimental, vá para **ferramentas**  >  **Gerenciador de trechos de código** e defina o **idioma** como **básico**. Você deve ver *HelloWorldVB* como uma das pastas e ser capaz de expandir a pasta para ver o snippet *HelloWorldVB*.

4. Teste o snippet. Na instância experimental, abra um projeto do Visual Basic e abra um dos arquivos de código. Coloque o cursor em algum lugar no código, clique com o botão direito do mouse e, no menu de contexto, selecione **Inserir Snippet**.

5. Você deve ver *HelloWorldVB* como uma das pastas. Clique duas vezes nesse item. Você deve ver um pop-up **Inserir snippet: HelloWorldVB &gt;** que tem uma lista suspensa **HelloWorldVB**. Clique na lista suspensa **HelloWorldVB**.

   A seguinte linha é adicionada ao arquivo de código:

    ```vb
    Console.WriteLine("Hello, World!")
    ```

## <a name="see-also"></a>Veja também

- [Trechos de código](../ide/code-snippets.md)
