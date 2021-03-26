---
title: Suporte para trechos de código em um serviço de linguagem herdada | Microsoft Docs
description: Saiba como um serviço de linguagem herdado dá suporte a trechos de código. Um trecho de código é uma parte do código que é inserido no arquivo de origem.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- snippets, supporting in language services
- code snippets, supporting in language services [managed package framework]
- language services [managed package framework], supporting code snippets
ms.assetid: 7490325b-acee-4c2d-ac56-1cd5db1a1083
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9578159554f77a9ad7553a56c054a863b3b63fd5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080756"
---
# <a name="support-for-code-snippets-in-a-legacy-language-service"></a>Suporte para snippets de código em um serviço de linguagem herdado
Um trecho de código é uma parte do código que é inserido no arquivo de origem. O trecho em si é um modelo baseado em XML com um conjunto de campos. Esses campos são realçados após o trecho de código ser inserido e podem ter valores diferentes, dependendo do contexto no qual o trecho de código é inserido. Imediatamente após a inserção do trecho de código, o serviço de linguagem pode formatar o trecho de código.

 O trecho de código é inserido em um modo de edição especial que permite que os campos do trecho de código sejam navegados usando a tecla TAB. Os campos podem dar suporte a menus suspensos estilo IntelliSense. O usuário confirma o trecho de código para o arquivo de origem digitando a tecla ENTER ou ESC. Para saber mais sobre trechos de código, consulte [trechos de códigos](../../ide/code-snippets.md).

 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente de implementar recursos de serviço de linguagem é usar extensões de MEF. Para obter mais informações, consulte [Walkthrough: implementando trechos de código](../../extensibility/walkthrough-implementing-code-snippets.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor o mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

## <a name="managed-package-framework-support-for-code-snippets"></a>Suporte à estrutura de pacote gerenciado para trechos de código
 A MPF (estrutura de pacote gerenciada) dá suporte à maioria das funcionalidades de trecho de código, desde a leitura do modelo até a inserção do trecho e a habilitação do modo de edição especial. O suporte é gerenciado por meio da <xref:Microsoft.VisualStudio.Package.ExpansionProvider> classe.

 Quando a <xref:Microsoft.VisualStudio.Package.Source> classe é instanciada, o <xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe é chamado para obter um <xref:Microsoft.VisualStudio.Package.ExpansionProvider> objeto (Observe que a classe base <xref:Microsoft.VisualStudio.Package.LanguageService> sempre retorna um novo <xref:Microsoft.VisualStudio.Package.ExpansionProvider> objeto para cada <xref:Microsoft.VisualStudio.Package.Source> objeto).

 O MPF não oferece suporte a funções de expansão. Uma função de expansão é uma função nomeada que é inserida em um modelo de trecho e retorna um ou mais valores a serem colocados em um campo. Os valores são retornados pelo próprio serviço de linguagem por meio de um <xref:Microsoft.VisualStudio.Package.ExpansionFunction> objeto. O <xref:Microsoft.VisualStudio.Package.ExpansionFunction> objeto deve ser implementado pelo serviço de linguagem para dar suporte a funções de expansão.

## <a name="providing-support-for-code-snippets"></a>Fornecendo suporte para trechos de código
 Para habilitar o suporte para trechos de código, você deve fornecer ou instalar os trechos e deve fornecer os meios para que o usuário insira esses trechos. Há três etapas para habilitar o suporte para trechos de código:

1. Instalando os arquivos de trecho de código.

2. Habilitando trechos de código para seu serviço de idioma.

3. Invocando o <xref:Microsoft.VisualStudio.Package.ExpansionProvider> objeto.

### <a name="installing-the-snippet-files"></a>Instalando os arquivos de trecho de código
 Todos os trechos de código de um idioma são armazenados como modelos em arquivos XML, normalmente um modelo de trecho por arquivo. Para obter detalhes sobre o esquema XML usado para modelos de trecho de código, consulte [referência de esquema de trechos de código](../../ide/code-snippets-schema-reference.md). Cada modelo de trecho de código é identificado com uma ID de idioma. Essa ID de idioma é especificada no registro e é colocada no `Language` atributo da \<Code> marca no modelo.

 Normalmente, há dois locais em que os arquivos de modelo de trecho são armazenados: 1) em que o idioma foi instalado e 2) na pasta do usuário. Esses locais são adicionados ao registro para que o **Gerenciador de trechos de código** do Visual Studio possa encontrar os trechos. A pasta do usuário é onde os trechos de código criados pelo usuário são armazenados.

 O layout de pasta típico para os arquivos de modelo de trecho instalados é semelhante a este: *[InstallRoot]* \\ *[TestLanguage]* \Snippets \\ *[LCID]* \Snippets.

 *[InstallRoot]* é a pasta na qual seu idioma está instalado.

 *[TestLanguage]* é o nome do seu idioma como um nome de pasta.

 *[LCID]* é a ID de localidade. É assim que as versões localizadas dos trechos de código são armazenadas. Por exemplo, a ID de localidade para inglês é 1033, portanto, *[LCID]* é substituído por 1033.

 Um arquivo adicional deve ser fornecido e é um arquivo de índice, normalmente chamado de SnippetsIndex.xml ou de ExpansionsIndex.xml (você pode usar qualquer nome de arquivo válido que termine em. xml). Normalmente, esse arquivo é armazenado na pasta *[InstallRoot]* \\ *[TestLanguage]* e especifica o local exato da pasta de trechos de código, bem como a ID de idioma e o GUID do serviço de idioma que usa os trechos de código. O caminho exato do arquivo de índice é colocado no registro, conforme descrito posteriormente em "Instalando as entradas do registro". Aqui está um exemplo de um arquivo de SnippetsIndex.xml:

```
<?xml version="1.0" encoding="utf-8" ?>
<SnippetCollection>
    <Language Lang="Testlanguage" Guid="{b614a40a-80d9-4fac-a6ad-fc2868fff7cd}">
        <SnippetDir>
            <OnOff>On</OnOff>
            <Installed>true</Installed>
            <Locale>1033</Locale>
            <DirPath>%InstallRoot%\TestLanguage\Snippets\%LCID%\Snippets\</DirPath>
            <LocalizedName>Snippets</LocalizedName>
        </SnippetDir>
    </Language>
</SnippetCollection>
```

 A \<Language> marca especifica a ID do idioma (o `Lang` atributo) e o GUID do serviço de idioma.

 Este exemplo pressupõe que você instalou o serviço de idioma na pasta de instalação do Visual Studio. O% LCID% é substituído pela ID de localidade atual do usuário. Várias \<SnippetDir> marcas podem ser adicionadas, uma para cada diretório e localidade diferentes. Além disso, uma pasta de trecho de código pode conter subpastas, cada uma identificada no arquivo de índice com a \<SnippetSubDir> marca que é inserida em uma \<SnippetDir> marca.

 Os usuários também podem criar seus próprios trechos de código para seu idioma. Normalmente, eles são armazenados na pasta de configurações do usuário, por exemplo, *[TestDocs]* \Code Snippets \\ *[TestLanguage]* \test trechos de código, em que *[TestDocs]* é o local da pasta de configurações do usuário para o Visual Studio.

 Os seguintes elementos de substituição podem ser colocados no caminho armazenado na \<DirPath> marca no arquivo de índice.

|Elemento|Descrição|
|-------------|-----------------|
|LCID|ID da localidade.|
|InstallRoot|Pasta de instalação raiz do Visual Studio, por exemplo, C:\Program Files\Microsoft Visual Studio 8.|
|%ProjDir%|Pasta que contém o projeto atual.|
|%ProjItem%|Pasta que contém o item de projeto atual.|
|%TestDocs%|Na pasta configurações do usuário, por exemplo, C:\Documents and Settings \\ *[nome de usuário]* \Meus Documentos\Visual Studio\8.|

### <a name="enabling-code-snippets-for-your-language-service"></a>Habilitando trechos de código para seu serviço de idioma
 Você pode habilitar trechos de código para seu serviço de idioma adicionando o <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute> atributo ao seu VSPackage (consulte [registrando um serviço de idioma herdado](../../extensibility/internals/registering-a-legacy-language-service1.md) para obter detalhes). Os <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute.ShowRoots%2A> <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute.SearchPaths%2A> parâmetros e são opcionais, mas você deve incluir o `SearchPaths` parâmetro nomeado para informar o **Gerenciador de trechos de código** do local dos trechos.

 Veja a seguir um exemplo de como usar esse atributo:

```
[ProvideLanguageCodeExpansion(
         typeof(TestSnippetLanguageService),
         "Test Snippet Language",          // Name of language used as registry key
         0,                               // Resource ID of localized name of language service
         "Test Snippet Language",        // Name of Language attribute in snippet template
         @"%InstallRoot%\Test Snippet Language\Snippets\%LCID%\SnippetsIndex.xml",  // Path to snippets index
         SearchPaths = @"%InstallRoot%\Test Snippet Language\Snippets\%LCID%\")]    // Path to snippets
```

### <a name="calling-the-expansion-provider"></a>Chamando o provedor de expansão
 O serviço de linguagem controla a inserção de qualquer trecho de código, bem como a inserção de como é invocada.

## <a name="calling-the-expansion-provider-for-code-snippets"></a>Chamando o provedor de expansão para trechos de código
 Há duas maneiras de invocar o provedor de expansão: usando um comando de menu ou usando um atalho de uma lista de conclusão.

### <a name="inserting-a-code-snippet-by-using-a-menu-command"></a>Inserindo um trecho de código usando um comando de menu
 Para usar um comando de menu para exibir o navegador de trechos de código, você adiciona um comando de menu e, em seguida, chama o <xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A> método na <xref:Microsoft.VisualStudio.Package.ExpansionProvider> interface em resposta a esse comando de menu.

1. Adicione um comando e um botão ao seu arquivo. vsct. Você pode encontrar instruções para fazer isso na [criação de uma extensão com um comando de menu](../../extensibility/creating-an-extension-with-a-menu-command.md).

2. Derive uma classe da <xref:Microsoft.VisualStudio.Package.ViewFilter> classe e substitua o <xref:Microsoft.VisualStudio.Package.ViewFilter.QueryCommandStatus%2A> método para indicar suporte para o novo comando de menu. Este exemplo sempre habilita o comando de menu.

    ```csharp
    using Microsoft.VisualStudio.Package;

    namespace TestLanguagePackage
    {
        class TestViewFilter : ViewFilter
        {
            public TestViewFilter(CodeWindowManager mgr, IVsTextView view)
                : base(mgr, view)
            {
            }

            protected override int QueryCommandStatus(ref Guid guidCmdGroup,
                                                      uint nCmdId)
            {
                int hr = base.QueryCommandStatus(ref guidCmdGroup, nCmdId);
                // If the base class did not recognize the command then
                // see if we can handle the command.
                if (hr == (int)Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_UNKNOWNGROUP)
                {
                    if (guidCmdGroup == GuidList.guidTestLanguagePackageCmdSet)
                    {
                        if (nCmdId == PkgCmdIDList.InvokeCodeSnippetsBrowser)
                        {
                            hr = (int)(OLECMDF.OLECMDF_SUPPORTED | OLECMDF.OLECMDF_ENABLED);
                        }
                    }
                }
                return hr;
            }
        }
    }
    ```

3. Substitua o <xref:Microsoft.VisualStudio.Package.ViewFilter.HandlePreExec%2A> método na <xref:Microsoft.VisualStudio.Package.ViewFilter> classe para obter o <xref:Microsoft.VisualStudio.Package.ExpansionProvider> objeto e chamar o <xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A> método nesse objeto.

    ```csharp
    using Microsoft.VisualStudio.Package;

    namespace TestLanguagePackage
    {
        class TestViewFilter : ViewFilter
        {
            public override bool HandlePreExec(ref Guid guidCmdGroup,
                                               uint nCmdId,
                                               uint nCmdexecopt,
                                               IntPtr pvaIn,
                                               IntPtr pvaOut)
            {
                if (base.HandlePreExec(ref guidCmdGroup,
                                       nCmdId,
                                       nCmdexecopt,
                                       pvaIn,
                                       pvaOut))
                {
                    // Base class handled the command.  Do nothing more here.
                    return true;
                }

                if (guidCmdGroup == GuidList.guidTestLanguagePackageCmdSet)
                {
                    if (nCmdId == PkgCmdIDList.InvokeCodeSnippetsBrowser)
                    {
                        ExpansionProvider ep = this.GetExpansionProvider();
                        if (this.TextView != null && ep != null)
                        {
                            bool bDisplayed = ep.DisplayExpansionBrowser(
                                this.TextView,
                                "TestLanguagePackage Snippet:",
                                null,
                                false,
                                null,
                                false);
                        }
                        return true;   // Handled the command.
                    }
                }
                return false;   // Did not handle the command.
            }
        }
    }

    ```

     Os métodos a seguir na <xref:Microsoft.VisualStudio.Package.ExpansionProvider> classe são chamados pelo Visual Studio na ordem determinada durante o processo de inserção do trecho de código:

4. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnItemChosen%2A>

5. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>

6. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>

7. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>

8. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>

     Depois que o <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A> método é chamado, o trecho de código foi inserido e o <xref:Microsoft.VisualStudio.Package.ExpansionProvider> objeto está em um modo de edição especial usado para modificar um trecho de código que acabou de ser inserido.

### <a name="inserting-a-code-snippet-by-using-a-shortcut"></a>Inserindo um trecho de código usando um atalho
 A implementação de um atalho de uma lista de conclusão é muito mais envolvida do que a implementação de um comando de menu. Primeiro, você deve adicionar atalhos de trecho à lista de preenchimento de palavra do IntelliSense. Em seguida, você deve detectar quando um nome de atalho de trecho de código foi inserido como resultado da conclusão. Por fim, você deve obter o título e o caminho do trecho de código usando o nome do atalho e passar essas informações para o <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> método no <xref:Microsoft.VisualStudio.Package.ExpansionProvider> método.

 Para adicionar atalhos de trecho à lista de preenchimento de palavras, adicione-os ao <xref:Microsoft.VisualStudio.Package.Declarations> objeto em sua <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe. Você deve certificar-se de que você possa identificar o atalho como um nome de trecho de código. Para obter um exemplo, consulte [Walkthrough: obtendo uma lista de trechos de código instalados (implementação herdada)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md).

 Você pode detectar a inserção do atalho de trecho de código no <xref:Microsoft.VisualStudio.Package.Declarations.OnAutoComplete%2A> método da <xref:Microsoft.VisualStudio.Package.Declarations> classe. Como o nome do trecho de código já foi inserido no arquivo de origem, ele deve ser removido quando a expansão é inserida. O <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> método usa um Span que descreve o ponto de inserção para o trecho de código; se a extensão incluir o nome inteiro do trecho no arquivo de origem, esse nome será substituído pelo trecho.

 Aqui está uma versão de uma <xref:Microsoft.VisualStudio.Package.Declarations> classe que manipula a inserção de trecho de código dado um nome de atalho. Outros métodos na <xref:Microsoft.VisualStudio.Package.Declarations> classe foram omitidos para maior clareza. Observe que o construtor dessa classe usa um <xref:Microsoft.VisualStudio.Package.LanguageService> objeto. Isso pode ser passado de sua versão do <xref:Microsoft.VisualStudio.Package.AuthoringScope> objeto (por exemplo, sua implementação da <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe pode levar o <xref:Microsoft.VisualStudio.Package.LanguageService> objeto em seu construtor e passar esse objeto para seu `TestDeclarations` Construtor de classe).

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    internal class TestDeclarations : Declarations
    {
        private ArrayList       declarations;
        private LanguageService languageService;
        private TextSpan        commitSpan;

        public TestDeclarations(LanguageService langService)
            : base()
        {
            languageService = langService;
            declarations = new ArrayList();
        }

        // This method is used to add declarations to the internal list.
        public void AddDeclaration(TestDeclaration declaration)
        {
            declarations.Add(declaration);
        }

        // This method is called to get the string to commit to the source buffer.
        // Note that the initial extent is only what the user has typed so far.
        public override string OnCommit(IVsTextView textView,
                                        string textSoFar,
                                        char commitCharacter,
                                        int index,
                                        ref TextSpan initialExtent)
        {
            // We intercept this call only to get the initial extent
            // of what was committed to the source buffer.
            commitSpan = initialExtent;

            return base.OnCommit(textView,
                                 textSoFar,
                                 commitCharacter,
                                 index,
                                 ref initialExtent);
        }

        // This method is called after the string has been committed to the source buffer.
        public override char OnAutoComplete(IVsTextView textView,
                                            string committedText,
                                            char commitCharacter,
                                            int index)
        {
            TestDeclaration item = declarations[index] as TestDeclaration;
            if (item != null)
            {
                // In this example, TestDeclaration identifies types with a string.
                // You can choose a different approach.
                if (item.Type == "snippet")
                {
                    Source src = languageService.GetSource(textView);
                    if (src != null)
                    {
                        ExpansionProvider ep = src.GetExpansionProvider();
                        if (ep != null)
                        {
                            string title;
                            string path;
                            int commitLength = commitSpan.iEndIndex - commitSpan.iStartIndex;
                            if (commitLength < committedText.Length)
                            {
                                // Replace everything that was inserted
                                // so calculate the span of the full
                                // insertion, taking into account what
                                // was inserted when the commitSpan
                                // was obtained in the first place.
                                commitSpan.iEndIndex += (committedText.Length - commitLength);
                            }

                            if (ep.FindExpansionByShortcut(textView,
                                                           committedText,
                                                           commitSpan,
                                                           true,
                                                           out title,
                                                           out path))
                            {
                                ep.InsertNamedExpansion(textView,
                                                        title,
                                                        path,
                                                        commitSpan,
                                                        false);
                            }
                        }
                    }
                }
            }
            return '\0';
        }
    }
}
```

 Quando o serviço de linguagem Obtém o nome do atalho, ele chama o <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FindExpansionByShortcut%2A> método para obter o nome de arquivo e o título do trecho de código. Em seguida, o serviço de linguagem chama o <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> método na <xref:Microsoft.VisualStudio.Package.ExpansionProvider> classe para inserir o trecho de código. Os métodos a seguir são chamados pelo Visual Studio na ordem especificada na <xref:Microsoft.VisualStudio.Package.ExpansionProvider> classe durante o processo de inserção do trecho de código:

1. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>

2. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>

3. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>

4. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>

   Para obter mais informações sobre como obter uma lista de trechos de código instalados para seu serviço de idioma, consulte [passo a passos: obtendo uma lista de trechos de código instalados (implementação herdada)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md).

## <a name="implementing-the-expansionfunction-class"></a>Implementando a classe ExpansionFunction
 Uma função de expansão é uma função nomeada que é inserida em um modelo de trecho e retorna um ou mais valores a serem colocados em um campo. Para dar suporte a funções de expansão em seu serviço de idioma, você deve derivar uma classe da <xref:Microsoft.VisualStudio.Package.ExpansionFunction> classe e implementar o <xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetCurrentValue%2A> método. Em seguida, você deve substituir o <xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe para retornar uma nova instanciação da sua versão da <xref:Microsoft.VisualStudio.Package.ExpansionFunction> classe para cada função de expansão com suporte. Se você oferecer suporte a uma lista de valores possíveis de uma função de expansão, você também deverá substituir o <xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetIntellisenseList%2A> método na <xref:Microsoft.VisualStudio.Package.ExpansionFunction> classe para retornar uma lista desses valores.

 Uma função de expansão que usa argumentos ou precisa acessar outros campos não deve ser associada a um campo editável, pois o provedor de expansão pode não ser totalmente inicializado pelo tempo que a função de expansão é chamada. Como resultado, a função de expansão não é capaz de obter o valor de seus argumentos ou de qualquer outro campo.

### <a name="example"></a>Exemplo
 Aqui está um exemplo de como uma função de expansão simples chamada `GetName` pode ser implementada. Essa função de expansão acrescenta um número a um nome de classe base cada vez que a função de expansão é instanciada (que corresponde a cada vez que o trecho de código associado é inserido).

```csharp
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private int classNameCounter = 0;

        public override ExpansionFunction CreateExpansionFunction(
            ExpansionProvider provider,
            string functionName)
        {
            ExpansionFunction function = null;
            if (functionName == "GetName")
            {
                ++classNameCounter;
                function = new TestGetNameExpansionFunction(provider, classNameCounter);
            }
            return function;
        }
    }

    internal class TestGetNameExpansionFunction : ExpansionFunction
    {
        private int nameCount;

        TestGetNameExpansionFunction(ExpansionProvider provider, int counter)
            : base(provider)
        {
            nameCount = counter;
        }

        public override string GetCurrentValue()
        {
            string name = "TestClass";
            name += nameCount.ToString();
            return name;
        }
    }
}
```

## <a name="see-also"></a>Confira também
- [Recursos do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-features1.md)
- [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)
- [Snippets de código](../../ide/code-snippets.md)
- [Passo a passo: Obtendo uma lista de snippets de código instalados (implementação herdada)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)
