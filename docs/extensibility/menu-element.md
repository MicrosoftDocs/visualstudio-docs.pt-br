---
title: Elemento menu | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Menus
- Menus element (VSCT XML schema)
ms.assetid: ce0560f3-b4c9-4ab2-a99c-d4e10f37b9e0
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3120a64db5c493f8e49ddeac42be0b2e89a40c45
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49908819"
---
# <a name="menu-element"></a>Elemento menu
Define um item de menu. Esses são os seis tipos de menus: contexto, Menu, MenuController, MenuControllerLatched, barra de ferramentas e ToolWindowToolbar.  
  
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
|GUID|Necessário. GUID do identificador de comando/ID de GUID.|  
|id|Necessário. ID do identificador de comando/ID de GUID.|  
|priority|Opcional. Um valor numérico que especifica a posição relativa de um menu em um grupo de menus.|  
|ToolbarPriorityInBand|Opcional. Um valor numérico que especifica a posição relativa de uma barra de ferramentas em uma faixa quando a janela estiver encaixada.|  
|tipo|Opcional. Um valor enumerado que especifica o tipo de elemento.<br /><br /> Se não estiver presente, o tipo padrão é o Menu.<br /><br /> Contexto<br /> Um menu de atalho que é mostrado quando um usuário clica uma janela. Um menu de atalho tem as seguintes características:<br /><br /> -Não usa o **pai** e **prioridade** campos quando o menu será exibido como um menu de atalho.<br />-Pode ser usado como um submenu e também como um menu de atalho. Nesse caso, ambas **ID do grupo** e **prioridade** campos serão respeitados.<br />-É sempre não está disponível.<br /><br /> Um menu de atalho é exibido somente quando as seguintes condições forem verdadeiras:<br /><br /> -A janela que o hospeda é exibida.<br />-Um manipulador de mouse no VSPackage detecta o botão direito do mouse na janela e, em seguida, chama um método que manipula o comando.<br />-O menu de atalho é exibido ao chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager.ShowContextMenu%2A> método (a abordagem recomendada) ou o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A> método.<br /><br /> Menu<br /> Fornece um menu suspenso. Um menu suspenso tem as seguintes características:<br /><br /> -Respeita o pai em sua definição.<br />-Deve ter um grupo pai, ou um CommandPlacement a um grupo.<br />-Pode ser um submenu em qualquer outro tipo de menu.<br />-É exibida automaticamente sempre que seu menu pai é exibido.<br />-Não requer a implementação de qualquer código de VSPackage para torná-la exibida.<br /><br /> MenuController<br /> Fornece um menu suspenso do botão de divisão, que normalmente é usado em barras de ferramentas. Um menu MenuController tem as seguintes características:<br /><br /> -Deve estar contido em outro menu por meio do pai ou CommandPlacement.<br />-Respeita o pai em sua definição.<br />-Pode ter qualquer tipo de menu pai.<br />-É automaticamente disponibilizado sempre que seu menu pai é exibido.<br />-Não requer suporte programático para tornar o menu exibido.<br /><br /> Um comando de menu do botão de divisão é exibido no botão de menu. O comando exibido tem uma das seguintes características:<br /><br /> -É o último comando que foi usado se o comando ainda é exibido e habilitado.<br />-É o primeiro comando exibido.<br /><br /> MenuControllerLatched<br /> Fornece um menu de lista suspensa do botão de divisão para o qual um comando pode ser especificado como a seleção padrão, marcando o comando conforme travada.<br /><br /> Um comando travado é um comando que está marcado como no menu conforme selecionado, normalmente, exibindo uma marca de seleção. Um comando pode ser marcado como travada se ele tiver o OLECMDF_LATCHED sinalizador definido nela em uma implementação da `QueryStatus` método da <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface. Um menu MenuControllerLatched tem as seguintes características:<br /><br /> -Deve estar contido em outro menu por meio de um grupo pai ou CommandPlacement.<br />-Respeita o pai em sua definição.<br />-Pode ter qualquer tipo de menu pai.<br />-Se torna disponível sempre que seu menu pai é exibido.<br />-Não requer suporte programático para tornar o menu exibido.<br /><br /> Um comando de menu do botão de divisão é exibido no botão de menu. O comando exibido tem uma das seguintes características:<br /><br /> -É o primeiro comando exibido que é travado.<br />-É o primeiro comando exibido.<br /><br /> Barra de ferramentas<br /> Fornece uma barra de ferramentas. Uma barra de ferramentas tem as seguintes características:<br /><br /> -Ignora o pai em sua definição.<br />-Não pode ser feita um submenu de qualquer grupo, nem mesmo usando CommandPlacement.<br />-Sempre podem ser exibidos clicando **barras de ferramentas** sobre o **exibição** menu.<br />-Pode ser exibida usando um [VisibilityItem](../extensibility/visibilityitem-element.md).<br />-Não requer nenhum código para criá-lo. Para obter um exemplo sobre como criar uma barra de ferramentas, consulte [adicionar uma barra de ferramentas](../extensibility/adding-a-toolbar.md).<br /><br /> ToolWindowToolbar<br /> Fornece uma barra de ferramentas que está anexada a uma janela de ferramenta específica, assim como uma barra de ferramentas é anexada ao ambiente de desenvolvimento.<br /><br /> -Ignora o pai em sua definição.<br />-Não pode ser feita um submenu de qualquer grupo, nem mesmo usando CommandPlacement.<br />-É exibida somente quando a janela de ferramenta que hospeda a barra de ferramentas é exibida e o VSPackage explicitamente adiciona a barra de ferramentas para a janela da ferramenta. Isso normalmente é feito quando a janela da ferramenta é criada, obtendo a propriedade de host de barra de ferramentas (conforme representado pela <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost> interface) do quadro de janela de ferramenta e, em seguida, chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost.AddToolbar%2A> método.|  
|Condição|Opcional. Ver [atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|Pai|Opcional. O elemento pai do item de menu.|  
|CommandFlag|Necessário. Ver [elemento Command flag](../extensibility/command-flag-element.md). Os valores válidos de CommandFlag para um Menu são da seguinte maneira:<br /><br /> -   **AlwaysCreate**<br />-   **DefaultDocked**<br />-   **DefaultInvisible** -esse sinalizador não afeta a exibição das barras de ferramentas.<br />-   **DontCache**<br />-   **DynamicVisibility** -esse sinalizador não afeta a exibição das barras de ferramentas.<br />-   **IconAndText**<br />-   **NoCustomize**<br />-   **NotInTBList**<br />-   **NoToolbarClose**<br />-   **TextoAltera**<br />-   **TextIsAnchorCommand**|  
|Cadeias de caracteres|Necessário. Ver [elemento cadeias de caracteres](../extensibility/strings-element.md). O filho `ButtonText` elemento deve ser definido.|  
|Anotação|Comentário opcional.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Elemento menus](../extensibility/menus-element.md)|Define todos os menus que implementa um VSPackage.|  
  
## <a name="example"></a>Exemplo  
  
```  
<Menu guid="cmdGuidWidgetCommands" id="menuIDEditWidget"  
  priority="0x0002" type="Menu">  
  <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit">  
    <CommandFlag>AlwaysCreate</CommandFlag>  
    <Strings>  
      <ButtonText>Edit Widget</ButtonText>  
    </Strings>  
    </Parent>  
</Menu>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos da tabela de comando do Visual Studio (. VSCT)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)