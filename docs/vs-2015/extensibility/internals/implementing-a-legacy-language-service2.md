---
title: Implementando uma função de linguagem herdado2 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- language services [managed package framework], implementing
ms.assetid: 5bcafdc5-f922-48f6-a12e-6c8507a79a05
caps.latest.revision: 27
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: b6c84a848d75302f5744e812e43a1bd7979472e7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51753919"
---
# <a name="implementing-a-legacy-language-service"></a>Implementando um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Para implementar um serviço de linguagem usando a estrutura de pacote gerenciado (MPF), você deve derivar uma classe a partir de <xref:Microsoft.VisualStudio.Package.LanguageService> classe e implementar os seguintes métodos abstratos e as propriedades:  
  
- O método <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>  
  
- O método <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>  
  
- O método <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>  
  
- A propriedade <xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A>  
  
  Consulte as seções apropriadas abaixo para obter detalhes sobre como implementar esses métodos e propriedades.  
  
  Para dar suporte a recursos adicionais, o serviço de linguagem pode ter que derivar uma classe de uma das classes de serviço de linguagem MPF; Por exemplo, para dar suporte a comandos de menu adicionais, você deve derivar uma classe a partir o <xref:Microsoft.VisualStudio.Package.ViewFilter> de classe e substituir vários do métodos de manipulação de comando (consulte <xref:Microsoft.VisualStudio.Package.ViewFilter> para obter detalhes). O <xref:Microsoft.VisualStudio.Package.LanguageService> classe fornece vários métodos que são chamados para criar novas instâncias de várias classes e você substituir o método de criação apropriado para fornecer uma instância de sua classe. Por exemplo, você precisa substituir os <xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe para retornar uma instância do seu próprio <xref:Microsoft.VisualStudio.Package.ViewFilter> classe. Consulte a seção "Criando uma instância de Classes personalizadas" para obter mais detalhes.  
  
  O serviço de linguagem também pode fornecer seus próprios ícones, que são usadas em muitos lugares. Por exemplo, quando uma lista de conclusão do IntelliSense é exibida, cada item na lista pode ter um ícone associado a ele, o item de marcação como método, classe, namespace, propriedade, ou que for necessário para sua linguagem. Esses ícones são usados em todas as listas do IntelliSense, o **barra de navegação**e, nas **lista de erros** janela de tarefas. Consulte a seção "Imagens de serviço de linguagem" abaixo para obter detalhes.  
  
## <a name="getlanguagepreferences-method"></a>Método GetLanguagePreferences  
 O <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> método sempre retorna a mesma instância de um <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe. Você pode usar a base <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe se você não precisa quaisquer preferências adicionais para seu serviço de linguagem. As classes de serviço de linguagem MPF supor que a presença de pelo menos a base de dados de <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe.  
  
### <a name="example"></a>Exemplo  
 Este exemplo mostra uma implementação típica do <xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A> método. Este exemplo usa a base de <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe.  
  
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
  
## <a name="getscanner-method"></a>Método GetScanner  
 Esse método retorna uma instância de um <xref:Microsoft.VisualStudio.Package.IScanner> objeto que implementa um analisador orientada por linha ou um scanner usado para a obtenção de tokens e seus tipos e gatilhos. Este verificador é usado no <xref:Microsoft.VisualStudio.Package.Colorizer> classe para colorização, embora o scanner também pode ser usado para obter os gatilhos e tipos de token como um prelúdio para uma operação de análise mais complexa. Você deve fornecer a classe que implementa o <xref:Microsoft.VisualStudio.Package.IScanner> interface e você deve implementar todos os métodos de <xref:Microsoft.VisualStudio.Package.IScanner> interface.  
  
### <a name="example"></a>Exemplo  
 Este exemplo mostra uma implementação típica do <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> método. O `TestScanner` classe implementa o <xref:Microsoft.VisualStudio.Package.IScanner> interface (não mostrado).  
  
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
  
## <a name="parsesource-method"></a>Método ParseSource  
 Analisa o arquivo de origem com base em uma série de motivos diferentes. Esse método recebe um <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto que descreve o que é esperado de uma determinada operação de análise. O <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método invoca um analisador mais complexo que determina o escopo e a funcionalidade de token. O <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método é usado no suporte para operações do IntelliSense, bem como correspondência de chaves. Mesmo se você não suportam tais operações avançadas, você ainda deve retornar um válido <xref:Microsoft.VisualStudio.Package.AuthoringScope> objeto e que exige que você crie uma classe que implementa o <xref:Microsoft.VisualStudio.Package.AuthoringScope> de interface e implementar todos os métodos nessa interface. Você pode retornar valores nulos de todos os métodos, mas o <xref:Microsoft.VisualStudio.Package.AuthoringScope> objeto em si não deve ser um valor nulo.  
  
### <a name="example"></a>Exemplo  
 Este exemplo mostra uma implementação mínima dos <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método e o <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe, suficiente para permitir que o serviço de linguagem compilar e funcionar sem, na verdade, que dão suporte a qualquer um dos recursos mais avançados.  
  
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
 Essa propriedade retorna o nome do serviço de linguagem. Isso deve ser o mesmo nome fornecido quando o serviço de linguagem foi registrado. Esse nome é usado em vários locais, é o mais proeminente de <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe em que o nome é usado para acessar o registro. O nome retornado por essa propriedade não deve ser localizado, pois ele será usado para a entrada do registro e nomes de chave no registro.  
  
### <a name="example"></a>Exemplo  
 Este exemplo mostra uma possível implementação de <xref:Microsoft.VisualStudio.Package.LanguageService.Name%2A> propriedade. Observe que aqui o nome é embutido em código: o nome real deve ser obtido de um arquivo de recurso para que possa ser usado no registro de um serviço de linguagem (consulte [registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)).  
  
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
  
## <a name="instantiating-custom-classes"></a>Criando uma instância de Classes personalizadas  
 Os seguintes métodos nas classes especificados podem ser substituídos para fornecer instâncias de suas próprias versões de cada classe.  
  
### <a name="in-the-languageservice-class"></a>Na classe LanguageService  
  
|Método|Classe retornado|Descrição|  
|------------|--------------------|-----------------|  
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateCodeWindowManager%2A>|<xref:Microsoft.VisualStudio.Package.CodeWindowManager>|Para dar suporte a adições personalizadas para o modo de texto.|  
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDocumentProperties%2A>|<xref:Microsoft.VisualStudio.Package.DocumentProperties>|Para dar suporte a propriedades personalizadas do documento.|  
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A>|<xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars>|Para dar suporte a **barra de navegação**.|  
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionFunction>|Para dar suporte a funções no modelo de trecho de código.|  
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A>|<xref:Microsoft.VisualStudio.Package.ExpansionProvider>|Para dar suporte a trechos de código (esse método normalmente não será substituído).|  
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateParseRequest%2A>|<xref:Microsoft.VisualStudio.Package.ParseRequest>|Para dar suporte à personalização do <xref:Microsoft.VisualStudio.Package.ParseRequest> estrutura (esse método normalmente não será substituído).|  
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateSource%2A>|<xref:Microsoft.VisualStudio.Package.Source>|Para dar suporte à formatação código-fonte, especificando os caracteres de comentário e personalização de assinaturas de método.|  
|<xref:Microsoft.VisualStudio.Package.LanguageService.CreateViewFilter%2A>|<xref:Microsoft.VisualStudio.Package.ViewFilter>|Para dar suporte a comandos de menu adicionais.|  
|<xref:Microsoft.VisualStudio.Package.Source.GetColorizer%2A>|<xref:Microsoft.VisualStudio.Package.Colorizer>|Para dar suporte a realce de sintaxe (esse método normalmente não será substituído).|  
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetLanguagePreferences%2A>|<xref:Microsoft.VisualStudio.Package.LanguagePreferences>|Para dar suporte ao acesso às preferências de idioma. Esse método deve ser implementado, mas pode retornar uma instância da classe base.|  
|<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>|<xref:Microsoft.VisualStudio.Package.IScanner>|Para fornecer um analisador usado para identificar os tipos de tokens em uma linha. Esse método deve ser implementado e <xref:Microsoft.VisualStudio.Package.IScanner> deve ser derivado de.|  
|<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringScope>|Para fornecer um analisador usado para identificar a funcionalidade e o escopo em todo um arquivo de origem inteira. Esse método deve ser implementado e deve retornar uma instância de sua versão do <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe. Se tudo o que você deseja dar suporte é realce de sintaxe (que exige o <xref:Microsoft.VisualStudio.Package.IScanner> analisador retornado do <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> método), você pode fazer nada nesse método que não seja o retorno de uma versão do <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe cujos métodos todos retornam valores nulos.|  
  
### <a name="in-the-source-class"></a>Na classe de origem  
  
|Método|Classe retornado|Descrição|  
|------------|--------------------|-----------------|  
|<xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A>|<xref:Microsoft.VisualStudio.Package.CompletionSet>|Para personalizar a exibição de listas de conclusão do IntelliSense (esse método normalmente não será substituído).|  
|<xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A>|<xref:Microsoft.VisualStudio.Package.DocumentTask>|Para dar suporte a marcadores na lista de tarefas da lista de erros; Especificamente, suporte para recursos além da abertura do arquivo e saltar para a linha que causou o erro.|  
|<xref:Microsoft.VisualStudio.Package.Source.CreateMethodData%2A>|<xref:Microsoft.VisualStudio.Package.MethodData>|Para personalizar a exibição de dica de ferramenta de informações de parâmetro IntelliSense.|  
|<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A>|<xref:Microsoft.VisualStudio.Package.CommentInfo>|Para dar suporte a comentários de código.|  
|<xref:Microsoft.VisualStudio.Package.Source.CreateAuthoringSink%2A>|<xref:Microsoft.VisualStudio.Package.AuthoringSink>|Para coletar informações durante a operação de análise.|  
  
### <a name="in-the-authoringscope-class"></a>Na classe AuthoringScope  
  
|Método|Classe retornado|Descrição|  
|------------|--------------------|-----------------|  
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A>|<xref:Microsoft.VisualStudio.Package.Declarations>|Fornece uma lista de declarações, como tipos ou membros. Esse método deve ser implementado, mas pode retornar um valor nulo. Se este método retorna um objeto válido, o objeto deve ser uma instância de sua versão do <xref:Microsoft.VisualStudio.Package.Declarations> classe.|  
|<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetMethods%2A>|<xref:Microsoft.VisualStudio.Package.Methods>|Fornece uma lista de assinaturas de método para um determinado contexto. Esse método deve ser implementado, mas pode retornar um valor nulo. Se este método retorna um objeto válido, o objeto deve ser uma instância de sua versão do <xref:Microsoft.VisualStudio.Package.Methods> classe.|  
  
## <a name="language-service-images"></a>Imagens do serviço de linguagem  
 Para fornecer uma lista de ícones a serem usados em todo o serviço de linguagem, substitua os <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe e retornar um <xref:System.Windows.Forms.ImageList> que contém os ícones. A base de <xref:Microsoft.VisualStudio.Package.LanguageService> classe carrega um conjunto de ícones padrão. Uma vez que você especifique o índice de imagem exata nesses locais que precisam de ícones, como você organiza sua própria lista de imagens é integralmente com você.  
  
### <a name="images-used-in-intellisense-completion-lists"></a>Imagens usadas em listas de conclusão do IntelliSense  
 Para listas de conclusão do IntelliSense, o índice de imagem é especificado para cada item na <xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A> método da <xref:Microsoft.VisualStudio.Package.Declarations> classe, que você deve substituir se você quiser fornecer um índice de imagem. O valor retornado do <xref:Microsoft.VisualStudio.Package.Declarations.GetGlyph%2A> método é um índice na lista de imagens fornecido para o <xref:Microsoft.VisualStudio.Package.CompletionSet> construtor de classe e que é a mesma lista de imagem retornados da <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> método no <xref:Microsoft.VisualStudio.Package.LanguageService> classe (você pode alterar qual lista de imagens para usar para o <xref:Microsoft.VisualStudio.Package.CompletionSet> se você substituir o <xref:Microsoft.VisualStudio.Package.Source.CreateCompletionSet%2A> método no <xref:Microsoft.VisualStudio.Package.Source> classe para fornecer uma lista de imagens diferentes).  
  
### <a name="images-used-in-the-navigation-bar"></a>Imagens usadas na barra de navegação  
 O **barra de navegação** exibe listas de tipos e membros e é usado para navegação rápida pode mostrar ícones. Esses ícones são obtidos a partir de <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> de classe e não pode ser substituído especificamente para o **barra de navegação**. Os índices usados para cada item nas caixas de combinação são especificados quando as listas que representa as caixas de combinação são preenchidas a <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> método na <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> classe (consulte [suporte para a barra de navegação em um serviço de linguagem herdado](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)). Esses índices de imagem são obtidos de alguma forma, o analisador, normalmente por meio de sua versão do <xref:Microsoft.VisualStudio.Package.Declarations> classe. Como os índices são obtidos cabe a você.  
  
### <a name="images-used-in-the-error-list-task-window"></a>Imagens usadas na janela de tarefas da lista de erros  
 Sempre que o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> analisador de método (consulte [analisador de serviço de linguagem herdado e o Scanner](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)) encontra um erro e passa esse erro para o <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A> método no <xref:Microsoft.VisualStudio.Package.AuthoringSink> classe, o erro é relatado no  **Lista de erros** janela de tarefas. Um ícone pode ser associado a cada item que aparece na janela de tarefas e esse ícone é fornecido na mesma lista de imagem retornada do <xref:Microsoft.VisualStudio.Package.LanguageService.GetImageList%2A> método no <xref:Microsoft.VisualStudio.Package.LanguageService> classe. O comportamento padrão das classes MPF é não mostrar uma imagem com a mensagem de erro. No entanto, você pode substituir esse comportamento derivando uma classe do <xref:Microsoft.VisualStudio.Package.Source> classe e substituir o <xref:Microsoft.VisualStudio.Package.Source.CreateErrorTaskItem%2A> método. Nesse método, você cria um novo <xref:Microsoft.VisualStudio.Package.DocumentTask> objeto. Antes de retornar esse objeto, você pode usar o <xref:Microsoft.VisualStudio.Shell.Task.ImageIndex%2A> propriedade no <xref:Microsoft.VisualStudio.Package.DocumentTask> objeto para definir o índice de imagem. Isso seria algo parecido com o exemplo a seguir. Observe que `TestIconImageIndex` é uma enumeração que lista todos os ícones e é específico para este exemplo. Você pode ter uma maneira diferente de identificação de ícones em seu serviço de linguagem.  
  
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
            TastPriority      priority,  
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
  
## <a name="the-default-image-list-for-a-language-service"></a>A lista de imagens padrão para um serviço de linguagem  
 A lista de imagens padrão fornecida com as classes de serviço de linguagem MPF base contém um número de ícones associados com os elementos de linguagem mais comuns. A maior parte desses ícones são organizadas em conjuntos de seis variações, os conceitos de acesso do público, interno, amigo, protegido, privado e o atalho correspondente. Por exemplo, você pode ter diferentes ícones para um método dependendo se ela é pública, protegida ou privada.  
  
 A enumeração a seguir especifica nomes típicos para cada conjunto de ícones e especifica o índice associado. Por exemplo, baseada na enumeração, você pode especificar o índice de imagem para um método protegido como `(int)IconImageIndex.Method + (int)IconImageIndex.AccessProtected`. Você pode alterar os nomes nesta enumeração conforme desejado.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Implementando um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service1.md)   
 [Visão geral do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-overview.md)   
 [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)   
 [Analisador e scanner do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

