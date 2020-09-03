---
title: Como usar o contexto de interface do usuário baseado em regra para extensões do Visual Studio | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 8dd2cd1d-d8ba-49b9-870a-45acf3a3259d
author: acangialosi
ms.author: anthc
ms.workload:
- vssdk
ms.openlocfilehash: 4ee29937b11110ee6aae65628b81ea49588fdd22
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "86972303"
---
# <a name="how-to-use-rule-based-ui-context-for-visual-studio-extensions"></a>Como usar o contexto de interface do usuário baseado em regra para extensões do Visual Studio

O Visual Studio permite o carregamento de VSPackages quando determinados s bem conhecidos <xref:Microsoft.VisualStudio.Shell.UIContext> são ativados. No entanto, esses contextos de interface do usuário não são refinados, o que deixa os autores de extensão sem opção, mas escolhe um contexto de interface do usuário disponível que é ativado antes do ponto que realmente desejavam carregar o VSPackage. Para obter uma lista de contextos de interface do usuário conhecidos, consulte <xref:Microsoft.VisualStudio.Shell.KnownUIContexts> .

O carregamento de pacotes pode ter um impacto no desempenho e carregá-los antes do necessário não é a prática recomendada. O Visual Studio 2015 introduziu o conceito de contextos de interface do usuário baseados em regras, um mecanismo que permite aos autores de extensão definir as condições precisas sob as quais um contexto de interface do usuário é ativado e VSPackages associados são carregados.

## <a name="rule-based-ui-context"></a>Contexto de interface do usuário baseado em regra

Uma "regra" consiste em um novo contexto de interface do usuário (um GUID) e uma expressão booliana que faz referência a um ou mais "termos" combinados com operações lógicas "e", "ou", "não". "Termos" são avaliados dinamicamente no tempo de execução e a expressão é reavaliada sempre que qualquer um de seus termos é alterado. Quando a expressão é avaliada como true, o contexto de interface do usuário associado é ativado. Caso contrário, o contexto de interface do usuário será desativado.

O contexto da interface do usuário baseada em regras pode ser usado de várias maneiras:

1. Especifique restrições de visibilidade para comandos e janelas de ferramentas. Você pode ocultar as janelas de comandos/ferramentas até que a regra de contexto da interface do usuário seja atendida.

2. Como restrições de carregamento automático: carregar automaticamente pacotes somente quando a regra for atendida.

3. Como uma tarefa atrasada: atraso no carregamento até que um intervalo especificado tenha passado e a regra ainda seja atendida.

   O mecanismo pode ser usado por qualquer extensão do Visual Studio.

## <a name="create-a-rule-based-ui-context"></a>Criar um contexto de interface do usuário baseado em regras
 Suponha que você tenha uma extensão chamada TestPackage, que oferece um comando de menu que se aplica somente a arquivos com a extensão *. config* . Antes de VS2015, a melhor opção era carregar TestPackage quando o <xref:Microsoft.VisualStudio.Shell.KnownUIContexts.SolutionExistsAndFullyLoadedContext%2A> contexto da interface do usuário foi ativado. Carregar TestPackage dessa maneira não é eficiente, já que a solução carregada pode nem mesmo conter um arquivo *. config* . Estas etapas mostram como o contexto de interface do usuário baseado em regras pode ser usado para ativar um contexto de interface do usuário somente quando um arquivo com a extensão *. config* é selecionado e carrega TestPackage quando esse contexto de interface do usuário é ativado.

1. Defina um novo GUID UIContext e adicione à classe VSPackage <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> e <xref:Microsoft.VisualStudio.Shell.ProvideUIContextRuleAttribute> .

    Por exemplo, vamos supor que um novo UIContext "UIContextGuid" seja adicionado. O GUID criado (você pode criar um GUID clicando em **ferramentas**  >  **Criar GUID**) é "8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B". Em seguida, adicione a seguinte declaração dentro de sua classe de pacote:

   ```csharp
   public const string UIContextGuid = "8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B";
   ```

    Para os atributos, adicione os seguintes valores: (os detalhes desses atributos serão explicados posteriormente)

   ```csharp
   [ProvideAutoLoad(TestPackage.UIContextGuid)]
   [ProvideUIContextRule(TestPackage.UIContextGuid,
       name: "Test auto load",
       expression: "DotConfig",
       termNames: new[] { "DotConfig" },
       termValues: new[] { "HierSingleSelectionName:.config$" })]
   ```

    Esses metadados definem o novo UIContext GUID (8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B) e uma expressão referente a um único termo, "DotConfig". O termo "DotConfig" é avaliado como true sempre que a seleção atual na hierarquia ativa tiver um nome que corresponda ao padrão de expressão regular " \\ . config $" (termina com *. config*). O valor (padrão) define um nome opcional para a regra útil para depuração.

    Os valores do atributo são adicionados ao pkgdef gerado durante o tempo de compilação posteriormente.

2. No arquivo VSCT para os comandos do TestPackage, adicione o sinalizador "DynamicVisibility" aos comandos apropriados:

   ```xml
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

3. Na seção visibilidades do VSCT, vincule os comandos apropriados para o novo GUID UIContext definido em #1:

   ```xml
   <VisibilityConstraints>
       <VisibilityItem guid="guidTestPackageCmdSet" id="TestId"  context="UIContextGuid"/>
   </VisibilityConstraints>
   ```

4. Na seção símbolos, adicione a definição do UIContext:

   ```xml
   <GuidSymbol name="UIContextGuid" value="{8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B}" />
   ```

    Agora, os comandos do menu de contexto para arquivos * \* . config* serão visíveis somente quando o item selecionado no Gerenciador de soluções for um arquivo *. config* e o pacote não será carregado até que um desses comandos seja selecionado.

   Em seguida, use um depurador para confirmar se o pacote é carregado somente quando você espera. Para depurar o TestPackage:

5. Defina um ponto de interrupção no <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> método.

6. Compile o TestPackage e inicie a depuração.

7. Crie um projeto ou abra um.

8. Selecione qualquer arquivo com uma extensão diferente de *. config*. O ponto de interrupção não deve ser atingido.

9. Selecione o arquivo de *App.Config* .

   O TestPackage é carregado e interrompido no ponto de interrupção.

## <a name="add-more-rules-for-ui-context"></a>Adicionar mais regras para o contexto de interface do usuário
 Como as regras de contexto da interface do usuário são expressões booleanas, você pode adicionar mais regras restritas para um contexto de interface do usuário. Por exemplo, no contexto da interface do usuário acima, você pode especificar que a regra se aplique somente quando uma solução com um projeto for carregada. Dessa forma, os comandos não aparecerão se você abrir um arquivo *. config* como um arquivo autônomo, não como parte de um projeto.

```csharp
[ProvideAutoLoad(TestPackage.UIContextGuid)]
[ProvideUIContextRule(TestPackage.UIContextGuid,
    name: "Test auto load",
    expression: "(SingleProject | MultipleProjects) & DotConfig",
    termNames: new[] { "SingleProject", "MultipleProjects","DotConfig" },
    termValues: new[] { VSConstants.UICONTEXT.SolutionHasSingleProject_string , VSConstants.UICONTEXT.SolutionHasMultipleProjects_string , "HierSingleSelectionName:.config$" })]
```

 Agora, a expressão faz referência a três termos. Os dois primeiros termos, "SingleProject" e "MultipleProjects", referem-se a outros contextos de interface do usuário conhecidos (por seus GUIDs). O terceiro termo, "DotConfig", é o contexto de interface do usuário baseado em regras definido anteriormente neste artigo.

## <a name="delayed-activation"></a>Ativação atrasada
 As regras podem ter um "atraso" opcional. O atraso é especificado em milissegundos. Se presente, o atraso faz com que a ativação ou desativação do contexto da interface do usuário de uma regra seja atrasada nesse intervalo de tempo. Se a regra mudar de volta antes do intervalo de atraso, nada acontecerá. Esse mecanismo pode ser usado para etapas de inicialização "escalonadas", especialmente inicialização única, sem depender de temporizadores ou de registro para notificações ociosas.

 Por exemplo, você pode especificar que a regra de carga de teste tenha um atraso de 100 milissegundos:

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

Aqui estão os vários tipos de termo com suporte:

|Termo|Descrição|
|-|-|
|{nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn}|O GUID refere-se a um contexto de interface do usuário. O termo será true sempre que o contexto da interface do usuário estiver ativo; caso contrário, false.|
|HierSingleSelectionName:\<pattern>|O termo será true sempre que a seleção na hierarquia ativa for um único item e o nome do item selecionado corresponder à expressão regular do .net fornecida por "Pattern".|
|UserSettingsStoreQuery:\<query>|"Query" representa um caminho completo para o armazenamento de configurações do usuário, que deve ser avaliado como um valor diferente de zero. A consulta é dividida em uma "coleção" e "propertyName" na última barra.|
|ConfigSettingsStoreQuery:\<query>|"Query" representa um caminho completo para o repositório de configurações de configuração, que deve ser avaliado como um valor diferente de zero. A consulta é dividida em uma "coleção" e "propertyName" na última barra.|
|ActiveProjectFlavor:\<projectTypeGuid>|O termo será true sempre que o projeto selecionado no momento for redado (agregado) e tiver um tipo correspondente ao GUID do tipo de projeto especificado.|
|ActiveEditorContentType:\<contentType>|O termo será true quando o documento selecionado for um editor de texto com o tipo de conteúdo fornecido. Observação: quando o documento selecionado for renomeado, esse termo não será atualizado até que o arquivo seja fechado e reaberto.|
|ActiveProjectCapability:\<Expression>|O termo é true quando os recursos do projeto ativo correspondem à expressão fornecida. Uma expressão pode ser algo como VB &#124; CSharp.|
|SolutionHasProjectCapability:\<Expression>|Semelhante a acima, mas o termo é verdadeiro quando a solução tem qualquer projeto carregado que corresponde à expressão.|
|SolutionHasProjectFlavor:\<projectTypeGuid>|O termo será verdadeiro sempre que uma solução tiver um projeto que seja reindicado (agregado) e tenha um tipo correspondente ao GUID do tipo de projeto especificado.|
|ProjectAddedItem:\<pattern>| O termo é true quando um arquivo que corresponde ao "Pattern" é adicionado a um projeto no soluion que é aberto.|
|ActiveProjectOutputType:\<outputType>|O termo será true quando o tipo de saída para o projeto ativo corresponder exatamente.  O OutputType pode ser um número inteiro ou um <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROJOUTPUTTYPE> tipo.|
|ActiveProjectBuildProperty:\<buildProperty>=\<regex>|O termo é true quando o projeto ativo tem a propriedade de compilação especificada e as correspondências de valor de propriedade ao filtro Regex fornecido. Consulte [persistindo dados em arquivos de projeto do MSBuild](internals/persisting-data-in-the-msbuild-project-file.md) para obter mais detalhes sobre as propriedades de compilação.|
|SolutionHasProjectBuildProperty:\<buildProperty>=\<regex>|O termo é true quando a solução tem um projeto carregado com a propriedade de compilação especificada e correspondências de valor de propriedade ao filtro Regex fornecido.|

## <a name="compatibility-with-cross-version-extension"></a>Compatibilidade com extensão de versão cruzada

Os contextos de interface do usuário baseados em regras são um novo recurso do Visual Studio 2015 e não seriam portados para versões anteriores. Não portar para versões anteriores cria um problema com extensões/pacotes direcionados a várias versões do Visual Studio. Essas versões teriam que ser carregadas automaticamente em Visual Studio 2013 e anteriores, mas podem se beneficiar de contextos de interface do usuário baseados em regras para evitar que sejam carregados automaticamente no Visual Studio 2015.

Para oferecer suporte a esses pacotes, as entradas AutoLoadPackages no registro agora podem fornecer um sinalizador em seu campo de valor para indicar que a entrada deve ser ignorada no Visual Studio 2015 e superior. Isso pode ser feito adicionando-se uma opção flags a <xref:Microsoft.VisualStudio.Shell.PackageAutoLoadFlags> . VSPackages agora pode adicionar a opção **SkipWhenUIContextRulesActive** ao <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> atributo para indicar que a entrada deve ser ignorada no Visual Studio 2015 e superior.
## <a name="extensible-ui-context-rules"></a>Regras de contexto de interface do usuário extensível

Às vezes, os pacotes não podem usar regras de contexto de interface do usuário estáticas. Por exemplo, suponha que você tenha um pacote com suporte para extensibilidade de modo que o estado do comando seja baseado em tipos de editor com suporte pelos provedores de MEF importados. O comando será habilitado se houver uma extensão com suporte para o tipo de edição atual. Nesses casos, o pacote em si não pode usar uma regra de contexto de interface do usuário estática, pois os termos seriam alterados dependendo de quais extensões de MEF estão disponíveis.

Para dar suporte a esses pacotes, contextos de interface do usuário baseados em regras dão suporte a uma expressão codificada "*" que indica todos os termos abaixo que ele será Unido a ou. Isso permite que o pacote mestre defina um contexto de interface do usuário baseado em regra conhecido e vincule seu estado de comando a esse contexto. Depois, qualquer extensão do MEF direcionada para o pacote mestre pode adicionar seus termos aos editores que ele dá suporte sem afetar outros termos ou a expressão mestra.

A documentação do construtor <xref:Microsoft.VisualStudio.Shell.ProvideExtensibleUIContextRuleAttribute.%23ctor%2A> mostra a sintaxe para regras de contexto de interface do usuário extensível.
