---
title: Elemento de símbolos | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Symbols element (VSCT XML schema)
- VSCT XML schema elements, Symbols
ms.assetid: 1cda43d8-42a5-4b1b-a3c8-cf0401c3202f
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 81b6c5dcbd3601a6075097a44d2cd5dd625b4a87
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56706685"
---
# <a name="symbols-element"></a>Elemento Symbols
Define os GUIDs e IDs que são usadas por outros elementos VSCT. Para código não gerenciado, essas informações geralmente vem dos arquivos de cabeçalho que são especificados por [elemento Extern](../extensibility/extern-element.md). O código gerenciado usa os elementos filho do elemento símbolos para definir essas informações.

 Se você criar um arquivo. VSCT de um arquivo CTO já existente, os símbolos serão gerados como filhos do elemento de símbolos. Para obter mais informações, confira [Como: Criar um. Arquivo VSCT de um existente. Arquivo CTO](../extensibility/internals/how-to-create-a-dot-vsct-file.md#how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file).

 O elemento de símbolos não deve ser confundido com o [definem o elemento](../extensibility/define-element.md), que define os pares nome-valor para uso pelo pré-processador.

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
|GuidSymbol|Define um símbolo GUID. GuidSymbol possui dois atributos obrigatórios: nome e valor. O nome é o nome do símbolo e o valor é o valor do GUID como uma cadeia de caracteres.<br /><br /> For example:\<GuidSymbol name="guidVsPackage1Pkg"   value="{c5f54698-101a-4846-84d3-dc748f9cd848}" />|
|IDSymbol|Define um símbolo. IDSymbol possui dois atributos obrigatórios: nome e valor. O nome é o nome do símbolo e o valor é o valor do símbolo, como uma cadeia de caracteres.<br /><br /> Por exemplo:\<IDSymbol nome = "MyMenuGroup" value = "0x1020" / >|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento CommandTable](../extensibility/commandtable-element.md)|O elemento raiz do arquivo. VSCT.|

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
- [Arquivos da tabela de comandos do Visual Studio (.Vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)