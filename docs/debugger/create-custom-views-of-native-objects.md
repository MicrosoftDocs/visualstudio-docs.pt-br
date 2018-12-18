---
title: Criar exibições personalizadas de objetos nativos
description: Use a estrutura do Natvis para personalizar a maneira como o Visual Studio exibe os tipos nativos no depurador
ms.custom: ''
ms.date: 10/31/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- natvis
dev_langs:
- C++
ms.assetid: 2d9a177a-e14b-404f-a6af-49498eff0bd7
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: 937692f11cbd642da823d6f7d13bcd90de59b388
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51000855"
---
# <a name="create-custom-views-of-native-objects-in-the-debugger"></a>Criar exibições personalizadas de objetos nativos no depurador

O Visual Studio *Natvis* framework personaliza a forma como tipos nativos aparecem nas janelas de variáveis do depurador, como o **Locals** e **Assista** windows e em **DataTips**. Visualizações do Natvis podem ajudar a tornar os tipos que você crie mais visível durante a depuração. 

Natvis substitui o *autoexp. dat* arquivo nas versões anteriores do Visual Studio com a sintaxe XML, diagnósticos melhores, controle de versão e vários arquivos de suporte.  

Natvis não funciona para:

- Projetos de área de trabalho do Windows C++ com o **tipo de depurador** definido como **misto** sob **propriedades de configuração** > **depuração**. 
- [Depuração de modo misto](how-to-debug-in-mixed-mode.md) para aplicativos de desktop do Windows no modo de compatibilidade gerenciado (**ferramentas** > **opções** > **depuração**  >  **Gerais** > **usar o modo de compatibilidade gerenciado**).

## <a name="BKMK_Why_create_visualizations_"></a>Visualizações do Natvis

Você pode usar a estrutura do Natvis para criar regras de visualização para os tipos que você cria, para que os desenvolvedores podem vê-los com mais facilidade durante a depuração.  

Por exemplo, a ilustração a seguir mostra uma variável do tipo [Windows::UI::Xaml::Controls::TextBox](http://go.microsoft.com/fwlink/?LinkId=258422) em uma janela de depurador sem quaisquer visualizações personalizados aplicadas.  

![Visualização de padrão de caixa de texto](../debugger/media/dbg_natvis_textbox_default.png "visualização padrão de caixa de texto")  

A linha realçada mostra a `Text` propriedade do `TextBox` classe. A hierarquia de classe complexa torna difícil localizar essa propriedade. O depurador não sabe como interpretar o tipo de cadeia de caracteres personalizada, portanto, não é possível ver a cadeia de caracteres mantida na caixa de texto.  

O mesmo `TextBox` se parece muito mais simples na janela variável quando são aplicadas regras do Natvis visualizador personalizado. Os membros importantes da classe aparecem juntas, e o depurador mostra o valor de cadeia de caracteres subjacente do tipo cadeia de caracteres personalizada.  

![Usando o Visualizador de dados de caixa de texto](../debugger/media/dbg_natvis_textbox_visualizer.png "usando o Visualizador de dados de caixa de texto")  

##  <a name="BKMK_Using_Natvis_files"></a>Usar arquivos. natvis em projetos do C++  

Usa Natvis *. natvis* arquivos para especificar regras de visualização. Um *. natvis* arquivo é um arquivo XML com um *. natvis* extensão. O esquema do Natvis é definido em *%VSINSTALLDIR%\Xml\Schemas\natvis.xsd*.  

A estrutura básica de um *. natvis* arquivo é um ou mais `Type` elementos que representam entradas de visualização. O nome totalmente qualificado de cada `Type` elemento é especificado no seu `Name` atributo.  

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

O Visual Studio fornece alguns *. natvis* arquivos de *%VSINSTALLDIR%\Common7\Packages\Debugger\Visualizers* pasta. Esses arquivos têm regras de visualização para muitos tipos comuns e podem servir como exemplos para escrever visualizações para novos tipos.  

### <a name="add-a-natvis-file-to-a-c-project"></a>Adicionar um arquivo. natvis para um projeto do C++  

Você pode adicionar um *. natvis* arquivo a qualquer projeto do C++.  

**Para adicionar uma nova *. natvis* arquivo:**

1. Selecione o nó de projeto do C++ no **Gerenciador de soluções**e selecione **Project** > **adicionar novo item**, ou clique com botão direito no projeto e selecione **adicionar**   >  **Novo item**.
   
1. No **Adicionar Novo Item** caixa de diálogo, selecione **Visual C++** > **utilitário** > **arquivo de visualização do depurador (. natvis)**. 
   
1. Nomeie o arquivo e, em seguida, selecione **adicionar**.
   
   O novo arquivo é adicionado ao **Gerenciador de soluções**e é aberto no painel de documento do Visual Studio. 

O depurador do Visual Studio carrega *. natvis* arquivos em projetos do C++ automaticamente e, por padrão, também inclui-los na *. PDB* arquivo quando o projeto é compilado. Se você depurar o aplicativo interno, o depurador carrega as *. natvis* arquivo o *. PDB* arquivo, mesmo se você não tiver o projeto aberto. Se não quiser que o *. natvis* arquivo incluído na *. PDB*, você pode excluí-lo do internos *. PDB* arquivo.

**Para excluir uma *. natvis* do arquivo de um *. PDB*:**

1. Selecione o *. natvis* arquivo no **Gerenciador de soluções**e selecione o **propriedades** ícone, ou o arquivo com o botão direito e selecione **propriedades**.
   
1. Lista suspensa na seta ao lado **excluídos do Build** e selecione **Yes**e, em seguida, selecione **Okey**.  

>[!NOTE]
>Para depurar projetos executáveis, use os itens de solução para adicionar qualquer *. natvis* arquivos que não estão na *. PDB*, porque não há nenhum projeto C++.  

>[!NOTE]
>Regras do Natvis carregado de um *. PDB* se aplicam somente a tipos nos módulos que o *. PDB* refere-se a. Por exemplo, se *Module1.pdb* tem uma entrada do Natvis para um tipo chamado `Test`, ele só se aplica ao `Test` classe na *Module1.dll*. Se o outro módulo também define uma classe chamada `Test`, o *Module1.pdb* entrada do Natvis não se aplica a ele.  

### <a name="BKMK_natvis_location"></a> Locais de arquivos do Natvis  

Você pode adicionar *. natvis* arquivos para seu diretório de usuário ou para um diretório do sistema, se você deseja que eles se aplicam a vários projetos.  

O *. natvis* arquivos são avaliados na seguinte ordem:  

1. Qualquer *. natvis* arquivos que são inseridos em uma *. PDB* você está depurando, a menos que um arquivo de mesmo nome existe no projeto carregado.  

1. Qualquer *. natvis* arquivos que estão em um projeto de C++ carregado ou uma solução de nível superior. Esse grupo inclui carregados todos os projetos do C++, incluindo bibliotecas de classes, mas não a projetos em outras linguagens. 

1.  O diretório do Natvis específicas do usuário (por exemplo, *%USERPROFILE%\Documents\Visual Studio 2017\Visualizers*).  

1.  O diretório do sistema Natvis (*%VSINSTALLDIR%\Common7\Packages\Debugger\Visualizers*). Esse diretório tem o *. natvis* arquivos que são instalados com o Visual Studio. Se você tiver permissões de administrador, você pode adicionar arquivos nesse diretório.  

## <a name="modify-natvis-files-while-debugging"></a>Modificar arquivos. natvis durante a depuração  

Você pode modificar uma *. natvis* arquivo no IDE durante a depuração de seu projeto. Abra o arquivo na mesma instância do Visual Studio que você estiver depurando com, modificá-la e salvá-lo. Assim que o arquivo é salvo, o **Watch** e **Locals** windows são atualizados para refletir a alteração. 

Você também pode adicionar ou excluir *. natvis* arquivos em uma solução que você está depurando, e o Visual Studio adiciona ou remove as visualizações relevantes.  

Não é possível atualizar *. natvis* arquivos que são inseridos na *. PDB* arquivos enquanto você estiver depurando.  

Se você modificar a *. natvis* arquivo fora do Visual Studio, as alterações não entram em vigor automaticamente. Para atualizar as janelas do depurador, é possível reavaliar o **.natvisreload** comando as **inspeção** janela. Em seguida, as alterações entram em vigor sem reiniciar a sessão de depuração.  

Use também o **.natvisreload** comando para atualizar o *. natvis* arquivo para uma versão mais recente. Por exemplo, o *. natvis* arquivo pode ser verificado no controle de origem, e você deseja acompanhar as alterações recentes criado por outra pessoa. 

##  <a name="BKMK_Expressions_and_formatting"></a> Expressões e formatação  
As visualizações do Natvis usam expressões do C++ para especificar os itens de dados a serem exibidos. Além dos aprimoramentos e as limitações das expressões C++ no depurador, que são descritos em [operador de contexto (C++)](../debugger/context-operator-cpp.md), esteja ciente das seguintes opções:  

- As expressões do Natvis são avaliadas no contexto do objeto que está sendo visualizado, não do registro de ativação atual. Por exemplo, `x` um Natvis expressão se refere ao campo denominado **x** no objeto que está sendo visualizado, não a uma variável local chamada **x** na função atual. Você não pode acessar variáveis locais em expressões do Natvis, embora você possa acessar as variáveis globais.  

- As expressões do Natvis não permitem a avaliação da função ou efeitos colaterais. Chamadas de função e operadores de atribuição são ignorados. Porque [funções intrínsecas do depurador](../debugger/expressions-in-the-debugger.md#BKMK_Using_debugger_intrinisic_functions_to_maintain_state) têm efeitos colaterais gratuitamente, elas podem ser livremente chamadas de qualquer expressão do Natvis, mesmo que outras chamadas de função não são permitidas.  

- Para controlar como uma expressão exibe, você pode usar qualquer um dos especificadores de formato descritos na [especificadores em C++ de formato](format-specifiers-in-cpp.md#BKMK_Visual_Studio_2012_format_specifiers). Especificadores de formato são ignorados quando a entrada é usada internamente pelo Natvis, como o `Size` expressão em uma [expansão de ArrayItems](../debugger/create-custom-views-of-native-objects.md#BKMK_ArrayItems_expansion).  

## <a name="natvis-views"></a>Modos de exibição do Natvis  

Você pode definir diferentes modos de exibição do Natvis para exibir os tipos de maneiras diferentes. Por exemplo, aqui está uma visualização dos `std::vector` que define uma exibição simplificada chamada `simple`. O `DisplayString` e o `ArrayItems` elementos mostram na exibição padrão e o `simple` modo de exibição, enquanto o `[size]` e `[capacity]` itens não aparecem no `simple` modo de exibição. 

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


No **Watch** janela, use o **, modo de exibição** especificador para especificar uma exibição alternativa de formato. O modo de exibição simple é exibido como **vec,view(simple)**:  

![Janela de observação com o modo de exibição simple](../debugger/media/watch-simpleview.png "janela Inspeção com o modo de exibição simple")  

##  <a name="BKMK_Diagnosing_Natvis_errors"></a> Erros do natvis&lt;1}  

Quando o depurador encontrar erros em uma entrada de visualização, ele ignora-los. Ele exibe o tipo em sua forma bruta, ou seleciona outra visualização apropriada. Você pode usar o diagnóstico do Natvis para entender por que o depurador ignorada uma entrada de visualização e para ver a sintaxe subjacente e erros de análise. 

**Para ativar o diagnóstico do Natvis:**

- Sob **ferramentas** > **opções** (ou **depurar** > **opções**) > **dedepuração**  >  **Janela de saída**, defina **mensagens de diagnóstico Natvis (somente C++)** para **erro**, **aviso**, ou  **Verbose**e, em seguida, selecione **Okey**. 

Os erros exibidos na **saída** janela.  

##  <a name="BKMK_Syntax_reference"></a> Referência de sintaxe do Natvis  

###  <a name="BKMK_AutoVisualizer"></a> Elemento AutoVisualizer  
O `AutoVisualizer` elemento é o nó raiz do *. natvis* do arquivo e contém o namespace `xmlns:` atributo. 

```xml
<?xml version="1.0" encoding="utf-8"?>  
<AutoVisualizer xmlns="http://schemas.microsoft.com/vstudio/debugger/natvis/2010">  
.  
.  
</AutoVisualizer>  
```  

O `AutoVisualizer` elemento pode ter [tipo](#BKMK_Type), [HResult](#BKMK_HResult), [UIVisualizer](#BKMK_UIVisualizer), e [CustomVisualizer](#BKMK_CustomVisualizer) filhos. 

###  <a name="BKMK_Type"></a> Elemento Type  

Um básico `Type` se parece com este exemplo:  

```xml
<Type Name="[fully qualified type name]">  
  <DisplayString Condition="[Boolean expression]">[Display value]</DisplayString>  
  <Expand>  
    ...  
  </Expand>  
</Type>  
```  

 O `Type` elemento especifica:  

1. O que a visualização de tipo deve ser usada para (o `Name` atributo).  
   
2. O valor de um objeto desse tipo de aparência (o `DisplayString` elemento).  
   
3. Os membros do tipo de aparência quando o usuário expande o tipo em uma janela variável (o `Expand` nó).  
   
#### <a name="templated-classes"></a>Classes com modelo
O `Name` atributo o `Type` elemento aceita um asterisco `*` como um caractere curinga que pode ser usado para nomes de classe de modelo.  

No exemplo a seguir, a mesma visualização é usada se o objeto é uma `CAtlArray<int>` ou um `CAtlArray<float>`. Se não houver uma entrada de visualização específico para um `CAtlArray<float>`, em seguida, ela terá precedência sobre a genérica.  

```xml
<Type Name="ATL::CAtlArray&lt;*&gt;">  
    <DisplayString>{{Count = {m_nSize}}}</DisplayString>  
</Type>  
```  

Você pode fazer referência a parâmetros de modelo na entrada de visualização usando macros $T1, $T2 e assim por diante. Para localizar exemplos dessas macros, consulte a *. natvis* arquivos enviados com o Visual Studio.  

####  <a name="BKMK_Visualizer_type_matching"></a> Correspondência de tipo de Visualizador  
Se uma entrada de visualização não for validado, a próxima visualização disponível será usada.  

#### <a name="inheritable-attribute"></a>Atributo herdável  
Opcional `Inheritable` atributo especifica se uma visualização só se aplica a um tipo base ou para um tipo base e todos os tipos derivados. O valor padrão de `Inheritable` é `true`.  

No exemplo a seguir, a visualização só é aplicável a `BaseClass` tipo:  

```xml
<Type Name="Namespace::BaseClass" Inheritable="false">  
    <DisplayString>{{Count = {m_nSize}}}</DisplayString>  
</Type>  
```  

#### <a name="priority-attribute"></a>Atributo de prioridade  

Opcional `Priority` atributo especifica a ordem na qual usar definições alternativas, se uma definição de falha ao ser analisada. Os valores possíveis da `Priority` são: `Low`, `MediumLow`,`Medium`, `MediumHigh`, e `High`. O valor padrão é `Medium`. O `Priority` atributo distingue somente entre as prioridades dentro do mesmo *. natvis* arquivo.  

O exemplo a seguir primeiro analisa a entrada que corresponde ao STL 2015. Se isso falhar ao analisar, ele usa a entrada alternativa para a versão 2013 STL:  

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
Você pode colocar um `Optional` atributo em qualquer nó. Se uma subexpressão dentro de um nó opcional falhar ao analisar, o depurador ignora esse nó, mas aplica-se o restante do `Type` regras. Na seguinte, digite `[State]` não seja opcional, mas `[Exception]` é opcional.  Se `MyNamespace::MyClass` tem um campo chamado _`M_exceptionHolder`, ambas as a `[State]` nó e o `[Exception]` nó são exibidos, mas se não há nenhum `_M_exceptionHolder` campo, somente o `[State]` nó aparece.

```xml
<Type Name="MyNamespace::MyClass">  
    <Expand>  
      <Item Name="[State]">_M_State</Item>  
      <Item Name="[Exception]" Optional="true">_M_exceptionHolder</Item>  
    </Expand>  
</Type>  
```  

###  <a name="BKMK_Condition_attribute"></a> Atributo de condição  

Opcional `Condition` atributo está disponível para muitos elementos de visualização e especifica quando usar uma regra de visualização. Se a expressão dentro do atributo condition for resolvida como `false`, a regra de visualização não se aplica. Se for avaliada como `true`, ou não há nenhum `Condition` atributo, a visualização se aplica. Você pode usar esse atributo para lógica if-else nas entradas de visualização. 

Por exemplo, a seguinte visualização tem dois `DisplayString` elementos para um tipo de ponteiro inteligente. Quando o `_Myptr` membro está vazio, a condição do primeiro `DisplayString` elemento resolve para `true`, portanto, esse formulário exibe. Quando o `_Myptr` membro não estiver vazio, a condição for avaliada como `false`e a segunda `DisplayString` elemento exibe.  

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

O `IncludeView` e `ExcludeView` atributos especificam elementos para exibir ou não nos modos de exibição específicos. Por exemplo, na seguinte Natvis da especificação de `std::vector`, o `simple` modo de exibição não exibe o `[size]` e `[capacity]` itens.

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

Você pode usar o `IncludeView` e `ExcludeView` atributos, tipos e membros individuais.  

###  <a name="BKMK_Versioning"></a> Elemento Version  
O `Version` elemento tem como escopo uma entrada para um módulo específico e uma versão de visualização. O `Version` elemento ajuda a evitar colisões de nome, reduz a incompatibilidades acidentais e permite visualizações diferentes para diferentes versões de tipo.  

Se um arquivo de cabeçalho comum que é usado por diferentes módulos define um tipo, a visualização com versão só aparece quando o tipo é a versão do módulo especificado.  

No exemplo a seguir, a visualização é aplicável somente para o `DirectUI::Border` tipo encontrado na `Windows.UI.Xaml.dll` da versão 1.0 a 1.5. 

```xml
<Type Name="DirectUI::Border">  
  <Version Name="Windows.UI.Xaml.dll" Min="1.0" Max="1.5"/>  
  <DisplayString>{{Name = {*(m_pDO->m_pstrName)}}}</DisplayString>  
  <Expand>  
    <ExpandedItem>*(CBorder*)(m_pDO)</ExpandedItem>  
  </Expand>  
</Type>  
```  

###  <a name="BKMK_DisplayString"></a> Elemento DisplayString 
O `DisplayString` elemento Especifica uma cadeia de caracteres para mostrar como o valor de uma variável. Aceita cadeias de caracteres arbitrárias misturadas a expressões. Tudo dentro das chaves é interpretado como uma expressão. Por exemplo, o seguinte `DisplayString` entrada:  

```xml
<Type Name="CPoint">  
  <DisplayString>{{x={x} y={y}}}</DisplayString>   
</Type>  
```  

Significa que variáveis do tipo `CPoint` exibir como esta ilustração:  

 ![Usar um elemento de DisplayString](../debugger/media/dbg_natvis_cpoint_displaystring.png "usar um elemento de DisplayString")  

No `DisplayString` expressão, `x` e `y`, que são membros de `CPoint`, estão entre chaves, portanto, seus valores são avaliados. O exemplo também mostra como você pode fazer o escape uma chave usando chaves duplas ( `{{` ou `}}` ).  

> [!NOTE]
> O `DisplayString` é o único elemento que aceita cadeias de caracteres arbitrárias e a sintaxe da chave. Todos os outros elementos de visualização aceitam apenas expressões o depurador pode avaliar.  

###  <a name="BKMK_StringView"></a> Elemento StringView 

O `StringView` elemento define um valor que o depurador pode enviar ao Visualizador interno de texto. Por exemplo, dada a seguinte visualização para o `ATL::CStringT` tipo:  

```xml
<Type Name="ATL::CStringT&lt;wchar_t,*&gt;">  
  <DisplayString>{m_pszData,su}</DisplayString>  
</Type>
```  

O `CStringT` objeto exibe em uma janela variável, como neste exemplo:   

![Elemento CStringT DisplayString](../debugger/media/dbg_natvis_displaystring_cstringt.png "elemento CStringT DisplayString")  

Adicionando um `StringView` elemento informa o depurador pode exibir o valor como uma visualização de texto.  

```xml
<Type Name="ATL::CStringT&lt;wchar_t,*&gt;">
  <DisplayString>{m_pszData,su}</DisplayString>  
  <StringView>m_pszData,su</StringView>  
</Type>  
```  

Durante a depuração, você pode selecionar o ícone de lupa ao lado da variável e, em seguida, selecione **Visualizador de texto** para exibir a cadeia de caracteres que **m_pszData** aponta.  

 ![CStringT dados com o Visualizador de StringView](../debugger/media/dbg_natvis_stringview_cstringt.png "CStringT dados com o Visualizador de StringView")  

A expressão `{m_pszData,su}` inclui um especificador de formato de C++ **su**, para exibir o valor como uma cadeia de caracteres Unicode. Para obter mais informações, consulte [especificadores em C++ de formato](../debugger/format-specifiers-in-cpp.md).  

###  <a name="BKMK_Expand"></a> Expanda o elemento 

Opcional `Expand` nó personaliza os filhos de um tipo visualizado quando você expande o tipo em uma janela variável. O `Expand` nó aceita uma lista de nós filho que definem os elementos filho.  

- Se um `Expand` nó não for especificado em uma entrada de visualização, os filhos usam as regras de expansão do padrão.  
  
- Se um `Expand` nó é especificado sem nós filhos abaixo dele, o tipo não for expansível nas janelas do depurador.  

####  <a name="BKMK_Item_expansion"></a> Expansão de item  

 O `Item` é o maior elemento básico e comuns em um `Expand` nó. `Item` define um único elemento filho. Por exemplo, uma `CRect` classe com campos `top`, `left`, `right`, e `bottom` tem a seguinte entrada de visualização:  

```xml
<Type Name="CRect">  
  <DisplayString>{{top={top} bottom={bottom} left={left} right={right}}}</DisplayString>  
  <Expand>  
    <Item Name="Width">right - left</Item>  
    <Item Name="Height">bottom - top</Item>  
  </Expand>  
</Type>  
```  

Na janela do depurador, o `CRect` tipo se pareça com este exemplo:  

![CRect com expansão de elemento do Item](../debugger/media/dbg_natvis_expand_item_crect1.png "CRect com expansão de elemento do Item")  

O depurador avalia as expressões especificadas na `Width` e `Height` elementos e mostra os valores a **valor** coluna da janela variável. 

O depurador cria automaticamente o **[modo de exibição bruto]** nó para cada uma expansão personalizada. Captura de tela anterior exibe a **[modo de exibição bruto]** nó expandido para mostrar como o modo de exibição bruto padrão do objeto difere de sua visualização Natvis. A expansão padrão cria uma subárvore para a classe base e lista todos os membros de dados da classe base como filhos.  

> [!NOTE]
> Se a expressão de elemento do item apontar para um tipo complexo, o **Item** próprio nó for expansível.  

####  <a name="BKMK_ArrayItems_expansion"></a> Expansão de ArrayItems  
Use o nó `ArrayItems` para que o depurador do Visual Studio interprete o tipo como uma matriz e exiba seus elementos individuais. A visualização para `std::vector` é um bom exemplo:  

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

![std:: Vector usando a expansão de ArrayItems](../debugger/media/dbg_natvis_expand_arrayitems_stdvector.png "std:: Vector usando a expansão de ArrayItems")  

O `ArrayItems` nó deve ter:  

- Um `Size` expressão (que deve ser avaliada como um número inteiro) para que o depurador entenda o comprimento da matriz.  
- Um `ValuePointer` expressão que aponta para o primeiro elemento (que deve ser um ponteiro de um tipo de elemento que não é `void*`).  

O valor padrão do limite inferior de matriz é 0. Para substituir o valor, use um `LowerBound` elemento. O *. natvis* arquivos acompanham o Visual Studio têm exemplos.  

>[!NOTE]
>Você pode usar o `[]` operador, por exemplo `vector[i]`, com qualquer visualização de matriz unidimensional que usa `ArrayItems`, mesmo se o próprio tipo (por exemplo `CATLArray`) não permite esse operador.  

Você também pode especificar a matrizes multidimensionais. Nesse caso, o depurador precisa saber um pouco para exibir corretamente os elementos filho:  

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

- `Direction` Especifica se a matriz está na ordem de linhas principais ou de coluna principal. 
- `Rank` especifica a classificação da matriz. 
- O `Size` elemento aceita implícito `$i` parâmetro, o que ele substitui pelo índice de dimensão para encontrar o comprimento da matriz nessa dimensão. No exemplo anterior, a expressão `_M_extent.M_base[0]` deve fornecer o comprimento da dimensão 0º, `_M_extent._M_base[1]` o 1º dia e assim por diante.  

Aqui está como bidimensional `Concurrency::array` objeto fica na janela do depurador:  

![Uma matriz bidimensional com expansão de ArrayItems](../debugger/media/dbg_natvis_expand_arrayitems_2d.png "matriz bidimensional com expansão de ArrayItems")  

####  <a name="BKMK_IndexListItems_expansion"></a> Expansão de IndexListItems  

Você pode usar `ArrayItems` expansão somente se os elementos da matriz são dispostos contiguamente na memória. Obtém o depurador para o próximo elemento incrementando o ponteiro. Se você precisar manipular o índice do nó de valor, use `IndexListItems` nós. Aqui está uma visualização com um `IndexListItems` nó:  

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

A única diferença entre `ArrayItems` e `IndexListItems` é o `ValueNode`, que espera a expressão completa para o i<sup>th</sup> elemento com o implícita `$i` parâmetro.  

>[!NOTE]
>Você pode usar o `[]` operador, por exemplo `vector[i]`, com qualquer visualização de matriz unidimensional que usa `IndexListItems`, mesmo se o próprio tipo (por exemplo `CATLArray`) não permite esse operador.  

####  <a name="BKMK_LinkedListItems_expansion"></a> Expansão de LinkedListItems  

Se o tipo visualizado representa uma lista vinculada, o depurador pode exibir seus filhos usando um nó `LinkedListItems`. A seguinte visualização para o `CAtlList` usos de tipo `LinkedListItems`:  

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

O depurador avalia a `NextPointer` e `ValueNode` expressões no contexto do `LinkedListItems` elemento de nó, não o tipo da lista pai. No exemplo anterior, `CAtlList` tem uma `CNode` classe (encontrada no `atlcoll.h`) que é um nó da lista vinculada. `m_pNext` e `m_element` são campos dessa `CNode` classe, não do `CAtlList` classe.  

`ValueNode` pode ser deixada em branco ou use `this` para fazer referência a `LinkedListItems` próprio nó.  

#### <a name="customlistitems-expansion"></a>Expansão de CustomListItems  
O `CustomListItems` expansão permite que você escreva uma lógica personalizada para percorrer uma estrutura de dados como uma tabela de hash. Use `CustomListItems` visualizar as estruturas de dados que podem usar expressões C++ para tudo que você precisa para avaliar, mas não muito ajustar o ciclo para `ArrayItems`, `IndexListItems`, ou `LinkedListItems`.  

O visualizador a seguir para `CAtlMap` é um excelente exemplo onde `CustomListItems` é apropriado.  

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

Você pode usar `Exec` para executar o código dentro de um `CustomListItems` expansão, usando as variáveis e objetos definidos na expansão. Você pode usar operadores lógicos, operadores aritméticos e operadores de atribuição com `Exec`. Não é possível usar `Exec` para avaliar funções.

`CustomListItems` suporta as seguintes funções intrínsecas:

- `strlen`, `wcslen`, `strnlen`, `wcsnlen`, `strcmp`, `wcscmp`, `_stricmp`, `_strcmpi`, `_wcsicmp`, `strncmp`, `wcsncmp`, `_strnicmp`, `_wcsnicmp`, `memcmp`, `memicmp`, `wmemcmp`, `strchr`, `wcschr`, `memchr`, `wmemchr`, `strstr`, `wcsstr`, `__log2`, `__findNonNull`
- `GetLastError`, `TlsGetValue`, `DecodeHString`, `WindowsGetStringLen`, `WindowsGetStringRawBuffer`, `WindowsCompareStringOrdinal`, `RoInspectCapturedStackBackTrace`, `CoDecodeProxy`, `GetEnvBlockLength`, `DecodeWinRTRestrictedException`, `DynamicMemberLookup`, `DecodePointer`, `DynamicCast`
- `ConcurrencyArray_OperatorBracket_idx // Concurrency::array<>::operator[index<>] and operator(index<>)`
- `ConcurrencyArray_OperatorBracket_int // Concurrency::array<>::operator(int, int, ...)`
- `ConcurrencyArray_OperatorBracket_tidx // Concurrency::array<>::operator[tiled_index<>] and operator(tiled_index<>)`
- `ConcurrencyArrayView_OperatorBracket_idx // Concurrency::array_view<>::operator[index<>] and operator(index<>)`
- `ConcurrencyArrayView_OperatorBracket_int // Concurrency::array_view<>::operator(int, int, ...)`
- `ConcurrencyArrayView_OperatorBracket_tidx // Concurrency::array_view<>::operator[tiled_index<>] and operator(tiled_index<>)`
- `Stdext_HashMap_Int_OperatorBracket_idx`
- `Std_UnorderedMap_Int_OperatorBracket_idx`
- `TreeTraverse_Init // Initializes a new tree traversal`
- `TreeTraverse_Next // Returns nodes in a tree`
- `TreeTraverse_Skip // Skips nodes in a pending tree traversal`

####  <a name="BKMK_TreeItems_expansion"></a> Expansão de TreeItems  
 Se o tipo visualizado representa uma árvore, o depurador pode percorrer a árvore e exibir seus filhos usando um nó `TreeItems`. Esta é a visualização para o `std::map` um tipo usando um `TreeItems` nó:  

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

A sintaxe é semelhante ao `LinkedListItems` nó. `LeftPointer`, `RightPointer`, e `ValueNode` são avaliados no contexto da classe de nó de árvore. `ValueNode` pode ser deixada em branco ou use `this` para fazer referência a `TreeItems` próprio nó.  

####  <a name="BKMK_ExpandedItem_expansion"></a> Expansão de ExpandedItem  
 O `ExpandedItem` elemento gera uma exibição filho agregada exibindo propriedades de membros de dados ou classes base, como se fossem filhos do tipo visualizado. O depurador avalia a expressão especificada e anexa os nós filho do resultado para a lista de filhos do tipo visualizado. 

Por exemplo, o tipo de ponteiro inteligente `auto_ptr<vector<int>>` normalmente é exibida como:  

 ![automático&#95;ptr&#60;vetor&#60;int&#62; &#62; expansão padrão](../debugger/media/dbg_natvis_expand_expandeditem_default.png "expansão padrão")  

 Para ver os valores do vetor, você precisa fazer drill down dois níveis na janela variável, passando por meio de `_Myptr` membro. Adicionando um `ExpandedItem` elemento, você pode eliminar o `_Myptr` variável da hierarquia e diretamente exibir os elementos do vetor:  

```xml
<Type Name="std::auto_ptr&lt;*&gt;">  
  <DisplayString>auto_ptr {*_Myptr}</DisplayString>  
  <Expand>  
    <ExpandedItem>_Myptr</ExpandedItem>  
  </Expand>  
</Type>  
```  

 ![automático&#95;ptr&#60;vetor&#60;int&#62; &#62; expansão de ExpandedItem](../debugger/media/dbg_natvis_expand_expandeditem_visualized.png "expansão de ExpandedItem")  

O exemplo a seguir mostra como agregar propriedades da classe base em uma classe derivada. Suponha que a classe `CPanel` seja derivada de `CFrameworkElement`. Em vez de repetir as propriedades que vêm de base `CFrameworkElement` classe, o `ExpandedItem` visualização de nó acrescenta essas propriedades à lista de filhos a `CPanel` classe. 

```xml
<Type Name="CPanel">  
  <DisplayString>{{Name = {*(m_pstrName)}}}</DisplayString>  
  <Expand>  
    <Item Name="IsItemsHost">(bool)m_bItemsHost</Item>  
    <ExpandedItem>*(CFrameworkElement*)this,nd</ExpandedItem>  
  </Expand>  
</Type>  
```  

O **nd** especificador de formato, o que desativa a visualização de correspondência para a classe derivada, é necessário aqui. Caso contrário, a expressão `*(CFrameworkElement*)this` causaria a `CPanel` visualização a ser aplicada novamente, porque as regras de correspondência de tipo de visualização padrão considerá-la mais apropriada. Use o **nd** especificador para instruir o depurador a usar a visualização da classe base, ou a expansão padrão se a classe base não tenha nenhuma visualização de formato.  

####  <a name="BKMK_Synthetic_Item_expansion"></a> Expansão de item sintético  
 Enquanto o `ExpandedItem` elemento fornece uma exibição mais simples de dados, eliminando as hierarquias, o `Synthetic` nó faz o oposto. Ele permite que você crie um elemento filho artificial que não é um resultado de uma expressão. O elemento artificial pode ter elementos filho de seu próprio. No exemplo a seguir, a visualização do tipo `Concurrency::array` usa um nó de `Synthetic` para mostrar uma mensagem de diagnóstico para o usuário:  

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

###  <a name="BKMK_HResult"></a> Elemento HResult 
 O `HResult` elemento permite que você personalize as informações exibidas para um **HRESULT** nas janelas do depurador. O `HRValue` elemento deve conter o valor de 32 bits do **HRESULT** que deve ser personalizado. O `HRDescription` elemento contém as informações serão exibidas na janela do depurador.  

```xml

<HResult Name="MY_E_COLLECTION_NOELEMENTS">  
  <HRValue>0xABC0123</HRValue>  
  <HRDescription>No elements in the collection.</HRDescription>  
</HResult>  
```  

###  <a name="BKMK_UIVisualizer"></a> Elemento UIVisualizer 
Um elemento `UIVisualizer` registra um plug-in de visualizador gráfico no depurador. Um visualizador gráfico cria uma caixa de diálogo ou outra interface que mostra uma variável ou objeto de maneira consistente com seu tipo de dados. O Visualizador de plug-in deve ser criado como um [VSPackage](../extensibility/internals/vspackages.md)e deve expor um serviço que o depurador pode consumir. O *. natvis* arquivo contém informações de registro para o plug-in, como seu nome, o GUID do serviço exposto e os tipos que ele pode visualizar.  

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

- Um `ServiceId`  -  `Id` par atributo identifica um `UIVisualizer`. O `ServiceId` é o GUID do serviço Visualizador de pacote expõe. `Id` é um identificador exclusivo que diferencia os visualizadores, se um serviço fornecer mais de um. No exemplo anterior, o mesmo serviço de visualizador fornece dois visualizadores.  
  
- O `MenuName` atributo define um nome de visualizador para exibir na lista suspensa ao lado do ícone de lupa no depurador. Por exemplo:  

  ![Menu de atalho do menu UIVisualizer](../debugger/media/dbg_natvis_vectorvisualizer.png "UIVisualizer menu de atalho de menu")  

Cada tipo definido na *. natvis* arquivo deve listar explicitamente qualquer visualizadores de interface do usuário que podem exibi-lo. O depurador corresponde as referências do visualizador nas entradas de tipo aos visualizadores registrados. Por exemplo, a seguinte entrada de tipo para `std::vector` referências a `UIVisualizer` no exemplo anterior.  

```xml
<Type Name="std::vector&lt;int,*&gt;">  
  <UIVisualizer ServiceId="{5452AFEA-3DF6-46BB-9177-C0B08F318025}" Id="1" />  
</Type>  
```  

 Você pode ver um exemplo de uma `UIVisualizer` no [imagem inspeção](https://marketplace.visualstudio.com/items?itemName=VisualCPPTeam.ImageWatch2017) extensão usada para exibir os bitmaps de na memória. 

### <a name="BKMK_CustomVisualizer"></a>Elemento CustomVisualizer  
 `CustomVisualizer` é um ponto de extensibilidade que especifica uma extensão do VSIX que você escreve para controlar as visualizações no Visual Studio code. Para obter mais informações sobre como escrever extensões VSIX, consulte o [SDK do Visual Studio](../extensibility/visual-studio-sdk.md). 

É muito mais trabalho para escrever um visualizador personalizado que uma definição de XML Natvis, mas você tem a liberdade de restrições sobre o que faz Natvis ou não dá suporte. Os visualizadores personalizados têm acesso ao conjunto completo de APIs, o que pode consultar e modificar o processo a ser depurado ou se comunicar com outras partes do Visual Studio de extensibilidade do depurador.  

 Você pode usar o `Condition`, `IncludeView`, e `ExcludeView` atributos em `CustomVisualizer` elementos.
