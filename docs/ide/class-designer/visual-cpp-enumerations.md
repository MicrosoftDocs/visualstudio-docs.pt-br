---
title: Enumerações do Visual C++ no Designer de Classe
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Class Designer [Visual Studio], enumerations
ms.assetid: 11e90ba1-18cd-44f8-9e26-e3746a7a19d1
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: a42dfb65cc70704bbed662e35b2e2eb0e9c237c4
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31922014"
---
# <a name="visual-c-enumerations-in-class-designer"></a>Enumerações do Visual C++ no Designer de Classe

O **Designer de Classe** é compatível com os tipos `enum` e `enum class` no escopo do C++. Veja um exemplo a seguir:

```cpp
enum CardSuit {
   Diamonds = 1,
   Hearts = 2,
   Clubs = 3,
   Spades = 4
};

// or...
enum class CardSuit {
   Diamonds = 1,
   Hearts = 2,
   Clubs = 3,
   Spades = 4
};
```

Uma forma de enumeração do C++ em um diagrama de classes parece e funciona como uma forma de estrutura, exceto pelo seguinte: o rótulo exibe **Enum** ou **Enum class**, ele é rosa em vez de azul e tem uma borda colorida nas margens esquerda e superior. As formas de enumeração e formas de estrutura tem cantos quadrados.

Para obter mais informações sobre o uso do tipo `enum`, consulte [Enumerações](/cpp/cpp/enumerations-cpp).

## <a name="see-also"></a>Consulte também

- [Trabalhando com código do Visual C++](working-with-visual-cpp-code.md)
- [Enumerações](/cpp/cpp/enumerations-cpp)