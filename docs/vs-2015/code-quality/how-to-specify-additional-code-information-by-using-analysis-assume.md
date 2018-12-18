---
title: 'Como: especificar informações de código adicionais usando analysis_assume | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- __analysis_assume
helpviewer_keywords:
- __analysis_assume
ms.assetid: 51205d97-4084-4cf4-a5ed-3eeaf67deb1b
caps.latest.revision: 12
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: de4d70dc615c14e9f9355608fa6b352b799c2c1a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51776896"
---
# <a name="how-to-specify-additional-code-information-by-using-analysisassume"></a>Como especificar informações de código adicionais usando __analysis_assume
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode fornecer dicas para a ferramenta de análise de código para código C/C++ que ajudam no processo de análise e reduzir os avisos. Para fornecer informações adicionais, use a função a seguir:  
  
 `__analysis_assume(`  `expr`  `)`  
  
 `expr` -qualquer expressão supostamente avaliada como true.  
  
 A ferramenta de análise de código pressupõe que a condição representada pela expressão é verdadeira no ponto em que a função aparece e permanece verdadeira até que a expressão for alterada, por exemplo, por atribuição a uma variável.  
  
> [!NOTE]
>  `__analysis_assume` não afeta a otimização de código. Fora a ferramenta de análise de código, `__analysis_assume` é definido como inoperante.  
  
## <a name="example"></a>Exemplo  
 O seguinte código usa `__analysis_assume` para corrigir o aviso de análise de código [C6388](../code-quality/c6388.md):  
  
```  
#include<windows.h>  
#include<codeanalysis\sourceannotations.h>  
  
using namespace vc_attributes;  
  
// calls free and sets ch to null  
void FreeAndNull(char* ch);  
  
//requires pc to be null  
void f([Pre(Null=Yes)] char* pc);  
  
void test( )  
{  
  char *pc = (char*)malloc(5);  
  FreeAndNull(pc);  
  __analysis_assume(pc == NULL);   
  f(pc);  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [__assume](http://msdn.microsoft.com/library/d8565123-b132-44b1-8235-5a8c8bff85a7)



