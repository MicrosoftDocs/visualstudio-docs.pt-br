---
title: Operador de contexto (C++) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.operators
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- expressions [C++], native debugger
- evaluation
- format specifiers, expressions
- context operator, in expressions
- debugging [C++], expressions
- native expression evaluator
ms.assetid: 73cc9afe-f4a4-474e-bb89-5a33fb5e570c
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5807b8e3c6a85c25511374e756b02fabfa5abba5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51731681"
---
# <a name="context-operator-c"></a>Operador de contexto (C++)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar o operador de contexto em C++ para qualificar um local de ponto de interrupção, nome de variável ou expressão. O operador de contexto é útil para especificar um nome de um escopo externo que está oculto por um nome local.  
  
##  <a name="BKMK_Using_context_operators_to_specify_a_symbol"></a> Sintaxe  
 Há duas maneiras de especificar o contexto:  
  
1.  {, [*módulo*]} *expressão*  
  
     As chaves devem conter duas vírgulas e o nome do módulo (executável ou DLL) ou o caminho completo.  
  
     Por exemplo, para definir um ponto de interrupção na função `SomeFunction` de EXAMPLE.dll:  
  
    ```cpp  
    {,,EXAMPLE.dll}SomeFunction  
    ```  
  
2.  *módulo*! *expressão*  
  
    ```cpp  
    EXAMPLE.dll!SomeFunction  
    ```  
  
- *módulo* é o nome de um módulo. Você pode usar um caminho completo para resolver a ambiguidade entre módulos com o mesmo nome.  
  
   Se o *módulo* caminho inclui uma vírgula, um espaço inserido ou uma chave, você deve usar aspas em torno do caminho para que o analisador de contexto possa reconhecer corretamente a cadeia de caracteres. As aspas simples são consideradas parte de um nome de arquivo do Windows, portanto, você deve usar aspas duplas. Por exemplo,  
  
  ```cpp  
  {,,"a long, long, library name.dll"} g_Var  
  ```  
  
- *expressão* é qualquer expressão C++ válida que resolve para um destino válido, como um nome de função, o nome de variável ou o endereço do ponteiro no *módulo*.  
  
  Quando o avaliador de expressão localiza um símbolo em uma expressão, procura pelo símbolo na seguinte ordem:  
  
1.  Escopo léxico externo, começando com o bloco atual, série de instruções incluídas entre chaves e a continuação externa com o bloco delimitador. O bloco atual é o código que contém o local atual, endereço do ponteiro de instrução.  
  
2.  Escopo da função. A função atual.  
  
3.  Escopo da classe, se o local atual estiver dentro de uma função de membro C ++. O escopo da classe inclui todas as classes base. O avaliador de expressão usa regras de dominância normais.  
  
4.  Símbolos globais no módulo atual.  
  
5.  Símbolos públicos no programa atual.





