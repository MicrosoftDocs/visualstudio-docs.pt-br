---
title: Atributos condicionais de esquema XML do VSCT | Microsoft Docs
description: Saiba como aplicar atributos condicionais a listas e itens de esquema XML do VSCT. Os atributos são avaliadas como true ou false, controlando a saída resultante.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, conditional attributes
- conditional attributes (VSCT XML schema)
ms.assetid: 754d4f32-319b-44c9-915f-f7c60e53222e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e91207016ed6e1baab80b323680d10a40e0331d8
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905248"
---
# <a name="vsct-xml-schema-conditional-attributes"></a>Atributos condicionais do esquema XML do VSCT
Você pode aplicar atributos condicionais a todas as listas e itens. Operadores lógicos e expressões de expansão de símbolo são avaliadas como true ou false. Se true, a lista ou o item associado será incluído na saída resultante.

 Você pode testar expansões de token em relação a outras expansões de token ou constantes. A função `Defined()` testa se um nome específico foi definido, mesmo que não tenha nenhum valor.

 Quando um atributo Condition é aplicado a uma lista, a condição é aplicada a cada elemento filho na lista. Se um elemento filho contiver um atributo Condition, sua condição será combinada com a expressão pai por uma operação AND.

 Os valores 1, '1' e 'true' são avaliados como true e 0, '0' e 'false' são avaliados como false.

## <a name="operators"></a>Operadores
 Use os operadores a seguir para avaliar expressões condicionais.

|Operador|Definição|
|--------------|----------------|
|(,)|Agrupamento|
|!|Não lógico|
|\<, >, \<=, >=, ==, !=|Igualdade e relacional|
|e|Boolean|
|ou|Boolean|

## <a name="examples"></a>Exemplos

```xml
<Menu Condition="Defined(DEBUG)" ...
</Menu>

<Menu Condition="%(SKU_MODE) = 'Demo'" ...
</Menu>

<Menus Condition="Defined(DEBUG)">
    <Menu ...
    </Menu>
</Menus>

<Menus Condition="Defined(DEMO_SKU)">
    <Menus Condition="!Defined(DEBUG)">
        <Menu ...
        </Menu>
    </Menus>

    <Menu ...
    </Menu>
</Menus>

<Menus Condition="(Defined(DEMO_SKU) or Defined(SAMPLE_SKU))
and !Defined(DEBUG)">
    <Menu ...
    </Menu>
</Menus>
```

## <a name="see-also"></a>Confira também
- [Visual Studio de comando (. Arquivos vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
