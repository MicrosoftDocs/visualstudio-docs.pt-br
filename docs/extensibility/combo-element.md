---
title: Elemento Combo | Microsoft Docs
description: 'O elemento Combo define comandos que aparecem em uma caixa de combinação. Há quatro tipos: DropDownCombo, DynamicCombo, IndexCombo e MRUCombo.'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Combos element (VSCT XML schema)
- VSCT XML schema elements, Combos
ms.assetid: 392e3063-f0a0-4130-9583-23bd2aa3fa36
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 431d68b6e545506f5fc90cc5a98a52dd4f1c33ad
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904948"
---
# <a name="combo-element"></a>Elemento Combo
Define comandos que aparecem em uma caixa de combinação. Há quatro tipos de caixas de combinação, da seguinte forma: DropDownCombo, DynamicCombo, IndexCombo e MRUCombo.

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
|guid|Obrigatórios. GUID do identificador de comando GUID/ID.|
|id|Obrigatórios. ID do identificador de comando GUID/ID.|
|defaultWidth|Obrigatórios. Um inteiro que especifica uma largura de pixel para a caixa de combinação.|
|idCommandList|Obrigatórios. Uma ID enviada ao destino de comando ativo para recuperar a lista de itens a serem exibidos na caixa de combinação. A ID estará no mesmo escopo guid que o controle .|
|priority|Opcional. Um valor numérico que especifica a prioridade.|
|tipo|Opcional. Um valor enumerado que especifica o tipo de botão.<br /><br /> Se não for dado, o usará Button.<br /><br /> DropDownCombo<br /> O VSPackage é responsável por preencher o conteúdo dessa caixa de combinação. O usuário não pode digitar nada na caixa de texto deste lista listada.<br /><br /> DynamicCombo<br /> O VSPackage é responsável por preencher o conteúdo dessa caixa de combinação. O usuário pode editar essa combinação e também selecionar itens nele.<br /><br /> IndexCombo<br /> O mesmo que DynamicCombo, exceto que ele gera o índice do item em vez de seu texto.<br /><br /> MRUCombo<br /> Preenchido pelo IDE (ambiente de desenvolvimento integrado) em nome do VSPackage.  O usuário pode editar nesta caixa de combinação. O IDE lembra até as últimas 16 entradas por caixa de combinação.<br /><br /> Quando o usuário seleciona algo na caixa de combinação ou insula algo novo, o IDE notifica o VSPackage apropriado.|
|Condição|Opcional. Consulte [Atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|Pai|Opcional. O elemento pai do botão.|
|CommandFlag|Obrigatórios. Consulte [Elemento de sinalizador de comando](../extensibility/command-flag-element.md). Os valores de CommandFlag válidos para um Botão são os a seguir.<br /><br /> - CaseSensitive<br /><br /> - CommandWellOnly<br /><br /> – DefaultDisabled<br /><br /> – DefaultInvisible<br /><br /> - DynamicVisibility<br /><br /> – FilterKeys<br /><br /> - IconAndText<br /><br /> - NoAutoComplete<br /><br /> - NoButtonCustomize<br /><br /> - NoCustomize<br /><br /> - NoKeyCustomize<br /><br /> – StretchHorizontally|
|Cadeias de caracteres|Obrigatórios. Consulte [o elemento Strings](../extensibility/strings-element.md). O elemento ButtonText filho deve ser definido.|
|Annotation|Comentário opcional.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento Commands](../extensibility/commands-element.md)|Representa a coleção de comandos na barra de ferramentas vsPackage.|

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

## <a name="see-also"></a>Confira também
- [Visual Studio de tabela de comandos (.vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
