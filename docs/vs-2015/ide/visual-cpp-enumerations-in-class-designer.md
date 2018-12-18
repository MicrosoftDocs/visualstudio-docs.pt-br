---
title: Enumerações do Visual C++ no Designer de Classe | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Class Designer [Visual Studio], enumerations
ms.assetid: 11e90ba1-18cd-44f8-9e26-e3746a7a19d1
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: b9d88cb954e89cfd6401f674fbbbc901ac634982
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49236347"
---
# <a name="visual-c-enumerations-in-class-designer"></a>Enumerações do Visual C++ no Designer de Classe
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Designer de Classe oferece suporte ao `enum` do C++ e a tipos `enum class` de escopo. Veja um exemplo a seguir:  
  
```  
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
  
 Para obter mais informações sobre o uso do tipo `enum`, consulte [Enumerações](http://msdn.microsoft.com/library/081829db-5dca-411e-a53c-bffef315bcb3).  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com código do Visual C++ (Designer de Classe)](../ide/working-with-visual-cpp-code-class-designer.md)   
 [Enumerações](http://msdn.microsoft.com/library/081829db-5dca-411e-a53c-bffef315bcb3)



