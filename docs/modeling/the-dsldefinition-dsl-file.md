---
title: O arquivo DslDefinition.dsl
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, definition file
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 99145768ef4e0c37f729477ee598628a3b8d0e9a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72605985"
---
# <a name="the-dsldefinitiondsl-file"></a>O arquivo DslDefinition.dsl

Este tópico descreve a estrutura do arquivo DslDefinition. DSL no projeto de DSL de uma solução de [!INCLUDE[dsl](../modeling/includes/dsl_md.md)], que define uma *linguagem específica de domínio*. O arquivo DslDefinition. DSL descreve as classes e relações de uma linguagem específica de domínio, junto com o diagrama, as formas, os conectores, o formato de serialização e a **caixa de ferramentas** da linguagem específica do domínio e suas ferramentas de edição. Em uma solução de linguagem específica do domínio, o código que define essas ferramentas é gerado de acordo com as informações no arquivo DslDefinition.dsl.

Geralmente, você usa o *Designer de linguagem específica de domínio* para editar o arquivo DslDefinition. DSL. No entanto, seu formato bruto é XML e você pode abrir um arquivo DslDefinition.dsl em um editor XML. Você pode achá-lo útil para entender quais informações o arquivo contém e como elas são organizadas para fins de depuração e de extensão.

Os exemplos neste tópico são obtidos a partir do modelo de solução Diagrama de Componente. Para ver um exemplo, crie uma solução de linguagem específica do domínio baseada no modelo de solução Modelos de Componente. Depois de criar a solução, o arquivo DslDefinition.dsl aparece no Designer de Linguagem Específica do Domínio. Feche o arquivo, clique com o botão direito do mouse no **Gerenciador de soluções**, aponte para **abrir com**, clique em **Editor de XML**e em **OK**.

## <a name="sections-of-the-dsldefinitiondsl-file"></a>Seções do Arquivo DslDefinition.dsl

O elemento raiz é \<Dsl >, e seus atributos identificam o nome da linguagem específica do domínio, o namespace e os números de versão principal e secundária para controle de versão. O esquema `DslDefinitionModel` define o conteúdo e a estrutura de um arquivo DslDefinition.dsl válido.

Os elementos filho do elemento raiz do \<Dsl > são os seguintes:

### <a name="classes"></a>Classes

Esta seção define cada classe de domínio que gera uma classe no código gerado.

### <a name="relationships"></a>Relações

Esta seção define cada relação do modelo. A origem e o destino representam os dois lados de uma relação.

### <a name="types"></a>Tipos

Esta seção define cada tipo e seu namespace. As propriedades do domínio possuem dois tipos. `DomainEnumerations` são definidas no modelo e geram tipos no DomainModel.cs. `ExternalTypes` refere-se a tipos que são definidos em qualquer lugar (tal como `String` ou `Int32`) e não geram coisa alguma.

### <a name="shapes"></a>Formas

Esta seção define as formas que descrevem como o modelo aparece em um designer. Essas formas geométricas são mapeadas para as classes no modelo na seção Diagrama.

### <a name="connectors"></a>Conectores

Esta seção define a aparência dos conectores que aparecem em um designer. Essas descrições de estilo geométrico são mapeadas para relacionamentos específicos no modelo na seção Diagrama.

### <a name="xmlserializationbehavior"></a>XmlSerializationBehavior

Esta seção define um esquema de serialização e fornece informações adicionais sobre como cada classe é salva em um arquivo.

### <a name="explorerbehavior"></a>ExplorerBehavior

Esta seção define como a janela **Gerenciador de DSL** é exibida quando o usuário está editando um modelo.

### <a name="connectionbuilders"></a>ConnectionBuilders

Esta seção define um construtor de conexão para cada ferramenta do conector (a ferramenta para criar vínculos entre duas classes que podem ser conectadas). Esta seção determina se você pode conectar uma classe de origem e uma classe de destino.

### <a name="diagram"></a>Diagrama

Esta seção define um diagrama e você o utiliza para especificar propriedades, tais como cor do plano de fundo e a classe raiz. (A classe raiz é a classe de domínio representada pelo diagrama como um todo.) A seção de diagrama também contém elementos ShapeMap e ConnectorMap, que especificam a forma ou o conector que representa cada classe de domínio ou relação.

### <a name="designer"></a>Designer

Esta seção define um designer (editor), que reúne uma **caixa de ferramentas**, configurações de validação, um diagrama e um esquema de serialização. A seção Designer define também a classe raiz do modelo, que também é geralmente a classe raiz do diagrama.

### <a name="explorer"></a>Gerenciador

Esta seção identifica o comportamento do **Gerenciador de DSL** (definido na seção XmlSerializationBehavior).

## <a name="monikers-in-the-dsldefinitiondsl-file"></a>Monikers no arquivo DslDefinition.dsl

Em todo o arquivo DslDefinition.dsl, você pode usar monikers para criar referências cruzadas para itens específicos. Por exemplo, cada definição de Relação contém uma subseção de Origem e uma subseção de Destino. Cada subseção contém o moniker da classe de objeto que pode ser vinculada a essa relação:

```xml
<DomainRelationship ...        Name="LibraryHasMembers" Namespace="ExampleNamespace" >    <Source>      <DomainRole ...>
       <RolePlayer>
         <DomainClassMoniker Name="Library" />
       </RolePlayer>
     </DomainRole>
   </Source>
```

Geralmente, o namespace do item referenciado (neste exemplo, a classe de domínio `Library`) é o mesmo que o item referenciado (neste caso, a relação do domínio LibraryHasMembers). Nesses casos, o moniker deve fornecer somente o nome da classe. Caso contrário, você deve usar a forma completa /Namespace/Nome:

```xml
<DomainClassMoniker Name="/ExampleNameSpace/Library" />
```

O sistema de moniker requer que irmãos na árvore XML tenham nomes distintos. Por esse motivo, ocorrerão erros de validação se você tentar salvar uma definição de linguagem específica do domínio que tenha, por exemplo, duas classes com o mesmo nome. Você deve sempre corrigir tais erros de nome duplicado antes de salvar o arquivo DslDefinition.dsl para que possa recarregá-lo corretamente mais tarde.

Cada tipo tem seu próprio tipo de moniker: DomainClassMoniker, DomainRelationshipMoniker etc.

## <a name="types"></a>Tipos

A seção Tipos especifica todos os tipos que o arquivo DslDefinition.dsl contém como tipos de propriedades. Esses tipos são de dois tipos: tipos externos, tais como System.String, e tipos enumerados.

### <a name="external-types"></a>Tipos externos

O exemplo do Diagrama de Componente lista um conjunto de tipos primitivos padrão, embora somente alguns deles sejam usados.

Cada definição de Tipo Externo consiste em somente um nome e um namespace, tal como Cadeia de Caracteres e Sistema:

```xml
<ExternalType Name="String" Namespace="System" />
```

Os nomes completos dos tipos são usados, em vez das palavras-chave do compilador equivalente, tal como "cadeia de caracteres".

Os tipos externos não estão restritos aos tipos de biblioteca padrão.

### <a name="enumerations"></a>Enumerações

Uma especificação de Enumeração típica se assemelha a este exemplo:

```xml
<DomainEnumeration IsFlags="true" Name="PageSort"          Namespace="Fabrikam.Wizard">
  <Literals>
    <EnumerationLiteral Name="Start" Value="1"/>
    <EnumerationLiteral Name="Decision" Value="2"/>
  </Literals>
</DomainEnumeration>
```

O atributo `IsFlags` controla se o código gerado é prefixado pelo atributo do Common Language Runtime (CLR) `[Flags]`, que determina se os valores da enumeração podem ser bit a bit combinado. Se esse atributo estiver configurado como true, você deverá especificar valores de potência de dois para os valores literais.

## <a name="classes"></a>Classes

A maioria dos elementos em qualquer definição de uma linguagem específica do domínio é direta ou indiretamente instâncias de `DomainClass`. As subclasses de `DomainClass` incluem `DomainRelationship`, `Shape`, `Connector` e `Diagram`. A seção `Classes` do arquivo DslDefinition.dsl lista as classes de domínio.

Cada classe tem um conjunto de propriedades e pode ter uma classe base. No exemplo de Diagrama de Componente, `NamedElement` é uma classe abstrata que possui uma propriedade `Name`, cujo tipo é cadeia de caracteres:

```xml
<DomainClass Id="ee3161ca-2818-42c8-b522-88f50fc72de8"  Name="NamedElement" Namespace="Fabrikam.CmptDsl5"      DisplayName="Named Element"  InheritanceModifier="Abstract">
  <Properties>
    <DomainProperty Id="ef553cf0-33b5-4e34-a30b-cfcfd86f2261"   Name="Name" DisplayName="Name"  DefaultValue="" Category="" IsElementName="true">
      <Type>
        <ExternalTypeMoniker Name="/System/String" />
      </Type>
    </DomainProperty>
  </Properties>
</DomainClass>
```

`NamedElement` é a base de muitas das outras classes, tais como `Component`, que possui suas próprias propriedades, além da propriedade `Name`, que é herdada de `NamedElement`. O nó filho BaseClass contém uma referência de moniker. Como a classe referenciada está no mesmo namespace, somente seu nome é necessário no moniker:

```xml
<DomainClass Name="Component" Namespace="Fabrikam.CmptDsl5"              DisplayName="Component">
  <BaseClass>
    <DomainClassMoniker Name="NamedElement" />
  </BaseClass>
  <Properties>
    <DomainProperty Name="Kind" DisplayName="Kind" >
      <Type>
        <ExternalTypeMoniker Name="/System/String" />
      </Type>
    </DomainProperty>
  </Properties>
```

Cada classe de domínio (incluindo relações, formas, conectores e diagramas) podem ter esses atributos e nós filho:

- **ID.** Esse atributo é um GUID. Se você não fornecer um valor no arquivo, o Designer de Linguagem Específica do Domínio criará um valor. (Nas ilustrações deste documento, esse atributo é geralmente omitido para economizar espaço.)

- **Nome e namespace.** Estes atributos especificam o nome e o namespace da classe no código gerado. Juntos, eles devem ser exclusivos dentro da linguagem específica do domínio.

- **InheritanceModifier.** Esse atributo é "abstrato", "lacrado" ou nenhum.

- **DisplayName.** Esse atributo é o nome que aparece na janela **Propriedades** . O atributo DisplayName pode conter espaços e outra pontuação.

- **GeneratesDoubleDerived.** Se este atributo estiver configurado como true, duas classes serão geradas e uma será uma subclasse da outra. Todos os métodos gerados estão na base e os construtores estão na subclasse. Ao configurar este atributo, você pode substituir qualquer método gerado no código personalizado.

- **HasCustomConstructor**. Se este atributo estiver configurado como true, o construtor será omitido do código gerado para que você possa gravar sua própria versão.

- **Atributos**. Este atributo contém os Atributos CLR da classe gerada.

- **BaseClass**. Se você especificar uma classe base, ela deverá ser do mesmo tipo. Por exemplo, uma classe de domínio deve ter outra classe de domínio como base, e uma forma de compartimento deve ter uma forma de compartimento. Se você não especificar uma classe base, a classe no código gerado será derivada de uma classe de estrutura padrão. Por exemplo, uma classe de domínio é derivada de `ModelElement`.

- **Propriedades**. Esse atributo contém as propriedades que são mantidas sob controle da transação e persistem quando o modelo é salvo.

- **ElementMergeDirectives**. Cada diretiva de mesclagem de elementos controla como uma instância diferente de outra classe é adicionada a uma instância da classe pai. Você pode encontrar mais detalhes sobre diretivas de mesclagem de elementos mais adiante neste tópico.

- Uma classe C# é gerada para cada classe de domínio listada na seção `Classes`. As classes C# são geradas em Dsl\GeneratedCode\DomainClasses.cs.

### <a name="properties"></a>Propriedades

Cada propriedade de domínio possui um nome e um tipo. O nome deve ser exclusivo dentro da classe de domínio e suas bases transitivas.

O tipo deve se referir a um dos tipos listados na seção `Types`. Geralmente, o moniker deve incluir o namespace.

```xml
<DomainProperty Name="Name" DisplayName="Name"  DefaultValue="" Category="" IsElementName="true">
  <Type>
    <ExternalTypeMoniker Name="/System/String" />
  </Type>
</DomainProperty>
```

Cada propriedade de domínio pode ter também estes atributos:

- **Isnavegável**. Esse atributo determina se a propriedade aparece na janela **Propriedades** quando o usuário clica em um objeto da classe pai.

- **IsUIReadOnly**. Esse atributo determina se o usuário pode alterar a propriedade na janela **Propriedades** ou por meio de um decorador no qual a propriedade é apresentada.

- **Tipo**. Você pode configurar este atributo como Normal, Calculado ou CustomStorage. Se você configurar este atributo como Calculado, deverá fornecer um código personalizado que determina o valor e a propriedade será somente leitura. Se você configurar esse atributo como CustomStorage, deverá fornecer o código que obtém e configura valores.

- **IsElementName**. Se esse atributo estiver configurado como true, seu valor será configurado automaticamente como um valor exclusivo quando uma instância da classe pai for criada. Este atributo pode ser configurado como true para somente uma propriedade em cada classe, que deve ter um tipo de cadeia de caracteres. No exemplo de Diagrama de Componente, a propriedade `Name` em `NamedElement` possui o `IsElementName` configurado como true. Sempre que um usuário cria um elemento `Component` (que herda do `NamedElement`), o nome é automaticamente inicializado para algo como "Component6."

- `DefaultValue` Se você tiver especificado este atributo, o valor especificado será atribuído a ele para novas instâncias desta classe. Se `IsElementName` estiver configurado, o atributo DefaultValue especifica a parte inicial da nova cadeia de caracteres.

- **Categoria** é o cabeçalho sob o qual a propriedade aparecerá na janela **Propriedades** .

## <a name="relationships"></a>Relações

A seção `Relationships` lista todos as relações na linguagem específica do domínio. Todo `Domain Relationship` é binário e direcionado, vinculando membros de uma classe de origem a membros de uma classe de destino. As classes de origem e de destino são geralmente classes de domínio, mas relações com outras relações também são permitidas.

Por exemplo, a relação de Conexão vincula membros da classe OutPort a membros da classe InPort. Cada instância da relação conecta uma instância de uma OutPort a uma instância de uma InPort. Uma vez que a relação é de muitos para muitos, cada OutPort pode ter muitos links de Conexão com origens nele e cada instância InPort pode ter muitos links de Conexão que o tenham como destino.

### <a name="source-and-target-roles"></a>Funções de origem e de destino

Todo relacionamento contém funções de origem e de destino que possuem os seguintes atributos:

- O atributo `RolePlayer` faz referências à classe de domínio das instâncias vinculadas: OutPort para origem, InPort para destino.

- O atributo `Multiplicity` possui quatro valores possíveis (ZeroMany, ZeroOne, One e OneMany). Este atributo se refere ao número de links desta relação que pode ser associado a um usuário.

- O atributo `PropertyName` especifica o nome que é usado na função que faz com que a classe acesse os objetos na outra extremidade. Esse nome é usado no modelo ou no código personalizado para percorrer a relação. Por exemplo, o atributo `PropertyName` da função de origem é configurado como `Targets`. Portanto, o código a seguir funcionará:

    ```
    OutPort op = ...; foreach (InPort ip in op.Targets) ...
    ```

     Por convenção, os nomes de propriedades serão plural se a multiplicidade for ZeroMany ou OneMany.

     A multiplicidade de uma função se refere a quanto da função oposta pode ser associada a cada instância dessa função. Por exemplo, na relação ComponentHasPorts, a função de destino possui o atributo `RolePlayer` configurado como Porta, o atributo `PropertyName` configurado como Componente e o atributo `Multiplicity` configurado como ZeroOne. Portanto, o código apropriado para usar essa função é:

    ```
    ComponentPort p = ...; Component c = p.Component; if (c != null) ...
    ```

- O `Name` da função é o nome usado dentro da classe Relação para se referir a essa extremidade de um link. Por convenção, um nome de função é sempre singular, pois cada link tem somente uma instância em cada extremidade. O seguinte código funcionaria:

    ```
    Connection connectionLink = ...; OutPort op = connectionLink.Source;
    ```

- Por padrão, o atributo `IsPropertyGenerator` está configurado como true. Se estiver configurado como false, nenhuma propriedade será criada na classe Usuário. (Nesse caso, `op.Targets`, por exemplo, não funcionaria). No entanto, ainda é possível usar o código personalizado para percorrer a relação ou obter acesso aos próprios links se o código personalizado usar a relação explicitamente:

    ```
    OutPort op = ...; foreach (InPort ip in Connection.GetTargets(op)) ...
    foreach (Connection link in Connection.GetLinksToTargets(op)) ...
    ```

### <a name="relationship-attributes"></a>Atributos da relação

Além disso, para os atributos e nós filho que estão disponíveis para todas as classes, cada relação possui estes atributos:

- **Isinserção**. Este atributo booliano especifica se o relacionamento faz parte da árvore inserida. Cada modelo deve formar uma árvore com as relações inseridas. Cada classe de domínio deve, portanto, ser o destino de pelo menos uma relação inserida, a menos que seja a raiz de um modelo.

- **AllowsDuplicates**. Este atributo booliano, que é false por padrão, aplica-se somente a relações que tenham uma multiplicidade "many" tanto na origem como no destino. Ele determina se os usuários da linguagem podem se conectar a um único par de elementos de origem e de destino por mais de um link da mesma relação.

## <a name="designer-and-toolbox-tabs"></a>Guias Designer e Caixa de Ferramentas

A parte principal da seção de **Designer** do arquivo DslDefinition. DSL é **ToolboxTab** elementos. Um designer pode ter vários desses elementos, cada um representando uma seção de pontas na **caixa de ferramentas**do designer gerado. Cada elemento **ToolboxTab** pode conter um ou mais elementos **ElementTool** , elementos **ConnectionTool** ou ambos.

As ferramentas de elementos podem criar instâncias de uma classe de domínio específica. Quando o usuário arrasta uma ferramenta de elemento no diagrama, o resultado é determinado pelas diretivas de mesclagem de elementos, conforme descrito na seção sobre diretivas de mesclagem de elementos mais adiante neste tópico.

Cada ferramenta de conexão pode invocar um construtor de conexões específico. Um construtor de conexões pode criar mais de um tipo de relação, dependendo se o usuário clicar no mouse, conforme descrito na seção sobre construtores de conexões.

Nenhum tipo de ferramenta constrói formas ou conectores diretamente. Todos instanciam uma classe de domínio ou uma relação de domínio, então, os mapeamentos Forma e Conector determinam como essa classe de domínio ou relação de domínio aparece.

## <a name="paths"></a>Caminhos

Os caminhos de domínio aparecem em vários locais no arquivo DslDefinition.dsl. Esses caminhos especificam uma série de links de um elemento em um modelo (ou seja, uma instância da linguagem específica do domínio) para outro. A sintaxe de caminho é simples, mas detalhada.

Os caminhos aparecem no arquivo DslDefinition.dsl, em marcas `<DomainPath>...</DomainPath>`. Embora os caminhos possam navegar por vários links, a maioria dos exemplos, na prática, percorre apenas um link.

Um caminho consiste em uma sequência de segmentos. Cada segmento é um salto de um objeto para um link ou de um link para um objeto. Portanto, os saltos geralmente se alternam em um caminho longo. O primeiro salto é de um objeto para um link, o segundo salto é para o objeto na outra extremidade do link, o terceiro salto é para o próximo link etc. A exceção ocasional para essa sequência ocorre quando uma relação é a própria origem ou o destino de outra relação.

Todo segmento inicia com um nome de relação. Em um salto de objeto para link, a relação precede um ponto e o nome da propriedade: "`Relationship . Property`". Em um salto de link para objeto, a relação precede um ponto de exclamação e o nome da função: "`Relationship ! Role`".

O exemplo de Diagrama de Componente contém um caminho no ParentElementPath do ShapeMap para InPort. Esse caminho inicia como indicado a seguir:

```
    ComponentHasPorts.Component
```

Neste exemplo, InPort é uma subclasse de ComponentPort e possui uma relação ComponentHasPorts. A propriedade é chamada de Componente.

Ao escrever C# em relação a esse modelo, você pode percorrer um link em uma etapa usando a propriedade que a relação gera em cada uma das classes que ele relaciona:

```
     InPort port; ...  Component c = port.Component;
```

No entanto, você deve executar ambos os saltos explicitamente na Sintaxe de Caminho. Em função desse requisito, você pode acessar o link intermediário com mais facilidade. O seguinte código completa o salto do link para o Componente:

```
    ComponentHasPorts.Component / ! Component
```

(Você pode omitir o nome da relação quando ele for igual ao do segmento anterior.)

## <a name="element-merge-directives"></a>Diretivas de mesclagem de elementos

Quando o usuário da linguagem arrasta um item da **caixa de ferramentas** para o diagrama, uma instância da classe da ferramenta é construída. Além disso, links são criados entre essa instância e os elementos de modelo existentes. Alguns itens, como componentes ou comentários, são criados quando o usuário da linguagem os arrasta da caixa de **ferramentas** para uma parte em branco do diagrama. Outros itens são criados quando o usuário da linguagem os arrasta de outros elementos do host. Por exemplo, uma OutPort ou InPort é criada quando o usuário da linguagem a arrasta para um componente.

Uma classe de host potencial, como Componente, aceitará um novo elemento somente se a classe do host tiver uma diretiva de mesclagem de elementos para a classe do novo elemento. Por exemplo, o nó DomainClass com Nome="Componente" contém:

```xml
<DomainClass Name="Component" ...> ...
    <ElementMergeDirective>
      <Index>
        <DomainClassMoniker Name="ComponentPort" />
      </Index>
      <LinkCreationPaths>
        <DomainPath>ComponentHasPorts.Ports</DomainPath>
      </LinkCreationPaths>
    </ElementMergeDirective> ...
```

O moniker da classe que está no nó Índice faz referências à classe de elemento que pode ser aceita. Nesse caso, ComponentPort é a classe base abstrata de InPort e OutPort. Portanto, qualquer um desses elementos pode ser aceito.

ComponentModel, a classe raiz da linguagem, possui diretivas de mesclagem de elementos para componentes e comentários. O usuário da linguagem pode arrastar itens para essas classes diretamente no diagrama, pois as partes em branco do diagrama representam a classe raiz. No entanto, ComponentModel não possui diretiva de mesclagem de elementos para ComponentPort. Portanto, o usuário da linguagem não pode arrastar InPorts ou OutPorts diretamente para o diagrama.

A diretiva de mesclagem de elementos determina qual link ou quais links são criados para que o novo elemento possa se integrar ou mesclar ao modelo existente. Para uma ComponentPort, uma instância de ComponentHasPorts é criada. O DomainPath identifica o relacionamento e a propriedade da classe pai, Portas, às quais o novo elemento será adicionado.

Você pode criar mais de um link em uma diretiva de mesclagem de elementos ao incluir mais de um caminho de criação de link. Um dos caminhos deve ser inserido.

Você pode usar mais de um segmento em um caminho de criação de link. Nesse caso, o último segmento define qual link deve ser criado. Os segmentos anteriores navegam da classe pai para o objeto a partir do qual o novo link deverá ser criado.

Por exemplo, você pode adicionar essa diretiva de mesclagem de elementos à classe Componente:

```xml
<DomainClass Name="Component" ...> ...
  <ElementMergeDirective>
    <Index>
       <DomainClassMoniker Name="Comment"/>
    </Index>
    <LinkCreationPaths>
       <DomainPath>          ComponentModelHasComponents . ComponentModel / !ComponentModel         / ComponentModelHasComments.Comments       </DomainPath>
       <DomainPath>CommentsReferenceComponents.Comments</DomainPath>
    </LinkCreationPaths>
  </ElementMergeDirective>
```

Os usuários da linguagem podem então arrastar um comentário para um componente e ter o novo comentário criado automaticamente com um link para o componente.

O caminho de criação do primeiro link navega do `Component` para o `ComponentModel` e cria uma instância da relação inserida `ComponentModelHasComments`. O caminho de criação do segundo link cria um link da relação de referência CommentsReferenceComponents do Componente do host para o novo Comentário. Todos os caminhos de criação de links devem iniciar com a classe do host e devem terminar em um link que avança em direção à classe recém-instanciada.

## <a name="xmlclassdata"></a>XmlClassData

Cada classe de domínio (incluindo relações e outros subtipos) podem ter informações extras fornecidas em um nó `XmlClassData`, que aparece na seção `XmlSerializationBehavior` do arquivo DslDefinition.dsl. Essas informações estão especificamente relacionadas a como as instâncias da classe são armazenadas na forma serializada quando um modelo é salvo em um arquivo.

A maior parte do código gerado que `XmlSerializationBehavior` influencia está em `Dsl\GeneratedCode\Serializer.cs`.

Todo nó `XmlClassData` inclui esses nós e atributos filhos:

- Um nó de moniker, que faz referência à classe na qual se aplicam os dados.

- **XmlPropertyData** para cada propriedade que é definida na classe.

- **XmlRelationshipData** para cada relação que é originada na classe. (Os relacionamentos também têm seus próprios nós XmlClassData.)

- O atributo de cadeia de caracteres **TypeName** , que determina o nome da classe auxiliar de serialização no código gerado.

- Cadeia de caracteres **ElementName** , que determina a marca XML de instâncias serializadas dessa classe. Por convenção, o ElementName é geralmente o mesmo que o nome da classe, exceto que a primeira letra é minúscula. Por exemplo, um arquivo de modelo de exemplo se inicia com o seguinte:

    ```xml
    <componentModel ...
    ```

- **MonikerElementName** nos arquivos de modelo serializado do usuário. Esse atributo apresenta um moniker que faz referências a esta classe.

- **MonikerAttributeName**, que identifica o nome do atributo XML dentro de um moniker. Nesse fragmento do arquivo serializado de um usuário, o autor da linguagem específica do domínio definiu **MonikerElementName** como "inPortMoniker" e **MonikerAttributeName** como "Path":

    ```xml
    <inPortMoniker path="//Component2/InPort1" />
    ```

### <a name="connectionbuilders"></a>ConnectionBuilders

Um construtor de conexões é definido para cada ferramenta de conexão. Cada construtor de conexões consiste em um ou mais elementos LinkConnectDirective, cada um dos quais contendo um ou mais elementos SourceDirective e um ou mais elementos TargetDirective. Depois de clicar em uma ferramenta de conexão, o usuário pode iniciar uma conexão a partir de qualquer forma mapeada para um elemento de modelo que aparece na lista de elementos SourceDirective. Com isso, a conexão pode ser concluída em uma forma mapeada para um elemento que aparece na lista de elementos TargetDirective. A classe de relação instanciada depende do elemento LinkConnectDirective designado por onde a conexão foi iniciada.

### <a name="xmlpropertydata"></a>XmlPropertyData

Um atributo **DomainPropertyMoniker** identifica a propriedade à qual os dados se referem. Esse atributo deve ser uma propriedade da classe delimitadora ClassData.

O atributo **XmlName** fornece o nome do atributo correspondente como ele deve aparecer no XML. Por convenção, essa cadeia de caracteres é igual ao nome da propriedade, exceto que a primeira letra é minúscula.

Por padrão, o atributo de **representação** é definido como atributo. Se **representação** for definida como elemento, um nó filho será criado no XML. Se **representação** for definida como ignorar, a propriedade não será serializada.

Os atributos **IsMonikerKey** e **IsMonikerQualifier** fornecem uma propriedade a uma função na identificação de instâncias da classe pai. Você pode definir **IsMonikerKey** como true para uma propriedade que é definida em ou herdada por uma classe. Esse atributo identifica uma instância individual da classe pai. A propriedade que você configura como `IsMonikerKey` é geralmente um nome ou outro identificador de chave. Por exemplo, a propriedade de cadeia de caracteres `Name` é a chave do moniker para NamedElement e suas classes derivadas. Quando o usuário salva um modelo no arquivo, esse atributo deve conter valores exclusivos para cada instância, entre seus irmãos na árvore de relações inseridas.

No arquivo de modelo serializado, o moniker completo de um elemento é um caminho da raiz do modelo até a árvore de relações inseridas, fazendo a cotação da chave do moniker em cada ponto. Por exemplo, InPorts são inseridas dentro de Componentes, que são, por sua vez, inseridos na raiz do modelo. Um moniker válido é portanto:

```xml
<inPortMoniker name="//Component2/InPort1" />
```

Você pode definir o atributo **IsMonikerQualifier** para uma propriedade de cadeia de caracteres e fornecer uma maneira adicional de construir o nome completo de um elemento. Por exemplo, no arquivo DslDefinition. DSL, **namespace** é um qualificador de moniker.

### <a name="xmlrelationshipdata"></a>XmlRelationshipData

Dentro de um arquivo de modelo serializado, os links (dos relacionamentos inserido e de referência) são representados por nós filho da extremidade de origem da relação. Para relações inseridas, o nó filho contém uma subárvore. Para relacionamentos de referência, o nó filho contém um moniker que faz referência a outra parte da árvore.

O atributo **XmlRelationshipData** em um atributo **XmlClassData** define exatamente como os nós filho são aninhados dentro do elemento Source. Cada relação que é uma origem na classe de domínio tem um atributo **XmlRelationshipData** .

O atributo **DomainRelationshipMoniker** identifica uma das relações originadas na classe.

O atributo **RoleElementName** fornece o nome da marca XML que coloca o nó filho nos dados serializados.

Por exemplo, o arquivo DslDefinition.dsl contém:

```xml
<XmlClassData ElementName="component" ...>
  <DomainClassMoniker Name="Component" />
  <ElementData>
    <XmlRelationshipData RoleElementName="ports">
      <DomainRelationshipMoniker Name="ComponentHasPorts" />
    </XmlRelationshipData>
```

Portanto, o arquivo serializado contém:

```xml
<component name="Component1"> <!-- parent -->
   <ports> <!-- role -->
     <outPort name="OutPort1"> <!-- child element -->
       ...
     </outPort>
   </ports> ...
```

Se o atributo **UseFullForm** for definido como true, uma camada extra de aninhamento será introduzida. Essa camada representa a relação propriamente dita. O atributo deve ser configurado como true se a relação tiver propriedades.

```xml
<XmlClassData ElementName="outPort">
   <DomainClassMoniker Name="OutPort" />
   <ElementData>
     <XmlRelationshipData UseFullForm="true" RoleElementName="targets">
       <DomainRelationshipMoniker Name="Connection" />
     </XmlRelationshipData>
   </ElementData>
 </XmlClassData>
```

O arquivo serializado contém:

```xml
<outPort name="OutPort1">  <!-- Parent -->
   <targets>  <!-- role -->
     <connection sourceRoleName="X">  <!-- relationship link -->
         <inPortMoniker name="//Component2/InPort1" /> <!-- child -->
     </connection>
    </targets>
  </outPort>
```

(A Relação de Conexão possui seus próprios dados de classe XML, que fornecem seus nomes de elemento e de atributo.)

Se o atributo **omitielement** for definido como true, o nome da função de relacionamento será omitido, o que abreviará o arquivo serializado e não será ambíguo se as duas classes não tiverem mais de uma relação. Por exemplo:

```xml
<component name="Component3">
  <!-- only one relationship could get here: -->
  <outPort name="OutPort1">
     <targets> ...
```

### <a name="serialization-of-a-domain-specific-language-definition"></a>Serialização de uma definição de linguagem específica do domínio

O arquivo DslDefinition.dsl é por si só um arquivo serializado e em conformidade com uma definição de linguagem específica do domínio. A seguir, estão alguns exemplos de definições de serialização de XML:

- **DSL** é o nó RootClass e a classe do diagrama. DomainClass, DomainRelationship e outros elementos são inseridos em `Dsl`.

- **Classes** é o **RoleElementName** da relação entre a linguagem específica do domínio e o DomainClass.

```xml
<Dsl Name="CmptDsl5" ...>
  <Classes>
    <DomainClass Name="NamedElement" InheritanceModifier="Abstract" ...
```

- O atributo **XmlSerializationBehavior** é inserido no atributo `Dsl`, mas o atributo **omitielement** foi definido na relação de incorporação. Portanto, nenhum atributo `RoleElementName` interfere. Por outro lado, um atributo **ClassData** é o atributo `RoleElementName` da relação incorporada entre um atributo **XmlSerializationBehavior** e um atributo **XmlClassData** .

```xml
<Dsl Name="CmptDsl5" ...> ...
  <XmlSerializationBehavior Name="ComponentsSerializationBehavior" >
    <ClassData>
      <XmlClassData ...>...</XmlClassData>
      <XmlClassData ...>...</XmlClassData>
```

- ConnectorHasDecorators é a relação inserida entre `Connector` e `Decorator`. `UseFullForm` foi configurado para que o nome da relação apareça com sua lista de propriedades de cada link do objeto Conector. No entanto, `OmitElement` também foi configurado para que nenhum `RoleElementName` inclua os vários links que são inseridos dentro do `Connector`:

```xml
<Connector Name="AssociationLink" ...>
  <ConnectorHasDecorators Position="TargetTop" ...>
    <TextDecorator Name="TargetRoleName"   />
  </ConnectorHasDecorators>
  <ConnectorHasDecorators Position="SourceTop" ...>
    <TextDecorator Name="SourceRoleName"   />
  </ConnectorHasDecorators>
</Connector>
```

## <a name="shapes-and-connectors"></a>Formas e Conectores

As definições de Forma e Conector herdam atributos e nós filhos de classes de domínio, além do seguinte:

- `Color` e atributos de `Line``Style` .

- **ExposesFillColorAsProperty** e vários atributos semelhantes. Esses atributos boolianos tornam variável a propriedade correspondente pelo usuário. Geralmente, quando um usuário de idioma clica em uma forma no diagrama, as propriedades que aparecem na janela **Propriedades** são aquelas da instância de classe de domínio na qual a forma é mapeada. Se `ExposesFillColorAsProperty` estiver configurado como true, uma propriedade da própria forma também aparece.

- **ShapeHasDecorators**. Uma instância deste atributo ocorre para cada texto, ícone ou expandir/recolher decorador. (No arquivo DslDefinition.dsl, `ShapeHasDecorators` é uma relação com `UseFullForm` configurado como true.)

## <a name="shape-maps"></a>Mapas de formas

Os mapas de formas determinam como as instâncias de uma determinada classe de domínios aparecem na tela, representadas por uma forma. Os mapas de forma e de conector aparecem na seção `Diagram` do arquivo DslDefinition.dsl.

Como no exemplo a seguir, os elementos `ShapeMap` têm, no mínimo, o moniker de uma classe de domínio, o moniker de uma forma e um elemento `ParentElementPath`:

```xml
<ShapeMap>
  <DomainClassMoniker Name="InPort" />
  <ParentElementPath>
    <DomainPath>ComponentHasPorts.Component/!Component</DomainPath>
  </ParentElementPath>
  <PortMoniker Name="InPortShape" />
</ShapeMap>
```

A função primária do elemento `ParentElementPath` é fazer com que a mesma classe de objetos apareça como uma forma diferente em contextos diferentes. Por exemplo, se uma `InPort` também puder ser inserida em um comentário, a `InPort` poderá aparecer como uma forma diferente dessa finalidade.

Em segundo lugar, o caminho determina como a forma se relaciona com seu pai. Nenhuma estrutura inserida é definida entre as formas em um arquivo DslDefinition.dsl. Você deve inferir a estrutura a partir dos mapas de forma. O pai de uma forma é a forma mapeada para o elemento de domínio que o caminho do elemento pai identifica. Nesse caso, o caminho identifica o componente ao qual pertence o `InPort`. Em outro mapa de forma, a classe Componente é mapeada para ComponentShape. Portanto, a nova forma `InPort` passa a ser uma forma filha de `ComponentShape` de seu componente.

Se, em vez disso, você anexou a forma InPort ao diagrama, o caminho do elemento pai deve ter outra etapa para o modelo de componente, que é mapeado para o diagrama:

```
ComponentHasPorts . Component / ! Component /    ComponentModelHasComponents . ComponentModel / ! ComponentModel
```

A raiz do modelo não tem um mapa de forma. Em vez disso, a raiz é referenciada diretamente do diagrama, que possui um elemento `Class`:

```xml
<Diagram Name="ComponentDiagram" >
    <Class>
      <DomainClassMoniker Name="ComponentModel" />
    </Class>...
```

### <a name="decorator-maps"></a>Mapas do decorador

Um mapa do decorador associa uma propriedade na classe mapeada para um decorador na forma. Se a propriedade for um tipo enumerado ou booliano, seu valor poderá determinar se o decorador é visível ou não. Se o decorador for um decorador de texto, o valor da propriedade poderá aparecer e o usuário poderá editá-lo.

### <a name="compartment-shape-maps"></a>Mapas de formas de compartimento

Os mapas de formas de compartimento são subtipos de mapas de forma.

## <a name="connector-maps"></a>Mapas do conector

O mapa do conector mínimo faz referência a um conector e a um relacionamento:

```xml
<ConnectorMap>
  <ConnectorMoniker Name="CommentLink" />
  <DomainRelationshipMoniker Name="CommentsReferenceComponents" />
</ConnectorMap>
```

Os mapas do conector também podem conter mapas do decorador.

## <a name="see-also"></a>Consulte também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
- [Como definir uma linguagem específica de domínio](../modeling/how-to-define-a-domain-specific-language.md)
- [Noções básicas sobre modelos, classes e relações](../modeling/understanding-models-classes-and-relationships.md)