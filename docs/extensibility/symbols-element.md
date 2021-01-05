---
title: Elemento Symbols | Microsoft Docs
description: O elemento Symbols define GUIDs e IDs que são usados por outros elementos VSCT. Este artigo contém um exemplo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Symbols element (VSCT XML schema)
- VSCT XML schema elements, Symbols
ms.assetid: 1cda43d8-42a5-4b1b-a3c8-cf0401c3202f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8e86406c4c10c2f65e8e43d8f3cb67f413ed3c63
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2020
ms.locfileid: "97715555"
---
# <a name="symbols-element"></a>Elemento Symbols
Define GUIDs e IDs que são usados por outros elementos VSCT. Para código não gerenciado, essas informações normalmente são provenientes dos arquivos de cabeçalho especificados pelo [elemento externo](../extensibility/extern-element.md). O código gerenciado usa os elementos filho do elemento Symbols para definir essas informações.

 Se você criar um arquivo. vsct de um arquivo. CTO existente, os símbolos serão gerados como filhos do elemento Symbols. Para obter mais informações, consulte [como: criar um. Arquivo vsct de um existente. Arquivo CTO](../extensibility/internals/how-to-create-a-dot-vsct-file.md#how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file).

 O elemento Symbols não deve ser confundido com o [elemento define](../extensibility/define-element.md), que define os pares de nome-valor para uso pelo pré-processador.

## <a name="syntax"></a>Sintaxe

```
<Symbols>
  <GuidSymbol>... </GuidSymbol>
  <GuidSymbol>... </GuidSymbol>
</Symbols>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|Nenhum||

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|GuidSymbol|Define um símbolo GUID. GuidSymbol tem dois atributos obrigatórios: nome e valor. O nome é o nome do símbolo e o valor é o valor do GUID como uma cadeia de caracteres.<br /><br /> Por exemplo: \<GuidSymbol name="guidVsPackage1Pkg"   value="{c5f54698-101a-4846-84d3-dc748f9cd848}" />|
|IDSymbol|Define um símbolo. IDSymbol tem dois atributos obrigatórios: nome e valor. O nome é o nome do símbolo e o valor é o valor do símbolo como uma cadeia de caracteres.<br /><br /> Por exemplo: \<IDSymbol name="MyMenuGroup" value="0x1020" />|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento CommandTable](../extensibility/commandtable-element.md)|O elemento raiz do arquivo. vsct.|

## <a name="example"></a>Exemplo

```
<Symbols>
  <GuidSymbol name="guidVsPackage1Pkg" value="{c5f54698-101a-4846-84d3-dc748f9cd848}" />
  <GuidSymbol name="guidVsPackage1CmdSet" value="{cb9dfd7f-2fcc-4a3e-aae8-f7fe30b1cfac}">
    <IDSymbol name="MyMenuGroup" value="0x1020" />
    <IDSymbol name="cmdidMyCommand" value="0x0100" />
    <IDSymbol name="cmdidMyTool" value="0x0101" />
  </GuidSymbol>
</Symbols>
```

## <a name="see-also"></a>Consulte também
- [Arquivos .Vsct (Visual Studio Command Table)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
