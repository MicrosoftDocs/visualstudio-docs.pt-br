---
title: Solução de problemas de métricas de código | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f2fdb995-4888-4246-85dc-7bacadd45968
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 2cc5c586e1e994ff2e14710b39c04bb424b770d2
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51800634"
---
# <a name="troubleshooting-code-metrics-issues"></a>Solucionando problemas de métricas do código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode encontrar alguns dos problemas a seguir ao coletar as métricas de código:  
  
-   [Alterações nos cálculos de complexidade de código do Visual Studio 2010](#Changes_in_Visual_Studio_2010_code_complexity_calculations)  
  
##  <a name="Changes_in_Visual_Studio_2010_code_complexity_calculations"></a>Alterações nos cálculos de complexidade de código do Visual Studio 2010  
 Para a mesma função, a métrica de complexidade do código calculada em [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] pode ser diferente da métrica calculada por versões anteriores do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] nas seguintes situações:  
  
-   A função contém um ou mais blocos catch. Nas versões anteriores do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)], os blocos catch não foram incluídos no cálculo. Em [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)], a complexidade de cada bloco catch é adicionada à complexidade da função.  
  
-   A função contém uma instrução de opção (selecione o caso em VB). Diferenças de compilador entre [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] e versões anteriores podem gerar códigos MSIL diferentes para algumas instruções de opção que contêm casos com falhas.  
  
## <a name="see-also"></a>Consulte também  
 [Medindo complexidade e facilidade de manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)



