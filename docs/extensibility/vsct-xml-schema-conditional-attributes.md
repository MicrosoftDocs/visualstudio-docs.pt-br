---
title: Atributos condicionais de esquema XML VSCT | Microsoft Docs
description: Saiba como aplicar atributos condicionais a listas e itens de esquema XML do VSCT. Os atributos são avaliados como true ou false, controlando a saída resultante.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, conditional attributes
- conditional attributes (VSCT XML schema)
ms.assetid: 754d4f32-319b-44c9-915f-f7c60e53222e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5bc1bcb9d80474b467e90de6262e797087589065
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062350"
---
# <a name="vsct-xml-schema-conditional-attributes"></a>Atributos condicionais de esquema XML VSCT
Você pode aplicar atributos condicionais a todas as listas e itens. Os operadores lógicos e as expressões de expansão de símbolo são avaliados como verdadeiro ou falso. Se for true, a lista ou o item associado será incluído na saída resultante.

 Você pode testar expansões de token em relação a outras expansões ou constantes de token. A função `Defined()` testa se um nome específico foi definido, mesmo se não tiver nenhum valor.

 Quando um atributo Condition é aplicado a uma lista, a condição é aplicada a todos os elementos filho na lista. Se um elemento filho contiver um atributo Condition, sua condição será combinada com a expressão pai por uma operação AND.

 Os valores 1, ' 1 ' e ' verdadeiro ' são avaliados como verdadeiros, e 0, ' 0 ' e ' falso ' são avaliados como falso.

## <a name="operators"></a>Operadores
 Use os operadores a seguir para avaliar expressões condicionais.

|Operador|Definição|
|--------------|----------------|
|(,)|Agrupamento|
|!|Não lógico|
|\<, >, \<=, >=, ==, !=|Relacional e igualdade|
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
- [Tabela de comandos do Visual Studio (. Arquivos de vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
