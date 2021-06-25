---
title: Elemento Group | Microsoft Docs
description: O elemento Group define um grupo de comandos VSPackage. Este artigo descreve atributos, elementos filho e elementos pai.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Groups
- Groups element (VSCT XML schema)
ms.assetid: 69faee18-cbf4-470a-b952-c1919c583df8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 422ff5d3d962198953a24210eaa3ffa30c7fc8a1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898585"
---
# <a name="group-element"></a>Elemento Group
Define um grupo de comandos VSPackage.

## <a name="syntax"></a>Sintaxe

```xml
<Group guid="guidMyCommandSet" id="MyGroup" priority="0x101">
  <Parent>... </Parent>
</Group>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|guid|Obrigatórios. GUID do identificador de comando GUID/ID.|
|id|Obrigatórios. ID do identificador de comando GUID/ID.|
|priority|Opcional. Um valor numérico que especifica a prioridade.|
|Condição|Opcional. Consulte [Atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|Pai|Opcional. O elemento pai do botão.|
|Annotation|Comentário opcional.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento Groups](../extensibility/groups-element.md)|Contém entradas que definem os grupos de comandos de um VSPackage.|

## <a name="example"></a>Exemplo

```xml
<Group guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit">
  <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_MAINMENU"/>
</Group>
```

## <a name="see-also"></a>Confira também
- [Visual Studio de tabela de comandos (.vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
