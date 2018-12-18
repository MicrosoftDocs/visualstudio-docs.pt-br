---
title: Elemento KeyBinding | Microsoft Docs
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
- VSCT XML schema elements, KeyBindings
- KeyBinding element (VSCT XML schema)
ms.assetid: e55a1098-15df-42a9-9f87-e3a99cf437dd
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 32dafc1b16282657db40531e34d1eccb02841481
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51780926"
---
# <a name="keybinding-element"></a>Elemento KeyBinding
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O elemento de associação de teclas Especifica atalhos de teclado para os comandos.  
  
 Comandos podem ter associações de teclas única e duplos associadas a eles. Um exemplo de uma associação de chave única é CTRL + S para o **salvar** comando. Associações de teclas duplas exigem duas combinações de teclas sucessivas para acionar um comando. Um exemplo de uma associação de chave dupla é CTRL + K, CTRL + K para definir um indicador.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<Keybinding guid="MyGuid" id="MyId" Editor="MyEditor" key1="B" key2="x" mod1="Control" mod2="Alt" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|GUID|Obrigatório.|  
|id|Obrigatório.|  
|editor|Obrigatório. O GUID do editor indica o contexto de edição para o qual este atalho de teclado estará ativo. O valor de escopo de associação global é "guidVSStd97".|  
|CHAVE1|Obrigatório. Os valores válidos incluem todos os caracteres alfanuméricos typable e também valores hexadecimais de dois dígitos precedidos por 0x e VK_constants.|  
|Mod1|Opcional. Qualquer combinação de CTRL, ALT e SHIFT separados por espaço.|  
|Key2|Opcional. Os valores válidos incluem todos os caracteres alfanuméricos typable e também valores hexadecimais de dois dígitos precedidos por 0x e VK_constants.|  
|Mod2|Opcional. Qualquer combinação de CTRL, ALT e SHIFT separados por espaço.|  
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
 [Arquivos da tabela de comandos do Visual Studio (.Vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)

