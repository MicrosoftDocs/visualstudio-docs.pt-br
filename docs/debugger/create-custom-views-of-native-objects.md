---
title: Criar exibições personalizadas dos objetos de C++
description: Use a estrutura Natvis para personalizar a forma como o Visual Studio exibe tipos nativos no depurador
ms.date: 03/02/2020
ms.topic: how-to
f1_keywords:
- natvis
dev_langs:
- C++
ms.assetid: 2d9a177a-e14b-404f-a6af-49498eff0bd7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 5720511c15526a54a82018b2079b91aaf5dd6430
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350700"
---
# <a name="create-custom-views-of-c-objects-in-the-debugger-using-the-natvis-framework"></a>Criar exibições personalizadas de objetos C++ no depurador usando a estrutura Natvis

A estrutura de *Natvis* do Visual Studio personaliza a maneira como os tipos nativos aparecem nas janelas de variáveis do depurador, como as janelas **locais** e de **inspeção** , e em **DataTips**. As visualizações de Natvis podem ajudar a tornar os tipos criados mais visíveis durante a depuração.

O Natvis substitui o arquivo *autoexp. dat* em versões anteriores do Visual Studio por sintaxe XML, melhor diagnóstico, controle de versão e suporte a vários arquivos.

> [!NOTE]
> As personalizações de Natvis funcionam com classes e estruturas, mas não com TYPEDEFs.

## <a name="natvis-visualizations"></a><a name="BKMK_Why_create_visualizations_"></a>Visualizações de Natvis

Você usa a estrutura Natvis para criar regras de visualização para os tipos criados, para que os desenvolvedores possam vê-las mais facilmente durante a depuração.

Por exemplo, a ilustração a seguir mostra uma variável do tipo [Windows:: UI:: XAML:: Controls:: TextBox](/uwp/api/Windows.UI.Xaml.Controls.TextBox) em uma janela do depurador sem nenhuma visualização personalizada aplicada.

![Visualização padrão da caixa de texto](../debugger/media/dbg_natvis_textbox_default.png "Visualização padrão da caixa de texto")

A linha realçada mostra a `Text` propriedade da `TextBox` classe. A hierarquia de classe complexa dificulta a localização dessa propriedade. O depurador não sabe como interpretar o tipo de cadeia de caracteres personalizada, portanto, você não pode ver a cadeia de caracteres mantida dentro da caixa de texto.

O mesmo `TextBox` parece muito mais simples na janela variável quando regras de visualizador personalizado de Natvis são aplicadas. Os membros importantes da classe aparecem juntos e o depurador mostra o valor da cadeia de caracteres subjacente do tipo de cadeia de caracteres personalizada.

![Dados de caixa de texto usando o visualizador](../debugger/media/dbg_natvis_textbox_visualizer.png "Dados de caixa de texto usando o visualizador")

## <a name="use-natvis-files-in-c-projects"></a><a name="BKMK_Using_Natvis_files"></a>Usar arquivos. natvis em projetos C++

O Natvis usa arquivos *. natvis* para especificar regras de visualização. Um arquivo *. natvis* é um arquivo XML com uma extensão *. natvis* . O esquema Natvis é definido em *%VSINSTALLDIR%\Xml\Schemas\natvis.xsd*.

A estrutura básica de um arquivo *. natvis* é um ou mais `Type` elementos que representam entradas de visualização. O nome totalmente qualificado de cada `Type` elemento é especificado em seu `Name` atributo.

```xml
<?xml version="1.0" encoding="utf-8"?>
<AutoVisualizer xmlns="http://schemas.microsoft.com/vstudio/debugger/natvis/2010">
  <Type Name="MyNamespace::CFoo">
    .
    .
  </Type>

  <Type Name="...">
    .
    .
  </Type>
</AutoVisualizer>
```

O Visual Studio fornece alguns arquivos *. natvis* na pasta *%VSINSTALLDIR%\Common7\Packages\Debugger\Visualizers* Esses arquivos têm regras de visualização para muitos tipos comuns e podem servir como exemplos para escrever visualizações para novos tipos.

### <a name="add-a-natvis-file-to-a-c-project"></a>Adicionar um arquivo. natvis a um projeto C++

Você pode adicionar um arquivo *. natvis* a qualquer projeto C++.

**Para adicionar um novo arquivo *. natvis* :**

1. Selecione o nó do projeto C++ em **Gerenciador de soluções**e selecione **projeto**  >  **Adicionar novo item**ou clique com o botão direito do mouse no projeto e selecione **Adicionar**  >  **novo item**.

1. Na caixa de diálogo **Adicionar novo item** , selecione **Visual C++**  >  **Utility**  >  **arquivo de visualização do depurador do utilitário (. natvis)**.

1. Nomeie o arquivo e selecione **Adicionar**.

   O novo arquivo é adicionado a **Gerenciador de soluções**e é aberto no painel do documento do Visual Studio.

O depurador do Visual Studio carrega arquivos *. natvis* em projetos C++ automaticamente e, por padrão, também os inclui no arquivo *. pdb* quando o projeto é compilado. Se você depurar o aplicativo criado, o depurador carregará o arquivo *. natvis* do arquivo *. pdb* , mesmo que você não tenha o projeto aberto. Se você não quiser que o arquivo *. natvis* seja incluído no *. pdb*, você poderá excluí-lo do arquivo *. pdb* criado.

**Para excluir um arquivo *. natvis* de um *. pdb*:**

1. Selecione o arquivo *. natvis* em **Gerenciador de soluções**e selecione o ícone **Propriedades** ou clique com o botão direito do mouse no arquivo e selecione **Propriedades**.

1. Solte a seta ao lado de **excluído da compilação** e selecione **Sim**e, em seguida, selecione **OK**.

>[!NOTE]
>Para depurar projetos executáveis, use os itens da solução para adicionar qualquer arquivo *. natvis* que não esteja no *. pdb*, já que não há nenhum projeto do C++ disponível.

>[!NOTE]
>As regras de Natvis carregadas de um *. pdb* se aplicam somente aos tipos nos módulos aos quais o *. pdb* se refere. Por exemplo, se *Module1. pdb* tiver uma entrada de Natvis para um tipo chamado `Test` , ele só se aplicará à `Test` classe em *Module1.dll*. Se outro módulo também definir uma classe chamada `Test` , a entrada Natvis *. pdb do Module1* não se aplicará a ela.

**Para instalar e registrar um arquivo *. natvis* por meio de um pacote VSIX:**

Um pacote VSIX pode instalar e registrar arquivos *. natvis* . Não importa onde eles estejam instalados, todos os arquivos *. natvis* registrados são automaticamente coletados durante a depuração.

1. Inclua o arquivo *. natvis* no pacote VSIX. Por exemplo, para o seguinte arquivo de projeto:
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ToolsVersion="14.0">
     <ItemGroup>
       <VSIXSourceItem Include="Visualizer.natvis" />
     </ItemGroup>
   </Project>
   ```

2. Registre o arquivo *. natvis* no arquivo *Source. Extension. vsixmanifest* :
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
     <Assets>
       <Asset Type="NativeVisualizer" Path="Visualizer.natvis"  />
     </Assets>
   </PackageManifest>
   ```

### <a name="natvis-file-locations"></a><a name="BKMK_natvis_location"></a>Locais de arquivo Natvis

Você pode adicionar arquivos *. natvis* ao seu diretório de usuário ou a um diretório do sistema, se quiser que eles se apliquem a vários projetos.

Os arquivos *. natvis* são avaliados na seguinte ordem:

1. Quaisquer arquivos *. natvis* inseridos em um *. pdb* que você está Depurando, a menos que exista um arquivo com o mesmo nome no projeto carregado.

2. Qualquer arquivo *. natvis* que esteja em um projeto C++ carregado ou solução de nível superior. Esse grupo inclui todos os projetos do C++ carregados, incluindo bibliotecas de classes, mas não projetos em outras linguagens.

3. Quaisquer arquivos *. natvis* instalados e registrados por meio de um pacote VSIX.

::: moniker range="vs-2017"

4. O diretório Natvis específico do usuário (por exemplo, *%USERPROFILE%\Documents\Visual Studio 2017 \ Visualizers*).

::: moniker-end

::: moniker range=">= vs-2019"

4. O diretório Natvis específico do usuário (por exemplo, *%USERPROFILE%\Documents\Visual Studio 2019 \ Visualizers*).

::: moniker-end

5. O diretório Natvis de todo o sistema (*%VSINSTALLDIR%\Common7\Packages\Debugger\Visualizers*). Esse diretório tem os arquivos *. natvis* instalados com o Visual Studio. Se você tiver permissões de administrador, poderá adicionar arquivos a esse diretório.

## <a name="modify-natvis-files-while-debugging"></a>Modificar arquivos. natvis durante a depuração

Você pode modificar um arquivo *. natvis* no IDE durante a depuração de seu projeto. Abra o arquivo na mesma instância do Visual Studio que você está Depurando, modifique-o e salve-o. Assim que o arquivo for salvo, o **Watch** e os **locais** do Windows Update para refletir a alteração.

Você também pode adicionar ou excluir arquivos *. natvis* em uma solução que está Depurando, e o Visual Studio adiciona ou remove as visualizações relevantes.

Você não pode atualizar arquivos *. natvis* inseridos em arquivos *. pdb* enquanto estiver depurando.

Se você modificar o arquivo *. natvis* fora do Visual Studio, as alterações não entrarão em vigor automaticamente. Para atualizar as janelas do depurador, você pode reavaliar o comando **. natvisreload** na janela **imediata** . Em seguida, as alterações entram em vigor sem reiniciar a sessão de depuração.

Use também o comando **. natvisreload** para atualizar o arquivo *. natvis* para uma versão mais recente. Por exemplo, o arquivo *. natvis* pode ser verificado no controle do código-fonte e você deseja escolher as alterações recentes feitas por outra pessoa.

## <a name="expressions-and-formatting"></a><a name="BKMK_Expressions_and_formatting"></a> Expressões e formatação
As visualizações do Natvis usam expressões do C++ para especificar os itens de dados a serem exibidos. Além dos aprimoramentos e limitações das expressões C++ no depurador, que são descritas em operador de [contexto (C++)](../debugger/context-operator-cpp.md), esteja ciente do seguinte:

- As expressões do Natvis são avaliadas no contexto do objeto que está sendo visualizado, não do registro de ativação atual. Por exemplo, `x` em uma expressão Natvis refere-se ao campo chamado **x** no objeto que está sendo visualizado, não a uma variável local chamada **x** na função atual. Você não pode acessar variáveis locais em expressões Natvis, embora possa acessar variáveis globais.

- As expressões Natvis não permitem a avaliação de função ou efeitos colaterais. As chamadas de função e os operadores de atribuição são ignorados. Como as [funções intrínsecas do depurador](../debugger/expressions-in-the-debugger.md#BKMK_Using_debugger_intrinisic_functions_to_maintain_state) não têm efeitos colaterais, elas podem ser livremente chamadas de qualquer expressão do natvis, mesmo que outras chamadas de função estejam desabilitadas.

- Para controlar como uma expressão é exibida, você pode usar qualquer um dos especificadores de formato descritos nos [especificadores de formato em C++](format-specifiers-in-cpp.md#BKMK_Visual_Studio_2012_format_specifiers). Os especificadores de formato são ignorados quando a entrada é usada internamente pelo Natvis, como a `Size` expressão em uma [expansão ArrayItems](../debugger/create-custom-views-of-native-objects.md#BKMK_ArrayItems_expansion).

## <a name="natvis-views"></a>Exibições de Natvis

Você pode definir exibições de Natvis diferentes para exibir tipos de maneiras diferentes. Por exemplo, aqui está uma visualização de `std::vector` que define uma exibição simplificada chamada `simple` . O `DisplayString` e os `ArrayItems` elementos são mostrados no modo de exibição padrão e no `simple` modo de exibição, enquanto os `[size]` `[capacity]` itens e não são mostrados na `simple` exibição.

```xml
<Type Name="std::vector&lt;*&gt;">
    <DisplayString>{{ size={_Mylast - _Myfirst} }}</DisplayString>
    <Expand>
        <Item Name="[size]" ExcludeView="simple">_Mylast - _Myfirst</Item>
        <Item Name="[capacity]" ExcludeView="simple">_Myend - _Myfirst</Item>
        <ArrayItems>
            <Size>_Mylast - _Myfirst</Size>
            <ValuePointer>_Myfirst</ValuePointer>
        </ArrayItems>
    </Expand>
</Type>
```

Na janela **Watch** , use o especificador de formato **View** para especificar uma exibição alternativa. A exibição simples aparece como **VEC, View (simples)**:

![janela Inspeção com exibição simples](../debugger/media/watch-simpleview.png "janela Inspeção com exibição simples")

## <a name="natvis-errors"></a><a name="BKMK_Diagnosing_Natvis_errors"></a>Erros de Natvis

Quando o depurador encontra erros em uma entrada de visualização, ele os ignora. Ele exibe o tipo em seu formato bruto ou escolhe outra visualização adequada. Você pode usar o diagnóstico de Natvis para entender por que o depurador ignorou uma entrada de visualização e para ver a sintaxe subjacente e os erros de análise.

**Para ativar o diagnóstico de Natvis:**

- Em **ferramentas**  >  **Opções** (ou **Debug**  >  **Opções**de depuração) > **depuração**  >  **janela de saída**, defina **mensagens de diagnóstico de Natvis (somente C++)** para **erro**, **aviso**ou **detalhado**e, em seguida, selecione **OK**.

Os erros aparecem na janela **saída** .

## <a name="natvis-syntax-reference"></a><a name="BKMK_Syntax_reference"></a>Referência de sintaxe de Natvis

### <a name="autovisualizer-element"></a><a name="BKMK_AutoVisualizer"></a> Elemento AutoVisualizer
O `AutoVisualizer` elemento é o nó raiz do arquivo *. natvis* e contém o `xmlns:` atributo namespace.

```xml
<?xml version="1.0" encoding="utf-8"?>
<AutoVisualizer xmlns="http://schemas.microsoft.com/vstudio/debugger/natvis/2010">
.
.
</AutoVisualizer>
```

O `AutoVisualizer` elemento pode ter os filhos [Type](#BKMK_Type), [HRESULT](#BKMK_HResult), [UIVisualizer](#BKMK_UIVisualizer)e [CustomVisualizer](#BKMK_CustomVisualizer) .

### <a name="type-element"></a><a name="BKMK_Type"></a>Elemento Type

Um básico `Type` é semelhante a este exemplo:

```xml
<Type Name="[fully qualified type name]">
  <DisplayString Condition="[Boolean expression]">[Display value]</DisplayString>
  <Expand>
    ...
  </Expand>
</Type>
```

 O `Type` elemento especifica:

1. Para qual tipo a visualização deve ser usada (o `Name` atributo).

2. Qual deve ser a aparência de um objeto desse tipo (semelhante à do elemento `DisplayString`).

3. Como deve ser a aparência dos membros do tipo quando o usuário expandir o tipo em uma janela variável (o `Expand` nó).

#### <a name="templated-classes"></a>Classes de modelo
O `Name` atributo do `Type` elemento aceita um asterisco `*` como um caractere curinga que pode ser usado para nomes de classe de modelo.

No exemplo a seguir, a mesma visualização é usada se o objeto for um `CAtlArray<int>` ou um `CAtlArray<float>` . Se houver uma entrada de visualização específica para um `CAtlArray<float>` , ela terá precedência sobre a genérica.

```xml
<Type Name="ATL::CAtlArray&lt;*&gt;">
    <DisplayString>{{Count = {m_nSize}}}</DisplayString>
</Type>
```

Você pode referenciar parâmetros de modelo na entrada de visualização usando macros $T 1, $T 2 e assim por diante. Para localizar exemplos dessas macros, confira os arquivos *.natvis* que acompanham o Visual Studio.

#### <a name="visualizer-type-matching"></a><a name="BKMK_Visualizer_type_matching"></a> Correspondência de tipo de visualizador
Se uma entrada de visualização não for validada, a próxima visualização disponível será usada.

#### <a name="inheritable-attribute"></a>Atributo herdável
O `Inheritable` atributo opcional especifica se uma visualização se aplica somente a um tipo base ou a um tipo base e a todos os tipos derivados. O valor padrão de `Inheritable` é `true`.

No exemplo a seguir, a visualização aplica-se somente ao `BaseClass` tipo:

```xml
<Type Name="Namespace::BaseClass" Inheritable="false">
    <DisplayString>{{Count = {m_nSize}}}</DisplayString>
</Type>
```

#### <a name="priority-attribute"></a>Atributo de prioridade

O `Priority` atributo opcional especifica a ordem na qual usar definições alternativas, se houver falha na análise de uma definição. Os valores possíveis de `Priority` são: `Low` ,,, `MediumLow` `Medium` `MediumHigh` e `High` . O valor padrão é `Medium`. O `Priority` atributo distingue apenas entre as prioridades no mesmo arquivo *. natvis* .

O exemplo a seguir primeiro analisa a entrada que corresponde à STL 2015. Se isso não for analisado, ele usará a entrada alternativa para a versão 2013 da STL:

```xml
<!-- VC 2013 -->
<Type Name="std::reference_wrapper&lt;*&gt;" Priority="MediumLow">
     <DisplayString>{_Callee}</DisplayString>
    <Expand>
        <ExpandedItem>_Callee</ExpandedItem>
    </Expand>
</Type>

<!-- VC 2015 -->
<Type Name="std::reference_wrapper&lt;*&gt;">
    <DisplayString>{*_Ptr}</DisplayString>
    <Expand>
        <Item Name="[ptr]">_Ptr</Item>
    </Expand>
</Type>
```

### <a name="optional-attribute"></a>Atributo opcional
Você pode colocar um `Optional` atributo em qualquer nó. Se uma subexpressão dentro de um nó opcional falhar na análise, o depurador ignorará esse nó, mas aplicará o restante das `Type` regras. No seguinte tipo, `[State]` é não opcional, mas `[Exception]` é opcional.  Se `MyNamespace::MyClass` tiver um campo chamado _ `M_exceptionHolder` , o `[State]` nó e o `[Exception]` nó aparecerão, mas se não houver nenhum `_M_exceptionHolder` campo, apenas o `[State]` nó será exibido.

```xml
<Type Name="MyNamespace::MyClass">
    <Expand>
      <Item Name="[State]">_M_State</Item>
      <Item Name="[Exception]" Optional="true">_M_exceptionHolder</Item>
    </Expand>
</Type>
```

### <a name="condition-attribute"></a><a name="BKMK_Condition_attribute"></a> Atributo de condição

O `Condition` atributo opcional está disponível para muitos elementos de visualização e especifica quando usar uma regra de visualização. Se a expressão dentro do atributo Condition for resolvida como `false` , a regra de visualização não se aplicará. Se ele for avaliado como `true` , ou não houver nenhum `Condition` atributo, a visualização se aplicará. Você pode usar esse atributo para a lógica if-else nas entradas de visualização.

Por exemplo, a visualização a seguir tem dois `DisplayString` elementos para um tipo de ponteiro inteligente. Quando o `_Myptr` membro está vazio, a condição do primeiro `DisplayString` elemento é resolvida para `true` , para que o formulário seja exibido. Quando o `_Myptr` membro não está vazio, a condição é avaliada como `false` e o segundo `DisplayString` elemento é exibido.

```xml
<Type Name="std::auto_ptr&lt;*&gt;">
  <DisplayString Condition="_Myptr == 0">empty</DisplayString>
  <DisplayString>auto_ptr {*_Myptr}</DisplayString>
  <Expand>
    <ExpandedItem>_Myptr</ExpandedItem>
  </Expand>
</Type>
```

### <a name="includeview-and-excludeview-attributes"></a>Atributos IncludeView e ExcludeView

Os `IncludeView` `ExcludeView` atributos e especificam os elementos a serem exibidos ou não exibidos em modos de exibição específicos. Por exemplo, na especificação Natvis a seguir do `std::vector` , a `simple` exibição não exibe os `[size]` `[capacity]` itens e.

```xml
<Type Name="std::vector&lt;*&gt;">
    <DisplayString>{{ size={_Mylast - _Myfirst} }}</DisplayString>
    <Expand>
        <Item Name="[size]" ExcludeView="simple">_Mylast - _Myfirst</Item>
        <Item Name="[capacity]" ExcludeView="simple">_Myend - _Myfirst</Item>
        <ArrayItems>
            <Size>_Mylast - _Myfirst</Size>
            <ValuePointer>_Myfirst</ValuePointer>
        </ArrayItems>
    </Expand>
</Type>
```

Você pode usar os `IncludeView` `ExcludeView` atributos e em tipos e em membros individuais.

### <a name="version-element"></a><a name="BKMK_Versioning"></a>Elemento Version
O `Version` elemento escopou uma entrada de visualização para um módulo e uma versão específicos. O `Version` elemento ajuda a evitar colisões de nome, reduz incompatibilidades involuntárias e permite diferentes visualizações para diferentes versões de tipo.

Se um arquivo de cabeçalho comum usado por diferentes módulos definir um tipo, a visualização com controle de versão aparecerá somente quando o tipo estiver na versão do módulo especificada.

No exemplo a seguir, a visualização é aplicável somente para o `DirectUI::Border` tipo encontrado na `Windows.UI.Xaml.dll` da versão de 1,0 a 1,5.

```xml
<Type Name="DirectUI::Border">
  <Version Name="Windows.UI.Xaml.dll" Min="1.0" Max="1.5"/>
  <DisplayString>{{Name = {*(m_pDO->m_pstrName)}}}</DisplayString>
  <Expand>
    <ExpandedItem>*(CBorder*)(m_pDO)</ExpandedItem>
  </Expand>
</Type>
```

Você não precisa `Min` de e `Max` . Eles são atributos opcionais. Não há suporte para caracteres curinga.

O `Name` atributo está no formato *filename. ext*, como *hello.exe* ou *some.dll*. Nenhum nome de caminho é permitido.

### <a name="displaystring-element"></a><a name="BKMK_DisplayString"></a>Elemento DisplayString
O `DisplayString` elemento Especifica uma cadeia de caracteres a ser mostrada como o valor de uma variável. Aceita cadeias de caracteres arbitrárias misturadas a expressões. Tudo dentro das chaves é interpretado como uma expressão. Por exemplo, a seguinte `DisplayString` entrada:

```xml
<Type Name="CPoint">
  <DisplayString>{{x={x} y={y}}}</DisplayString>
</Type>
```

Significa que as variáveis do tipo são `CPoint` exibidas como nesta ilustração:

 ![Usar um elemento DisplayString](../debugger/media/dbg_natvis_cpoint_displaystring.png "Usar um elemento DisplayString")

Na `DisplayString` expressão, `x` e `y` , que são membros de `CPoint` , estão dentro das chaves, portanto, seus valores são avaliados. O exemplo também mostra como você pode escapar uma chave usando chaves duplas ( `{{` ou `}}` ).

> [!NOTE]
> O `DisplayString` elemento é o único elemento que aceita cadeias de caracteres arbitrárias e a sintaxe de chaves. Todos os outros elementos de visualização aceitam apenas expressões que o depurador pode avaliar.

### <a name="stringview-element"></a><a name="BKMK_StringView"></a>Elemento StringView

O `StringView` elemento define um valor que o depurador pode enviar para o Visualizador de texto interno. Por exemplo, considerando a seguinte visualização para o `ATL::CStringT` tipo:

```xml
<Type Name="ATL::CStringT&lt;wchar_t,*&gt;">
  <DisplayString>{m_pszData,su}</DisplayString>
</Type>
```

O `CStringT` objeto é exibido em uma janela de variável como neste exemplo:

![Elemento CStringT DisplayString](../debugger/media/dbg_natvis_displaystring_cstringt.png "Elemento CStringT DisplayString")

A adição de um `StringView` elemento informa ao depurador que ele pode exibir o valor como uma visualização de texto.

```xml
<Type Name="ATL::CStringT&lt;wchar_t,*&gt;">
  <DisplayString>{m_pszData,su}</DisplayString>
  <StringView>m_pszData,su</StringView>
</Type>
```

Durante a depuração, você pode selecionar o ícone de lupa ao lado da variável e, em seguida, selecionar **Visualizador de texto** para exibir a cadeia de caracteres à qual **m_pszData** aponta.

 ![Dados do CStringT com o Visualizador do StringView](../debugger/media/dbg_natvis_stringview_cstringt.png "Dados do CStringT com o Visualizador do StringView")

A expressão `{m_pszData,su}` inclui um de especificador de formato C++ **Su**, para exibir o valor como uma cadeia de caracteres Unicode. Para obter mais informações, consulte [Formatar especificadores em C++](../debugger/format-specifiers-in-cpp.md).

### <a name="expand-element"></a><a name="BKMK_Expand"></a>Expandir elemento

O `Expand` nó opcional personaliza os filhos de um tipo visualizado quando você expande o tipo em uma janela variável. O `Expand` nó aceita uma lista de nós filho que definem os elementos filho.

- Se um `Expand` nó não for especificado em uma entrada de visualização, os filhos usarão as regras de expansão padrão.

- Se um `Expand` nó for especificado sem nós filho sob ele, o tipo não será expansível nas janelas do depurador.

#### <a name="item-expansion"></a><a name="BKMK_Item_expansion"></a> Expansão de item

 O `Item` elemento é o elemento mais básico e comum em um `Expand` nó. `Item` define um único elemento filho. Por exemplo, uma `CRect` classe com campos `top` , `left` , `right` e `bottom` tem a seguinte entrada de visualização:

```xml
<Type Name="CRect">
  <DisplayString>{{top={top} bottom={bottom} left={left} right={right}}}</DisplayString>
  <Expand>
    <Item Name="Width">right - left</Item>
    <Item Name="Height">bottom - top</Item>
  </Expand>
</Type>
```

Na janela do depurador, o `CRect` tipo é semelhante a este exemplo:

![CRect com expansão de elemento de item](../debugger/media/dbg_natvis_expand_item_crect1.png "CRect com expansão de elemento de item")

O depurador avalia as expressões especificadas nos `Width` `Height` elementos e e mostra os valores na coluna **valor** da janela variável.

O depurador cria automaticamente o nó **[modo de exibição bruto]** para cada expansão personalizada. A captura de tela anterior exibe o nó **[modo de exibição bruto]** expandido, para mostrar como a exibição bruta padrão do objeto difere de sua visualização de Natvis. A expansão padrão cria uma subárvore para a classe base e lista todos os membros de dados da classe base como filhos.

> [!NOTE]
> Se a expressão do elemento item apontar para um tipo complexo, o nó do **Item** em si será expansível.

#### <a name="arrayitems-expansion"></a><a name="BKMK_ArrayItems_expansion"></a> Expansão de ArrayItems
Use o nó `ArrayItems` para que o depurador do Visual Studio interprete o tipo como uma matriz e exiba seus elementos individuais. A visualização do `std::vector` é um bom exemplo:

```xml
<Type Name="std::vector&lt;*&gt;">
  <DisplayString>{{size = {_Mylast - _Myfirst}}}</DisplayString>
  <Expand>
    <Item Name="[size]">_Mylast - _Myfirst</Item>
    <Item Name="[capacity]">(_Myend - _Myfirst)</Item>
    <ArrayItems>
      <Size>_Mylast - _Myfirst</Size>
      <ValuePointer>_Myfirst</ValuePointer>
    </ArrayItems>
  </Expand>
</Type>
```

Um `std::vector` mostra os elementos individuais quando expandido na janela variável:

![std:: vector usando a expansão ArrayItems](../debugger/media/dbg_natvis_expand_arrayitems_stdvector.png "std:: vector usando a expansão ArrayItems")

O `ArrayItems` nó deve ter:

- Uma expressão `Size` (que deve ser avaliada como um inteiro) para que o depurador entenda o comprimento da matriz.
- Uma `ValuePointer` expressão que aponta para o primeiro elemento (que deve ser um ponteiro de um tipo de elemento que não seja `void*` ).

O valor padrão do limite inferior da matriz é 0. Para substituir o valor, use um `LowerBound` elemento. Os arquivos *. natvis* fornecidos com o Visual Studio têm exemplos.

>[!NOTE]
>Você pode usar o `[]` operador, por exemplo `vector[i]` , com qualquer visualização de matriz unidimensional que usa `ArrayItems` , mesmo que o próprio tipo (por exemplo `CATLArray` ) não permita esse operador.

Você também pode especificar matrizes multidimensionais. Nesse caso, o depurador precisa de um pouco mais de informações para exibir corretamente os elementos filho:

```xml
<Type Name="Concurrency::array&lt;*,*&gt;">
  <DisplayString>extent = {_M_extent}</DisplayString>
  <Expand>
    <Item Name="extent">_M_extent</Item>
    <ArrayItems Condition="_M_buffer_descriptor._M_data_ptr != 0">
      <Direction>Forward</Direction>
      <Rank>$T2</Rank>
      <Size>_M_extent._M_base[$i]</Size>
      <ValuePointer>($T1*) _M_buffer_descriptor._M_data_ptr</ValuePointer>
    </ArrayItems>
  </Expand>
</Type>
```

- `Direction`Especifica se a matriz está na ordem de linha-principal ou coluna-principal.
- `Rank` especifica a classificação da matriz.
- O elemento `Size` aceita o parâmetro implícito `$i`, que ele substitui pelo índice de dimensão para descobrir o tamanho da matriz na dimensão. No exemplo anterior, a expressão `_M_extent.M_base[0]` deve dar o comprimento da dimensão 0º, `_M_extent._M_base[1]` a 1ª e assim por diante.

Veja como um objeto bidimensional `Concurrency::array` procura na janela do depurador:

![Matriz bidimensional com expansão ArrayItems](../debugger/media/dbg_natvis_expand_arrayitems_2d.png "Matriz bidimensional com expansão ArrayItems")

#### <a name="indexlistitems-expansion"></a><a name="BKMK_IndexListItems_expansion"></a> Expansão de IndexListItems

Você poderá usar `ArrayItems` a expansão somente se os elementos da matriz forem dispostos de forma contígua na memória. O depurador chega ao próximo elemento simplesmente incrementando seu ponteiro. Se você precisar manipular o índice para o nó de valor, use `IndexListItems` nós. Veja uma visualização com um `IndexListItems` nó:

```xml
<Type Name="Concurrency::multi_link_registry&lt;*&gt;">
  <DisplayString>{{size = {_M_vector._M_index}}}</DisplayString>
  <Expand>
    <Item Name="[size]">_M_vector._M_index</Item>
    <IndexListItems>
      <Size>_M_vector._M_index</Size>
      <ValueNode>*(_M_vector._M_array[$i])</ValueNode>
    </IndexListItems>
  </Expand>
</Type>
```

A única diferença entre `ArrayItems` e `IndexListItems` é o `ValueNode` , que espera a expressão completa para o elemento<sup>th</sup> i com o parâmetro implícito `$i` .

>[!NOTE]
>Você pode usar o `[]` operador, por exemplo `vector[i]` , com qualquer visualização de matriz unidimensional que usa `IndexListItems` , mesmo que o próprio tipo (por exemplo `CATLArray` ) não permita esse operador.

#### <a name="linkedlistitems-expansion"></a><a name="BKMK_LinkedListItems_expansion"></a> Expansão de LinkedListItems

Se o tipo visualizado representa uma lista vinculada, o depurador pode exibir seus filhos usando um nó `LinkedListItems`. A visualização a seguir para o `CAtlList` tipo usa `LinkedListItems` :

```xml
<Type Name="ATL::CAtlList&lt;*,*&gt;">
  <DisplayString>{{Count = {m_nElements}}}</DisplayString>
  <Expand>
    <Item Name="Count">m_nElements</Item>
    <LinkedListItems>
      <Size>m_nElements</Size>
      <HeadPointer>m_pHead</HeadPointer>
      <NextPointer>m_pNext</NextPointer>
      <ValueNode>m_element</ValueNode>
    </LinkedListItems>
  </Expand>
</Type>
```

O elemento `Size` faz referência ao comprimento da lista. `HeadPointer` aponta para o primeiro elemento, `NextPointer` refere-se ao próximo elemento e `ValueNode` refere-se ao valor do item.

O depurador avalia as `NextPointer` expressões e `ValueNode` no contexto do `LinkedListItems` elemento node, não o tipo de lista pai. No exemplo anterior, `CAtlList` tem uma `CNode` classe (encontrada em `atlcoll.h` ) que é um nó da lista vinculada. `m_pNext`e `m_element` são campos dessa `CNode` classe, e não da `CAtlList` classe.

`ValueNode`pode ser deixado em branco ou usar `this` para se referir ao `LinkedListItems` próprio nó.

#### <a name="customlistitems-expansion"></a>Expansão de CustomListItems

A `CustomListItems` expansão permite que você escreva uma lógica personalizada para percorrer uma estrutura de dados, como uma tabela de hash. Use `CustomListItems` para visualizar estruturas de dados que podem usar expressões C++ para tudo que você precisa avaliar, mas não se ajustam perfeitamente ao molde para `ArrayItems` , `IndexListItems` ou `LinkedListItems` .

Você pode usar `Exec` para executar o código dentro de uma `CustomListItems` expansão, usando as variáveis e os objetos definidos na expansão. Você pode usar operadores lógicos, operadores aritméticos e operadores de atribuição com o `Exec` . Não é possível usar `Exec` o para avaliar funções, exceto para [funções intrínsecas do depurador](../debugger/expressions-in-the-debugger.md#BKMK_Using_debugger_intrinisic_functions_to_maintain_state) com suporte pelo avaliador de expressão do C++.

O seguinte Visualizador de `CAtlMap` é um exemplo excelente, onde `CustomListItems` é apropriado.

```xml
<Type Name="ATL::CAtlMap&lt;*,*,*,*&gt;">
    <AlternativeType Name="ATL::CMapToInterface&lt;*,*,*&gt;"/>
    <AlternativeType Name="ATL::CMapToAutoPtr&lt;*,*,*&gt;"/>
    <DisplayString>{{Count = {m_nElements}}}</DisplayString>
    <Expand>
      <CustomListItems MaxItemsPerView="5000" ExcludeView="Test">
        <Variable Name="iBucket" InitialValue="-1" />
        <Variable Name="pBucket" InitialValue="m_ppBins == nullptr ? nullptr : *m_ppBins" />
        <Variable Name="iBucketIncrement" InitialValue="-1" />

        <Size>m_nElements</Size>
        <Exec>pBucket = nullptr</Exec>
        <Loop>
          <If Condition="pBucket == nullptr">
            <Exec>iBucket++</Exec>
            <Exec>iBucketIncrement = __findnonnull(m_ppBins + iBucket, m_nBins - iBucket)</Exec>
            <Break Condition="iBucketIncrement == -1" />
            <Exec>iBucket += iBucketIncrement</Exec>
            <Exec>pBucket = m_ppBins[iBucket]</Exec>
          </If>
          <Item>pBucket,na</Item>
          <Exec>pBucket = pBucket->m_pNext</Exec>
        </Loop>
      </CustomListItems>
    </Expand>
</Type>
```

#### <a name="treeitems-expansion"></a><a name="BKMK_TreeItems_expansion"></a> Expansão de TreeItems
 Se o tipo visualizado representa uma árvore, o depurador pode percorrer a árvore e exibir seus filhos usando um nó `TreeItems`. Esta é a visualização para o `std::map` tipo usando um `TreeItems` nó:

```xml
<Type Name="std::map&lt;*&gt;">
  <DisplayString>{{size = {_Mysize}}}</DisplayString>
  <Expand>
    <Item Name="[size]">_Mysize</Item>
    <Item Name="[comp]">comp</Item>
    <TreeItems>
      <Size>_Mysize</Size>
      <HeadPointer>_Myhead->_Parent</HeadPointer>
      <LeftPointer>_Left</LeftPointer>
      <RightPointer>_Right</RightPointer>
      <ValueNode Condition="!((bool)_Isnil)">_Myval</ValueNode>
    </TreeItems>
  </Expand>
</Type>
```

A sintaxe é semelhante ao `LinkedListItems` nó. `LeftPointer`, `RightPointer` e `ValueNode` são avaliados sob o contexto da classe de nó de árvore. `ValueNode`pode ser deixado em branco ou usar `this` para se referir ao `TreeItems` próprio nó.

#### <a name="expandeditem-expansion"></a><a name="BKMK_ExpandedItem_expansion"></a> Expansão de ExpandedItem
 O `ExpandedItem` elemento gera uma exibição filho agregada exibindo as propriedades de classes base ou membros de dados como se fossem filhos do tipo visualizado. O depurador avalia a expressão especificada e acrescenta os nós filho do resultado à lista de filhos do tipo visualizado.

Por exemplo, o tipo de ponteiro inteligente `auto_ptr<vector<int>>` normalmente é exibido como:

 ![auto&#95;PTR&#60;vetor&#60;int&#62;&#62; expansão padrão](../debugger/media/dbg_natvis_expand_expandeditem_default.png "Expansão padrão")

 Para ver os valores do vetor, você precisa fazer uma busca detalhada de dois níveis na janela variável, passando pelo `_Myptr` membro. Adicionando um elemento `ExpandedItem`, você pode eliminar a variável `_Myptr` da hierarquia e exibir diretamente os elementos do vetor:

```xml
<Type Name="std::auto_ptr&lt;*&gt;">
  <DisplayString>auto_ptr {*_Myptr}</DisplayString>
  <Expand>
    <ExpandedItem>_Myptr</ExpandedItem>
  </Expand>
</Type>
```

 ![&#95;de vetor de&#60;PTR&#60;int&#62;&#62; a expansão de ExpandedItem](../debugger/media/dbg_natvis_expand_expandeditem_visualized.png "Expansão de ExpandedItem")

O exemplo a seguir mostra como agregar Propriedades da classe base em uma classe derivada. Suponha que a classe `CPanel` seja derivada de `CFrameworkElement`. Em vez de repetir as propriedades que vêm da `CFrameworkElement` classe base, a `ExpandedItem` visualização do nó acrescenta essas propriedades à lista filho da `CPanel` classe.

```xml
<Type Name="CPanel">
  <DisplayString>{{Name = {*(m_pstrName)}}}</DisplayString>
  <Expand>
    <Item Name="IsItemsHost">(bool)m_bItemsHost</Item>
    <ExpandedItem>*(CFrameworkElement*)this,nd</ExpandedItem>
  </Expand>
</Type>
```

O especificador de formato **nd**, que desativa a correspondência de visualização da classe derivada é necessário aqui. Caso contrário, a expressão `*(CFrameworkElement*)this` faria com que a `CPanel` Visualização fosse aplicada novamente, porque as regras de correspondência do tipo de visualização padrão consideram a mais apropriada. Use o especificador de formato **ND** para instruir o depurador a usar a visualização da classe base ou a expansão padrão se a classe base não tiver nenhuma visualização.

#### <a name="synthetic-item-expansion"></a><a name="BKMK_Synthetic_Item_expansion"></a> Expansão de item sintético
 Enquanto o elemento `ExpandedItem` fornece uma exibição de dados mais simples eliminando as hierarquias, o nó `Synthetic` faz o oposto. Ele permite que você crie um elemento filho artificial que não é um resultado de uma expressão. O elemento artificial pode ter elementos filho próprios. No exemplo a seguir, a visualização do tipo `Concurrency::array` usa um nó de `Synthetic` para mostrar uma mensagem de diagnóstico para o usuário:

```xml
<Type Name="Concurrency::array&lt;*,*&gt;">
  <DisplayString>extent = {_M_extent}</DisplayString>
  <Expand>
    <Item Name="extent" Condition="_M_buffer_descriptor._M_data_ptr == 0">_M_extent</Item>
    <ArrayItems Condition="_M_buffer_descriptor._M_data_ptr != 0">
      <Rank>$T2</Rank>
      <Size>_M_extent._M_base[$i]</Size>
      <ValuePointer>($T1*) _M_buffer_descriptor._M_data_ptr</ValuePointer>
    </ArrayItems>
    <Synthetic Name="Array" Condition="_M_buffer_descriptor._M_data_ptr == 0">
      <DisplayString>Array members can be viewed only under the GPU debugger</DisplayString>
    </Synthetic>
  </Expand>
</Type>
```

 ![Concurrency:: array com expansão de elemento sintético](../debugger/media/dbg_natvis_expand_synthetic.png "Concurrency:: array com expansão de elemento sintético")

### <a name="hresult-element"></a><a name="BKMK_HResult"></a>Elemento HResult
 O `HResult` elemento permite que você personalize as informações mostradas para um **HRESULT** nas janelas do depurador. O elemento `HRValue` deve conter o valor de 32 bits do **HRESULT** que deve ser personalizado. O `HRDescription` elemento contém as informações a serem exibidas na janela do depurador.

```xml

<HResult Name="MY_E_COLLECTION_NOELEMENTS">
  <HRValue>0xABC0123</HRValue>
  <HRDescription>No elements in the collection.</HRDescription>
</HResult>
```

### <a name="uivisualizer-element"></a><a name="BKMK_UIVisualizer"></a>Elemento UIVisualizer
Um elemento `UIVisualizer` registra um plug-in de visualizador gráfico no depurador. Um visualizador gráfico cria uma caixa de diálogo ou outra interface que mostra uma variável ou objeto de forma consistente com seu tipo de dados. O plug-in do visualizador deve ser criado como um [VSPackage](../extensibility/internals/vspackages.md)e deve expor um serviço que o depurador pode consumir. O arquivo *. natvis* contém informações de registro para o plug-in, como seu nome, o GUID do serviço exposto e os tipos que ele pode visualizar.

Veja um exemplo de um elemento UIVisualizer:

```xml
<?xml version="1.0" encoding="utf-8"?>
<AutoVisualizer xmlns="http://schemas.microsoft.com/vstudio/debugger/natvis/2010">
    <UIVisualizer ServiceId="{5452AFEA-3DF6-46BB-9177-C0B08F318025}"
        Id="1" MenuName="Vector Visualizer"/>
    <UIVisualizer ServiceId="{5452AFEA-3DF6-46BB-9177-C0B08F318025}"
        Id="2" MenuName="List Visualizer"/>
.
.
</AutoVisualizer>
```

- Um `ServiceId`  -  `Id` par de atributos identifica um `UIVisualizer` . O `ServiceId` é o GUID do serviço que o pacote do visualizador expõe. `Id`é um identificador exclusivo que diferencia os visualizadores, se um serviço fornecer mais de um. No exemplo anterior, o mesmo serviço de visualizador fornece dois visualizadores.

- O `MenuName` atributo define um nome do visualizador para exibir na lista suspensa ao lado do ícone de lupa no depurador. Por exemplo:

  ![Menu de atalho do menu UIVisualizer](../debugger/media/dbg_natvis_vectorvisualizer.png "Menu de atalho do menu UIVisualizer")

Cada tipo definido no arquivo *. natvis* deve listar explicitamente qualquer visualizador de interface do usuário que possa exibi-lo. O depurador corresponde às referências do visualizador nas entradas de tipo com os visualizadores registrados. Por exemplo, a entrada de tipo a seguir para `std::vector` faz referência ao `UIVisualizer` no exemplo anterior.

```xml
<Type Name="std::vector&lt;int,*&gt;">
  <UIVisualizer ServiceId="{5452AFEA-3DF6-46BB-9177-C0B08F318025}" Id="1" />
</Type>
```

 Você pode ver um exemplo de uma `UIVisualizer` na extensão de [inspeção de imagem](https://marketplace.visualstudio.com/search?term=%22Image%20Watch%22&target=VS&category=All%20categories&vsVersion=&sortBy=Relevance) usada para exibir bitmaps na memória.

### <a name="customvisualizer-element"></a><a name="BKMK_CustomVisualizer"></a>Elemento CustomVisualizer
 `CustomVisualizer`é um ponto de extensibilidade que especifica uma extensão VSIX que você escreve para controlar as visualizações no Visual Studio Code. Para obter mais informações sobre como escrever extensões VSIX, consulte o [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).

É muito mais trabalho escrever um visualizador personalizado do que uma definição de Natvis XML, mas você está livre de restrições sobre o que o Natvis faz ou não dá suporte. Visualizadores personalizados têm acesso ao conjunto completo de APIs de extensibilidade do depurador, que podem consultar e modificar o processo de depuração ou se comunicar com outras partes do Visual Studio.

 Você pode usar os `Condition` `IncludeView` atributos, e `ExcludeView` nos `CustomVisualizer` elementos.

 ## <a name="limitations"></a>Limitações

As personalizações de Natvis funcionam com classes e estruturas, mas não com TYPEDEFs.

O Natvis não oferece suporte a visualizadores para tipos primitivos (por exemplo, `int` `bool` ) ou para ponteiros para tipos primitivos. Nesse cenário, uma opção é usar o [especificador de formato](../debugger/format-specifiers-in-cpp.md) apropriado para seu caso de uso. Por exemplo, se você usar `double* mydoublearray` em seu código, poderá usar um especificador de formato de matriz na janela de **inspeção** do depurador, como a expressão `mydoublearray, [100]` , que mostra os primeiros 100 elementos.
