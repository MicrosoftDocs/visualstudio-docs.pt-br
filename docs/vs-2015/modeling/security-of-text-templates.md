---
title: Segurança de modelos de texto | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- text templates, security
ms.assetid: 567a2383-7d43-4acc-af4a-cd70b7a0151e
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 65b4b6616921dae0abb0bb54316d8b8262d1f652
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49214676"
---
# <a name="security-of-text-templates"></a>Segurança de modelos de texto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Modelos de texto têm as seguintes preocupações de segurança:  
  
-   Modelos de texto são vulneráveis a inserções de código arbitrário.  
  
-   Se o mecanismo que o host usa para encontrar um processador de diretriz não é seguro, um processador de diretriz mal-intencionado pode ser executado.  
  
## <a name="arbitrary-code"></a>Código arbitrário  
 Quando você escreve um modelo, você pode colocar qualquer código dentro de \<# # > marcas. Isso permite que o código arbitrário ser executado em um modelo de texto.  
  
 Certifique-se de que obter modelos de fontes confiáveis. Certifique-se avisar os usuários finais do seu aplicativo para não executar modelos que não vêm de fontes confiáveis.  
  
## <a name="malicious-directive-processor"></a>Processador de diretriz mal-intencionados  
 O mecanismo de modelo de texto interage com um host de transformação e um ou mais processadores de diretriz para transformar o texto do modelo para um arquivo de saída. Para obter mais informações, consulte [o processo de transformação de modelo de texto](../modeling/the-text-template-transformation-process.md).  
  
 Se o mecanismo que o host usa para encontrar um processador de diretriz não é seguro, ele corre o risco da execução de um processador de diretriz mal-intencionado. O processador de diretriz mal-intencionado poderia fornecer código que é executado em `FullTrust` modo quando o modelo é executado. Se você criar um host de transformação do modelo de texto personalizado, você deve usar um mecanismo seguro, como o registro, para o mecanismo localizar os processadores de diretriz.



