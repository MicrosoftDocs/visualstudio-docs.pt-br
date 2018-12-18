---
title: Como os VSPackages adicionam elementos da Interface do usuário | Microsoft Docs
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
- user interfaces, adding elements
- UI element design [Visual Studio SDK], VSPackages
- VSPackages, contributing UI elements
ms.assetid: abc5d9d9-b267-48a1-92ad-75fbf2f4c1b9
caps.latest.revision: 61
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 88b1a71964ddae67241025dd32c1a1384c79765f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51753367"
---
# <a name="how-vspackages-add-user-interface-elements"></a>Como os VSPackages adicionam elementos da interface do usuário
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um VSPackage pode adicionar elementos interface do usuário (IU), por exemplo, menus, barras de ferramentas e das janelas, para o Visual Studio por meio do arquivo. VSCT.  
  
 Você pode encontrar diretrizes de design para elementos de interface do usuário no [diretrizes de experiência de usuário do Visual Studio](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md).  
  
## <a name="the-visual-studio-command-table-architecture"></a>A arquitetura de tabela de comando do Visual Studio  
 Conforme observado, a arquitetura de tabela do comando dá suporte aos princípios de arquitetura acima. Os princípios por trás de abstrações, estruturas de dados e ferramentas da arquitetura de tabela do comando são da seguinte maneira:  
  
-   Há três tipos básicos de itens: menus, comandos e grupos. Menus podem ser expostos na interface do usuário como menus, submenus, barras de ferramentas ou janelas de ferramentas. Comandos são procedimentos que o usuário pode executar no IDE, e eles podem ser expostos como itens de menu, botões, caixas de listagem ou outros controles. Grupos são contêineres para os menus e comandos.  
  
-   Cada item é especificado por uma definição que descreve o item, sua prioridade em relação a outros itens e os sinalizadores de modificam seu comportamento.  
  
-   Cada item tem um posicionamento que descreve o pai do item. Um item pode ter vários pais, para que ele pode aparecer em vários locais na interface do usuário.  
  
     Todos os comandos devem ter um grupo como pai, mesmo se ele for o único filho desse grupo. Cada menu padrão também deve ter um grupo pai. Barras de ferramentas e janelas de ferramenta atuam como suas próprias pais. Um grupo pode ter como seu pai, a barra de menus principal do Visual Studio, ou qualquer menu, barra de ferramentas ou janela de ferramentas.  
  
### <a name="how-items-are-defined"></a>Como os itens são definidos  
 . VSCT arquivos são formatados em XML. Um arquivo. VSCT define os elementos de interface do usuário para um pacote e determina qual esses elementos são exibidos no IDE. Cada menu, um grupo ou um comando no pacote é atribuído pela primeira vez um GUID e ID no `Symbols` seção. Durante o resto da. VSCT arquivo, cada menu, o comando e o grupo é identificado por sua combinação de GUID e ID. O exemplo a seguir mostra um típico `Symbols` seção gerada pelo modelo de pacote do Visual Studio quando um **comando de Menu** está selecionado no modelo.  
  
```xml  
<Symbols>  
  <!-- This is the package guid. -->  
  <GuidSymbol name="guidMenuTextPkg" value="{b1253bc6-d266-402b-89e7-5e3d3b22c746}" />  
  
  <!-- This is the guid used to group the menu commands together -->  
  <GuidSymbol name="guidMenuTextCmdSet" value="{a633d4e4-6c65-4436-a138-1abeba7c9a69}">  
  
    <IDSymbol name="MyMenuGroup" value="0x1020" />  
    <IDSymbol name="cmdidMyCommand" value="0x0100" />  
  </GuidSymbol>  
  
  <GuidSymbol name="guidImages" value="{53323d9a-972d-4671-bb5b-9e418480922f}" >  
    <IDSymbol name="bmpPic1" value="1" />  
    <IDSymbol name="bmpPic2" value="2" />  
    <IDSymbol name="bmpPicSearch" value="3" />  
    <IDSymbol name="bmpPicX" value="4" />  
    <IDSymbol name="bmpPicArrows" value="5" />  
  </GuidSymbol>  
</Symbols>  
```  
  
 O elemento de nível superior a `Symbols` seção é o [elemento GuidSymbol](../../extensibility/guidsymbol-element.md). `GuidSymbol` elementos mapeiam nomes de GUIDs que são usados pelo IDE para identificar os pacotes e suas partes do componente.  
  
> [!NOTE]
>  GUIDs são gerados automaticamente pelo modelo de pacote do Visual Studio. Você também pode criar um GUID exclusivo clicando **criar GUID** sobre o **ferramentas** menu.  
  
 A primeira `GuidSymbol` elemento, "guid [PackageName] Pkg", é o GUID do pacote em si. Esse é o GUID que é usado pelo Visual Studio para carregar o pacote. Normalmente, ele não tem elementos filho.  
  
 Por convenção, os menus e comandos são agrupados em um segundo `GuidSymbol` elemento, "guid [PackageName] CmdSet", e bitmaps estão em um terceiro `GuidSymbol` elemento, "guidImages". Você não precisa seguir essa convenção, mas cada menu, o grupo, o comando e o bitmap devem ser um filho de um `GuidSymbol` elemento.  
  
 Na segunda `GuidSymbol` elemento, que representa o conjunto de comandos do pacote, são várias `IDSymbol` elementos. Cada [elemento IDSymbol](../../extensibility/idsymbol-element.md) mapeia um nome para um valor numérico e pode representar um menu, um grupo ou um comando que faz parte do conjunto de comandos. O `IDSymbol` elementos no terceiro `GuidSymbol` elemento representam bitmaps que podem ser usados como ícones para comandos. Porque os pares de ID do GUID devem ser exclusivos em um aplicativo, não há dois filhos do mesmo `GuidSymbol` elemento pode ter o mesmo valor.  
  
### <a name="menus-groups-and-commands"></a>Menus, grupos e comandos  
 Quando um menu, o grupo ou o comando tem um GUID e ID, podem ser adicionado ao IDE. Todos os elementos da interface do usuário devem ter o seguinte:  
  
-   Um `guid` que corresponde ao nome do atributo a `GuidSymbol` elemento que o elemento de interface do usuário é definido em.  
  
-   Uma `id` atributo que corresponde ao nome do associado `IDSymbol` elemento.  
  
     Juntos, o `guid` e `id` compõem atributos a *assinatura* do elemento de interface do usuário.  
  
-   Um `priority` que determina o posicionamento do elemento da interface do usuário no seu menu pai ou o grupo de atributo.  
  
-   Um [elemento pai](../../extensibility/parent-element.md) que tem `guid` e `id` atributos que especificam a assinatura do menu pai ou do grupo.  
  
#### <a name="menus"></a>Menus  
 Cada menu é definida como uma [elemento Menu](../../extensibility/menu-element.md) no `Menus` seção. Menus devem ter `guid`, `id`, e `priority` atributos e um `Parent` elemento e também os seguintes atributos adicionais e filhos:  
  
- Um `type` atributo que especifica se o menu deve aparecer no IDE, como um tipo de menu ou uma barra de ferramentas.  
  
- Um [elemento Strings](../../extensibility/strings-element.md) que contém uma [elemento ButtonText](../../extensibility/buttontext-element.md), que especifica o título de menu no IDE e uma [elemento CommandName](../../extensibility/commandname-element.md), que especifica o nome que é usado na **comando** janela para acessar o menu.  
  
- Sinalizadores opcionais. Um [elemento Command Flag](../../extensibility/command-flag-element.md) pode aparecer em uma definição de menu para alterar sua aparência ou comportamento no IDE.  
  
  Cada `Menu` elemento deve ter um grupo como pai, a menos que ele seja um elemento encaixável como uma barra de ferramentas. Um menu encaixável é seu próprio pai. Para obter mais informações sobre menus e valores para o `type` atributo, consulte a [elemento Menu](../../extensibility/menu-element.md) documentação.  
  
  O exemplo a seguir mostra um menu que aparece na barra de menus do Visual Studio, ao lado de **ferramentas** menu.  
  
```xml  
<Menu guid="guidTopLevelMenuCmdSet"  
id="TopLevelMenu" priority="0x700" type="Menu">  
  <Parent guid="guidSHLMainMenu"  
          id="IDG_VS_MM_TOOLSADDINS" />  
  <Strings>  
    <ButtonText>TestMenu</ButtonText>  
    <CommandName>TestMenu</CommandName>  
  </Strings>  
</Menu>  
```  
  
#### <a name="groups"></a>Grupos  
 Um grupo é um item que é definido no `Groups` seção do arquivo. VSCT. Os grupos são apenas contêineres. Eles não aparecem no IDE, exceto como uma linha divisória em um menu. Portanto, uma [elemento Group](../../extensibility/group-element.md) é definida somente por sua assinatura, a prioridade e o pai.  
  
 Um grupo pode ter um menu, outro grupo ou em si como pai. No entanto, o pai é normalmente um menu ou barra de ferramentas. No menu do exemplo anterior é um filho do `IDG_VS_MM_TOOLSADDINS` grupo e esse grupo é um filho da barra de menus do Visual Studio. O grupo no exemplo a seguir é um filho do menu no exemplo anterior.  
  
```  
 <Group guid="guidTopLevelMenuCmdSet" id="MyMenuGroup"  
priority="0x0600">  
   <Parent guid="guidTopLevelMenuCmdSet" id="TopLevelMenu"/>  
 </Group>  
```  
  
 Porque ele faz parte de um menu, este grupo seria normalmente contêm comandos. No entanto, ele também pode conter outros menus. Isso é como submenus são definidas, conforme mostrado no exemplo a seguir.  
  
```xml  
<Menu guid="guidTopLevelMenuCmdSet" id="SubMenu"  
priority="0x0100" type="Menu">  
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup"/>  
  <Strings>  
    <ButtonText>Sub Menu</ButtonText>  
    <CommandName>Sub Menu</CommandName>  
  </Strings>  
</Menu>  
```  
  
#### <a name="commands"></a>Comandos  
 Um comando que é fornecido para o IDE é definido como um [elemento Button](../../extensibility/button-element.md) ou um [elemento Combo](../../extensibility/combo-element.md). Para aparecer em um menu ou uma barra de ferramentas, o comando deve ter um grupo como pai.  
  
##### <a name="buttons"></a>Botões  
 Botões são definidos na `Buttons` seção. Qualquer item de menu, botão ou outro elemento que um usuário clica para executar um comando único é considerado um botão. Alguns tipos de botão também podem incluir a funcionalidade de lista. Botões têm o mesmo necessárias e os atributos opcionais que têm menus, e também pode ter um [ícone do elemento](../../extensibility/icon-element.md) que especifica o GUID e a ID do bitmap que representa o botão no IDE. Para obter mais informações sobre botões e seus atributos, consulte o [elemento Buttons](../../extensibility/buttons-element.md) documentação.  
  
 O botão no exemplo a seguir é um filho do grupo no exemplo anterior e apareceria no IDE, como um item de menu no menu pai desse grupo.  
  
```  
<Button guid="guidTopLevelMenuCmdSet" id="cmdidTestCommand" priority="0x0100" type="Button">  
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" />  
  <Icon guid="guidImages" id="bmpPic1" />  
  <Strings>  
    <CommandName>cmdidTestCommand</CommandName>  
    <ButtonText>Test Command</ButtonText>  
  </Strings>  
</Button>  
```  
  
##### <a name="combos"></a>Combos  
 Combos são definidos na `Combos` seção. Cada `Combo` elemento representa uma caixa de lista suspensa no IDE. A caixa de listagem pode ou não ser gravável por usuários, dependendo do valor da `type` atributo da caixa de combinação. Combos têm os mesmos elementos e o comportamento que os botões e também pode ter os seguintes atributos adicionais:  
  
- Um `defaultWidth` atributo que especifica a largura em pixels.  
  
- Um `idCommandList` atributo que especifica uma lista que contém os itens que são exibidos na caixa de listagem. A lista de comandos deve ser declarada no mesmo `GuidSymbol` nó que contém a caixa de combinação.  
  
  O exemplo a seguir define um elemento de caixa de combinação.  
  
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
 Comandos que serão exibidos junto com um ícone devem incluir um `Icon` elemento que se refere a um bitmap usando seu GUID e ID. Cada bitmap é definido como um [elemento Bitmap](../../extensibility/bitmap-element.md) no `Bitmaps` seção. O único necessário atributos para um `Bitmap` definição são `guid` e `href`, que aponta para o arquivo de origem. Se o arquivo de origem for uma faixa de recursos, uma **usedList** atributo também é necessário, para listar as imagens disponíveis na faixa de. Para obter mais informações, consulte o [elemento Bitmap](../../extensibility/bitmap-element.md) documentação.  
  
### <a name="parenting"></a>Gerenciamento do domínio pai  
 As seguintes regras regem como um item pode chamar outro item como seu pai.  
  
|Elemento|Definidas nesta seção da tabela de comando|Pode estar contido (como um pai ou posicionamento no `CommandPlacements` seção ou ambos)|Pode conter (conhecido como um pai)|  
|-------------|--------------------------------------------------|---------------------------------------------------------------------------------------------------|---------------------------------------------|  
|Group|[Elemento Groups](../../extensibility/groups-element.md), o IDE, outros VSPackages|Um menu, um grupo, o próprio item|Menus, grupos e comandos|  
|Menu|[Elemento menus](../../extensibility/menus-element.md), o IDE, outros VSPackages|1 para *n* grupos|0 para *n* grupos|  
|Barra de ferramentas|[Elemento menus](../../extensibility/menus-element.md), o IDE, outros VSPackages|O próprio item|0 para *n* grupos|  
|Item de menu|[Botões elemento](../../extensibility/buttons-element.md), o IDE, outros VSPackages|1 para *n* grupos, o próprio item|-0 para *n* grupos|  
|Botão|[Botões elemento](../../extensibility/buttons-element.md), o IDE, outros VSPackages|1 para *n* grupos, o próprio item||  
|Caixa de combinação|[Elemento combos](../../extensibility/combos-element.md), o IDE, outros VSPackages|1 para *n* grupos, o próprio item||  
  
### <a name="menu-command-and-group-placement"></a>Menu, o comando e o posicionamento do grupo  
 Um menu, um grupo ou um comando pode aparecer em mais de um local no IDE. Para um item seja exibido em vários locais, ele deve ser adicionado para o `CommandPlacements` seção como um [elemento CommandPlacement](../../extensibility/commandplacement-element.md). Qualquer menu, um grupo ou um comando pode ser adicionado como um posicionamento do comando. No entanto, as barras de ferramentas não podem ser posicionadas dessa maneira porque eles não podem aparecer em vários locais sensível ao contexto.  
  
 Posicionamentos de comandos têm `guid`, `id`, e `priority` atributos. O GUID e a ID devem corresponder do item que está posicionado. O `priority` atributo controla o posicionamento do item em relação a outros itens. Quando o IDE mescla dois ou mais itens que têm a mesma prioridade, seus posicionamentos serão indefinidos, porque o IDE não garante que os recursos de pacote são lidas na mesma ordem toda vez que o pacote é compilado.  
  
 Se um menu ou o grupo é exibido em vários locais, todos os filhos desse menu ou o grupo serão exibido em cada instância.  
  
## <a name="command-visibility-and-context"></a>Visibilidade de comando e contexto  
 Quando vários VSPackages forem instalados, uma profusão de menus, itens de menu e barras de ferramentas pode sobrecarregar o IDE. Para evitar esse problema, você pode controlar a visibilidade de elementos de interface do usuário individuais usando *restrições de visibilidade* e sinalizadores de comando.  
  
##### <a name="visibility-constraints"></a>Restrições de visibilidade  
 Uma restrição de visibilidade está definida como uma [elemento VisibilityItem](../../extensibility/visibilityitem-element.md) no `VisibilityConstraints` seção. Uma restrição de visibilidade define contextos de interface do usuário específicos em que o item de destino está visível. Um menu ou um comando que está incluído nesta seção só é visível quando um dos contextos definidos está ativo. Se um menu ou um comando não é referenciado nesta seção, está sempre visível por padrão. Esta seção não se aplica a grupos.  
  
 `VisibilityItem` elementos devem ter três atributos, da seguinte maneira: o `guid` e `id` do elemento de interface do usuário de destino, e `context`. O `context` atributo especifica quando o item de destino estarão visível e utiliza qualquer contexto de interface de usuário válido como seu valor. As constantes de contexto da interface do usuário para o Visual Studio são membros do <xref:Microsoft.VisualStudio.VSConstants> classe. Cada `VisibilityItem` elemento pode ter o valor de apenas um contexto. Para aplicar um contexto de segundo, crie um segundo `VisibilityItem` elemento que aponta para o mesmo item, conforme mostrado no exemplo a seguir.  
  
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
  
##### <a name="command-flags"></a>Sinalizadores de comando  
 Os sinalizadores de comando a seguir podem afetar a visibilidade dos menus e comandos que eles se aplicam ao.  
  
 AlwaysCreate  
 Menu é criado, mesmo se ele não possui grupos ou botões.  
  
 Válido para: `Menu`  
  
 CommandWellOnly  
 Aplica esse sinalizador se o comando não aparecer no menu de nível superior e você deseja disponibilizar para personalização adicional de shell, por exemplo, associação a uma chave. Depois de instalar o VSPackage, um usuário pode personalizar esses comandos, abrindo o **opções** caixa de diálogo e, em seguida, editando o posicionamento do comando sob o **teclado ambiente** categoria. Não afeta o posicionamento em menus de atalho, barras de ferramentas, os controladores de menu ou submenus.  
  
 Válido para: `Button`, `Combo`  
  
 DefaultDisabled  
 Por padrão, o comando está desabilitado se o VSPackage que implementa o comando não está carregado ou o método QueryStatus não foi chamado.  
  
 Válido para: `Button`, `Combo`  
  
 DefaultInvisible  
 Por padrão, o comando é invisível se o VSPackage que implementa o comando não está carregado ou o método QueryStatus não foi chamado.  
  
 Deve ser combinado com o `DynamicVisibility` sinalizador.  
  
 Válido para: `Button`, `Combo`, `Menu`  
  
 DynamicVisibility  
 A visibilidade do comando pode ser alterada por meio do método QueryStatus ou um GUID que é incluído no contexto de `VisibilityConstraints` seção.  
  
 Aplica-se aos comandos que aparecem nos menus, não em barras de ferramentas. Itens de nível superior da barra de ferramentas podem ser desabilitados, mas não ocultas, quando o sinalizador OLECMDF_INVISIBLE é retornado do método QueryStatus.  
  
 Em um menu, esse sinalizador indica também que ele deve ser automaticamente ocultado quando seus membros estão ocultos. Esse sinalizador normalmente é atribuído à submenus como menus de nível superior já têm esse comportamento.  
  
 Deve ser combinado com o `DefaultInvisible` sinalizador.  
  
 Válido para: `Button`, `Combo`, `Menu`  
  
 NoShowOnMenuController  
 Se um comando que tem esse sinalizador estiver posicionado em um controlador de menu, o comando não aparecer na lista suspensa.  
  
 Válido para: `Button`  
  
 Para obter mais informações sobre os sinalizadores de comando, consulte o [elemento Command Flag](../../extensibility/command-flag-element.md) documentação.  
  
##### <a name="general-requirements"></a>Requisitos gerais  
 O comando deve passar a seguinte série de testes antes de ser exibido e habilitado:  
  
-   O comando é posicionado corretamente.  
  
-   O `DefaultInvisible` sinalizador não estiver definido.  
  
-   Barra de ferramentas ou menu pai está visível.  
  
-   O comando não é invisível devido a uma entrada de contexto na [Element Visibilityconstraints](../../extensibility/visibilityconstraints-element.md) seção.  
  
-   Código de VSPackage que implementa o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface Exibe e permite que seu comando. Nenhum código de interface interceptamos e foi agiu sobre ele.  
  
-   Quando um usuário clica em seu comando, ele fique sujeita ao procedimento descrito em [algoritmo de roteamento](../../extensibility/internals/command-routing-algorithm.md).  
  
## <a name="calling-pre-defined-commands"></a>Comandos predefinidos de chamada  
 O [elemento UsedCommands](../../extensibility/usedcommands-element.md) permite que os VSPackages para acessar os comandos que são fornecidos por outros VSPackages ou pelo IDE. Para fazer isso, crie uma [elemento UsedCommand](../../extensibility/usedcommand-element.md) que tem o GUID e a ID do comando para usar. Isso garante que o comando será carregado pelo Visual Studio, mesmo se ele não é parte da configuração atual do Visual Studio. Para obter mais informações, consulte [elemento UsedCommand](../../extensibility/usedcommand-element.md).  
  
## <a name="interface-element-appearance"></a>Aparência do elemento de interface  
 Considerações para selecionar e posicionar os elementos de comando são da seguinte maneira:  
  
-   [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] oferece muitos elementos de interface do usuário que aparecem de forma diferente dependendo do posicionamento.  
  
-   Um elemento de interface do usuário que é definido usando o `DefaultInvisible` sinalizador não será exibido no IDE, a menos que ele seja exibido por sua implementação de VSPackage do <xref:EnvDTE.IDTCommandTarget.QueryStatus%2A> método, ou associado a um determinado contexto de interface do usuário no `VisibilityConstraints` seção.  
  
-   Não pode ser exibido até mesmo um comando posicionado com êxito. Isso é porque o IDE automaticamente oculta ou exibe alguns comandos, dependendo das interfaces que o VSPackage (ou não) implementado. Por exemplo, a implementação de um VSPackage de alguns criar interfaces de itens de menu relacionados à compilação de faz com que a ser mostrado automaticamente.  
  
-   Aplicando o `CommandWellOnly` sinalizador na definição de elemento de interface do usuário significa que o comando possa ser adicionado somente por personalização.  
  
-   Comandos podem estar disponíveis apenas em determinados contextos de interface do usuário, por exemplo, somente quando uma caixa de diálogo é exibida quando o IDE está no modo de exibição de design.  
  
-   Para fazer com que determinados elementos de interface do usuário a ser exibido no IDE, você deve implementar uma ou mais interfaces ou escrever um código.  
  
## <a name="see-also"></a>Consulte também  
 [Ampliar menus e comandos](../../extensibility/extending-menus-and-commands.md)

