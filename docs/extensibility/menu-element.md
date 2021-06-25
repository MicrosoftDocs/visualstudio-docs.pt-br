---
title: Elemento Menu | Microsoft Docs
description: O elemento Menu define um item de menu. Os tipos de menu são Context, Menu, MenuController, MenuControllerLatched, Toolbar e ToolWindowToolbar.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Menus
- Menus element (VSCT XML schema)
ms.assetid: ce0560f3-b4c9-4ab2-a99c-d4e10f37b9e0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a2ffa029dd05e7fe3d32a9df4a1d06c90c8b9c6b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901533"
---
# <a name="menu-element"></a>Elemento Menu
Define um item de menu. Esses são os seis tipos de menus: Context, Menu, MenuController, MenuControllerLatched, Toolbar e ToolWindowToolbar.

## <a name="syntax"></a>Sintaxe

```xml
<Menu guid="guidMyCommandSet" id="MyCommand" priority="0x100" type="button">
  <Parent>... </Parent>
  <CommandFlag>... </CommandFlag>
  <Strings>... </Strings>
</Menu>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|guid|Obrigatórios. GUID do identificador de comando GUID/ID.|
|id|Obrigatórios. ID do identificador de comando GUID/ID.|
|priority|Opcional. Um valor numérico que especifica a posição relativa de um menu em um grupo de menus.|
|ToolbarPriorityInBand|Opcional. Um valor numérico que especifica a posição relativa de uma barra de ferramentas em uma banda quando a janela é encaixada.|
|tipo|Opcional. Um valor enumerado que especifica o tipo de elemento.<br /><br /> Se não estiver presente, o tipo padrão será Menu.<br /><br /> Contexto<br /> Um menu de atalho que é mostrado quando um usuário clica com o botão direito do mouse em uma janela. Um menu de atalho tem as seguintes características:<br /><br /> - Não usa os **campos Pai** e **Prioridade** quando o menu deve ser exibido como um menu de atalho.<br />- Pode ser usado como um submenu e também como um menu de atalho. Nesse caso, os campos **ID do** Grupo e **Prioridade** são respeitados.<br />- Nem sempre está disponível.<br /><br /> Um menu de atalho é exibido somente quando as seguintes condições são verdadeiras:<br /><br /> - A janela que a hospeda é exibida.<br />– Um manipulador de mouse no VSPackage detecta um clique com o botão direito do mouse na janela e, em seguida, chama um método que trata o comando.<br />– O menu de atalho é exibido chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager.ShowContextMenu%2A> método (a abordagem recomendada) ou o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A> método .<br /><br /> Menu<br /> Fornece um menu suspenso. Um menu suspenso tem as seguintes características:<br /><br /> – respeita o Pai em sua definição.<br />- Deve ter um grupo Pai ou um CommandPlacement para um grupo.<br />– Pode ser um submenu em qualquer outro tipo de menu.<br />- É exibido automaticamente sempre que seu menu pai é exibido.<br />- Não exige a implementação de nenhum código VSPackage para torná-lo exibido.<br /><br /> MenuController<br /> Fornece um menu suspenso de botão dividido, que normalmente é usado em barras de ferramentas. Um menu MenuController tem as seguintes características:<br /><br /> - Deve estar contido em outro menu por meio de Parent ou CommandPlacement.<br />– respeita o Pai em sua definição.<br />- Pode ter qualquer tipo de menu como seu pai.<br />– É disponibilizado automaticamente sempre que seu menu pai é exibido.<br />- Não requer suporte programático para tornar o menu exibido.<br /><br /> Um comando do menu de botão dividido é exibido no botão de menu. O comando exibido tem uma das seguintes características:<br /><br /> - É o último comando que foi usado se o comando ainda for exibido e habilitado.<br />- É o primeiro comando exibido.<br /><br /> MenuControllerLatched<br /> Fornece um menu suspenso de botão dividido para o qual um comando pode ser especificado como a seleção padrão marcando o comando como travado.<br /><br /> Um comando travado é um comando marcado no menu como selecionado, normalmente exibindo uma marca de seleção. Um comando poderá ser marcado como travado se tiver o sinalizador OLECMDF_LATCHED definido em uma implementação do `QueryStatus` método da <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface . Um menu MenuControllerLatched tem as seguintes características:<br /><br /> - Deve estar contido em outro menu por meio de um grupo pai ou CommandPlacement.<br />– respeita o Pai em sua definição.<br />- Pode ter qualquer tipo de menu como seu pai.<br />- É disponibilizado sempre que seu menu pai é exibido.<br />- Não requer suporte programático para tornar o menu exibido.<br /><br /> Um comando do menu de botão dividido é exibido no botão de menu. O comando exibido tem uma das seguintes características:<br /><br /> – É o primeiro comando exibido que está travado.<br />- É o primeiro comando exibido.<br /><br /> Barra de ferramentas<br /> Fornece uma barra de ferramentas. Uma barra de ferramentas tem as seguintes características:<br /><br /> – ignora o Pai em sua definição.<br />- Não pode ser feito um submenu de nenhum grupo, nem mesmo usando CommandPlacement.<br />- Sempre é possível exibir clicando em Barras **de Ferramentas** **no** menu Exibir.<br />- Pode ser exibido usando um [VisibilityItem](../extensibility/visibilityitem-element.md).<br />- Não requer nenhum código para criar. Para ver um exemplo de como criar uma barra de ferramentas, consulte [Adicionar uma barra de ferramentas](../extensibility/adding-a-toolbar.md).<br /><br /> ToolWindowToolbar<br /> Fornece uma barra de ferramentas anexada a uma janela de ferramentas específica, assim como uma barra de ferramentas é anexada ao ambiente de desenvolvimento.<br /><br /> – ignora o Pai em sua definição.<br />- Não pode ser feito um submenu de nenhum grupo, nem mesmo usando CommandPlacement.<br />– É exibido somente quando a janela de ferramentas que hospeda a barra de ferramentas é exibida e o VSPackage adiciona explicitamente a barra de ferramentas à janela de ferramentas. Isso normalmente é feito quando a janela de ferramentas é criada obtendo a propriedade do host da barra de ferramentas (conforme representado pela interface) do quadro da janela de ferramentas e, em seguida, chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost> o <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost.AddToolbar%2A> método .|
|Condição|Opcional. Consulte [Atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|Pai|Opcional. O elemento pai do item de menu.|
|CommandFlag|Obrigatórios. Consulte [Elemento de sinalizador de comando](../extensibility/command-flag-element.md). Os valores de CommandFlag válidos para um Menu são os itens a seguir:<br /><br /> -   **Alwayscreate**<br />-   **DefaultDocked**<br />-   **DefaultInvisible** – esse sinalizador não afeta a exibição de barras de ferramentas.<br />-   **DontCache**<br />-   **DynamicVisibility** – esse sinalizador não afeta a exibição de barras de ferramentas.<br />-   **IconAndText**<br />-   **NoCustomize**<br />-   **NotInTBList**<br />-   **NoToolbarClose**<br />-   **TextChanges**<br />-   **TextIsAnchorCommand**|
|Cadeias de caracteres|Obrigatórios. Consulte [o elemento Strings](../extensibility/strings-element.md). O elemento `ButtonText` filho deve ser definido.|
|Annotation|Comentário opcional.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento Menus](../extensibility/menus-element.md)|Define todos os menus que um VSPackage implementa.|

## <a name="example"></a>Exemplo

```
<Menu guid="cmdGuidWidgetCommands" id="menuIDEditWidget"
  priority="0x0002" type="Menu">
  <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit"/>
  <CommandFlag>AlwaysCreate</CommandFlag>
  <Strings>
    <ButtonText>Edit Widget</ButtonText>
  </Strings>
</Menu>
```

## <a name="see-also"></a>Confira também
- [Visual Studio arquivos da tabela de comandos (.vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
