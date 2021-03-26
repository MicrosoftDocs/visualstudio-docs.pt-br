---
title: Como VSPackages adicionar elementos da interface do usuário | Microsoft Docs
description: Saiba como VSPackages adicionar elementos da interface do usuário (IU), como menus, barras de ferramentas e janelas de ferramentas, ao Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, adding elements
- UI element design [Visual Studio SDK], VSPackages
- VSPackages, contributing UI elements
ms.assetid: abc5d9d9-b267-48a1-92ad-75fbf2f4c1b9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f1d01c2ed91a5f4aad55c196dfb2e689aeea288a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086034"
---
# <a name="how-vspackages-add-user-interface-elements"></a>Como VSPackages adicionar elementos da interface do usuário
Um VSPackage pode adicionar elementos de interface do usuário (IU), por exemplo, menus, barras de ferramentas e janelas de ferramentas, ao Visual Studio por meio do arquivo *. vsct* .

Você pode encontrar diretrizes de design para elementos de interface do [usuário em diretrizes de experiência de usuários do Visual Studio](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md).

## <a name="the-visual-studio-command-table-architecture"></a>A arquitetura de tabela de comando do Visual Studio
Como observado, a arquitetura da tabela de comandos dá suporte aos princípios arquitetônicos acima. As filosofias por trás das abstrações, das estruturas de dados e das ferramentas da arquitetura de tabela de comando são as seguintes:

- Há três tipos básicos de itens: menus, comandos e grupos. Os menus podem ser expostos na interface do usuário como menus, submenus, barras de ferramentas ou janelas de ferramentas. Os comandos são procedimentos que o usuário pode executar no IDE e eles podem ser expostos como itens de menu, botões, caixas de listagem ou outros controles. Os grupos são contêineres para menus e comandos.

- Cada item é especificado por uma definição que descreve o item, sua prioridade em relação a outros itens e os sinalizadores que modificam seu comportamento.

- Cada item tem um posicionamento que descreve o pai do item. Um item pode ter vários pais, para que ele possa aparecer em vários locais na interface do usuário.

Cada comando deve ter um grupo como seu pai, mesmo se for o único filho nesse grupo. Todos os menus padrão também devem ter um grupo pai. As barras de ferramentas e as janelas de ferramentas atuam como seus próprios pais. Um grupo pode ter como pai a barra de menus principal do Visual Studio ou qualquer menu, barra de ferramentas ou janela de ferramentas.

### <a name="how-items-are-defined"></a>Como os itens são definidos
Um arquivo *. vsct* é formatado em XML. Ele define os elementos da interface do usuário para um pacote e determina onde esses elementos aparecem no IDE. Cada menu, grupo ou comando no pacote recebe primeiro um GUID e uma ID na `Symbols` seção. Em todo o restante do arquivo *. vsct* , cada menu, comando e grupo é identificado por sua combinação de GUID e ID. O exemplo a seguir mostra uma `Symbols` seção típica como gerada pelo modelo de pacote do Visual Studio quando um **comando de menu** é selecionado no modelo.

```xml
<Symbols>
  <!-- This is the package guid. -->
  <GuidSymbol name="guidMenuTextPkg" value="{b1253bc6-d266-402b-89e7-5e3d3b22c746}" />

  <!-- This is the guid used to group the menu commands together -->
  <GuidSymbol name="guidMenuTextCmdSet" value="{a633d4e4-6c65-4436-a138-1abeba7c9a69}">
    <IDSymbol name="MyMenuGroup" value="0x1020" />
    <IDSymbol name="cmdidMyCommand" value="0x0100" />
  </GuidSymbol>

  <GuidSymbol name="guidImages" value="{53323d9a-972d-4671-bb5b-9e418480922f}">
    <IDSymbol name="bmpPic1" value="1" />
    <IDSymbol name="bmpPic2" value="2" />
    <IDSymbol name="bmpPicSearch" value="3" />
    <IDSymbol name="bmpPicX" value="4" />
    <IDSymbol name="bmpPicArrows" value="5" />
  </GuidSymbol>
</Symbols>
```

O elemento de nível superior da `Symbols` seção é o [elemento GuidSymbol](../../extensibility/guidsymbol-element.md). `GuidSymbol` os elementos mapeiam nomes para GUIDs que são usados pelo IDE para identificar pacotes e suas partes de componente.

> [!NOTE]
> Os GUIDs são gerados automaticamente pelo modelo de pacote do Visual Studio. Você também pode criar um GUID exclusivo clicando em **Criar GUID** no menu **ferramentas** .

O primeiro `GuidSymbol` elemento, `guid<PackageName>Pkg` , é o GUID do próprio pacote. Esse é o GUID usado pelo Visual Studio para carregar o pacote. Normalmente, ele não tem elementos filho.

Por convenção, menus e comandos são agrupados em um segundo `GuidSymbol` elemento, `guid<PackageName>CmdSet` e os bitmaps estão em um terceiro `GuidSymbol` elemento, `guidImages` . Você não precisa seguir essa convenção, mas cada menu, grupo, comando e bitmap deve ser um filho de um `GuidSymbol` elemento.

No segundo `GuidSymbol` elemento, que representa o conjunto de comandos do pacote, há vários `IDSymbol` elementos. Cada [elemento IDSymbol](../../extensibility/idsymbol-element.md) mapeia um nome para um valor numérico e pode representar um menu, grupo ou comando que faz parte do conjunto de comandos. Os `IDSymbol` elementos no terceiro `GuidSymbol` elemento representam bitmaps que podem ser usados como ícones para comandos. Como os pares GUID/ID devem ser exclusivos em um aplicativo, dois filhos do mesmo `GuidSymbol` elemento podem ter o mesmo valor.

### <a name="menus-groups-and-commands"></a>Menus, grupos e comandos
Quando um menu, grupo ou comando tem um GUID e uma ID, ele pode ser adicionado ao IDE. Todo elemento de interface do usuário deve ter as seguintes opções:

- Um `guid` atributo que corresponde ao nome do `GuidSymbol` elemento no qual o elemento de interface do usuário está definido.

- Um `id` atributo que corresponde ao nome do elemento associado `IDSymbol` .

Juntos, os `guid` `id` atributos e compõem a *assinatura* do elemento de interface do usuário.

- Um `priority` atributo que determina o posicionamento do elemento de interface do usuário em seu menu ou grupo pai.

- Um [elemento pai](../../extensibility/parent-element.md) que tem `guid` `id` atributos e que especificam a assinatura do menu ou grupo pai.

#### <a name="menus"></a>Menus
Cada menu é definido como um [elemento de menu](../../extensibility/menu-element.md) na `Menus` seção. Os menus devem `guid` ter `id` os atributos,, e e `priority` um `Parent` elemento e também os seguintes atributos adicionais e filhos:

- Um `type` atributo que especifica se o menu deve aparecer no IDE como um tipo de menu ou como uma barra de ferramentas.

- Um [elemento Strings](../../extensibility/strings-element.md) que contém um [elemento ButtonText](../../extensibility/buttontext-element.md), que especifica o título do menu no IDE e um [elemento CommandName](../../extensibility/commandname-element.md), que especifica o nome usado na janela de **comando** para acessar o menu.

- Sinalizadores opcionais. Um [elemento CommandFlag](../../extensibility/command-flag-element.md) pode aparecer em uma definição de menu para alterar sua aparência ou comportamento no IDE.

Cada `Menu` elemento deve ter um grupo como seu pai, a menos que seja um elemento encaixáveis, como uma barra de ferramentas. Um menu encaixáveis é seu próprio pai. Para obter mais informações sobre menus e valores para o `type` atributo, consulte a documentação do [elemento de menu](../../extensibility/menu-element.md) .

O exemplo a seguir mostra um menu que aparece na barra de menus do Visual Studio, ao lado do menu **ferramentas** .

```xml
<Menu guid="guidTopLevelMenuCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
  <Parent guid="guidSHLMainMenu" id="IDG_VS_MM_TOOLSADDINS" />
  <Strings>
    <ButtonText>TestMenu</ButtonText>
    <CommandName>TestMenu</CommandName>
  </Strings>
</Menu>
```

#### <a name="groups"></a>Grupos
Um grupo é um item que é definido na `Groups` seção do arquivo *. vsct* . Os grupos são apenas contêineres. Eles não aparecem no IDE, exceto como uma linha divisória em um menu. Portanto, um [elemento de grupo](../../extensibility/group-element.md) é definido somente por sua assinatura, prioridade e pai.

Um grupo pode ter um menu, outro grupo ou ele mesmo como pai. No entanto, o pai é normalmente um menu ou barra de ferramentas. O menu no exemplo anterior é um filho do `IDG_VS_MM_TOOLSADDINS` grupo e esse grupo é filho da barra de menus do Visual Studio. O grupo no exemplo a seguir é um filho do menu no exemplo anterior.

```xml
<Group guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" priority="0x0600">
  <Parent guid="guidTopLevelMenuCmdSet" id="TopLevelMenu"/>
</Group>
```

Como ele faz parte de um menu, esse grupo normalmente contém comandos. No entanto, ele também pode conter outros menus. É assim que os submenus são definidos, conforme mostrado no exemplo a seguir.

```xml
<Menu guid="guidTopLevelMenuCmdSet" id="SubMenu" priority="0x0100" type="Menu">
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup"/>
  <Strings>
    <ButtonText>Sub Menu</ButtonText>
    <CommandName>Sub Menu</CommandName>
  </Strings>
</Menu>
```

#### <a name="commands"></a>Comandos
Um comando que é fornecido ao IDE é definido como um elemento de [botão](../../extensibility/button-element.md) ou um [elemento de combinação](../../extensibility/combo-element.md). Para aparecer em um menu ou em uma barra de ferramentas, o comando deve ter um grupo como seu pai.

##### <a name="buttons"></a>Botões
Os botões são definidos na `Buttons` seção. Qualquer item de menu, botão ou outro elemento em que um usuário clica para executar um único comando é considerado um botão. Alguns tipos de botão também podem incluir a funcionalidade de lista. Os botões têm os mesmos atributos obrigatórios e opcionais que os menus têm, e também podem ter um [elemento Icon](../../extensibility/icon-element.md) que especifica o GUID e a ID do bitmap que representa o botão no IDE. Para obter mais informações sobre os botões e seus atributos, consulte a documentação do [elemento Buttons](../../extensibility/buttons-element.md) .

O botão no exemplo a seguir é um filho do grupo no exemplo anterior e apareceria no IDE como um item de menu no menu pai desse grupo.

```xml
<Button guid="guidTopLevelMenuCmdSet" id="cmdidTestCommand" priority="0x0100" type="Button">
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <Strings>
    <CommandName>cmdidTestCommand</CommandName>
    <ButtonText>Test Command</ButtonText>
  </Strings>
</Button>
```

##### <a name="combos"></a>Combinações de
As combinações são definidas na `Combos` seção. Cada `Combo` elemento representa uma caixa de listagem suspensa no IDE. A caixa de listagem pode ou não ser gravável por usuários, dependendo do valor do `type` atributo da combinação. As combinações têm os mesmos elementos e comportamentos que os botões têm, e também podem ter os seguintes atributos adicionais:

- Um `defaultWidth` atributo que especifica a largura do pixel.

- Um `idCommandList` atributo que especifica uma lista que contém os itens que são exibidos na caixa de listagem. A lista de comandos deve ser declarada no mesmo `GuidSymbol` nó que contém a combinação.

O exemplo a seguir define um elemento de combinação.

```xml
<Combos>
  <Combo guid="guidFirstToolWinCmdSet"
         id="cmdidWindowsMediaFilename"
         priority="0x0100" type="DynamicCombo"
         idCommandList="cmdidWindowsMediaFilenameGetList"
         defaultWidth="130">
    <Parent guid="guidFirstToolWinCmdSet"
            id="ToolbarGroupID" />
    <CommandFlag>IconAndText</CommandFlag>
    <CommandFlag>CommandWellOnly</CommandFlag>
    <CommandFlag>StretchHorizontally</CommandFlag>
    <Strings>
      <CommandName>Filename</CommandName>
      <ButtonText>Enter a Filename</ButtonText>
    </Strings>
  </Combo>
</Combos>
```

##### <a name="bitmaps"></a>Bitmaps
Os comandos que serão exibidos junto com um ícone devem incluir um `Icon` elemento que se refere a um bitmap usando seu GUID e ID. Cada bitmap é definido como um [elemento de bitmap](../../extensibility/bitmap-element.md) na `Bitmaps` seção. Os únicos atributos necessários para uma `Bitmap` definição são `guid` e `href` , que aponta para o arquivo de origem. Se o arquivo de origem for uma faixa de recursos, um atributo **usedlist** também será necessário para listar as imagens disponíveis na faixa. Para obter mais informações, consulte a documentação do [elemento bitmap](../../extensibility/bitmap-element.md) .

### <a name="parenting"></a>Gerenciamento do domínio pai
As regras a seguir regem como um item pode chamar outro item como seu pai.

|Elemento|Definido nesta seção da tabela de comandos|Pode estar contido (como um pai ou por posicionamento na `CommandPlacements` seção, ou ambos)|Pode conter (chamado de pai)|
|-------------| - | - | - |
|Agrupar|[Elemento groups](../../extensibility/groups-element.md), IDE, Other VSPackages|Um menu, um grupo, o próprio item|Menus, grupos e comandos|
|Menu|[Elemento menus](../../extensibility/menus-element.md), IDE, outros VSPackages|1 a *n* grupos|0 a *n* grupos|
|Barra de ferramentas|[Elemento menus](../../extensibility/menus-element.md), IDE, outros VSPackages|O próprio item|0 a *n* grupos|
|Item de menu|[Elemento Buttons](../../extensibility/buttons-element.md), IDE, outros VSPackages|1 a *n* grupos, o próprio item|-0 a *n* grupos|
|Botão|[Elemento Buttons](../../extensibility/buttons-element.md), IDE, outros VSPackages|1 a *n* grupos, o próprio item||
|Combinação|[Elemento de combinação](../../extensibility/combos-element.md), IDE, outros VSPackages|1 a *n* grupos, o próprio item||

### <a name="menu-command-and-group-placement"></a>Posicionamento do menu, do comando e do grupo
Um menu, grupo ou comando pode aparecer em mais de um local no IDE. Para que um item apareça em vários locais, ele deve ser adicionado à `CommandPlacements` seção como um [elemento CommandPlacement](../../extensibility/commandplacement-element.md). Qualquer menu, grupo ou comando pode ser adicionado como um posicionamento de comando. No entanto, as barras de ferramentas não podem ser posicionadas dessa maneira porque não podem aparecer em vários locais sensíveis ao contexto.

Os posicionamentos de comando têm `guid` `id` atributos, e `priority` . O GUID e a ID devem corresponder àqueles do item que está posicionado. O `priority` atributo governa o posicionamento do item em relação a outros itens. Quando o IDE mescla dois ou mais itens que têm a mesma prioridade, seus posicionamentos são indefinidos porque o IDE não garante que os recursos do pacote sejam lidos na mesma ordem toda vez que o pacote for criado.

Se um menu ou grupo aparecer em vários locais, todos os filhos desse menu ou grupo serão exibidos em cada instância.

## <a name="command-visibility-and-context"></a>Visibilidade e contexto de comandos
Quando vários VSPackages são instalados, uma profusão de menus, itens de menu e barras de ferramentas pode obstruir o IDE. Para evitar esse problema, você pode controlar a visibilidade de elementos individuais da interface do usuário usando *restrições de visibilidade* e sinalizadores de comando.

### <a name="visibility-constraints"></a>Restrições de visibilidade
Uma restrição de visibilidade é definida como um [elemento VisibilityItem](../../extensibility/visibilityitem-element.md) na `VisibilityConstraints` seção. Uma restrição de visibilidade define contextos de interface do usuário específicos nos quais o item de destino está visível. Um menu ou comando que está incluído nesta seção é visível somente quando um dos contextos definidos está ativo. Se um menu ou comando não for referenciado nesta seção, ele estará sempre visível por padrão. Esta seção não se aplica a grupos.

`VisibilityItem` os elementos devem ter três atributos, da seguinte maneira: a `guid` e `id` do elemento de interface do usuário de destino e `context` . O `context` atributo especifica quando o item de destino será visível e usa qualquer contexto de interface do usuário válido como seu valor. As constantes de contexto da interface do usuário do Visual Studio são membros da <xref:Microsoft.VisualStudio.VSConstants> classe. Cada `VisibilityItem` elemento pode assumir apenas um valor de contexto. Para aplicar um segundo contexto, crie um segundo `VisibilityItem` elemento que aponte para o mesmo item, conforme mostrado no exemplo a seguir.

```xml
<VisibilityConstraints>
  <VisibilityItem guid="guidSolutionToolbarCmdSet"
        id="cmdidTestCmd"
        context="UICONTEXT_SolutionHasSingleProject" />
  <VisibilityItem guid="guidSolutionToolbarCmdSet"
        id="cmdidTestCmd"
        context="UICONTEXT_SolutionHasMultipleProjects" />
</VisibilityConstraints>
```

### <a name="command-flags"></a>Sinalizadores de comando
Os seguintes sinalizadores de comando podem afetar a visibilidade dos menus e comandos aos quais eles se aplicam.

`AlwaysCreate` O menu é criado mesmo que não tenha grupos ou botões.

Válido para: `Menu`

`CommandWellOnly` Aplique esse sinalizador se o comando não aparecer no menu de nível superior e você desejar disponibilizá-lo para personalização adicional do Shell, por exemplo, associando-o a uma chave. Depois que o VSPackage é instalado, um usuário pode personalizar esses comandos abrindo a caixa de diálogo **Opções** e editando o posicionamento do comando na categoria **ambiente do teclado** . Não afeta o posicionamento em menus de atalho, barras de ferramentas, controladores de menu ou submenus.

Válido para: `Button` , `Combo`

`DefaultDisabled` Por padrão, o comando será desabilitado se o VSPackage que implementa o comando não estiver carregado ou se o método QueryStatus não tiver sido chamado.

Válido para: `Button` , `Combo`

`DefaultInvisible` Por padrão, o comando será invisível se o VSPackage que implementa o comando não estiver carregado ou se o método QueryStatus não tiver sido chamado.

Deve ser combinado com o `DynamicVisibility` sinalizador.

Válido para: `Button` , `Combo` , `Menu`

`DynamicVisibility` A visibilidade do comando pode ser alterada usando o `QueryStatus` método ou um GUID de contexto que é incluído na `VisibilityConstraints` seção.

Aplica-se a comandos que aparecem em menus, não em barras de ferramentas. Itens de barra de ferramentas de nível superior podem ser desabilitados, mas não ocultos, quando o `OLECMDF_INVISIBLE` sinalizador é retornado do `QueryStatus` método.

Em um menu, esse sinalizador também indica que ele deve ser ocultado automaticamente quando seus membros estiverem ocultos. Esse sinalizador é normalmente atribuído a submenus porque os menus de nível superior já têm esse comportamento.

Deve ser combinado com o `DefaultInvisible` sinalizador.

Válido para: `Button` , `Combo` , `Menu`

`NoShowOnMenuController` Se um comando que tem esse sinalizador estiver posicionado em um controlador de menu, o comando não aparecerá na lista suspensa.

Válido para: `Button`

Para obter mais informações sobre sinalizadores de comando, consulte a documentação do [elemento CommandFlag](../../extensibility/command-flag-element.md) .

#### <a name="general-requirements"></a>Requisitos gerais
O comando deve passar a seguinte série de testes antes que ele possa ser exibido e habilitado:

- O comando está posicionado corretamente.

- O `DefaultInvisible` sinalizador não está definido.

- O menu pai ou a barra de ferramentas está visível.

- O comando não é invisível devido a uma entrada de contexto na seção do [elemento VisibilityConstraints](../../extensibility/visibilityconstraints-element.md) .

- O código VSPackage que implementa a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface exibe e habilita o comando. Nenhum código de interface interceptou e atuou.

- Quando um usuário clica no comando, ele se torna sujeito ao procedimento descrito no [algoritmo de roteamento](../../extensibility/internals/command-routing-algorithm.md).

## <a name="call-pre-defined-commands"></a>Chamar comandos predefinidos
O [elemento UsedCommands](../../extensibility/usedcommands-element.md) permite que o VSPackages acesse comandos que são fornecidos por outros VSPackages ou pelo IDE. Para fazer isso, crie um [elemento UsedCommand](../../extensibility/usedcommand-element.md) que tenha o GUID e a ID do comando a ser usado. Isso garante que o comando será carregado pelo Visual Studio, mesmo que ele não faça parte da configuração atual do Visual Studio. Para obter mais informações, consulte [elemento UsedCommand](../../extensibility/usedcommand-element.md).

## <a name="interface-element-appearance"></a>Aparência do elemento de interface
As considerações para selecionar e posicionar elementos de comando são as seguintes:

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] oferece muitos elementos de interface do usuário que aparecem de maneira diferente, dependendo do posicionamento.

- Um elemento de interface do usuário que é definido usando o `DefaultInvisible` sinalizador não será exibido no IDE, a menos que seja exibido por sua implementação VSPackage do <xref:EnvDTE.IDTCommandTarget.QueryStatus%2A> método ou associado a um contexto de interface do usuário específico na `VisibilityConstraints` seção.

- Até mesmo um comando posicionado com êxito não pode ser exibido. Isso ocorre porque o IDE oculta ou exibe alguns comandos automaticamente, dependendo das interfaces que o VSPackage tem (ou não) implementado. Por exemplo, a implementação de algumas interfaces de compilação de um VSPackage faz com que itens de menu relacionados à compilação sejam mostrados automaticamente.

- A aplicação do `CommandWellOnly` sinalizador na definição do elemento de interface do usuário significa que o comando pode ser adicionado somente pela personalização.

- Os comandos podem estar disponíveis apenas em determinados contextos da interface do usuário, por exemplo, somente quando uma caixa de diálogo é exibida quando o IDE está no modo de design.

- Para fazer com que determinados elementos da interface do usuário sejam exibidos no IDE, você deve implementar uma ou mais interfaces ou escrever algum código.

## <a name="see-also"></a>Confira também
- [Estender menus e comandos](../../extensibility/extending-menus-and-commands.md)
