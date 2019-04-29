---
title: Referência DGML
ms.date: 11/04/2016
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b473dc706cd7183835c5d84091fb53e45337c013
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62834211"
---
# <a name="directed-graph-markup-language-dgml-reference"></a>Referência DGML

Directed Graph Markup Language (DGML) descreve as informações usadas para visualização e para executar a análise de complexidade e é o formato usado para persistir os mapas de código no Visual Studio. Ele usa XML simples para descrever gráficos direcionados cíclicos e acíclicos. Um gráfico direcionado é um conjunto de nós conectados por links ou bordas. Nós e links podem ser usados representam estruturas de rede como, por exemplo, elementos em um projeto de software.

Observe que algumas versões do Visual Studio suporta apenas um subconjunto dos recursos DGML, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

> [!NOTE]
> Quando você edita um arquivo .dgml, o IntelliSense ajuda você a identificar atributos disponíveis para cada elemento e seus valores. Para especificar a cor em um atributo, use nomes de cores comuns como, por exemplo, "Azul", ou valores hexadecimais ARGB, como "#ffa0b1c3". DGML usa um subconjunto pequeno de formatos de definição de cor do WPF (Windows Presentation Foundation). Para obter mais informações, consulte [cores classe](http://go.microsoft.com/fwlink/?LinkId=182345).

## <a name="DGML"></a> Sintaxe DGML

A tabela a seguir descreve os tipos de elementos que são usados em DGML:

- `<DirectedGraph></DirectedGraph>`

   Esse elemento é o elemento raiz do documento de mapa (. dgml) do código. Todos os outros elementos de DGML são exibidos no escopo desse elemento.

   A seguinte lista descreve atributos opcionais que é possível incluir:

   `Background` – A cor do plano de fundo de mapa

   `BackgroundImage` -O local de um arquivo de imagem para usar como plano de fundo de mapa.

   `GraphDirection` -Quando o mapa é definido como layout da árvore (`Sugiyama`), organize os nós, de modo que a maioria dos links de fluxo na direção especificada: `TopToBottom`, `BottomToTop`, `LeftToRight`, ou `RightToLeft`. Ver [alterar o layout do mapa](../modeling/browse-and-rearrange-code-maps.md#Selecting).

   `Layout` -Definir o mapa para os seguintes layouts: `None`, `Sugiyama` (layout da árvore) `ForceDirected` (clusters rápidos) ou `DependencyMatrix`. Ver [alterar o layout do mapa](../modeling/browse-and-rearrange-code-maps.md#Selecting).

   `NeighborhoodDistance` -Quando o mapa é definido como o layout da árvore ou o layout de clusters rápidos, mostre apenas os nós que sejam números especificados (1-7) de links afastados de nós selecionados. Ver [alterar o layout do mapa](../modeling/browse-and-rearrange-code-maps.md#Selecting).

   Exemplo:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" Background="Blue" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        ...
     </Nodes>
     <Links>
        ...
     </Links>
     <Categories>
        ...
     </Categories>
     <Properties>
        ...
     </Properties>
  </DirectedGraph>
  ```

- `<Nodes></Nodes>`

   Esse elemento opcional contém uma lista de `<Node/>` elementos, que definem nós no mapa. Para obter mais informações, consulte o elemento `<Node/>`.

  > [!NOTE]
  > Quando você faz referência a um nó indefinido em um `<Link/>` o mapa de elemento, cria um `<Node/>` elemento automaticamente.

   Exemplo:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node ... />
     </Nodes>
     <Links>
        <Link ... />
     </Links>
  </DirectedGraph>
  ```

- `<Node/>`

   Esse elemento define um único nó. Ele é exibido na lista de elementos `<Nodes><Nodes/>`.

   Esse elemento deve incluir os seguintes atributos:

   `Id` - O nome exclusivo do nó e o valor padrão do atributo `Label`, caso nenhum atributo `Label` separado seja especificado. Esse nome deve corresponder ao atributo `Source` ou `Target` do link que faz referência a ele.

   A seguinte lista descreve alguns dos atributos opcionais que é possível incluir:

   `Label` -O nome de exibição do nó.

   Atributos de estilo. Consulte [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md).

   `Category` - O nome de uma categoria que identifica os elementos que compartilham esse atributo. Para obter mais informações, consulte o elemento `<Category/>`.

   `Property` - O nome de uma propriedade que identifica elementos que têm o mesmo valor da propriedade. Para obter mais informações, consulte o elemento `<Property/>`.

   `Group` - Se o nó contiver outros nós, defina esse atributo como `Expanded` ou `Collapsed` para mostrar ou ocultar seu conteúdo. Deve haver um elemento `<Link/>` que inclua o atributo `Category="Contains"` e especifique o nó pai como o nó de origem e o nó filho como o nó de destino. Ver [agrupar elementos de código](../modeling/customize-code-maps-by-editing-the-dgml-files.md#OrganizeNodes).

   `Visibility` - Defina esse atributo como `Visible`, `Hidden` ou `Collapsed`. Usa `System.Windows.Visibility`. Ver [ocultar ou Mostrar nós e links](../modeling/browse-and-rearrange-code-maps.md#HidingShowing).

   `Reference` - Defina esse atributo para vincular a um documento ou a uma URL. Ver [vincular documentos ou URLs para elementos de código e links](../modeling/customize-code-maps-by-editing-the-dgml-files.md#AddReferences).

   Exemplo:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Student" Category="Person" />
        <Node Id="Passenger" Label="Instructor" Category="Person" />
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
     </Nodes>
     <Links>
        <Link ... />
     </Links>
     <Categories>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
     </Categories>
  </DirectedGraph>
  ```

- `<Links></Links>`

   Esse elemento contém a lista de elementos `<Link>`, que definem links entre nós. Para obter mais informações, consulte o elemento `<Link/>`.

   Exemplo:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Links>
        <Link ... />
     </Links>
  </DirectedGraph>
  ```

- `<Link/>`

   Esse elemento define um único link que conecta um nó de origem a um nó de destino. Ele é exibido na lista de elementos `<Links></Links>`.

  > [!NOTE]
  > Se esse elemento fizer referência a um nó indefinido, o documento de mapa cria automaticamente um nó que possui os atributos especificados, se houver.

   Esse elemento deve incluir os seguintes atributos:

   `Source` - O nó de origem do link

   `Target` - O nó de destino do link

   A seguinte lista descreve alguns dos atributos opcionais que é possível incluir:

   `Label` - O nome para exibição do link

   Atributos de estilo. Consulte [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md).

   `Category` - O nome de uma categoria que identifica os elementos que compartilham esse atributo. Para obter mais informações, consulte o elemento `<Category/>`.

   `Property` - O nome de uma propriedade que identifica elementos que têm o mesmo valor da propriedade. Para obter mais informações, consulte o elemento `<Property/>`.

   Exemplo:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Student" Category="Person" />
        <Node Id="Passenger" Label="Instructor" Category="Person" />
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
     </Nodes>
     <Links>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
        <Link Source="Driver" Target="Car" Label="Passed" Stroke="Black" Background="Green" Category="PassedTest" />
        <Link Source="Driver" Target="Truck" Label="Failed" Stroke="Black" Background="Red" Category="PassedTest" />
     </Links>
  </DirectedGraph>
  ```

- `<Categories></Categories>`

   Esse elemento contém a lista de elementos `<Category/>`. Para obter mais informações, consulte o elemento `<Category/>`.

   Exemplo:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Categories>
         <Category ... />
     </Categories>
  </DirectedGraph>
  ```

- `<Category/>`

   Esse elemento define um atributo `Category`, que é usado para identificar os elementos que compartilham esse atributo. Um `Category` atributo pode ser usado para organizar os elementos do mapa, fornecer atributos compartilhados por meio de herança ou definir metadados adicionais.

   Esse elemento deve incluir os seguintes atributos:

   `Id` - O nome exclusivo da categoria e o valor padrão do atributo `Label`, caso nenhum atributo `Label` separado seja especificado.

   A seguinte lista descreve alguns dos atributos opcionais que é possível incluir:

   `Label` - Um nome amigável para o leitor da categoria.

   `BasedOn` - A categoria pai da qual `<Category/>` herda o elemento atual.

   No exemplo desse elemento, a categoria `FailedTest` herda seu atributo `Stroke` da categoria `PassedTest`. Consulte "para criar categorias hierárquicas" em [mapas de código de personalizar, editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md).

   As categorias também fornecem um comportamento do modelo básico que controla a aparência de nós e links quando eles são exibidos em um mapa. Consulte [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md).

   Exemplo:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Driver" Category="Person" />
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
        <Node Id="Passenger" Category="Person" />
     </Nodes>
     <Links>
        <Link Source="Driver" Target="Car" Label="Passed" Category="PassedTest" />
        <Link Source="Driver" Target="Truck" Label="Failed" Category="FailedTest" />
     </Links>
     <Categories>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
        <Category Id="PassedTest" Label="Passed" Stroke="Black" Background="Green" />
        <Category Id="FailedTest" Label="Failed" BasedOn="PassedTest" Background="Red" />
     </Categories>
  </DirectedGraph>
  ```

- `<Properties></Properties>`

   Esse elemento contém a lista de elementos `<Property/>`. Para obter mais informações, consulte o elemento `<Property/>`.

   Exemplo:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Properties>
         <Property ... />
     </Properties>
  </DirectedGraph>
  ```

- `<Property/>`

   Esse elemento define um atributo `Property` que é possível usar para atribuir um valor a qualquer elemento ou atributo DGML, inclusive categorias e outras propriedades.

   Esse elemento deve incluir os seguintes atributos:

  - `Id` - O nome exclusivo da propriedade e o valor padrão do atributo `Label`, caso nenhum atributo `Label` separado seja especificado.

  - `DataType` - O tipo de dados armazenado pela propriedade

    Se você quiser que a propriedade apareça na **propriedades** janela, use o `Label` propriedade para especificar o nome de exibição da propriedade.

    Ver [atribuir categorias a elementos de código e links](../modeling/customize-code-maps-by-editing-the-dgml-files.md#AssignCategories).

    Exemplo:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Driver" Category="Person" DrivingAge="18"/>
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
        <Node Id="Passenger" Category="Person" />
     </Nodes>
     <Links>
        <Link Source="Driver" Target="Car" Label="Passed" Category="PassedTest" />
        <Link Source="Driver" Target="Truck" Label="Failed" Category="FailedTest" />
     </Links>
     <Categories>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
        <Category Id="PassedTest" Label="Passed" Stroke="Black" Background="Green" />
        <Category Id="FailedTest" Label="Failed" BasedOn="PassedTest" Background="Red" />
     </Categories>
     <Properties>
         <Property Id="DrivingAge" Label="Driving Age" DataType="System.Int32" />
     </Properties>
  </DirectedGraph>
  ```

### <a name="AddAlias"></a> Aliases para caminhos mais usados

A substituição dos caminhos mais usados por aliases ajuda a reduzir o tamanho do arquivo .dgml e o tempo necessário para carregar ou salvar o arquivo. Para criar um alias, adicione uma seção `<Paths></Paths>` ao final do arquivo .dgml. Nesta seção, adicione um elemento `<Path/>` para definir um alias para o caminho:

```xml
<Paths>
   <Path Id="MyPathAlias" Value="C:\...\..." />
</Paths>
```

Para referenciar o alias de um elemento no arquivo. dgml, coloque o `Id` do \<caminho / > elemento com um sinal de cifrão ($) e parênteses (()):

```xml
<Nodes>
   <Node Id="MyNode" Reference="$(MyPathAlias)MyDocument.txt" />
</Nodes>
<Properties>
   <Property Id="Reference" Label="My Document" DataType="System.String" IsReference="True" />
</Properties>
```

## <a name="see-also"></a>Consulte também

- [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)
- [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)
- [Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)