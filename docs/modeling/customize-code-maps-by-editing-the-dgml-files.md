---
title: Personalizar mapa de códigos editando os arquivos DGML
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- dependency graphs, creating path aliases
- dependency graphs, linking items to nodes
- graph documents, creating path aliases
- dependency graphs, grouping nodes
- graph documents, editing
- graph documents, linking items to nodes
- graph documents, customizing
- graph documentings, assigning categories and properties
- dependency graphs, editing
- dependency graphs, customizing
- graph documents, grouping nodes
- dependency graphs, assigning categories and properties
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 24afbfcfe31de52ac51329bb67df41cc59dd6f1e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547271"
---
# <a name="customize-code-maps-by-editing-the-dgml-files"></a>Personalizar mapa de códigos editando os arquivos DGML

Para personalizar um mapa de código, você pode editar o arquivo direcionado do grafo Markup Language (. dgml). Por exemplo, você pode editar elementos para especificar estilos personalizados, atribuir propriedades e categorias a elementos de código e links, ou vincular documentos ou URLs a elementos de código ou links. Para obter mais informações sobre elementos DGML, consulte [referência de DGML (direcionado ao grafo Markup Language)](../modeling/directed-graph-markup-language-dgml-reference.md).

Edite o arquivo. dgml do mapa de código em um editor de texto ou XML. Se o mapa fizer parte de sua solução do Visual Studio, selecione-o em **Gerenciador de soluções**, abra o menu de atalho e escolha **abrir com**, **Editor de XML (texto)**.

> [!NOTE]
> Para criar mapas de código, você deve ter o Visual Studio Enterprise Edition. Quando você edita um mapa de código no Visual Studio, ele limpa todos os elementos e atributos DGML não utilizados, excluindo-os quando você salva o arquivo. dgml. Ele também cria elementos de código automaticamente quando você adiciona novos links manualmente. Quando você salva o arquivo .dgml, todos os atributos adicionados a um elemento podem se reorganizar em ordem alfabética.

## <a name="group-code-elements"></a><a name="OrganizeNodes"></a>Elementos de código de grupo
 Você pode adicionar novos grupos ou converter nós existentes em um grupo.

1. Abra o arquivo. dgml em um editor de texto ou XML.

2. Para converter um elemento de código em um grupo, localize o `<Node/>` elemento para esse elemento de código.

    \- ou –

    Para adicionar um novo grupo, localize a `<Nodes>` seção. Adicione um novo `<Node/>` elemento.

3. No elemento `<Node/>`, adicione um atributo `Group` para especificar se o grupo aparece expandido ou recolhido. Por exemplo:

   ```xml
   <Nodes>
      <Node Id="MyFirstGroup" Group="Expanded" />
      <Node Id="MySecondGroup" Group="Collapsed" />
   </Nodes>
   ```

4. Na seção, certifique-se de `<Links>` que um `<Link/>` elemento que tem os seguintes atributos exista para cada relação entre um elemento de código de grupo e seus elementos de código filho:

   - Um `Source` atributo que especifica o elemento de código de grupo

   - Um `Target` atributo que especifica o elemento de código filho

   - Um `Category` atributo que especifica uma `Contains` relação entre o elemento de código de grupo e seu elemento de código filho

     Por exemplo:

   ```xml
   <Links>
      <Link Category="Contains" Source="MyFirstNewGroup" Target="FirstGroupChildOne" />
      <Link Category ="Contains" Source="MyFirstNewGroup" Target="FirstGroupChildTwo" />
      <Link Category ="Contains" Source="MySecondNewGroup" Target="SecondGroupChildOne" />
      <Link Category="Contains" Source="MySecondNewGroup" Target="SecondGroupChildTwo" />
   </Links>
   ```

    Para obter mais informações sobre o `Category` atributo, consulte [atribuir categorias a elementos de código e links](#AssignCategories).

## <a name="change-the-style-of-the-map"></a><a name="ChangeGraphStyle"></a>Alterar o estilo do mapa
 Você pode alterar a cor do plano de fundo e a cor da borda do mapa editando o arquivo. dgml do mapa. Para alterar o estilo de elementos de código e links, consulte [alterar o estilo de elementos de código e links](#Highlight).

1. Abra o arquivo. dgml em um editor de texto ou XML.

2. No elemento `<DirectedGraph>`, adicione todos os seguintes atributos para alterar o estilo:

     Cor da tela de fundo

    ```xml
    Background="ColorNameOrHexadecimalValue"
    ```

     Cor da borda

    ```xml
    Stroke="StrokeValue"
    ```

     Por exemplo:

    ```xml
    <DirectedGraph Background="Green" xmlns="http://schemas.microsoft.com/vs/2009/dgml" >
       ...
       ...
    </DirectedGraph>
    ```

## <a name="change-the-style-of-code-elements-and-links"></a><a name="Highlight"></a>Alterar o estilo de elementos de código e links

### <a name="CreateCustomStyles"></a>
 Você pode aplicar estilos personalizados aos seguintes elementos de código:

- Elementos de código único e links

- Grupos de elementos de código e links

- Grupos de elementos de código e links com base em determinadas condições

> [!TIP]
> Se você tiver estilos repetidos em vários elementos de código ou links, poderá considerar aplicar uma categoria a esses elementos de código ou links e, em seguida, aplicar um estilo a essa categoria. Para obter mais informações, consulte [atribuir categorias a elementos de código e links](#AssignCategories) e [atribuir propriedades a elementos de código e links](#AssignProperties).

##### <a name="to-apply-a-custom-style-to-a-single-code-element"></a>Para aplicar um estilo personalizado a um único elemento de código

1. Abra o arquivo. dgml em um editor de texto ou XML.

2. Localize o elemento do elemento de código `<Node/>` . Adicione qualquer um desses atributos para personalizar seu estilo:

     Cor da tela de fundo

    ```xml
    Background="ColorNameOrHexadecimalValue"
    ```

     Contorno

    ```xml
    Stroke="ColorNameOrHexadecimalValue"
    ```

     Espessura do contorno

    ```xml
    StrokeThickness="StrokeValue"
    ```

     Cor do texto

    ```xml
    Foreground="ColorNameOrHexadecimalValue"
    ```

     Ícone

    ```xml
    Icon="IconFilePathLocation"
    ```

     Tamanho do texto

    ```xml
    FontSize="FontSizeValue"
    ```

     Tipo de texto

    ```xml
    FontFamily="FontFamilyName"
    ```

     Peso do texto

    ```xml
    FontWeight="FontWeightValue"
    ```

     Estilo de texto

    ```xml
    FontStyle="FontStyleName"
    ```

     Por exemplo, é possível especificar `Italic` como o estilo do texto.

     Textura

    ```xml
    Style="Glass"
    ```

     - ou –

    ```xml
    Style="Plain"
    ```

     Forma

     Para substituir a forma por um ícone, defina a propriedade `Shape` como `None` e defina a propriedade `Icon` como o caminho com o arquivo do ícone.

    ```xml
    Shape="ShapeFilePathLocation"
    ```

     Por exemplo:

    ```xml
    <Nodes>
       <Node Id="MyNode" Background="#FF008000" Stroke="#FF000000"
       Foreground="#FFFFFFFF" Icon="...\Icons\Globe.png"/>
    </Nodes>
    ```

##### <a name="to-apply-a-custom-style-to-a-single-link"></a>Para aplicar um estilo personalizado a um único link

1. Abra o arquivo. dgml em um editor de texto ou XML.

2. Localize o `<Link/>` elemento que contém os nomes do elemento de código-fonte e do elemento de código de destino.

3. No elemento `<Link/>`, adicione todos os seguintes atributos para personalizar o estilo:

     Contorno e cor da seta

    ```xml
    Stroke="ColorNameOrHexadecimalValue"
    ```

     Espessura do contorno

    ```xml
    StrokeThickness="StrokeValue"
    ```

     Estilo do contorno

    ```xml
    StrokeDashArray="StrokeArrayValues"
    ```

     Por exemplo:

    ```xml
    <Links>
       <Link Source="MyFirstNode" Target="MySecondNode" Background="Green" Stroke="#FF000000" StrokeDashArray="2,2"/>
    </Links>
    ```

##### <a name="to-apply-custom-styles-to-a-group-of-code-elements-or-links"></a>Para aplicar estilos personalizados a um grupo de elementos de código ou links

1. Abra o arquivo. dgml em um editor de texto ou XML.

2. Se um elemento `<Styles></Styles>` não existir, adicione um no elemento `<DirectedGraph></DirectedGraph>` depois do elemento `<Links></Links>`.

3. No elemento `<Styles></Styles>`, no elemento `<Style/>` e especifique os seguintes atributos:

   - `TargetType="Node` &#124; `Link | Graph"`

   - `GroupLabel="`*NameInLegendBox*`"`

   - `ValueLabel="`*NameInStylePickerBox*`"`

     Para aplicar um estilo personalizado a todos os tipos de destino, não use uma condição.

##### <a name="to-apply-a-conditional-style-to-groups-of-code-elements-or-links"></a>Para aplicar um estilo condicional a grupos de elementos de código ou links

1. Abra o arquivo. dgml em um editor de texto ou XML.

2. No elemento `<Style/>`, adicione um elemento `<Condition/>` que contém um atributo `Expression` para especificar uma expressão que retorna um valor Booliano.

    Por exemplo:

   ```xml
   <Condition Expression="MyCategory"/>
   ```

    - ou –

   ```xml
   <Condition Expression="MyCategory > 100"/>
   ```

    - ou –

   ```xml
   <Condition Expression="HasCategory('MyCategory')"/>
   ```

    Essa expressão usa a seguinte sintaxe BNF (Backus-Naur Form):

    \<Expression>:: = \<BinaryExpression> &#124; \<UnaryExpression> &#124; "(" \<Expression> ")" &#124; \<MemberBindings> &#124; \<Literal> &#124;\<Number>

    \<BinaryExpression>::= \<Expression> \<Operator>\<Expression>

    \<UnaryExpression>::= "!" \<Expression> &#124; "+" \<Expression> &#124; "-"\<Expression>

    \<Operator>:: = "<" &#124; " \<=" &#124; "=" &#124; "> =" &#124; ">" &#124; "! =" &#124; "ou" &#124; "e" &#124; "+" &#124; "*" &#124; "/" &#124; "-"

    \<MemberBindings>:: = \<MemberBindings> &#124; \<MemberBinding> "."\<MemberBinding>

    \<MemberBinding>:: = \<MethodCall> &#124;\<PropertyGet>

    \<MethodCall>::= \<Identifier> "(" \<MethodArgs> ")"

    \<PropertyGet>:: = Identificador

    \<MethodArgs>:: = \<Expression> &#124; \<Expression> "," \<MethodArgs> &#124;\<empty>

    \<Identifier>::= [^. ]*

    \<Literal>:: = literal de cadeia de caracteres de aspas simples ou dupla

    \<Number>:: = cadeia de dígitos com o ponto decimal opcional

    Você pode especificar vários `<Condition/>` elementos, que devem ser todos verdadeiros para aplicar o estilo.

3. Na próxima linha após o `<Condition/>` elemento, adicione um ou vários `<Setter/>` elementos para especificar um `Property` atributo e um atributo fixo `Value` ou um atributo computado `Expression` para aplicar ao mapa, aos elementos de código ou aos links que atendem à condição.

    Por exemplo:

   ```xml
   <Setter Property="BackGround" Value="Green"/>
   ```

   Como um exemplo completo simples, a condição a seguir especifica que um elemento de código aparece verde ou vermelho com base em se sua `Passed` categoria está definida como `True` ou `False` :

```xml
<?xml version="1.0" encoding="utf-8"?>
<DirectedGraph xmlns="http://schemas.microsoft.com/vs/2009/dgml">
   <Nodes>
      <Node Id="MyFirstNode" Passed="True" />
      <Node Id="MySecondNode" Passed="False" />
   </Nodes>
   <Links>
   </Links>
   <Styles>
      <Style TargetType="Node" GroupLabel="Passed" ValueLabel="True">
         <Condition Expression="Passed='True'"/>
         <Setter Property="Background" Value="Green"/>
      </Style>
      <Style TargetType="Node" GroupLabel="Passed" ValueLabel="False">
         <Condition Expression="Passed='False'"/>
         <Setter Property="Background" Value="Red"/>
      </Style>
   </Styles>
</DirectedGraph>
```

 A seguinte tabela inclui algumas condições de exemplo que é possível usar:

 Defina o tamanho da fonte como uma função do número de linhas de código, que também altera o tamanho do elemento de código. Este exemplo usa uma única expressão condicional para definir várias propriedades, `FontSize` e `FontFamily`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<DirectedGraph xmlns="http://schemas.microsoft.com/vs/2009/dgml">
<Nodes>
   <Node Id="Class1" LinesOfCode ="200" />
   <Node Id="Class2" LinesOfCode ="1000" />
   <Node Id="Class3" LinesOfCode ="20" />
</Nodes>
<Properties>
   <Property Id="LinesOfCode" Label="LinesOfCode" Description="LinesOfCode" DataType="System.Int32" />
</Properties>
<Styles>
   <Style TargetType="Node" GroupLabel="LinesOfCode" ValueLabel="Function">
      <Condition Expression="LinesOfCode > 0" />
      <Setter Property="FontSize" Expression="Math.Max(9,Math.Sqrt(LinesOfCode))" />
      <Setter Property="FontFamily" Value="Papyrus" />
   </Style>
</Styles>
</DirectedGraph>
```

 Define a cor do plano de fundo de um elemento de código com base na `Coverage` propriedade. Os estilos são avaliados na ordem em que são exibidos, algo semelhante às instruções `if-else`.

 Neste exemplo:

1. Se `Coverage` for > 80, defina a `Background` propriedade como verde.

2. Caso contrário `Coverage` , se for > 50, defina a `Background` propriedade como uma sombra de laranja com base no valor da `Coverage` propriedade.

3. Além disso, defina a propriedade `Background` como um sombreamento com base no valor da propriedade `Coverage`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<DirectedGraph xmlns="http://schemas.microsoft.com/vs/2009/dgml">
<Nodes>
   <Node Id="Class1" Coverage="58" />
   <Node Id="Class2" Coverage="95" />
   <Node Id="Class3" Coverage="32" />
</Nodes>
<Properties>
   <Property Id="Coverage" Label="Coverage" Description="Code coverage as a percentage of blocks" DataType="Double" />
</Properties>
<Styles>
   <Style TargetType="Node" GroupLabel="Coverage" ValueLabel="Good">
      <Condition Expression="Coverage > 80" />
      <Setter Property="Background" Value="Green" />
   </Style>
   <Style TargetType="Node" GroupLabel="Coverage" ValueLabel="OK">
      <Condition Expression="Coverage > 50" />
      <Setter Property="Background" Expression="Color.FromRgb(180 * Math.Max(1, (80 - Coverage) / 30), 180, 0)" />
   </Style>
   <Style TargetType="Node" GroupLabel="Coverage" ValueLabel="Bad">
      <Setter Property="Background" Expression="Color.FromRgb(180, 180 * Coverage / 50, 0)" />
   </Style>
</Styles>
</DirectedGraph>
```

 Defina a propriedade `Shape` como `None` de forma que o ícone substitua a forma. Use a propriedade `Icon` para especificar o local do ícone.

```xml
<DirectedGraph xmlns="http://schemas.microsoft.com/vs/2009/dgml">
<Nodes>
   <Node Id="Automation" Category="Test" Label="Automation" />
   <Node Id="C# Provider" Category="Provider" Label="C# Provider" />
</Nodes>
<Categories>
   <Category Id="Provider" Icon="...\Icons\Module.png" Shape="None" />
   <Category Id="Test" Icon="...\Icons\Page.png" Shape="None" />
</Categories>
<Properties>
   <Property Id="Icon" DataType="System.String" />
   <Property Id="Label" Label="Label" Description="Displayable label of an Annotatable object" DataType="System.String" />
   <Property Id="Shape" DataType="System.String" />
</Properties>
<Styles>
   <Style TargetType="Node" GroupLabel="Group" ValueLabel="Has category">
      <Condition Expression="HasCategory('Group')" />
      <Setter Property="Background" Value="#80008080" />
   </Style>
   <Style TargetType="Node">
      <Setter Property="HorizontalAlignment" Value="Center" />
   </Style>
</Styles>
</DirectedGraph>
```

## <a name="assign-properties-to-code-elements-and-links"></a><a name="AssignProperties"></a>Atribuir propriedades a elementos de código e links
 Você pode organizar elementos de código e links atribuindo Propriedades a eles. Por exemplo, você pode selecionar elementos de código que têm propriedades específicas para que você possa agrupá-los, alterar seu estilo ou ocultá-los.

#### <a name="to-assign-a-property-to-a-code-element"></a>Para atribuir uma propriedade a um elemento de código

1. Abra o arquivo. dgml em um editor de texto ou XML.

2. Localize o `<Node/>` elemento para esse elemento de código. Especifique o nome da propriedade e seu valor. Por exemplo:

    ```xml
    <Nodes>
       <Node Id="MyNode" MyPropertyName="PropertyValue" />
    </Nodes>
    ```

3. Adicione um elemento `<Property/>` à seção `<Properties>` para especificar atributos como seu nome e tipo de dados visíveis:

    ```xml
    <Properties>
       <Property Id="MyPropertyName" Label="My Property" DataType="System.DataType"/>
    </Properties>
    ```

#### <a name="to-assign-a-property-to-a-link"></a>Para atribuir uma propriedade a um link

1. Abra o arquivo. dgml em um editor de texto ou XML.

2. Localize o `<Link/>` elemento que contém os nomes do elemento de código-fonte e do elemento de código de destino.

3. No elemento `<Node/>`, especifique o nome da propriedade e seu valor. Por exemplo:

    ```xml
    <Links>
       <Link Source="MyFirstNode" Target="MySecondNode" MyPropertyName="PropertyValue" />
    </Links>
    ```

4. Adicione um elemento `<Property/>` à seção `<Properties>` para especificar atributos como seu nome e tipo de dados visíveis:

    ```xml
    <Properties>
       <Property Id="MyPropertyName" Label="My Property Name" DataType="System.DataType"/>
    </Properties>
    ```

## <a name="assign-categories-to-code-elements-and-links"></a><a name="AssignCategories"></a>Atribuir categorias a elementos de código e links
 As seções a seguir demonstram como você pode organizar elementos de código atribuindo categorias a eles e como você pode criar categorias hierárquicas que ajudam a organizar elementos de código e adicionar atributos a categorias filho usando a herança.

#### <a name="to-assign-a-category-to-a-code-element"></a>Para atribuir uma categoria a um elemento de código

- Abra o arquivo. dgml em um editor de texto ou XML.

- Localize o `<Node/>` elemento do elemento de código que você deseja.

- No elemento `<Node/>`, adicione um atributo `Category` para especificar o nome da categoria. Por exemplo:

    ```xml
    <Nodes>
       <Node Id="MyNode" Category="MyCategory" />
    </Nodes>
    ```

     Adicione um elemento `<Category/>` à seção `<Categories>` de forma que seja possível usar o atributo `Label` para especificar o texto de exibição dessa categoria:

    ```xml
    <Categories>
       <Category Id="MyCategory" Label="My Category" />
    </Categories>
    ```

#### <a name="to-assign-a-category-to-a-link"></a>Para atribuir uma categoria a um link

1. Abra o arquivo. dgml em um editor de texto ou XML.

2. Localize o `<Link/>` elemento que contém os nomes do elemento de código-fonte e do elemento de código de destino.

3. No elemento `<Link/>`, adicione um atributo `Category` para especificar o nome da categoria. Por exemplo:

    ```xml
    <Links>
       <Link Source="MyFirstNode" Target="MySecondNode" Category="MyCategory"
    </Links>
    ```

4. Adicione um elemento `<Category/>` à seção `<Categories>` de forma que seja possível usar o atributo `Label` para especificar o texto de exibição dessa categoria:

    ```xml
    <Categories>
       <Category Id="MyCategory" Label="My Category" />
    </Categories>
    ```

#### <a name="to-create-hierarchical-categories"></a>Para criar categorias hierárquicas

1. Abra o arquivo. dgml em um editor de texto ou XML.

2. Adicione um elemento `<Category/>` da categoria pai e o atributo `BasedOn` ao elemento `<Category/>` da categoria filho.

     Por exemplo:

    ```xml
    <Nodes>
       <Node Id="MyFirstNode" Label="My First Node" Category= "MyCategory" />
       <Node Id="MySecondNode" Label="My Second Node" />
    </Nodes>
    <Links>
       <Link Source="MyFirstNode" Target="MySecondNode" />
    </Links>
    <Categories>
       <Category Id="MyCategory" Label="My Category" BasedOn="MyParentCategory"/>
       <Category Id="MyParentCategory" Label="My Parent Category" Background="Green"/>
    </Categories>
    ```

     Neste exemplo, o plano de fundo de `MyFirstNode` é verde porque seu atributo `Category` herda o atributo `Background` de `MyParentCategory`.

## <a name="link-documents-or-urls-to-code-elements-and-links"></a><a name="AddReferences"></a>Vincular documentos ou URLs a elementos de código e links
 Você pode vincular documentos ou URLs a elementos de código ou a links editando o arquivo. dgml do mapa e adicionando um `Reference` atributo ao `<Node/>` elemento para um elemento de código ou o `<Link/>` elemento para um link. Em seguida, você pode abrir e exibir o conteúdo do elemento de código ou do link. O atributo `Reference` especifica o caminho desse conteúdo. Ele pode ser um caminho relativo ao local do arquivo .dgml ou um caminho absoluto.

> [!CAUTION]
> Se você usar caminhos relativos e o arquivo .dgml for movido para um local diferente, esses caminhos não serão mais resolvidos. Quando você tentar abrir e exibir o conteúdo vinculado, um erro indicando que o conteúdo não pode ser exibido será exibido.

 Por exemplo, talvez você queira vincular os seguintes elementos de código:

- Para descrever as alterações em uma classe, você pode vincular a URL de um elemento de código de trabalho, documento ou outro arquivo. dgml ao elemento de código para uma classe.

- Você pode vincular um diagrama de dependência a um elemento de código de grupo que representa uma camada na arquitetura lógica do software.

- Para mostrar mais informações sobre um componente que expõe uma interface, você pode vincular um diagrama de componente ao elemento de código para essa interface.

- Vincule um elemento de código a um Team Foundation Server item de trabalho ou bug ou algumas outras informações relacionadas ao elemento de código.

#### <a name="to-link-a-document-or-url-to-a-code-element"></a>Para vincular um documento ou uma URL a um elemento de código

1. Abra o arquivo. dgml em um editor de texto ou XML.

2. Localize o `<Node/>` elemento do elemento de código que você deseja.

3. Realize uma das tarefas na tabela a seguir:

    Um único elemento de código

   - No `<Node/>` elemento ou `<Link/>` , adicione um `Reference` atributo para especificar o local do elemento de código.

     > [!NOTE]
     > Só é possível ter um atributo `Reference` por elemento.

     Por exemplo:

   ```xml
   <Nodes>
      <Node Id="MyNode" Reference="MyDocument.txt" />
   </Nodes>
   <Properties>
      <Property Id="Reference" Label="My Document" DataType="System.String" IsReference="True" />
   </Properties>
   ```

    Vários elementos de código

   1. No elemento `<Node/>` ou `<Link/>`, adicione um novo atributo para especificar o local de cada referência.

   2. Na seção `<Properties>`:

      1. Adicione um elemento `<Property/>` para cada novo tipo de referência.

      2. Defina o atributo `Id` como o nome do novo atributo de referência.

      3. Adicione o `IsReference` atributo e defina-o como `True` para fazer com que a referência apareça no menu de atalho **ir para referência** do elemento de código.

      4. Use o `Label` atributo para especificar o texto de exibição no menu de atalho **ir para referência** do elemento de código.

      Por exemplo:

   ```xml
   <Nodes>
      <Node Id="MyNode" SequenceDiagram="MySequenceDiagram.sequencediagram" ActiveBugs="MyActiveBugs.wiq"/>
   </Nodes>
   <Properties>
      <Property Id="SequenceDiagram" Label="My Sequence Diagram" DataType="System.String" IsReference="True" />
      <Property Id="ActiveBugs" Label="Active Bugs" DataType="System.String" IsReference="True" />
   </Properties>
   ```

    No mapa, o nome do elemento de código aparece sublinhado. Ao abrir o menu de atalho para o elemento de código ou o link, você verá um menu de atalho **ir para referência** que contém os elementos de código vinculado para sua escolha.

4. Use o atributo `ReferenceTemplate` para especificar uma cadeia de caracteres comum, por exemplo, uma URL, usada por várias referências em vez de repetir a cadeia de caracteres na referência.

    O atributo `ReferenceTemplate` especifica um espaço reservado para o valor da referência. No exemplo a seguir, o `{0}` espaço reservado no `ReferenceTemplate` atributo será substituído pelos valores dos `MyFirstReference` `MySecondReference` atributos e no `<Node/>` elemento para produzir um caminho completo:

   ```xml
   <Nodes>
      <Node Id="MyNode" MyFirstReference="MyFirstDocument" MySecondReference="MySecondDocument"/>
      <Node Id="MySecondNode" MyFirstReference="AnotherFirstDocument" MySecondReference="AnotherSecondDocument"/>
   </Nodes>
   <Properties>
      <Property Id="MyFirstReference" Label="My First Document" DataType="System.String" IsReference="True" ReferenceTemplate="http://www.Fabrikam.com/FirstDocuments/{0}.asp"/>
      <Property Id="MySecondReference" Label="My Second Document" DataType="System.String" IsReference="True" ReferenceTemplate=" http://www.Fabrikam.com/SecondDocuments/{0}.asp"/>
   </Properties>
   ```

5. Para exibir o elemento de código ou elementos de código referenciados do mapa, abra o menu de atalho para o elemento de código ou o link. Escolha **ir para referência** e, em seguida, o elemento de código.

## <a name="see-also"></a>Confira também

- [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)
- [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)
- [Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)
- [Procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md)
- [Referência DGML](../modeling/directed-graph-markup-language-dgml-reference.md)
