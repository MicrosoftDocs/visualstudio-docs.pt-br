---
title: Modelos padrão XSLT | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 773dd34e-67d3-4997-8df9-b71e7f880d88
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4a26349a60c40552d350f156bf1109544a03d411
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49181344"
---
# <a name="xslt-default-templates"></a>Modelos de opção XSLT
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um modelo padrão será usado durante XSLT que processa quando não há nenhuma regra explícita modelo correspondente da folha de estilos. O modelo padrão, também conhecido como regra de modelo interno, é definido na seção 5,8 de recomendação W3C XSLT 1,0. O modelo padrão permite que o processador XSLT processe um nó, mesmo que não haja nenhuma regra explícita de modelo que corresponde a ele. Entretanto, porque a regra de modelo interno não é explicitamente definida na folha de estilos, isso pode levar a resultados inesperados ou confundindo de transformação XSLT.  
  
 O depurador XSLT agora exibe o código de modelos de opção XSLT. Quando você percorre uma transformação XSLT, se um modelo padrão é usado, o depurador exibe o modelo padrão em uma janela. Isso permite que você percorrer o código de modelo padrão e os pontos de interrupção em suas declarações.  
  
## <a name="see-also"></a>Consulte também  
 [Depuração de XSLT](../xml-tools/debugging-xslt.md)

