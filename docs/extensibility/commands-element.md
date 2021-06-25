---
title: Elemento Commands | Microsoft Docs
description: 'O elemento Commands representa a coleção de comandos na barra de ferramentas VSPackage e pode ter estas seções: menus, grupos, botões, combinações e bitmaps.'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- Commands
helpviewer_keywords:
- Commands element (VSCT XML schema)
- VSCT XML schema elements, Commands
ms.assetid: 47cf16a5-d78b-452e-86f6-b5893856dddf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e4c7b058acdd634079d0ca60dddb9f80e0e26ff0
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901861"
---
# <a name="commands-element"></a>Elemento Commands
Representa a coleção de comandos na barra de ferramentas VSPackage. A coleção pode ter até cinco subseções, da seguinte maneira: menus, grupos, botões, combinações e bitmaps.

 Cada elemento filho da subseção, por exemplo, \<Menu> , é identificado por uma ID de comando exclusiva que é um par GUID e identificador numérico. O GUID identifica o "conjunto de comandos" e é usado para agrupar comandos logicamente relacionados. O VSPackage deve definir seu próprio conjunto de comandos para evitar colisões com IDs de comando que são definidas por outros VSPackages.

## <a name="syntax"></a>Sintaxe

```xml
<Commands package="GuidMyPackage" >
  <Menus>... </Menus>
  <Groups>... </Groups>
  <Buttons>... </Buttons>
  <Combos>... </Combos>
  <Bitmaps>... </Bitmaps>
</Commands>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|pacote|Um GUID que identifica o VSPackage que fornece os comandos.<br /><br /> Por exemplo, Package = "guidVsPackage1Pkg".|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento menus](../extensibility/menus-element.md)|Define todos os menus que um VSPackage implementa.|
|[Elemento groups](../extensibility/groups-element.md)|Contém entradas que definem os grupos de comandos em um VSPackage.|
|[Elemento Buttons](../extensibility/buttons-element.md)|Elementos de botão de grupos.|
|[Elemento bitmaps](../extensibility/bitmaps-element.md)|Agrupa elementos de bitmap.|
|[Elemento de combinação](../extensibility/combos-element.md)|Agrupa elementos de combinação.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento commandtable](../extensibility/commandtable-element.md)|Define todos os elementos que representam os comandos que um VSPackage fornece ao IDE. Os elementos possíveis são itens de menu, menus, barras de ferramentas e caixas de combinação.|

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra como usar um [elemento Commands](../extensibility/commands-element.md).

```
<Commands package="guidMyPackage">
    <Menus>
      <Menu Condition="'%(DEBUG)' != 'true'"
        guid="cmdSetGuidMyProductCommands" id="menuIDMainMenu"
        priority="0x0000" type="Menu">
        <Annotation>
          <Documentation>this is an annotation</Documentation>
          <AppInfo>
            <CustomData>
              <CustomSubElement>Some data</CustomSubElement>
            </CustomData>
          </AppInfo>
        </Annotation>
        <CommandFlag>AlwaysCreate</CommandFlag>
        <Strings>
          <ButtonText>MainMenu</ButtonText>
        </Strings>
      </Menu>
  </Menus>
<Commands>
```

## <a name="see-also"></a>Confira também
- [Como VSPackages adicionar elementos da interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)
