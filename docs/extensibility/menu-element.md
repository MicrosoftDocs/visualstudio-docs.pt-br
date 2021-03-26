---
title: Elemento de menu | Microsoft Docs
description: O elemento menu define um item de menu. Os tipos de menu são Context, menu, MenuController, MenuControllerLatched, Toolbar e ToolWindowToolbar.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Menus
- Menus element (VSCT XML schema)
ms.assetid: ce0560f3-b4c9-4ab2-a99c-d4e10f37b9e0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7427b826249bd29c73c928630eed0941c57b997d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064040"
---
# <a name="menu-element"></a>Elemento de menu
Define um item de menu. Esses são os seis tipos de menus: contexto, menu, MenuController, MenuControllerLatched, barra de ferramentas e ToolWindowToolbar.

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
|id|Obrigatórios. ID do identificador de comando de GUID/ID.|
|priority|Opcional. Um valor numérico que especifica a posição relativa de um menu em um grupo de menus.|
|ToolbarPriorityInBand|Opcional. Um valor numérico que especifica a posição relativa de uma barra de ferramentas em uma banda quando a janela é encaixada.|
|tipo|Opcional. Um valor enumerado que especifica o tipo de elemento.<br /><br /> Se não estiver presente, o tipo padrão é menu.<br /><br /> Contexto<br /> Um menu de atalho que é mostrado quando um usuário clica com o botão direito do mouse em uma janela. Um menu de atalho tem as seguintes características:<br /><br /> -Não usa os campos **pai** e **prioridade** quando o menu é exibido como um menu de atalho.<br />-Pode ser usado como um submenu e também como um menu de atalho. Nesse caso, os campos **ID do grupo** e **prioridade** são respeitados.<br />-Nem sempre está disponível.<br /><br /> Um menu de atalho é exibido somente quando as seguintes condições são verdadeiras:<br /><br /> -A janela que hospeda ela é exibida.<br />-Um manipulador de mouse no VSPackage detecta um clique com o botão direito do mouse na janela e, em seguida, chama um método que manipula o comando.<br />-O menu de atalho é exibido chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager.ShowContextMenu%2A> método (a abordagem recomendada) ou o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A> método.<br /><br /> Menu<br /> Fornece um menu suspenso. Um menu suspenso tem as seguintes características:<br /><br /> -Respeita o pai em sua definição.<br />-Deve ter um grupo pai ou um CommandPlacement para um grupo.<br />-Pode ser um submenu em qualquer outro tipo de menu.<br />-É exibido automaticamente sempre que seu menu pai é exibido.<br />-Não requer a implementação de nenhum código VSPackage para torná-lo exibido.<br /><br /> MenuController<br /> Fornece um menu suspenso de botão de divisão, que é normalmente usado em barras de ferramentas. Um menu MenuController tem as seguintes características:<br /><br /> -Deve estar contido em outro menu por meio de pai ou CommandPlacement.<br />-Respeita o pai em sua definição.<br />-Pode ter qualquer tipo de menu como seu pai.<br />-É disponibilizado automaticamente sempre que seu menu pai é exibido.<br />-Não requer suporte programático para fazer com que o menu seja exibido.<br /><br /> Um comando do menu de botão de divisão é exibido no botão de menu. O comando exibido tem uma das seguintes características:<br /><br /> -É o último comando que foi usado se o comando ainda for exibido e habilitado.<br />-É o primeiro comando exibido.<br /><br /> MenuControllerLatched<br /> Fornece um menu suspenso de botão de divisão para o qual um comando pode ser especificado como a seleção padrão marcando o comando como travado.<br /><br /> Um comando travado é um comando que é marcado no menu como selecionado, normalmente exibindo uma marca de seleção. Um comando pode ser marcado como travado se tiver o sinalizador OLECMDF_LATCHED definido nele em uma implementação do `QueryStatus` método da <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface. Um menu MenuControllerLatched tem as seguintes características:<br /><br /> -Deve estar contido em outro menu por meio de um grupo pai ou CommandPlacement.<br />-Respeita o pai em sua definição.<br />-Pode ter qualquer tipo de menu como seu pai.<br />-É disponibilizado sempre que seu menu pai é exibido.<br />-Não requer suporte programático para fazer com que o menu seja exibido.<br /><br /> Um comando do menu de botão de divisão é exibido no botão de menu. O comando exibido tem uma das seguintes características:<br /><br /> -É o primeiro comando exibido que é travado.<br />-É o primeiro comando exibido.<br /><br /> Barra de ferramentas<br /> Fornece uma barra de ferramentas. Uma barra de ferramentas tem as seguintes características:<br /><br /> – Ignora o pai em sua definição.<br />-Não pode se tornar um submenu de nenhum grupo, nem mesmo usando CommandPlacement.<br />-Pode sempre ser exibido clicando-se em **barras de ferramentas** no menu **Exibir** .<br />-Pode ser exibido usando um [VisibilityItem](../extensibility/visibilityitem-element.md).<br />-Não requer nenhum código para criá-lo. Para obter um exemplo de como criar uma barra de ferramentas, consulte [Adicionar uma barra de ferramentas](../extensibility/adding-a-toolbar.md).<br /><br /> ToolWindowToolbar<br /> Fornece uma barra de ferramentas que é anexada a uma janela de ferramentas específica, assim como uma barra de ferramentas é anexada ao ambiente de desenvolvimento.<br /><br /> – Ignora o pai em sua definição.<br />-Não pode se tornar um submenu de nenhum grupo, nem mesmo usando CommandPlacement.<br />-É exibido somente quando a janela de ferramentas que hospeda a barra de ferramentas é exibida e o VSPackage adiciona explicitamente a barra de ferramentas à janela de ferramentas. Isso normalmente é feito quando a janela de ferramentas é criada com a obtenção da propriedade de host da barra de ferramentas (conforme representado pela <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost> interface) no quadro da janela de ferramentas e, em seguida, a chamada do <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost.AddToolbar%2A> método.|
|Condição|Opcional. Consulte [atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|Pai|Opcional. O elemento pai do item de menu.|
|CommandFlag|Obrigatórios. Consulte o [elemento flag de comando](../extensibility/command-flag-element.md). Os valores de CommandFlag válidos para um menu são os seguintes:<br /><br /> -   **AlwaysCreate**<br />-   **Defaultdocked**<br />-   **Defaultvisible** – esse sinalizador não afeta a exibição de barras de ferramentas.<br />-   **DontCache**<br />-   **DynamicVisibility** -esse sinalizador não afeta a exibição das barras de ferramentas.<br />-   **IconAndText**<br />-   **Nocustomizate**<br />-   **NotInTBList**<br />-   **NoToolbarClose**<br />-   **Textchanges**<br />-   **TextIsAnchorCommand**|
|Cadeias de caracteres|Obrigatórios. Consulte [elemento Strings](../extensibility/strings-element.md). O `ButtonText` elemento filho deve ser definido.|
|Annotation|Comentário opcional.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento menus](../extensibility/menus-element.md)|Define todos os menus que um VSPackage implementa.|

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
- [Arquivos de tabela de comando do Visual Studio (. vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
