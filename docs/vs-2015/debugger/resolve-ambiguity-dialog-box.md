---
title: Caixa de diálogo de ambiguidade resolver | Microsoft Docs
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
- vs.debug.Disambig
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Resolve Ambiguity dialog box
- debugger, Resolve Ambiguity dialog box
- debugging [C++], resolving ambiguity
ms.assetid: d9f47455-a116-4c84-8bad-2dfbf4d77f74
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 13458279d1970bd1b398a0de6e74b34b0b3a99a0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51807570"
---
# <a name="resolve-ambiguity-dialog-box"></a>Caixa de diálogo Resolver Ambiguidade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A caixa de diálogo `Resolve Ambiguity` aparece quando o depurador não pode escolher o local para exibir. Por exemplo, se você estiver usando modelos C++, poderá criar várias funções de um único modelo da função. Se o depurador para em um local de origem no modelo, e você escolher `Go To Disassembly`, o depurador tem várias opções. Cada função criada do modelo tem seu próprio código de desmontagem, e o depurador não sabe qual código você deseja exibir. A caixa de diálogo `Resolve Ambiguity` permite que você selecione o local desejado de uma lista de todos os locais correspondentes.  
  
 `Choose the specific location`  
 Lista todos os lugares que correspondem ao comando.  
  
 `Address`  
 Mostra os endereços de memória para cada função.  
  
 `Function`  
 Mostra o nome de cada função.  
  
 `Module`  
 Mostra o módulo (EXE ou DLL) que contém o código de objeto para a função.  
  
## <a name="see-also"></a>Consulte também  
 [Expressões no depurador](../debugger/expressions-in-the-debugger.md)



