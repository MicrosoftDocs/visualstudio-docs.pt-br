---
title: Elemento combo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Combos element (VSCT XML schema)
- VSCT XML schema elements, Combos
ms.assetid: 392e3063-f0a0-4130-9583-23bd2aa3fa36
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7cfce045531a871e4630a6175d2fc24f4a50ebd8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62926612"
---
# <a name="combo-element"></a>Elemento combo
Define os comandos que aparecem em uma caixa de combinação. Há quatro tipos de caixas de combinação, da seguinte maneira: DropDownCombo, DynamicCombo, IndexCombo e MRUCombo.

## <a name="syntax"></a>Sintaxe

```xml
<combo guid="guidMyCommandSet" id="MyCommand" defaultWidth="20" idCommandList="MyCommandListID" priority="0x102" type="DropDownCombo">
  <Parent>... </Parent
  <CommandFlag>... </CommandFlag>
  <Strings>... </Strings>
</combo>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|GUID|Necessário. GUID do identificador de comando/ID de GUID.|
|id|Necessário. ID do identificador de comando/ID de GUID.|
|defaultWidth|Necessário. Um inteiro que especifica uma largura de pixel para a caixa de combinação.|
|idCommandList|Necessário. Uma ID que é enviada para o destino do comando Active Directory para recuperar a lista de itens a serem exibidos na caixa de combinação. A ID será no mesmo escopo GUID como o controle.|
|priority|Opcional. Um valor numérico que especifica a prioridade.|
|tipo|Opcional. Um valor enumerado que especifica o tipo de botão.<br /><br /> Se não for especificado, usa o botão.<br /><br /> DropDownCombo<br /> O VSPackage é responsável por preencher o conteúdo desta caixa de combinação. O usuário não é possível digitar qualquer coisa na caixa de texto nesta lista suspensa.<br /><br /> DynamicCombo<br /> O VSPackage é responsável por preencher o conteúdo dessa caixa de combinação. O usuário pode editar essa combinação e também selecionar itens nele.<br /><br /> IndexCombo<br /> O mesmo que DynamicCombo, exceto que ele gera o índice do item em vez de seu texto.<br /><br /> MRUCombo<br /> Preenchido pelo ambiente de desenvolvimento integrado (IDE) em nome de VSPackage.  O usuário pode editar nessa caixa de combinação. O IDE relembra até as últimas 16 entradas por caixa de combinação.<br /><br /> Quando o usuário seleciona algo na caixa de combinação ou digita algo novo, o IDE notifica o VSPackage apropriado.|
|Condição|Opcional. Ver [atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|Pai|Opcional. O elemento pai do botão.|
|CommandFlag|Necessário. Ver [elemento Command flag](../extensibility/command-flag-element.md). Os valores válidos de CommandFlag para um botão serão o seguinte.<br /><br /> -CaseSensitive<br /><br /> - CommandWellOnly<br /><br /> -DefaultDisabled<br /><br /> - DefaultInvisible<br /><br /> -DynamicVisibility<br /><br /> -As teclas de filtragem<br /><br /> - IconAndText<br /><br /> -NoAutoComplete<br /><br /> -NoButtonCustomize<br /><br /> -NoCustomize<br /><br /> -NoKeyCustomize<br /><br /> -StretchHorizontally|
|Cadeias de caracteres|Necessário. Ver [elemento cadeias de caracteres](../extensibility/strings-element.md). Elemento ButtonText filho deve ser definido.|
|Anotação|Comentário opcional.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento Commands](../extensibility/commands-element.md)|Representa a coleção de comandos na barra de ferramentas do VSPackage.|

## <a name="example"></a>Exemplo

```xml
<Combo guid="guidWidgetPackage" id="cmdidInsertOptions"
  defaultWidth="100" idCommandList="cmdidGetInsertOptionsList">
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <ButtonText>Select Insert Options</ButtonText>
  </Strings>
</Combo>

<Combo guid="guidWidgetPackage" id="cmdidInsertOptions"
  priority="0x0500" type="DropDownCombo" defaultWidth="100"
  idCommandList="cmdidGetInsertOptionsList">
  <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit">
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <ButtonText>Select Insert Options</ButtonText>
  </Strings>
</Combo>
```

## <a name="see-also"></a>Consulte também
- [Arquivos de tabela (. VSCT) de comando do Visual Studio](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
