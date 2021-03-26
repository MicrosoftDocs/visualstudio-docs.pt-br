---
title: Elemento de combinação | Microsoft Docs
description: 'O elemento de combinação define os comandos que aparecem em uma caixa de combinação. Há quatro tipos: DropDownCombo, DynamicCombo, IndexCombo e MRUCombo.'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Combos element (VSCT XML schema)
- VSCT XML schema elements, Combos
ms.assetid: 392e3063-f0a0-4130-9583-23bd2aa3fa36
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2e4a4895997e5c7511c694511000f7a0ac671db2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089739"
---
# <a name="combo-element"></a>Elemento de combinação
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
|guid|Obrigatórios. GUID do identificador de comando GUID/ID.|
|id|Obrigatórios. ID do identificador de comando de GUID/ID.|
|defaultwidth|Obrigatórios. Um inteiro que especifica uma largura de pixel para a caixa de combinação.|
|idCommandList|Obrigatórios. Uma ID que é enviada ao destino de comando ativo para recuperar a lista de itens a serem exibidos na caixa de combinação. A ID estará no mesmo escopo do GUID que o controle.|
|priority|Opcional. Um valor numérico que especifica a prioridade.|
|tipo|Opcional. Um valor enumerado que especifica o tipo de botão.<br /><br /> Se não for fornecido, o usará o botão.<br /><br /> DropDownCombo<br /> O VSPackage é responsável por preencher o conteúdo dessa caixa de combinação. O usuário não pode digitar nada na caixa de texto dessa lista suspensa.<br /><br /> DynamicCombo<br /> O VSPackage é responsável por preencher o conteúdo dessa caixa de combinação. O usuário pode editar essa combinação e também selecionar itens nela.<br /><br /> IndexCombo<br /> O mesmo que DynamicCombo, exceto pelo fato de que ele gera o índice do item em vez de seu texto.<br /><br /> MRUCombo<br /> Preenchido pelo IDE (ambiente de desenvolvimento integrado) em nome do VSPackage.  O usuário pode editar nessa caixa de combinação. O IDE se lembra das últimas 16 entradas por caixa de combinação.<br /><br /> Quando o usuário seleciona algo na caixa de combinação ou insere algo novo, o IDE notifica o VSPackage apropriado.|
|Condição|Opcional. Consulte [atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|Pai|Opcional. O elemento pai do botão.|
|CommandFlag|Obrigatórios. Consulte o [elemento flag de comando](../extensibility/command-flag-element.md). Os valores de CommandFlag válidos para um botão são os seguintes.<br /><br /> -CaseSensitive<br /><br /> - CommandWellOnly<br /><br /> -Defaultdesabilitoud<br /><br /> -Invisible<br /><br /> - DynamicVisibility<br /><br /> -Teclas de filtragem<br /><br /> - IconAndText<br /><br /> - NoAutoComplete<br /><br /> - NoButtonCustomize<br /><br /> -Nopersonalizar<br /><br /> - NoKeyCustomize<br /><br /> - StretchHorizontally|
|Cadeias de caracteres|Obrigatórios. Consulte [elemento Strings](../extensibility/strings-element.md). O elemento ButtonText filho deve ser definido.|
|Annotation|Comentário opcional.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento Commands](../extensibility/commands-element.md)|Representa a coleção de comandos na barra de ferramentas VSPackage.|

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
- [Arquivos de tabela de comando do Visual Studio (. vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
