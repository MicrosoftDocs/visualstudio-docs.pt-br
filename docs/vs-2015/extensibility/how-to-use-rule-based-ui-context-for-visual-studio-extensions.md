---
title: 'Como: usar o contexto de interface do usuário baseada em regras para extensões do Visual Studio | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8dd2cd1d-d8ba-49b9-870a-45acf3a3259d
caps.latest.revision: 8
ms.author: gregvanl
ms.openlocfilehash: 1c7f1bf5aa80316e0b663f247ce905060f6029fa
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51784319"
---
# <a name="how-to-use-rule-based-ui-context-for-visual-studio-extensions"></a>Como: usar o contexto de interface do usuário baseada em regras para extensões do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio permite o carregamento de VSPackages quando determinados bem conhecidos <xref:Microsoft.VisualStudio.Shell.UIContext>s são ativados. Entretanto, nesses contextos de interface do usuário não são muito bem mais refinado, não deixando os autores de extensão nenhuma opção, mas para selecionar um contexto de interface do usuário disponível que ativa antes do ponto realmente desejasse o VSPackage ao carregar. Para obter uma lista de contextos de interface do usuário bem conhecidos, consulte <xref:Microsoft.VisualStudio.Shell.KnownUIContexts>.  
  
 Carregando pacotes pode ter um impacto no desempenho e carregá-los mais cedo do que eles são necessários não é a prática recomendada. Visual Studio 2015 introduziu o conceito de com base em regras de contextos de interface do usuário, um mecanismo que permite que os autores de extensão definir as condições precisas sob as quais um contexto de interface do usuário é ativado e carregar VSPackages associados.  
  
## <a name="rule-based-ui-context"></a>Contexto de interface do usuário baseada em regra  
 Uma "regra" consiste em um novo contexto de interface do usuário (um GUID) e uma expressão booliana que faz referência a um ou mais "termos de" combinada com lógica "and", "ou", "não" operações. "Termos de" são avaliados dinamicamente em tempo de execução e a expressão é avaliada novamente sempre que qualquer uma das suas alterações de termos. Quando a expressão é avaliada como true, o contexto de interface do usuário associado é ativado. Caso contrário, o contexto de interface do usuário é desativado.  
  
 Contexto de interface do usuário com base em regra pode ser usado em uma variedade de maneiras:  
  
1. Especifique as restrições de visibilidade para comandos e janelas de ferramentas. Você pode ocultar as janelas de ferramentas/comandos até que a regra de contexto de interface do usuário seja atendida.  
  
2. Restrições de carga como automático: pacotes de carregamento automático somente quando a regra for atendida  
  
3. Tarefa com atraso: atrasar o carregamento até que um intervalo especificado tiver passado e a regra ainda é atendida.  
  
   O mecanismo pode ser usado por qualquer extensão do Visual Studio.  
  
## <a name="create-a-rule-based-ui-context"></a>Criar um contexto de interface do usuário baseada em regra  
 Suponha que você tenha uma extensão chamada TestPackage, que oferece um comando de menu que se aplica somente a arquivos com extensão. "config". Antes de VS2015, a melhor opção foi carregar TestPackage quando <xref:Microsoft.VisualStudio.Shell.KnownUIContexts.SolutionExistsAndFullyLoadedContext%2A> contexto de interface do usuário foi ativado. Isso não é eficiente, pois a solução carregada não pode conter até mesmo um arquivo. config. Informe-nos como contexto de interface do usuário com base em regras pode ser usado para ativar um contexto de interface do usuário apenas quando um arquivo com extensão. config está selecionada e carregar TestPackage quando esse contexto de interface do usuário é ativado.  
  
1. Definir um novo GUID UIContext e adicione à classe VSPackage <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> e <xref:Microsoft.VisualStudio.Shell.ProvideUIContextRuleAttribute>.  
  
    Por exemplo, vamos supor que um novo UIContext "UIContextGuid" deve ser adicionado. O GUID criado (você pode criar um GUID clicando em Ferramentas -> criar guid) é "8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B". Você, em seguida, adicione o seguinte dentro de sua classe de pacote:  
  
   ```csharp  
   public const string UIContextGuid = "8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B";  
   ```  
  
    Para os atributos, adicione o seguinte: (os detalhes desses atributos serão explicados posteriormente)  
  
   ```csharp  
   [ProvideAutoLoad(TestPackage.UIContextGuid)]      
   [ProvideUIContextRule(TestPackage.UIContextGuid,  
       name: "Test auto load",   
       expression: "DotConfig",  
       termNames: new[] { "DotConfig" },  
       termValues: new[] { "HierSingleSelectionName:.config$" })]  
   ```  
  
    Esses metadados definem o novo GUID UIContext (8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B) e uma expressão referindo-se a um único termo, "DotConfig". O termo "DotConfig" é avaliada como true, sempre que a seleção atual na hierarquia do Active Directory tem um nome que corresponda ao padrão de expressão regular "\\. config$" (termina com ". config"). O valor (padrão) define um nome opcional para a regra útil para depuração.  
  
    Os valores do atributo são adicionados ao pkgdef gerado durante o tempo de compilação posteriormente.  
  
2. No arquivo VSCT para comandos do TestPackage, adicione o sinalizador "DynamicVisibility" para os comandos apropriados:  
  
   ```xml  
   <CommandFlag>DynamicVisibility</CommandFlag>  
   ```  
  
3. Na seção Visibilidades o VSCT, ligar os comandos apropriados para o novo UIContext GUID definido em 1 #:  
  
   ```xml  
   <VisibilityConstraints>   
       <VisibilityItem guid="guidTestPackageCmdSet" id="TestId"  context="guidTestUIContext"/>   
   </VisibilityConstraints>  
   ```  
  
4. Na seção símbolos, adicione a definição do UIContext:  
  
   ```xml  
   <GuidSymbol name="guidTestUIContext" value="{8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B}" />  
   ```  
  
    Agora, os comandos de menu de contexto para arquivos Config estará visíveis apenas quando o item selecionado no Gerenciador de soluções é um arquivo ". config" e o pacote não será carregado até que um desses comandos é selecionado.  
  
   Em seguida, vamos usar um depurador para confirmar que o pacote carrega apenas quando podemos esperar que ele. Para depurar TestPackage:  
  
5. Defina um ponto de interrupção no <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> método.  
  
6. Compile o TestPackage e iniciar a depuração.  
  
7. Criar um projeto ou abrir um.  
  
8. Selecione qualquer arquivo com uma extensão diferente. config. O ponto de interrupção não deverá ser atingido.  
  
9. Selecione o arquivo App. config.  
  
   O TestPackage carrega e para no ponto de interrupção.  
  
## <a name="adding-more-rules-for-ui-context"></a>Adicionar mais regras para o contexto de interface do usuário  
 Como as regras de contexto de interface do usuário são expressões Boolianas, você pode adicionar regras mais restritas para um contexto de interface do usuário. Por exemplo, no contexto da interface do usuário acima, você pode especificar que a regra se aplica somente quando uma solução com um projeto é carregada. Dessa forma, os comandos não aparecerão se você abrir um arquivo ". config" como um arquivo autônomo, e não como parte de um projeto.  
  
```csharp  
[ProvideAutoLoad(TestPackage.UIContextGuid)]      
[ProvideUIContextRule(TestPackage.UIContextGuid,    
    name: "Test auto load",  
    expression: "(SingleProject | MultipleProjects) & DotConfig",    
    termNames: new[] { "SingleProject", "MultipleProjects","DotConfig" },     
    termValues: new[] { VSConstants.UICONTEXT_SolutionHasSingleProject_string , VSConstants.UICONTEXT_SolutionHasMultipleProjects_string , "HierSingleSelectionName:.config$" })]  
```  
  
 Agora a expressão fizer referência a três termos. Os primeiros dois termos, "SingleProject" e "MultipleProjects", consultem outros contextos de interface do usuário conhecida (pelas suas GUIDs). O terceiro termo, "DotConfig" é o contexto de interface do usuário baseada em regras definido anteriormente.  
  
## <a name="delayed-activation"></a>Ativação atrasada  
 Regras podem ter um "atraso" opcional. O atraso especificado em milissegundos. Se estiver presente, o atraso faz com que a ativação ou desativação de contexto de interface de usuário de uma regra a ser atrasado por desse intervalo de tempo. Se as alterações de regra de volta antes do intervalo de atraso, em seguida, nada acontecerá. Esse mecanismo pode ser usado para "escalonar" as etapas de inicialização - especialmente a inicialização única sem depender de temporizadores ou se registrar para notificações ociosas.  
  
 Por exemplo, você pode especificar sua regra de carga de teste para ter um atraso de 100 milissegundos:  
  
```csharp  
[ProvideAutoLoad(TestPackage.UIContextGuid)]  
[ProvideUIContextRule(TestPackage.UIContextGuid,   
    name: "Test auto load",  
    expression: "DotConfig",   
    termNames: new[] { "DotConfig" },  
    termValues: new[] { "HierSingleSelectionName:.config$" },   
    delay: 100)]  
```  
  
## <a name="term-types"></a>Tipos de termo  
 Aqui estão os vários tipos de termo que têm suporte:  
  
|||  
|-|-|  
|{nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn}|O GUID se refere a um contexto de interface do usuário. O termo será true sempre que o contexto de interface do usuário está ativo e false caso contrário.|  
|HierSingleSelectionName:\<padrão >|O termo será true sempre que a seleção na hierarquia do Active Directory é um único item e o nome do item selecionado corresponde à expressão regular .net fornecido pelo "padrão".|  
|UserSettingsStoreQuery:\<consulta >|"consulta" representa um caminho completo para o repositório de configurações de usuário que deve ser avaliada como um valor diferente de zero. A consulta é dividida em uma "coleção" e "propertyName" em que a última barra.|  
|ConfigSettingsStoreQuery:\<consulta >|"consulta" representa um caminho completo para o repositório de configurações de configuração que deve ser avaliada como um valor diferente de zero. A consulta é dividida em uma "coleção" e "propertyName" em que a última barra.|  
|ActiveProjectFlavor:\<projectTypeGuid >|O termo será true sempre que o projeto selecionado atualmente é tipo (agregado) e tem um tipo correspondente ao tipo de projeto determinado GUID.|  
|ActiveEditorContentType:\<contentType >|O termo será true quando o documento selecionado é um editor de texto com o tipo de conteúdo fornecido.|  
|ActiveProjectCapability:\<expressão >|O termo é verdadeiro quando os recursos de projeto ativo corresponde à expressão fornecida. Uma expressão pode ser algo parecido com VB &#124; CSharp|  
|SolutionHasProjectCapability:\<expressão >|Semelhante ao acima mas termo é verdadeiro quando a solução tem qualquer projeto carregado que corresponde à expressão.|  
|SolutionHasProjectFlavor:\<projectTypeGuid >|O termo será true sempre que uma solução tem um projeto que é o tipo (agregado) e tem um tipo correspondente ao tipo de projeto determinado GUID.|


  
## <a name="compatibility-with-cross-version-extension"></a>Compatibilidade com a extensão de versão cruzada  
 A regra com base contextos de interface do usuário é um novo recurso no Visual Studio 2015 e não ser transportado para versões anteriores. Isso cria um problema com as extensões/pacotes destinados a várias versões do Visual Studio que teria de ser carregados automaticamente no Visual Studio 2013 e versões anteriores, mas podem se beneficiar de contextos de interface do usuário com base em regra para impedir que está sendo carregado automaticamente no Visual Studio 2015.  
  
 Para dar suporte a esses pacotes, AutoLoadPackages entradas no registro agora podem fornecer um sinalizador em seu campo de valor para indicar que a entrada deve ser ignorada no Visual Studio 2015 e versões posteriores. Isso pode ser feito pela adição de uma opção de sinalizadores para <xref:Microsoft.VisualStudio.Shell.PackageAutoLoadFlags>. Agora pode adicionar os VSPackages **SkipWhenUIContextRulesActive** opção ao seus <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> atributo para indicar a entrada deve ser ignorada no Visual Studio 2015 e superior.  
  
## <a name="extensible-ui-context-rules"></a>Regras de contexto de interface do usuário extensível  
 Às vezes, os pacotes não podem usar regras estáticas do contexto de interface do usuário. Por exemplo, suponha que você tenha um pacote de suporte a extensibilidade, de modo que o estado do comando baseia-se nos tipos de editor que são suportados por provedores MEF importados. O comando será habilitado se há uma extensão que dão suporte a tipo de edição atual. Em tais casos o pacote propriamente dito não pode usar uma regra de contexto de interface do usuário estática, uma vez que os termos seriam alterado dependendo de qual MEF extensões estão disponíveis.  
  
 Para dar suporte a esses pacotes, contextos de interface do usuário com base em regra dar suporte a uma expressão codificada "*" que indica que todos os termos abaixo será junto com ou. Isso permite que o pacote mestre definir uma regra conhecida com base em contexto de interface do usuário e ligar seu estado de comando para este contexto. Depois disso qualquer extensão MEF direcionado para o pacote mestre pode adicionar seus termos para editores que dá suporte a sem afetar outros termos ou a expressão mestre.  
  
 O construtor <xref:Microsoft.VisualStudio.Shell.ProvideExtensibleUIContextRuleAttribute.%23ctor%2A> documentação mostra a sintaxe para as regras de contexto de interface do usuário extensíveis.

