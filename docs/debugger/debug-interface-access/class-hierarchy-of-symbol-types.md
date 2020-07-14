---
title: Hierarquia de classes de tipos de símbolo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK], class hierarchies
ms.assetid: 0ccd6990-4654-44cd-a6f3-bdd82fe90f6c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ed6817c5c01b66143739b2f81899f2b58886d8e8
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85462269"
---
# <a name="class-hierarchy-of-symbol-types"></a>Hierarquia de classes de tipos de símbolos
A tabela a seguir descreve os tipos de símbolo na hierarquia de classes.

## <a name="symbol-types"></a>Tipos de símbolo

|Tipo de símbolo|Descrição|
|-----------------|-----------------|
|[UDT](../../debugger/debug-interface-access/udt.md)|Símbolo usado para representar cada classe, estrutura e União.|
|[Enum (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/enum-debug-interface-access-sdk.md)|Símbolo para tipos enumerados.|
|[PointerType](../../debugger/debug-interface-access/pointertype.md)|Símbolo para tipos de ponteiro.|
|[ArrayType](../../debugger/debug-interface-access/arraytype.md)|Símbolo para tipos de matriz.|
|[BaseType](../../debugger/debug-interface-access/basetype.md)|Símbolo para tipos base|
|[Typedef (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/typedef-debug-interface-access-sdk.md)|Símbolo que introduz nomes para outros tipos.|
|[BaseClass](../../debugger/debug-interface-access/baseclass.md)|Símbolo usado para cada classe base de um tipo definido pelo usuário (UDT).|
|[Friend (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/friend-debug-interface-access-sdk.md)|Símbolo para classes Friend e funções Friend.|
|[FunctionType](../../debugger/debug-interface-access/functiontype.md)|Símbolo para cada assinatura de função exclusiva.|
|[FunctionArgType](../../debugger/debug-interface-access/functionargtype.md)|Símbolo para cada parâmetro para uma função.|
|[VTableShape](../../debugger/debug-interface-access/vtableshape.md)|Símbolo do tamanho da tabela virtual.|
|[VTable](../../debugger/debug-interface-access/vtable.md)|Símbolo de uma tabela virtual.|
|[CustomType](../../debugger/debug-interface-access/customtype.md)|Símbolo do tipo definido pelo fornecedor.|
|[ManagedType](../../debugger/debug-interface-access/managedtype.md)|Símbolo para um tipo definido em metadados.|
|[Dimensão](../../debugger/debug-interface-access/dimension.md)|Símbolo para dimensões de matriz.|

> [!NOTE]
> Cada símbolo pode ter propriedades que contêm informações sobre o símbolo, bem como referências a outros símbolos. Essas propriedades são listadas nos tópicos de símbolos individuais.

## <a name="see-also"></a>Confira também
- [Enumeração CV_access_e](../../debugger/debug-interface-access/cv-access-e.md)
- [Hierarquia lexical de tipos de símbolo](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [Símbolos e marcas de símbolos](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)