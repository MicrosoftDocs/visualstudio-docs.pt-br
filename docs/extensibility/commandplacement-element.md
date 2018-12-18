---
title: Elemento CommandPlacement | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- CommandPlacements element (VSCT XML schema)
- VSCT XML schema elements, CommandPlacements
ms.assetid: 2cbd7ac8-c55a-43d8-a26d-713b3d790016
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4d7288de9b0724d8ff4ef7b6174f59e747a9879d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49870257"
---
# <a name="commandplacement-element"></a>Elemento CommandPlacement
O elemento CommandPlacement permite que os botões, grupos e menus a serem incluídos em mais de um grupo ou menu. Usando o elemento CommandPlacement, não é preciso redefinir completamente esses itens para modificar a aparência de uma interface do usuário.  
  
 Para obter mais informações, consulte [criar grupos reutilizáveis de botões](../extensibility/creating-reusable-groups-of-buttons.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<CommandPlacement guid="guidMyCommandSet" id="MyCommand" priority="0x001" >  
  <Parent>... </Parent>  
</CommandPlacement>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|GUID|Necessário. O guid do conjunto de comandos, conforme definido na [elemento Symbols](../extensibility/symbols-element.md).|  
|id|Necessário. A id do menu, grupo ou o comando a ser colocado, conforme definido no `Symbols Element`.|  
|priority|Necessário. Determina a posição visual do item em seu elemento pai.|  
|Condição|Opcional. Ver [Aattributes condicional](../extensibility/vsct-xml-schema-conditional-attributes.md).|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|Pai|Necessário. O menu ou grupo que hospeda o item a ser colocado.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Elemento CommandPlacements](../extensibility/commandplacements-element.md)|Especifica os grupos de elementos CommandPlacements e CommandPlacement.|  
  
## <a name="example"></a>Exemplo  
  
```  
<CommandPlacements>  
  <CommandPlacement guid="guidWidgetPackage" id="cmdidInsertOptions"  
    priority="0x0300">  
    <Parent guid="cmdGuidWidgetCommands" id="menuIDEditWidget"/>  
  </CommandPlacement>  
</CommandPlacements>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Elemento CommandPlacements](../extensibility/commandplacements-element.md)   
 [Arquivos de tabela (. VSCT) de comando do Visual Studio](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
