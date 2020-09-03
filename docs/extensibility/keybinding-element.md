---
title: Elemento keybind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, KeyBindings
- KeyBinding element (VSCT XML schema)
ms.assetid: e55a1098-15df-42a9-9f87-e3a99cf437dd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b458e70a9a85c11707c50da2e16e3aa73f51bc12
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80703140"
---
# <a name="keybinding-element"></a>Elemento keybind
O elemento KeyBinding especifica atalhos de teclado para os comandos.

 Os comandos podem ter associações de chave única e dupla associadas a eles. Um exemplo de uma única Associação de chave é **Ctrl** + **S** para o comando **Save** . Associações de chave dupla exigem duas combinações de chave sucessivas para disparar um comando. Um exemplo de uma associação de tecla dupla é <strong>Ctrl *+</strong> k<strong>,</strong>CTRL <strong>+</strong> k** para definir um indicador.

## <a name="syntax"></a>Sintaxe

```
<Keybinding guid="MyGuid" id="MyId" Editor="MyEditor" key1="B" key2="x" mod1="Control" mod2="Alt" />
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|guid|Obrigatórios.|
|id|Obrigatórios.|
|editor|Obrigatórios. O GUID do editor indica o contexto de edição para o qual esse atalho de teclado estará ativo. O valor do escopo de associação global é "guidVSStd97".|
|key1|Obrigatórios. Os valores válidos incluem todos os alfanuméricos typable e também valores hexadecimais de dois dígitos precedidos por 0x e [VK_constants](/windows/desktop/inputdev/virtual-key-codes).|
|mod1|Opcional. Qualquer combinação de **Ctrl**, **ALT**e **Shift** separada por espaço.|
|key2|Opcional. Os valores válidos incluem todos os alfanuméricos typable e também valores hexadecimais de dois dígitos precedidos por 0x e [VK_constants](/windows/desktop/inputdev/virtual-key-codes).|
|mod2|Opcional. Qualquer combinação de **Ctrl**, **ALT**e **Shift** separada por espaço.|
|emulador|Opcional.|
|Condição|Opcional. Consulte [atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|Pai||
|Anotação||

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento keybindings](../extensibility/keybindings-element.md)|Agrupa os elementos de keybindling e outros agrupamentos de keybindings.|

## <a name="example"></a>Exemplo

```
<KeyBindings>
  <KeyBinding guid="guidWidgetPackage" id="cmdidUpdateWidget"
    editor="guidWidgetEditor" key1="VK_F5"/>
  <KeyBinding guid="guidWidgetPackage" id="cmdidRunWidget"
    editor="guidWidgetEditor" key1="VK_F5" mod1="Control"/>
</KeyBindings>
```

## <a name="see-also"></a>Confira também
- [Elemento keybindings](../extensibility/keybindings-element.md)
- [Arquivos de tabela de comando do Visual Studio (. vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
