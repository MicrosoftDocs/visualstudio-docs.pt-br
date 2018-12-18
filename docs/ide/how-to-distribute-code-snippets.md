---
title: Como distribuir trechos de código
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- code snippets, distributing
ms.assetid: 5f717abd-e167-47ae-818c-6b0bae100ceb
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: cd6aba7c20c920c0c4351a1e9aa263fc73cd4415
ms.sourcegitcommit: 495bba1d8029646653f99ad20df2f80faad8d58b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39380411"
---
# <a name="how-to-distribute-code-snippets"></a>Como distribuir trechos de código

Você pode fornecer os trechos de código a seus amigos e solicitar a eles que instalem os trechos em seus próprios computadores usando o **Gerenciador de Trechos de Código**. No entanto, se você tiver vários trechos para distribuir ou desejar distribuí-los mais amplamente, inclua o arquivo de trecho em uma extensão do Visual Studio. Em seguida, os usuários do Visual Studio podem instalar a extensão.

Você deve instalar o SDK do Visual Studio para criar extensões do Visual Studio. Localize a versão do VSSDK que corresponde à sua instalação do Visual Studio em [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).

## <a name="set-up-the-extension"></a>Configurar a extensão

Neste procedimento, usaremos o mesmo trecho de código Olá, Mundo criado no [Passo a passo: Criar um trecho de código](../ide/walkthrough-creating-a-code-snippet.md). Forneceremos o texto *.snippet*, de modo que você não precise voltar e criar um.

1. Crie um novo projeto do VSIX chamado **TestSnippet**. (**Arquivo** > **Novo** > **Projeto** > **Visual C# (ou Visual Basic)** > **Extensibilidade**).

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

1. No **Gerenciador de Soluções**, selecione o nó do projeto e adicione uma pasta que tenha o nome que deseja que o trecho tenha no **Gerenciador de Trechos de Código**. Neste caso, deve ser **HelloWorldVB**.

2. Mova o arquivo *.snippet* para a pasta *HelloWorldVB*.

3. Selecione o arquivo *.snippet* no **Gerenciador de Soluções** e, na janela **Propriedades**, garanta que **Ação de Build** esteja definida como **Conteúdo**, **Copiar para Diretório de Saída** esteja definido como **Copiar sempre** e **Incluir no VSIX** esteja definido como **true**.

### <a name="add-the-pkgdef-file"></a>Adicionar o arquivo .pkgdef

1. Adicione um arquivo de texto à pasta *HelloWorldVB* e dê a ele o nome de *HelloWorldVB.pkgdef*. Esse arquivo é usado para adicionar determinadas chaves ao Registro. Nesse caso, ele adiciona uma nova subchave à chave **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\15.0\Languages\CodeExpansions\Basic**.

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

### <a name="test-the-snippet"></a>Teste o trecho

1. Agora você pode verificar se o trecho de código funciona na instância experimental do Visual Studio. A instância experimental é uma segunda cópia do Visual Studio, que é separada daquela que você usa para escrever código. Ela permite que você trabalhe em uma extensão sem afetar seu ambiente de desenvolvimento.

2. Compile o projeto e comece a depuração.

   Uma segunda instância do Visual Studio é exibida.

3. Na instância experimental, acesse **Ferramentas** > **Gerenciador de Trechos de Código** e defina a **Linguagem** como **Basic**. Você deve ver *HelloWorldVB* como uma das pastas e ser capaz de expandir a pasta para ver o trecho *HelloWorldVB*.

4. Teste o trecho. Na instância experimental, abra um projeto do Visual Basic e abra um dos arquivos de código. Coloque o cursor em algum lugar no código, clique com o botão direito do mouse e, no menu de contexto, selecione **Inserir Trecho**.

5. Você deve ver *HelloWorldVB* como uma das pastas. Clique duas vezes nesse item. Você deve ver um pop-up **Inserir trecho: HelloWorldVB >** que tem uma lista suspensa **HelloWorldVB**. Clique na lista suspensa **HelloWorldVB**. Você deve ver a seguinte linha adicionada ao arquivo:

    ```vb
    Console.WriteLine("Hello, World!")
    ```

## <a name="see-also"></a>Consulte também

- [Trechos de código](../ide/code-snippets.md)