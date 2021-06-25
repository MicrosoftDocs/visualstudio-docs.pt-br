---
title: Implementando uma linguagem herdada Service2 | Microsoft Docs
description: Saiba como implementar um serviço de linguagem herdado que dá suporte a recursos de serviço de linguagem estendida, usando o MPF (estrutura de pacote gerenciada). Parte 2 de 2.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- language services [managed package framework], implementing
ms.assetid: 5bcafdc5-f922-48f6-a12e-6c8507a79a05
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fca2548ddb0c8281241b14de0ec470cfe22db1a1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900116"
---
# <a name="implementing-a-legacy-language-service-2"></a>Implementando um serviço de linguagem herdada 2
Para implementar um serviço de linguagem usando a MPF (estrutura de pacote gerenciada), você deve derivar uma classe da <xref:Microsoft.VisualStudio.Package.LanguageService> classe e implementar os seguintes métodos e propriedades abstratos:

- O método <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>

- O método <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>

- O método <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>

- A propriedade <xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A>

  Consulte as seções apropriadas abaixo para obter detalhes sobre como implementar esses métodos e propriedades.

  Para dar suporte a recursos adicionais, o serviço de linguagem pode ter que derivar uma classe de uma das classes de serviço de idioma do MPF; por exemplo, para dar suporte a comandos de menu adicionais, você deve derivar uma classe da <xref:Microsoft.VisualStudio.Package.ViewFilter> classe e substituir vários dos métodos de manipulação de comandos (consulte <xref:Microsoft.VisualStudio.Package.ViewFilter> para obter detalhes). A <xref:Microsoft.VisualStudio.Package.LanguageService> classe fornece vários métodos que são chamados para criar novas instâncias de várias classes e você substitui o método de criação apropriado para fornecer uma instância de sua classe. Por exemplo, você precisa substituir o <xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe para retornar uma instância de sua própria <xref:Microsoft.VisualStudio.Package.ViewFilter> classe. Consulte a seção "instanciando classes personalizadas" para obter mais detalhes.

  O serviço de linguagem também pode fornecer seus próprios ícones, que são usados em muitos lugares. Por exemplo, quando uma lista de conclusão do IntelliSense é mostrada, cada item da lista pode ter um ícone associado a ele, marcando o item como um método, classe, namespace, propriedade ou o que for necessário para seu idioma. Esses ícones são usados em todas as listas do IntelliSense, na **barra de navegação** e na janela da tarefa **lista de erros** . Consulte a seção "imagens do serviço de idioma" abaixo para obter detalhes.

## <a name="getlanguagepreferences-method"></a>Método GetLanguagePreferences
 O <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> método sempre retorna a mesma instância de uma <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe. Você pode usar a <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe base se não precisar de preferências adicionais para o serviço de idioma. As classes de serviço de linguagem MPF pressupõem a presença de pelo menos a <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe base.

### <a name="example"></a>Exemplo
 Este exemplo mostra uma implementação típica do <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> método. Este exemplo usa a <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe base.

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private LanguagePreferences m_preferences;

        public override LanguagePreferences GetLanguagePreferences()
        {
            if (m_preferences == null)
            {
                m_preferences = new LanguagePreferences(this.Site,
                                                        typeof(TestLanguageService).GUID,
                                                        this.Name );
                m_preferences.Init();
            }
            return m_preferences;
        }
    }
}
```

## <a name="getscanner-method"></a>Método getscanner
 Esse método retorna uma instância de um <xref:Microsoft.VisualStudio.Package.IScanner> objeto que implementa um analisador orientado a linha ou um scanner usado para obter tokens e seus tipos e gatilhos. Esse scanner é usado na <xref:Microsoft.VisualStudio.Package.Colorizer> classe para a colorização, embora o verificador também possa ser usado para obter tipos de token e gatilhos como um prelúdio para uma operação de análise mais complexa. Você deve fornecer a classe que implementa a <xref:Microsoft.VisualStudio.Package.IScanner> interface e deve implementar todos os métodos na <xref:Microsoft.VisualStudio.Package.IScanner> interface.

### <a name="example"></a>Exemplo
 Este exemplo mostra uma implementação típica do <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> método. A `TestScanner` classe implementa a <xref:Microsoft.VisualStudio.Package.IScanner> interface (não mostrada).

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private TestScanner m_scanner;

        public override IScanner GetScanner(IVsTextLines buffer)
        {
            if (m_scanner == null)
            {
                m_scanner = new TestScanner(buffer);
            }
            return m_scanner;
        }
    }
}
    internal class TestScanner : IScanner
    {
        private IVsTextBuffer m_buffer;
        string m_source;

        public TestScanner(IVsTextBuffer buffer)
        {
            m_buffer = buffer;
        }

        bool IScanner.ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo, ref int state)
        {
            tokenInfo.Type = TokenType.Unknown;
            tokenInfo.Color = TokenColor.Text;
            return true;
        }

        void IScanner.SetSource(string source, int offset)
        {
            m_source = source.Substring(offset);
        }
    }

```

## <a name="parsesource-method"></a>Método Parse
 Analisa o arquivo de origem com base em vários motivos diferentes. Esse método recebe um <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto que descreve o que é esperado de uma operação de análise específica. O <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método invoca um analisador mais complexo que determina a funcionalidade e o escopo do token. O <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método é usado no suporte para operações do IntelliSense, bem como correspondência de chaves. Mesmo que você não dê suporte a essas operações avançadas, você ainda deve retornar um <xref:Microsoft.VisualStudio.Package.AuthoringScope> objeto válido e isso exige que você crie uma classe que implementa a <xref:Microsoft.VisualStudio.Package.AuthoringScope> interface e implemente todos os métodos nessa interface. Você pode retornar valores nulos de todos os métodos, mas o <xref:Microsoft.VisualStudio.Package.AuthoringScope> próprio objeto não deve ser um valor nulo.

### <a name="example"></a>Exemplo
 Este exemplo mostra uma implementação mínima do <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método e da <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe, o suficiente para permitir que o serviço de linguagem compile e funcione sem realmente dar suporte a qualquer um dos recursos mais avançados.

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        public override AuthoringScope ParseSource(ParseRequest req)
        {
            return new TestAuthoringScope();
        }
    }

    internal class TestAuthoringScope : AuthoringScope
    {
        public override string GetDataTipText(int line, int col, out TextSpan span)
        {
            span = new TextSpan();
            return null;
        }

        public override Declarations GetDeclarations(IVsTextView view,
                                                     int line,
                                                     int col,
                                                     TokenInfo info,
                                                     ParseReason reason)
        {
            return null;
        }

        public override string Goto(VSConstants.VSStd97CmdID cmd, IVsTextView textView, int line, int col, out TextSpan span)
        {
            span = new TextSpan();
            return null;
        }

        public override Methods GetMethods(int line, int col, string name)
        {
            return null;
        }
}
```

## <a name="name-property"></a>Propriedade Name
 Essa propriedade retorna o nome do serviço de idioma. Deve ser o mesmo nome fornecido quando o serviço de idioma foi registrado. Esse nome é usado em vários lugares, o mais proeminente deles é a <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe em que o nome é usado para acessar o registro. O nome retornado por essa propriedade não deve ser localizado, pois é usado no registro para a entrada do registro e nomes de chave.

### <a name="example"></a>Exemplo
 Este exemplo mostra uma implementação possível da <xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A> propriedade. Observe que o nome aqui é embutido em código: o nome real deve ser obtido de um arquivo de recurso para que possa ser usado no registro de um serviço de linguagem (consulte [registrando um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)).

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        public override string Name
        {
            get { return "Test Language"; }
        }
    }
}
```

## <a name="instantiating-custom-classes"></a>Instanciando classes personalizadas
 Os métodos a seguir nas classes especificadas podem ser substituídos para fornecer instâncias de suas próprias versões de cada classe.

### <a name="in-the-languageservice-class"></a>Na classe LanguageService

|Método|Classe retornada|Descrição|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateCodeWindowManager%2A>|<xref:Microsoft.VisualStudio.Package.CodeWindowManager>|Para dar suporte a adições personalizadas na exibição de texto.|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDocumentProperties%2A>|<xref:Microsoft.VisualStudio.Package.DocumentProperties>|Para dar suporte a propriedades de documento personalizadas.|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>|<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>|Para dar suporte à **barra de navegação**.|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionFunction>|Para dar suporte a funções em modelos de trecho de código.|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionProvider>|Para dar suporte a trechos de código (esse método normalmente não é substituído).|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateParseRequest%2A>|<xref:Microsoft.VisualStudio.Package.ParseRequest>|Para dar suporte à personalização da <xref:Microsoft.VisualStudio.Package.ParseRequest> estrutura (esse método normalmente não é substituído).|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateSource%2A>|<xref:Microsoft.VisualStudio.Package.Source>|Para dar suporte à formatação do código-fonte, à especificação de caracteres de comentário e à personalização de assinaturas de método.|
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A>|<xref:Microsoft.VisualStudio.Package.ViewFilter>|Para dar suporte a comandos de menu adicionais.|
|<xref:Microsoft.VisualStudio.Package.Source.GetColorizer%2A>|<xref:Microsoft.VisualStudio.Package.Colorizer>|Para dar suporte ao realce de sintaxe (esse método normalmente não é substituído).|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>|<xref:Microsoft.VisualStudio.Package.LanguagePreferences>|Para dar suporte ao acesso às preferências de idioma. Esse método deve ser implementado, mas pode retornar uma instância da classe base.|
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>|<xref:Microsoft.VisualStudio.Package.IScanner>|Para fornecer um analisador usado para identificar tipos de tokens em uma linha. Esse método deve ser implementado e <xref:Microsoft.VisualStudio.Package.IScanner> deve ser derivado de.|
|<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringScope>|Para fornecer um analisador usado para identificar a funcionalidade e o escopo em todo um arquivo de origem. Esse método deve ser implementado e deve retornar uma instância da sua versão da <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe. Se tudo o que você deseja dar suporte é o realce de sintaxe (que requer o <xref:Microsoft.VisualStudio.Package.IScanner> analisador retornado do <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> método), você pode não fazer nada nesse método além de retornar uma versão da <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe cujos métodos todos retornam valores nulos.|

### <a name="in-the-source-class"></a>Na classe de origem

|Método|Classe retornada|Descrição|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A>|<xref:Microsoft.VisualStudio.Package.CompletionSet>|Para personalizar a exibição de listas de conclusão do IntelliSense (esse método normalmente não é substituído).|
|<xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A>|<xref:Microsoft.VisualStudio.Package.DocumentTask>|Para dar suporte a marcadores na lista de tarefas Lista de Erros; especificamente, o suporte para recursos além de abrir o arquivo e saltar para a linha que causou o erro.|
|<xref:Microsoft.VisualStudio.Package.Source.CreateMethodData%2A>|<xref:Microsoft.VisualStudio.Package.MethodData>|Para personalizar a exibição de dicas de ferramenta de informações de parâmetro do IntelliSense.|
|<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A>|<xref:Microsoft.VisualStudio.Package.CommentInfo>|Para dar suporte ao código de comentário.|
|<xref:Microsoft.VisualStudio.Package.Source.CreateAuthoringSink%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringSink>|Para coletar informações durante a operação de análise.|

### <a name="in-the-authoringscope-class"></a>Na classe AuthoringScope

|Método|Classe retornada|Descrição|
|------------|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A>|<xref:Microsoft.VisualStudio.Package.Declarations>|Fornece uma lista de declarações como membros ou tipos. Esse método deve ser implementado, mas pode retornar um valor nulo. Se esse método retornar um objeto válido, o objeto deverá ser uma instância da sua versão da <xref:Microsoft.VisualStudio.Package.Declarations> classe.|
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetMethods%2A>|<xref:Microsoft.VisualStudio.Package.Methods>|Fornece uma lista de assinaturas de método para um determinado contexto. Esse método deve ser implementado, mas pode retornar um valor nulo. Se esse método retornar um objeto válido, o objeto deverá ser uma instância da sua versão da <xref:Microsoft.VisualStudio.Package.Methods> classe.|

## <a name="language-service-images"></a>Imagens de serviço de linguagem
 Para fornecer uma lista de ícones a serem usados em todo o serviço de idioma, substitua o <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe e retorne um <xref:System.Windows.Forms.ImageList> contendo os ícones. A <xref:Microsoft.VisualStudio.Package.LanguageService> classe base carrega um conjunto padrão de ícones. Como você especifica o índice de imagem exato nesses locais que precisam de ícones, a maneira de organizar sua própria lista de imagens depende inteiramente de você.

### <a name="images-used-in-intellisense-completion-lists"></a>Imagens usadas em listas de conclusão do IntelliSense
 Para listas de conclusão do IntelliSense, o índice de imagem é especificado para cada item no <xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A> método da <xref:Microsoft.VisualStudio.Package.Declarations> classe, que você deve substituir se desejar fornecer um índice de imagem. O valor retornado do <xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A> método é um índice na lista de imagens fornecido para o <xref:Microsoft.VisualStudio.Package.CompletionSet> Construtor de classe e que é a mesma lista de imagens retornada do <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe (você pode alterar a lista de imagens a ser usada para o <xref:Microsoft.VisualStudio.Package.CompletionSet> se substituir o <xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A> método na <xref:Microsoft.VisualStudio.Package.Source> classe para fornecer uma lista de imagens diferente).

### <a name="images-used-in-the-navigation-bar"></a>Imagens usadas na barra de navegação
 A **barra de navegação** exibe listas de tipos e membros e é usada para navegação rápida pode mostrar ícones. Esses ícones são obtidos do <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe e não podem ser substituídos especificamente para a **barra de navegação**. Os índices usados para cada item nas caixas de combinação são especificados quando as listas que representam as caixas de combinação são preenchidas no <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> método na <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> classe (consulte [suporte para a barra de navegação em um serviço de idioma herdado](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)). Esses índices de imagem são obtidos de alguma forma do analisador, normalmente por meio de sua versão da <xref:Microsoft.VisualStudio.Package.Declarations> classe. A forma como os índices são obtidos depende inteiramente de você.

### <a name="images-used-in-the-error-list-task-window"></a>Imagens usadas na janela tarefa de Lista de Erros
 Sempre que o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> analisador de método (consulte [analisador e verificador de serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)) encontra um erro e passa esse erro para o <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A> método na <xref:Microsoft.VisualStudio.Package.AuthoringSink> classe, o erro é relatado na janela de tarefa **lista de erros** . Um ícone pode ser associado a cada item que aparece na janela de tarefas e esse ícone vem da mesma lista de imagens retornada do <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe. O comportamento padrão das classes MPF é não mostrar uma imagem com a mensagem de erro. No entanto, você pode substituir esse comportamento derivando uma classe da <xref:Microsoft.VisualStudio.Package.Source> classe e substituindo o <xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A> método. Nesse método, você cria um novo <xref:Microsoft.VisualStudio.Package.DocumentTask> objeto. Antes de retornar esse objeto, você pode usar a <xref:Microsoft.VisualStudio.Shell.Task.ImageIndex%2A> propriedade no <xref:Microsoft.VisualStudio.Package.DocumentTask> objeto para definir o índice da imagem. Isso deve ser semelhante ao exemplo a seguir. Observe que `TestIconImageIndex` é uma enumeração que lista todos os ícones e é específica para este exemplo. Você pode ter uma maneira diferente de identificar ícones em seu serviço de idioma.

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    class TestSource : Source
    {
        public override DocumentTask CreateErrorTaskItem(
            TextSpan          span,
            string            filename,
            string            message,
            TaskPriority      priority,
            TaskCategory      category,
            MARKERTYPE        markerType,
            TaskErrorCategory errorCategory)
        {
            DocumentTask taskItem = base.CreateErrorTaskItem(
                                           span,
                                           filename,
                                           message,
                                           priority,
                                           category,
                                           markerType,
                                           errorCategory);
            if (errorCategory == TaskErrorCategory.Error)
            {
                taskItem.ImageIndex = TestIconImageIndex.Error;
            }
            return taskItem;
        }
    }
}
```

## <a name="the-default-image-list-for-a-language-service"></a>A lista de imagens padrão para um serviço de idioma
 A lista de imagens padrão fornecida com as classes de serviço de idiomas do MPF base contém vários ícones associados aos elementos de linguagem mais comuns. A maior parte desses ícones é organizada em conjuntos de seis variações, correspondentes aos conceitos de acesso de público, interno, amigo, protegido, privado e de atalho. Por exemplo, você pode ter ícones diferentes para um método, dependendo se ele é público, protegido ou privado.

 A enumeração a seguir especifica nomes típicos para cada conjunto de ícones e especifica o índice associado. Por exemplo, com base na enumeração, você pode especificar o índice de imagem para um método protegido como `(int)IconImageIndex.Method + (int)IconImageIndex.AccessProtected` . Você pode alterar os nomes dessa enumeração conforme desejado.

```csharp
public enum IconImageIndex
        {
            // access types
            AccessPublic = 0,
            AccessInternal = 1,
            AccessFriend = 2,
            AccessProtected = 3,
            AccessPrivate = 4,
            AccessShortcut = 5,

            Base = 6,
            // Each of the following icon type has 6 versions,
            //corresponding to the access types
            Class = Base + 0,
            Constant = Base + 1,
            Delegate = Base + 2,
            Enumeration = Base + 3,
            EnumMember = Base + 4,
            Event = Base + 5,
            Exception = Base + 6,
            Field = Base + 7,
            Interface = Base + 8,
            Macro = Base + 9,
            Map = Base + 10,
            MapItem = Base + 11,
            Method = Base + 12,
            OverloadedMethod = Base + 13,
            Module = Base + 14,
            Namespace = Base + 15,
            Operator = Base + 16,
            Property = Base + 17,
            Struct = Base + 18,
            Template = Base + 19,
            Typedef = Base + 20,
            Type = Base + 21,
            Union = Base + 22,
            Variable = Base + 23,
            ValueType = Base + 24,
            Intrinsic = Base + 25,
            JavaMethod = Base + 26,
            JavaField = Base + 27,
            JavaClass = Base + 28,
            JavaNamespace = Base + 29,
            JavaInterface = Base + 30,
            // Miscellaneous icons with one icon for each type.
            Error = 187,
            GreyedClass = 188,
            GreyedPrivateMethod = 189,
            GreyedProtectedMethod = 190,
            GreyedPublicMethod = 191,
            BrowseResourceFile = 192,
            Reference = 193,
            Library = 194,
            VBProject = 195,
            VBWebProject = 196,
            CSProject = 197,
            CSWebProject = 198,
            VB6Project = 199,
            CPlusProject = 200,
            Form = 201,
            OpenFolder = 202,
            ClosedFolder = 203,
            Arrow = 204,
            CSClass = 205,
            Snippet = 206,
            Keyword = 207,
            Info = 208,
            CallBrowserCall = 209,
            CallBrowserCallRecursive = 210,
            XMLEditor = 211,
            VJProject = 212,
            VJClass = 213,
            ForwardedType = 214,
            CallsTo = 215,
            CallsFrom = 216,
            Warning = 217,
        }
```

## <a name="see-also"></a>Confira também
- [Implementando um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [Visão geral do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-overview.md)
- [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)
- [Analisador e scanner do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
