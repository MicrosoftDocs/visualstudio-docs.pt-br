---
title: Suporte a trechos de código em um serviço de linguagem herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- snippets, supporting in language services
- code snippets, supporting in language services [managed package framework]
- language services [managed package framework], supporting code snippets
ms.assetid: 7490325b-acee-4c2d-ac56-1cd5db1a1083
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a7ad314e5a160ae280b33586fb7dfe1b42ec470f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49858102"
---
# <a name="support-for-code-snippets-in-a-legacy-language-service"></a>Suporte para snippets de código em um serviço de linguagem herdado
Um trecho de código é um trecho de código que é inserido no arquivo de origem. O trecho de código em si é um modelo baseado em XML com um conjunto de campos. Esses campos são realçados depois que o trecho de código é inserido e pode ter valores diferentes dependendo do contexto no qual o trecho de código é inserido. Imediatamente depois de inserir o trecho de código, o serviço de linguagem pode formatar o trecho de código.  
  
 O trecho de código é inserido em um modo de edição especial que permite que os campos do trecho de código para ser navegado usando a tecla TAB. Os campos podem dar suporte a menus suspensos de estilo de IntelliSense. O usuário confirma o trecho de código ao arquivo de origem, digitando o ENTER ou a tecla ESC. Para saber mais sobre os trechos de código, consulte [trechos de código](../../ide/code-snippets.md).  
  
 Serviços de linguagem herdado são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações, consulte [instruções passo a passo: Implementando trechos de código](../../extensibility/walkthrough-implementing-code-snippets.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitem que você tirar proveito dos novos recursos do editor.  
  
## <a name="managed-package-framework-support-for-code-snippets"></a>Suporte de estrutura de pacote de trechos de código gerenciados  
 A estrutura de pacote gerenciado (MPF) dá suporte a mais funcionalidade de trecho de código, leia o modelo para inserir o trecho de código e habilitando especiais do modo de edição. O suporte é gerenciado por meio de <xref:Microsoft.VisualStudio.Package.ExpansionProvider> classe.  
  
 Quando o <xref:Microsoft.VisualStudio.Package.Source> classe é instanciada, o <xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe é chamado para obter uma <xref:Microsoft.VisualStudio.Package.ExpansionProvider> objeto (Observe que a base <xref:Microsoft.VisualStudio.Package.LanguageService> classe sempre retorna um novo <xref:Microsoft.VisualStudio.Package.ExpansionProvider> para cada objeto <xref:Microsoft.VisualStudio.Package.Source> objeto).  
  
 MPF não oferece suporte a funções de expansão. Uma função de expansão é uma função nomeada que é inserida em um modelo de trecho de código e retorna um ou mais valores sejam colocados em um campo. Os valores são retornados pela linguagem de serviço em si por meio de um <xref:Microsoft.VisualStudio.Package.ExpansionFunction> objeto. O <xref:Microsoft.VisualStudio.Package.ExpansionFunction> objeto deve ser implementado pelo serviço de linguagem para dar suporte a funções de expansão.  
  
## <a name="providing-support-for-code-snippets"></a>Fornecendo suporte a trechos de código  
 Para habilitar o suporte de trechos de código, você deve fornecer ou instalar os trechos de código e você deve fornecer os meios para o usuário inserir os trechos de código. Há três etapas para habilitar o suporte a trechos de código:  
  
1.  Instalando os arquivos de trecho de código.  
  
2.  Habilitando os trechos de código para seu serviço de linguagem.  
  
3.  Invocar o <xref:Microsoft.VisualStudio.Package.ExpansionProvider> objeto.  
  
### <a name="installing-the-snippet-files"></a>Instalando os arquivos de trecho de código  
 Todos os trechos de código para um idioma são armazenados como modelos em arquivos XML, normalmente um modelo de trecho de código por arquivo. Para obter detalhes sobre o esquema XML usado para modelos de trecho de código, consulte [referência de esquema de trechos de código](../../ide/code-snippets-schema-reference.md). Cada modelo de trecho de código é identificado com uma ID de idioma. Essa linguagem ID é especificada no registro e é colocada na `Language` atributo do \<código > marca no modelo.  
  
 Normalmente, há dois locais onde estão armazenados os arquivos de modelo de trecho de código: 1) em que o seu idioma foi instalado e 2) na pasta do usuário. Esses locais são adicionados ao registro até que o Visual Studio **Gerenciador de trechos de código** pode encontrar os trechos de código. A pasta do usuário é onde os trechos de código criados pelo usuário são armazenados.  
  
 O layout de pasta comum para os arquivos de modelo de trecho de código instalado tem esta aparência: *[InstallRoot]*\\ *[TestLanguage]* \snippets.\\ *[LCID]* \Snippets.  
  
 *[InstallRoot]*  é a pasta que o idioma é instalado em.  
  
 *[TestLanguage]*  é o nome do seu idioma como um nome de pasta.  
  
 *[LCID]*  é a ID de localidade. Isso é que as versões localizadas como trechos de código são armazenados. Por exemplo, a ID de localidade inglês é 1033, então *[LCID]* é substituído pelo 1033.  
  
 Um arquivo adicional deve ser fornecido e que é um arquivo de índice, geralmente chamado SnippetsIndex.xml ou ExpansionsIndex.xml (você pode usar qualquer nome de arquivo válido que terminam em. xml). Normalmente, esse arquivo é armazenado na *[InstallRoot]*\\ *[TestLanguage]* pasta e especifica o local exato da pasta de trechos de código, bem como a ID de idioma e o GUID da linguagem serviço que usa os trechos de código. O caminho exato do arquivo de índice é colocado no registro, conforme descrito posteriormente em "Instalar as entradas do Registro". Aqui está um exemplo de um arquivo SnippetsIndex.xml:  
  
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
  
 O \<Language > marca Especifica a ID de idioma (o `Lang` atributo) e o GUID do serviço de linguagem.  
  
 Este exemplo pressupõe que você instalou o serviço de linguagem na pasta de instalação do Visual Studio. O % LCID % é substituído pelo ID atual localidade. do usuário Vários \<SnippetDir > marcas podem ser adicionados, um para cada diretório diferente e a localidade. Além disso, uma pasta de trecho de código pode conter subpastas, cada um deles é identificado no arquivo de índice com o \<SnippetSubDir > marca é inserida em um \<SnippetDir > marca.  
  
 Os usuários também podem criar seus próprios trechos para sua linguagem. Eles normalmente são armazenados na pasta de configurações do usuário, por exemplo *[TestDocs]* \Code trechos\\ *[TestLanguage]* \Test trechos de código, onde *[TestDocs]* é o local da pasta de configurações do usuário para o Visual Studio.  
  
 Os seguintes elementos de substituição podem ser colocados no caminho armazenado no \<DirPath > marca no arquivo de índice.  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|% LCID %|ID de localidade.|  
|% InstallRoot %|Pasta de instalação raiz para o Visual Studio, por exemplo, C:\Program Files\Microsoft Visual Studio 8.|  
|% ProjDir %|Pasta que contém o projeto atual.|  
|% ProjItem %|Pasta que contém o item de projeto atual.|  
|% TestDocs %|Na pasta de configurações do usuário, por exemplo, C:\Documents and Settings\\ *[username]* Documents\Visual Studio\8.|  
  
### <a name="enabling-code-snippets-for-your-language-service"></a>Habilitando os trechos de código para seu serviço de linguagem  
 Você pode habilitar os trechos de código para seu serviço de linguagem, adicionando a <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute> de atributo para o VSPackage (consulte [Registrando um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md) para obter detalhes). O <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute.ShowRoots%2A> e <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute.SearchPaths%2A> parâmetros são opcionais, mas você deve incluir o `SearchPaths` parâmetro nomeado para informar o **Gerenciador de trechos de código** do local dos seus trechos de código.  
  
 Este é um exemplo de como usar esse atributo:  
  
```  
[ProvideLanguageCodeExpansion(  
         typeof(TestSnippetLanguageService),  
         "Test Snippet Language",          // Name of language used as registry key  
         0,                               // Resource ID of localized name of language service  
         "Test Snippet Language",        // Name of Language attribute in snippet template  
         @"%InstallRoot%\Test Snippet Language\Snippets\%LCID%\SnippetsIndex.xml",  // Path to snippets index  
         SearchPaths = @"%InstallRoot%\Test Snippet Language\Snippets\%LCID%\")]    // Path to snippets  
```  
  
### <a name="calling-the-expansion-provider"></a>Chamar o provedor de expansão  
 O serviço de linguagem controla a inserção de qualquer trecho de código, bem como a maneira de inserção é invocada.  
  
## <a name="calling-the-expansion-provider-for-code-snippets"></a>Chamar o provedor de expansão de trechos de código  
 Há duas maneiras para chamar o provedor de expansão: usando um comando de menu ou usando um atalho de uma lista de conclusão.  
  
### <a name="inserting-a-code-snippet-by-using-a-menu-command"></a>Inserindo um trecho de código usando um comando de Menu  
 Para usar um comando de menu para exibir o navegador de trecho de código, você pode adicionar um comando de menu e, em seguida, chame o <xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A> método no <xref:Microsoft.VisualStudio.Package.ExpansionProvider> interface em resposta a esse comando de menu.  
  
1.  Adicione um comando e um botão ao arquivo. VSCT. Você pode encontrar instruções sobre como fazer isso no [criar uma extensão com um comando de Menu](../../extensibility/creating-an-extension-with-a-menu-command.md).  
  
2.  Derive uma classe do <xref:Microsoft.VisualStudio.Package.ViewFilter> de classe e substituir o <xref:Microsoft.VisualStudio.Package.ViewFilter.QueryCommandStatus%2A> método para indicar o suporte para o novo comando de menu. Este exemplo sempre permite que o comando de menu.  
  
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
  
3.  Substituir a <xref:Microsoft.VisualStudio.Package.ViewFilter.HandlePreExec%2A> método na <xref:Microsoft.VisualStudio.Package.ViewFilter> classe para obter o <xref:Microsoft.VisualStudio.Package.ExpansionProvider> objeto e chame o <xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A> método naquele objeto.  
  
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
  
     Os seguintes métodos no <xref:Microsoft.VisualStudio.Package.ExpansionProvider> classe são chamados pelo Visual Studio na ordem fornecida durante o processo de inserir o trecho de código:  
  
4.  <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnItemChosen%2A>  
  
5.  <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>  
  
6.  <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>  
  
7.  <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>  
  
8.  <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>  
  
     Após o <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A> método é chamado, o trecho de código foi inserido e o <xref:Microsoft.VisualStudio.Package.ExpansionProvider> objeto está em um modo de edição especial usado para modificar um trecho de código que foi inserido.  
  
### <a name="inserting-a-code-snippet-by-using-a-shortcut"></a>Inserindo um trecho de código usando um atalho  
 Implementação de um atalho de uma lista de conclusão é muito mais envolvida do que a implementação de um comando de menu. Primeiro, você deve adicionar atalhos de trecho de código para a lista de preenchimento de palavra do IntelliSense. Em seguida, você deve detectar quando um nome de atalho de trecho de código foi inserido como resultado da conclusão. Por fim, você deve obter o título do trecho de código e o caminho usando o nome do atalho e passar essa informação para o <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> método no <xref:Microsoft.VisualStudio.Package.ExpansionProvider> método.  
  
 Para adicionar atalhos de trecho de código para a lista de preenchimento de palavra, adicioná-los para o <xref:Microsoft.VisualStudio.Package.Declarations> do objeto no seu <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe. Certifique-se de que você pode identificar o atalho como um nome de trecho de código. Por exemplo, consulte [instruções passo a passo: obtendo uma lista de instalados trechos de código (implementação herdada)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md).  
  
 Você pode detectar a inserção do atalho de trecho de código na <xref:Microsoft.VisualStudio.Package.Declarations.OnAutoComplete%2A> método da <xref:Microsoft.VisualStudio.Package.Declarations> classe. Porque o nome do trecho de código já foi inserido no arquivo de origem, ele deverá ser removido quando a expansão é inserida. O <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> método usa uma extensão que descreve o ponto de inserção para o trecho de código; se o alcance inclui o nome do trecho de código inteira no arquivo de origem, esse nome é substituído pelo trecho de código.  
  
 Aqui está uma versão de um <xref:Microsoft.VisualStudio.Package.Declarations> classe que manipula a inserção de trecho de código recebe um nome de atalho. Outros métodos de <xref:Microsoft.VisualStudio.Package.Declarations> classe foram omitidos por motivos de clareza. Observe que o construtor dessa classe usa um <xref:Microsoft.VisualStudio.Package.LanguageService> objeto. Isso pode ser passado de sua versão do <xref:Microsoft.VisualStudio.Package.AuthoringScope> objeto (por exemplo, sua implementação do <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe pode levar a <xref:Microsoft.VisualStudio.Package.LanguageService> do objeto em seu construtor e passa esse objeto para sua `TestDeclarations` construtor de classe).  
  
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
  
 Quando o serviço de linguagem obtém o nome do atalho, ele chama o <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FindExpansionByShortcut%2A> método para obter o título do trecho de código de nome de arquivo e código. O serviço de linguagem, em seguida, chama o <xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A> método no <xref:Microsoft.VisualStudio.Package.ExpansionProvider> classe para inserir o trecho de código. Os seguintes métodos são chamados pelo Visual Studio na ordem fornecida no <xref:Microsoft.VisualStudio.Package.ExpansionProvider> classe durante o processo de inserir o trecho de código:  
  
1. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>  
  
2. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>  
  
3. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>  
  
4. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>  
  
   Para obter mais informações sobre como obter uma lista de trechos de código instalado para seu serviço de linguagem, consulte [instruções passo a passo: obtendo uma lista de instalados trechos de código (implementação herdada)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md).  
  
## <a name="implementing-the-expansionfunction-class"></a>Implementando a classe ExpansionFunction  
 Uma função de expansão é uma função nomeada que é inserida em um modelo de trecho de código e retorna um ou mais valores sejam colocados em um campo. Para dar suporte a funções de expansão em seu serviço de linguagem, você deve derivar uma classe a partir de <xref:Microsoft.VisualStudio.Package.ExpansionFunction> de classe e implementar o <xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetCurrentValue%2A> método. Em seguida, você deve substituir o <xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A> método no <xref:Microsoft.VisualStudio.Package.LanguageService> classe para retornar uma nova instanciação da sua versão do <xref:Microsoft.VisualStudio.Package.ExpansionFunction> classe para cada função de expansão que você oferece suporte. Se você oferecer suporte a uma lista de valores possíveis de uma função de expansão, você também deve substituir a <xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetIntellisenseList%2A> método no <xref:Microsoft.VisualStudio.Package.ExpansionFunction> classe para retornar uma lista desses valores.  
  
 Uma função de expansão que usa argumentos ou precisa acessar outros campos não deve ser associada um campo editável, pois o provedor de expansão pode não ser totalmente inicializado no momento em que a expansão de função é chamada. Como resultado, a função de expansão não é capaz de obter o valor de seus argumentos ou qualquer outro campo.  
  
### <a name="example"></a>Exemplo  
 Aqui está um exemplo de como uma função de expansão simples chamada `GetName` pode ser implementado. Essa função de expansão acrescenta um número para um nome de classe base sempre que a função de expansão é instanciada (que corresponde a cada vez que o trecho de código associado é inserido).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Recursos do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-features1.md)   
 [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)   
 [Snippets de código](../../ide/code-snippets.md)   
 [Passo a passo: Obter uma lista de snippets de código instalados (implementação herdada)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)