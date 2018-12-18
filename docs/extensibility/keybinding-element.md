---
title: Elemento KeyBinding | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, KeyBindings
- KeyBinding element (VSCT XML schema)
ms.assetid: e55a1098-15df-42a9-9f87-e3a99cf437dd
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 77fb94e702615d0d27ce2587c034000f6c4b3e3d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49905097"
---
# <a name="keybinding-element"></a>Elemento KeyBinding
O elemento de associação de teclas Especifica atalhos de teclado para os comandos.  
  
 Comandos podem ter associações de teclas única e duplos associadas a eles. É um exemplo de uma associação de chave única **Ctrl**+**S** para o **salvar** comando. Associações de teclas duplas exigem duas combinações de teclas sucessivas para acionar um comando. É um exemplo de uma associação de chave dupla <strong>Ctrl*+</strong>K<strong>,</strong>Ctrl<strong>+</strong>K** para definir um indicador.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<Keybinding guid="MyGuid" id="MyId" Editor="MyEditor" key1="B" key2="x" mod1="Control" mod2="Alt" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|GUID|Necessário.|  
|id|Necessário.|  
|editor|Necessário. O GUID do editor indica o contexto de edição para o qual este atalho de teclado estará ativo. O valor de escopo de associação global é "guidVSStd97".|  
|CHAVE1|Necessário. Os valores válidos incluem todos os typable alfanuméricos e valores hexadecimais de dois dígitos precedidos por 0x e [VK_constants](/windows/desktop/inputdev/virtual-key-codes).|  
|Mod1|Opcional. Qualquer combinação de **Ctrl**, **Alt**, e **Shift** separados por espaço.|  
|Key2|Opcional. Os valores válidos incluem todos os typable alfanuméricos e valores hexadecimais de dois dígitos precedidos por 0x e [VK_constants](/windows/desktop/inputdev/virtual-key-codes).|  
|Mod2|Opcional. Qualquer combinação de **Ctrl**, **Alt**, e **Shift** separados por espaço.|  
|Emulador|Opcional.|  
|Condição|Opcional. Ver [atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|Pai||  
|Anotação||  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Elemento KeyBindings](../extensibility/keybindings-element.md)|Agrupa elementos de associação de teclas e os outros agrupamentos de associações de teclas.|  
  
## <a name="example"></a>Exemplo  
  
```  
<KeyBindings>  
  <KeyBinding guid="guidWidgetPackage" id="cmdidUpdateWidget"   
    editor="guidWidgetEditor" key1="VK_F5"/>  
  <KeyBinding guid="guidWidgetPackage" id="cmdidRunWidget"   
    editor="guidWidgetEditor" key1="VK_F5" mod1="Control"/>  
</KeyBindings>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Elemento KeyBindings](../extensibility/keybindings-element.md)   
 [Arquivos de tabela (. VSCT) de comando do Visual Studio](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
