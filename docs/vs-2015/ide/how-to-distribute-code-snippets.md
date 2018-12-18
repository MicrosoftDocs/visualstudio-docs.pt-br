---
title: Como distribuir snippets de código | Microsoft Docs
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
- code snippets, distributing
ms.assetid: 5f717abd-e167-47ae-818c-6b0bae100ceb
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 14dea3842289b626b79d8dc7e294ba5f335d0351
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49185699"
---
# <a name="how-to-distribute-code-snippets"></a>Como distribuir snippets de código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode simplesmente fornecer seus snippets de código a seus amigos e fazer com que instalem os snippets em seus próprios computadores usando o Gerenciador de Snippets de Código. No entanto, se você tiver vários snippets para distribuir ou gostaria de distribuí-los mais amplamente, inclua seu arquivo de snippet em uma extensão do Visual Studio, que usuários do Visual Studio podem instalar.  
  
 Você deve instalar o SDK do Visual Studio para criar extensões do Visual Studio. Localizar a versão do VSSDK que corresponde à sua instalação do Visual Studio em [Downloads do Visual Studio 2015](http://www.visualstudio.com/downloads/visual-studio-2015-downloads-vs.aspx).  
  
## <a name="setting-up-the-extension"></a>Configurando a extensão  
 Neste procedimento, usaremos o mesmo snippet de código Hello World criado no [Passo a passo: criando um snippet de código](../ide/walkthrough-creating-a-code-snippet.md). Forneceremos o texto .snippet, portanto, você não precisa voltar e criar um.  
  
1.  Crie um novo projeto do VSIX chamado **TestSnippet**. (**Arquivo/Novo/Projeto/Visual C# (ou Visual Basic/Extensibilidade**)  
  
2.  No projeto **TestSnippet**, adicione um novo arquivo XML e chame-o de **VBCodeSnippet.snippet**. Substitua o conteúdo pelo seguinte:  
  
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
  
#### <a name="setting-up-the-directory-structure"></a>Configurando a estrutura de diretório  
  
1.  No Gerenciador de Soluções, selecione o nó do projeto e adicione uma pasta que tenha o nome que você deseja que o snippet tenha no Gerenciador de Snippets de Código. Neste caso, deve ser **HelloWorldVB**.  
  
2.  Mova o arquivo .snippet para a pasta **HelloWorldVB**.  
  
3.  Selecione o arquivo .snippet no Gerenciador de Soluções e, na janela **Propriedades**, garanta que **Ação de Build** esteja definida como **Conteúdo**; **Copiar para Diretório de Saída** esteja definido como **Copiar Sempre**; e **Incluir em VSIX** esteja definido como **true**.  
  
#### <a name="adding-the-pkgdef-file"></a>Adicionando o arquivo .pkgdef  
  
1.  Adicione um arquivo de texto à pasta **HelloWorldVB** e dê a ele o nome de **HelloWorldVB.pkgdef**. Esse arquivo é usado para adicionar determinadas chaves ao Registro. Nesse caso, ele adiciona uma nova chave a  
  
     **HKCU\Software\Microsoft\VisualStudio\14.0\Languages\CodeExpansions\Basic**.  
  
2.  Adicione as seguintes linhas ao arquivo.  
  
    ```  
    // Visual Basic   
    [$RootKey$\Languages\CodeExpansions\Basic\Paths]   
    "HelloWorldVB"="$PackageFolder$"  
    ```  
  
     Se você examinar essa chave, poderá ver como especificar diferentes idiomas.  
  
3.  Selecione o arquivo .pkgdef no Gerenciador de Soluções e, na janela **Propriedades**, garanta que **Ação de Build** esteja definida como **Conteúdo**; **Copiar para Diretório de Saída** esteja definido como **Copiar Sempre**; e **Incluir em VSIX** esteja definido como **true**.  
  
4.  Adicione o arquivo .pkgdef como um ativo no manifesto VSIX. No arquivo source.extension.vsixmanifest, vá para a guia **Ativos** e clique em **Novo**.  
  
5.  Na caixa de diálogo **Adicionar Novo Ativo**, defina o **Tipo** como **Microsoft.VisualStudio.VsPackage**; o **Tipo** como **Arquivo no filesystem**; e o **Caminho** como **HelloWorldVB.pkgdef** (que deve aparecer na lista suspensa).  
  
### <a name="testing-the-snippet"></a>Testando o snippet  
  
1.  Agora você pode verificar se o snippet de código funciona na instância experimental do Visual Studio. A instância experimental é uma segunda cópia do Visual Studio, que é separada daquela que você usa para escrever código. Ela permite que você trabalhe em uma extensão sem afetar seu ambiente de desenvolvimento.  
  
2.  Compile o projeto e comece a depuração. Uma segunda instância do Visual Studio deve ser exibida.  
  
3.  Na instância experimental, vá para **Ferramentas /Gerenciador de Snippets de Código** e defina a **Linguagem** como **Básica**. Você deve ver HelloWorldVB como uma das pastas e ser capaz de expandir a pasta para ver o snippet HelloWorldVB.  
  
4.  Teste o snippet. Na instância experimental, abra um projeto do Visual Basic e abra um dos arquivos de código. Coloque o cursor em algum lugar no código, clique com o botão direito do mouse e, no menu de contexto, selecione **Inserir Snippet**.  
  
5.  Você deve ver HelloWorldVB como uma das pastas. Clique duas vezes nesse item. Você deve ver um pop-up **Inserir Snippet: HellowWorldVB >** que tem uma lista suspensa **HelloWorldVB**. Clique na lista suspensa HelloWorldVB. Você deve ver a seguinte linha adicionada ao arquivo:  
  
    ```vb  
    Console.WriteLine("Hello, World!")  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Snippets de código](../ide/code-snippets.md)



