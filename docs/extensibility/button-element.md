---
title: Elemento Button | Microsoft Docs
description: 'O elemento Button define um elemento com o qual o usuário pode interagir. Os botões podem ser tipos diferentes: Button, MenuButton e SplitDropDown.'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Buttons element (VSCT XML schema)
- VSCT XML schema elements, Buttons
ms.assetid: 96dccf51-2b00-4700-9d28-924b34c21ecd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 630d848c40b13a929c3dd91b47e1c35529efaa50
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901741"
---
# <a name="button-element"></a>Elemento Button
Define um elemento com o qual o usuário pode interagir. Os botões podem ser de tipos diferentes: Button, MenuButton e SplitDropDown.

## <a name="syntax"></a>Sintaxe

```
<Button guid="guidMyCommandSet" id="MyCommand" priority="0x102" type="button">
  <Parent>... </Parent>
  <Icon>... </Icon>
  <CommandFlag>... </CommandFlag>
  <Strings>... </Strings>
</Button>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|guid|Obrigatórios. GUID do identificador de comando GUID/ID.|
|id|Obrigatórios. ID do identificador de comando GUID/ID.|
|priority|Opcional. Um valor numérico que especifica a prioridade.|
|tipo|Opcional. Um valor enumerado que especifica o tipo de botão.<br /><br /> Se não for dado, o usará Button.<br /><br /> Botão<br /> Um comando padrão que aparece em barras de ferramentas (normalmente como um botão de ícone), menus e menus de contexto.<br /><br /> MenuButton<br /> Um item de menu que não executa um comando, mas produz outro menu.<br /><br /> SplitDropDown<br /> Controles, como os botões Desfazer e Refazer na barra de ferramentas padrão no Microsoft Word.|
|Condição|Opcional. Consulte [Atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento pai](../extensibility/parent-element.md)|Opcional. O elemento pai do botão.|
|[Elemento Icon](../extensibility/icon-element.md)|Opcional. O ícone associado ao botão.|
|[Elemento de sinalizador de comando](../extensibility/command-flag-element.md)|Obrigatórios. Os valores de CommandFlag válidos para um Botão são os a seguir.<br /><br /> - AllowParams<br /><br /> - CommandWellOnly<br /><br /> – DefaultDisabled<br /><br /> – DefaultInvisible<br /><br /> - DontCache<br /><br /> – DynamicItemStart<br /><br /> - DynamicVisibility<br /><br /> - FixMenuController<br /><br /> - IconAndText<br /><br /> - NoButtonCustomize<br /><br /> - NoCustomize<br /><br /> - NoKeyCustomize<br /><br /> - NoShowOnMenuController<br /><br /> - Pict<br /><br /> - PostExec<br /><br /> - ProfferedCmd<br /><br /> - RouteToDocs<br /><br /> - TextCascadeUseBtn<br /><br /> - TextMenuUseButton<br /><br /> – TextChanges<br /><br /> - TextChangesButton<br /><br /> - TextContextUseButton<br /><br /> - TextMenuCtrlUseMenu<br /><br /> - TextMenuUseButton<br /><br /> – TextOnly|
|[Elemento Strings](../extensibility/strings-element.md)|Obrigatórios. O elemento [ButtonText filho deve](../extensibility/buttontext-element.md) ser definido.|
|Annotation|Comentário opcional.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento Buttons](../extensibility/buttons-element.md)|Elementos do Botão de Grupos.|

## <a name="example"></a>Exemplo
 O exemplo a seguir define um botão em um *arquivo .vsct.*

 ```xml
<Button guid="guidMenuTextCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">
    <Parent guid="guidMenuTextCmdSet" id="MyMenuGroup" />
    <Icon guid="guidImages" id="bmpPic1" />
    <CommandFlag>TextChanges</CommandFlag>
    <Strings>
          <CommandName>cmdidMyCommand</CommandName>
          <ButtonText>My Command name</ButtonText>
    </Strings>
</Button>
 ```

## <a name="see-also"></a>Confira também
- [Visual Studio de tabela de comandos (.vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
