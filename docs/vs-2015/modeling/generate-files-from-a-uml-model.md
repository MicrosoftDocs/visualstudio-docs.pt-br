---
title: Gerar arquivos de um modelo UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML model, generating files
ms.assetid: 4e28b0e6-ce8f-45ee-9e3a-e4d600a0ad81
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: afbb81a67d8d5f8f587979ab8adca4251562072a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51804522"
---
# <a name="generate-files-from-a-uml-model"></a>Gerar arquivos por meio de um modelo UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em um modelo UML, você pode gerar o código do programa, esquemas, documentos, recursos e outros artefatos de qualquer tipo. Um método conveniente de geração de arquivos de texto em um modelo UML é usar [modelos de texto](../modeling/code-generation-and-t4-text-templates.md). Eles permitem que você inserir o código do programa dentro do texto que você deseja gerar.  
  
 Há três cenários principais:  
  
- [Gerando arquivos de um comando de menu](#Command) ou de gesto. Você define um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] comando que está disponível em modelos UML.  
  
- [Gerando arquivos de um aplicativo](#Application). Você escreve um aplicativo que lê de modelos UML e gera arquivos.  
  
- [Gerando em tempo de design](#Design). Usar um modelo para definir algumas das funcionalidades do seu aplicativo e gerar código, recursos, e assim por diante no seu [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solução.  
  
  Este tópico termina com uma discussão sobre [como usar a geração de texto](#What). Para obter mais informações, consulte [geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md).  
  
##  <a name="Command"></a> Gerando arquivos de um comando de menu  
 Você pode usar modelos de texto dentro de um comando de menu UML de pré-processamento. Dentro do código do modelo de texto ou em uma classe parcial separada, você pode ler o modelo que é exibido no diagrama.  
  
 Para obter mais informações sobre esses recursos, leia os tópicos a seguir:  
  
- [Definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)  
  
- [Geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md)  
  
- [Navegar no modelo UML](../modeling/navigate-the-uml-model.md)  
  
  A abordagem demonstrada no exemplo a seguir é adequada para gerar o texto de um único modelo, quando você inicia a operação de um dos diagramas de modelo. Para processar um modelo em um contexto separado, considere o uso de [Visual Studio Modelbus](../modeling/integrate-uml-models-with-other-models-and-tools.md) para acessar o modelo e seus elementos.  
  
### <a name="example"></a>Exemplo  
 Para executar este exemplo, crie um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projeto VSIX (extensão). O nome do projeto que é usado neste exemplo é `VdmGenerator`. No **vsixmanifest** arquivo, clique em **adicionar conteúdo** e defina o campo de tipo como **componente MEF** e referenciar o projeto atual do caminho de origem. Para obter mais informações sobre como configurar esse tipo de projeto, consulte [definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md).  
  
 Adicione ao projeto um arquivo c# que contém o código a seguir. Essa classe define um comando de menu que aparecerá em um diagrama de classe UML.  
  
```  
using System;  
using System.ComponentModel.Composition;  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;  
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;  
  
namespace VdmGenerator  
{  
  [Export(typeof(ICommandExtension))]  
  [ClassDesignerExtension]  
  public class GenerateVdmFromClasses : ICommandExtension  
  {  
    [Import] public IDiagramContext DiagramContext { get; set; }  
    public void Execute(IMenuCommand command)  
    {  
      // Initialize the template with the Model Store.  
      VdmGen generator = new VdmGen(  
             DiagramContext.CurrentDiagram.ModelStore);  
      // Generate the text and write it.  
      System.IO.File.WriteAllText  
        (System.IO.Path.Combine(  
            Environment.GetFolderPath(  
                Environment.SpecialFolder.Desktop),  
            "Generated.txt")   
         , generator.TransformText());  
    }  
    public void QueryStatus(IMenuCommand command)  
    {  
      command.Enabled = command.Visible = true;  
    }  
    public string Text  
    { get { return "Generate VDM"; } }  
  }  
}  
```  
  
 O arquivo a seguir é o modelo de texto. Ele gera uma linha de texto para cada classe UML no modelo e uma linha para cada atributo em cada classe. O código para ler o modelo é inserido no texto, delimitado por `<# ... #>`.  
  
 Para criar esse arquivo, clique com botão direito no projeto no Gerenciador de soluções, aponte para **Add**e, em seguida, clique em **Novo Item**. Selecione **modelo de texto pré-processado**. O nome do arquivo para este exemplo deve ser **VdmGen.tt**. O **Custom Tool** propriedade do arquivo deve ser **TextTemplatingFilePreprocessor**. Para obter mais informações sobre modelos de texto pré-processado, consulte [geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md).  
  
```  
<#@ import namespace="Microsoft.VisualStudio.Uml.Classes" #>  
<#   
   foreach (IClass classElement in store.AllInstances<IClass>())   {  
#>  
Type <#= classElement.Name #> ::  
<#  
     foreach (IProperty attribute in classElement.OwnedAttributes)     {  
#>  
       <#= attribute.Name #> : <#=   
           attribute.Type == null ? ""  
                                  : attribute.Type.Name #>   
<#  
     }   }  
#>  
```  
  
 O modelo de texto gera uma c# classe parcial, que se tornará parte de seu [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projeto. Em um arquivo separado, adicione outra declaração parcial da mesma classe. Esse código fornece o modelo com acesso ao armazenamento de modelos UML:  
  
```  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
namespace VdmGenerator  
{  
    public partial class VdmGen  
    {  
        private IModelStore store;  
        public VdmGen(IModelStore s)  
        { store = s; }  
    }  
}  
```  
  
 Para testar o projeto, pressione **F5**. Uma nova instância da [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] será iniciado. Nesse caso, abra ou crie um modelo UML que contém um diagrama de classe. Adicionar algumas classes ao diagrama e adicione alguns atributos para cada classe. Clique com botão direito no diagrama e, em seguida, clique no comando de exemplo `Generate VDM`. O comando cria o arquivo `C:\Generated.txt`. Inspecione esse arquivo. Seu conteúdo deve se parecer com o seguinte texto, mas ele listará suas próprias classes e atributos:  
  
```  
Type Class1 ::  
          Attribute1 : int   
          Attribute2 : string   
Type Class2 ::   
          Attribute3 : string   
```  
  
##  <a name="Application"></a> Gerando arquivos de um aplicativo  
 Você pode gerar arquivos de um aplicativo que lê um modelo UML. Para essa finalidade, o método mais robusto e flexível de acessar o modelo e seus elementos é [Visual Studio Modelbus](../modeling/integrate-uml-models-with-other-models-and-tools.md).  
  
 Você também pode usar a API básica para carregar o modelo e passar o modelo para modelos de texto usando as mesmas técnicas como na seção anterior. Para obter mais informações sobre como carregar um modelo, consulte [ler um modelo UML no código do programa](../modeling/read-a-uml-model-in-program-code.md).  
  
##  <a name="Design"></a> Gerando arquivos em tempo de Design  
 Se o projeto tiver um método padrão de interpretação UML como código, você pode criar modelos de texto que permitem que você gerar o código dentro de seu projeto de um modelo UML. Normalmente, você teria uma solução que contém o projeto de modelo UML e um ou mais projetos para o código do aplicativo. Cada projeto de código pode conter vários modelos que geram arquivos de código, recursos e configuração do programa, com base no conteúdo do modelo. O desenvolvedor pode executar todos os modelos clicando o **transformar todos os modelos** na barra de ferramentas do Gerenciador de soluções. Geralmente, o código do programa é gerado na forma de classes parciais, para torná-lo mais fácil integrar partes escrito manualmente.  
  
 Um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projeto desse tipo pode ser distribuído na forma de um modelo, para que todos os membros de uma equipe é capaz de criar projetos que geram o código de um modelo da mesma maneira. Normalmente, o modelo faz parte de um pacote de extensão que inclui restrições de validação no modelo para garantir que as pré-condições do código de geração sejam atendidas.  
  
### <a name="outline-procedure-for-generating-files"></a>Estrutura de tópicos de procedimento para geração de arquivos  
  
-   Para adicionar um modelo a um projeto, selecione **modelo de texto** na caixa de diálogo Adicionar novo arquivo. Você pode adicionar um modelo para a maioria dos tipos de projeto, mas não os projetos de modelagem.  
  
-   A propriedade de ferramentas personalizada do arquivo de modelo deve ser **TextTemplatingFileGenerator**, e a extensão de nome de arquivo deve ser. tt.  
  
-   O modelo deve ter pelo menos uma diretiva de saída:  
  
     `<#@ output extension=".cs" #>`  
  
     Defina o campo de extensão de acordo com a linguagem do seu projeto.  
  
-   Para permitir que o código de geração em seu modelo para acessar o modelo, escrever `<#@ assembly #>` diretivas para os assemblies necessários para ler um modelo UML. Use `ModelingProject.LoadReadOnly()` para abrir o modelo. Para obter mais informações, consulte [ler um modelo UML no código do programa](../modeling/read-a-uml-model-in-program-code.md).  
  
-   O modelo é executado quando você salvar e quando você clica em **transformar todos os modelos** na barra de ferramentas do Gerenciador de soluções.  
  
-   Para obter mais informações sobre este tipo de modelo, consulte [geração de código de tempo de Design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md).  
  
-   Em um projeto típico, você terá vários modelos que geram arquivos diferentes do mesmo modelo. A primeira parte de cada modelo será o mesmo. Para reduzir essa duplicação, mover as partes comuns para um arquivo de texto separado e, em seguida, invoque-o usando a diretiva `<#@include file="common.txt"#>` em cada modelo.  
  
-   Você também pode definir um processador de diretriz especializado que permite que você forneça parâmetros para o processo de geração de texto. Para obter mais informações, consulte [personalizando transformação de texto T4](../modeling/customizing-t4-text-transformation.md).  
  
### <a name="example"></a>Exemplo  
 Este exemplo gera uma classe c# para cada classe UML no modelo de origem.  
  
##### <a name="to-set-up-a-visual-studio-solution-for-this-example"></a>Para configurar uma solução do Visual Studio para este exemplo  
  
1. Crie um diagrama de classe UML em um projeto de modelagem em uma nova solução.  
  
   1.  No **arquitetura** menu, clique em **novo diagrama**.  
  
   2.  Selecione **diagrama de classe UML**.  
  
   3.  Siga os prompts para criar um novo projeto de modelagem e de solução.  
  
   4.  Adicione algumas classes ao diagrama arrastando a ferramenta de classe UML da caixa de ferramentas.  
  
   5.  Salve o arquivo.  
  
2. Crie um projeto c# ou Visual Basic na mesma solução.  
  
   -   No Gerenciador de soluções, clique com botão direito a solução, aponte para **Add**e, em seguida, clique em **novo projeto**. Sob **modelos instalados**, clique em **Visual Basic** ou **Visual c#** e, em seguida, selecione um tipo de projeto como **aplicativo de Console**.  
  
3. Adicione um arquivo de texto sem formatação para o projeto c# ou Visual Basic. Esse arquivo conterá código compartilhado para gravar vários modelos de texto.  
  
   - No Gerenciador de soluções, clique com botão direito no projeto, aponte para **Add**e, em seguida, clique em **Novo Item**. Selecione **arquivo de texto**.  
  
     Insira o texto que é mostrado na seção a seguir.  
  
4. Adicione um arquivo de modelo de texto para o projeto c# ou Visual Basic.  
  
   - No Gerenciador de soluções, clique com botão direito no projeto, aponte para **Add**e, em seguida, clique em **Novo Item**. Selecione **modelo de texto**.  
  
     Insira o código a seguir no arquivo de modelo de texto.  
  
5. Salve o arquivo de modelo de texto.  
  
6. Inspecione o código no arquivo subsidiário. Ele deve conter uma classe para cada classe UML no modelo.  
  
   1.  Em um projeto do Visual Basic, clique em **Show All Files** na barra de ferramentas do Gerenciador de soluções.  
  
   2.  Expanda o nó do arquivo de modelo no Gerenciador de soluções.  
  
#### <a name="content-of-the-shared-text-file"></a>Conteúdo do arquivo de texto compartilhado  
 Neste exemplo, o arquivo é chamado SharedTemplateCode.txt e ele está na mesma pasta que os modelos de texto.  
  
```  
<# /* Common material for inclusion in my model templates */ #>  
<# /* hostspecific allows access to the Visual Studio API */ #>  
<#@ template debug="false" hostspecific="true" language="C#" #>  
<#@ assembly name="Microsoft.VisualStudio.Uml.Interfaces.dll"#>  
<#@ assembly name="Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll"#>  
<#@ assembly name="EnvDTE" #>  
<#@ import namespace="Microsoft.VisualStudio.Uml.Classes" #>  
<#@ import namespace="Microsoft.VisualStudio.ArchitectureTools.Extensibility" #>  
<#@ import namespace="Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml" #>  
<#+  // Note this is a Class Feature Block  
///<summary>  
/// Text templates are run in a common AppDomain, so   
/// we can cache the model store that we find.  
///</summary>  
private IModelStore StoreCache  
{  
  get { return AppDomain.CurrentDomain.GetData("ModelStore") as IModelStore; }  
  set { AppDomain.CurrentDomain.SetData("ModelStore", value); }   
}  
private bool CacheIsOld()  
{  
    DateTime? dt = AppDomain.CurrentDomain  
           .GetData("latestAccessTime") as DateTime?;  
    DateTime t = dt.HasValue ? dt.Value : new DateTime();   
    DateTime now = DateTime.Now;  
    AppDomain.CurrentDomain.SetData("latestAccessTime", now);  
    return now.Subtract(t).Seconds > 3;  
}  
  
///<summary>  
/// Find the UML modeling project in this solution,  
/// and load the model.  
///</summary>  
private IModelStore ModelStore  
{  
  get   
  {  
    // Avoid loading the model for every template:  
    if (StoreCache == null || CacheIsOld())  
    {  
      // Use Visual Studio API to find modeling project:  
      EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)  
                       .GetService(typeof(EnvDTE.DTE));  
      EnvDTE.Project project = null;  
      foreach (EnvDTE.Project p in dte.Solution.Projects)  
      {  
        if (p.FullName.EndsWith(".modelproj"))  
        {  
          project = p;  
          break;  
        }              
      }  
      if (project == null) return null;  
  
      // Load UML model into this AppDomain  
      // and access model store:  
      IModelingProjectReader reader =   
           ModelingProject.LoadReadOnly(project.FullName);  
      StoreCache = reader.Store;  
    }  
    return StoreCache;  
  }  
}  
#>  
```  
  
#### <a name="content-of-the-text-template-file"></a>Conteúdo do arquivo de modelo de texto  
 O seguinte texto é colocado na **. TT** arquivo. Este exemplo gera classes em um arquivo c# de classes UML no modelo. No entanto, você pode gerar arquivos de qualquer tipo. O idioma do arquivo gerado não está relacionado à linguagem em que o código de modelo de texto é escrito.  
  
```  
<#@include file="SharedTemplateCode.txt"#>  
<#@ output extension=".cs" #>  
namespace Test{  
<#  
      foreach (IClass c in ModelStore.AllInstances<IClass>())  
      {  
#>  
   public partial class <#=c.Name#>  
   {   }  
<#  
      }  
#>  
}  
```  
  
##  <a name="What"></a> Como usar a geração de texto  
 O poder real de modelagem é obtido quando você usa modelos para design no nível da arquitetura ou requisitos. Você pode usar modelos de texto para fazer parte do trabalho de converter as ideias de alto nível em código. Em muitos casos, isso não resulta em uma correspondência direta entre os elementos em modelos UML e classes ou outras partes do código do programa.  
  
 Além disso, a transformação depende de seu domínio problemático; Não há nenhum mapeamento universal entre modelos e o código.  
  
 Aqui estão alguns exemplos de geração de código de modelos:  
  
-   **Linhas de produtos**. Fabrikam, Inc. cria e instala o tratamento de sistemas de bagagem de aeroporto. Grande parte do software é muito semelhante entre uma instalação e a próxima, mas a configuração de software depende de quais maquinário de tratamento de recipiente está instalado e como essas partes são interconectadas por belts transportadora. No início de um contrato, analistas da Fabrikam discutem os requisitos com o gerenciamento de aeroporto e capturam o plano de hardware usando um diagrama de atividade UML. Nesse modelo, a equipe de desenvolvimento gera arquivos de configuração, código do programa, planos e documentos do usuário. Eles concluem o trabalho manuais adições e ajustes no código. Conforme eles obtêm a experiência de um trabalho para o próximo, eles estendem o escopo do material gerado.  
  
-   **Padrões**. Geralmente, os desenvolvedores na Contoso, Ltd criem sites da Web e projetar o esquema de navegação usando diagramas de classe UML. Cada página da Web é representada por uma classe, e as associações representam os links de navegação. Os desenvolvedores geram grande parte do código de um site do modelo. Cada página da Web corresponde a várias classes e as entradas do arquivo de recurso.  Esse método tem os benefícios que a construção de cada página está em conformidade com um padrão único, tornando mais confiável e flexível do que o código escrito manualmente. O padrão é em modelos de geração, enquanto o modelo é usado para capturar os aspectos de variável.  
  
-   **Esquemas**. A Humongous Insurance tem milhares de sistemas em todo o mundo. Esses sistemas usam bancos de dados diferentes, linguagens e interfaces. Internamente, a equipe de arquitetura central publica modelos de processos e conceitos de negócios. Desses modelos, as equipes locais geram partes de seus esquemas de banco de dados e de intercâmbio, as declarações no código do programa e assim por diante. A apresentação gráfica dos modelos ajuda as equipes a discutir propostas. As equipes de criam vários diagramas que mostram subconjuntos do modelo que se aplicam a diferentes áreas de negócios. Eles também usar cor para realçar áreas sujeitas a alterações.  
  
## <a name="important-techniques-for-generating-artifacts"></a>Técnicas importantes para a geração de artefatos  
 Nos exemplos anteriores, modelos são usados para fins de negócios dependente diversificados, e a interpretação dos elementos, como classes e atividades de modelagem varia de um aplicativo para outro. As técnicas a seguir são úteis quando você gerar artefatos de modelos.  
  
-   **Perfis de**. Mesmo dentro de área de negócios, a interpretação de um tipo de elemento pode variar. Por exemplo, em um diagrama de site da Web, algumas classes podem representar as páginas da Web e outras pessoas representam os blocos de conteúdo. Para tornar mais fácil para os usuários registrar essas distinções, defina estereótipos. Estereótipos também tornam possível anexar propriedades adicionais que se aplicam a elementos desse tipo. Estereótipos são empacotados dentro de perfis. Para obter mais informações, consulte [definir um perfil para estender UML](../modeling/define-a-profile-to-extend-uml.md).  
  
     No código de modelo, é fácil acessar os estereótipos que são definidos em um objeto. Por exemplo:  
  
    ```  
    public bool HasStereotype(IClass c, string profile, string stereo)  
    { return c.AppliedStereotypes.Any  
       (s => s.Profile == profile && s.Name == stereo ); }  
    ```  
  
-   **Restrita modelos**. Nem todos os modelos que você pode criar são válidos para cada finalidade. Por exemplo, em modelos de bagagem de aeroporto da Fabrikam, seria incorreto para ter uma mesa de check-in sem uma transportadora de saída. Você pode definir funções de validação que ajudam os usuários para observar essas restrições. Para obter mais informações, consulte [definir restrições de validação para modelos UML](../modeling/define-validation-constraints-for-uml-models.md).  
  
-   **Preservar alterações manuais**. Apenas alguns dos arquivos da solução podem ser gerado de um modelo. Na maioria dos casos, você precisa ser capaz de adicionar ou ajustar o conteúdo gerado manualmente. No entanto, é importante que essas alterações manuais devem ser preservadas quando a transformação do modelo é executada novamente.  
  
     Onde seus modelos de geram código em [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] idiomas, elas devem gerar classes parciais para que os desenvolvedores podem adicionar métodos e código. Também é útil gerar cada classe como um par: uma classe base abstrata que contém os métodos e uma classe herdada que contém somente o construtor. Isso permite aos desenvolvedores substituir os métodos. Para permitir a inicialização a ser substituído, ela é feita em um método separado, em vez de nos construtores.  
  
     Sempre que um modelo gera XML e outros tipos de saída, ele pode ser mais difícil de manter o conteúdo de manual separados do conteúdo gerado. Um método é criar uma tarefa no processo de compilação que combina dois arquivos. Outro método é para os desenvolvedores ajustar uma cópia local do modelo de geração.  
  
-   **Mova o código em assemblies separados**. Não recomendamos escrever grandes corpos de código em modelos. É preferível manter o conteúdo gerado separado da computação e modelos de texto são também não dão suporte para edição de código.  
  
     Em vez disso, se você tiver que executar computações substanciais para gerar texto, crie essas funções em um assembly separado e chamar seus métodos do modelo.



