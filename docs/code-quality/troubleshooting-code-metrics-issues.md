---
title: Solucionando problemas de métricas do código
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: troubleshooting
ms.assetid: f2fdb995-4888-4246-85dc-7bacadd45968
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9575020135846edc9cb86bd89ff72682500d8a9d
ms.sourcegitcommit: 159ed9d4f56cdc1dff2fd19d9dffafe77e46cd4e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2018
ms.locfileid: "53739556"
---
# <a name="troubleshooting-code-metrics-issues"></a>Solucionando problemas de métricas do código
Você pode encontrar alguns dos problemas a seguir ao coletar as métricas de código:

-   [Alterações nos cálculos de complexidade de código do Visual Studio 2010](#Changes_in_Visual_Studio_2010_code_complexity_calculations)

##  <a name="Changes_in_Visual_Studio_2010_code_complexity_calculations"></a>Alterações nos cálculos de complexidade de código do Visual Studio 2010
 Para a mesma função, a métrica de complexidade do código calculada em [!INCLUDE[vs_dev10_long](../code-quality/includes/vs_dev10_long_md.md)] pode ser diferente da métrica calculada por versões anteriores do [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] nas seguintes situações:

- A função contém um ou mais blocos catch. Nas versões anteriores do [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)], os blocos catch não foram incluídos no cálculo. Em [!INCLUDE[vs_dev10_long](../code-quality/includes/vs_dev10_long_md.md)], a complexidade de cada bloco catch é adicionada à complexidade da função.

- A função contém uma instrução de opção (selecione o caso em VB). Diferenças de compilador entre [!INCLUDE[vs_dev10_long](../code-quality/includes/vs_dev10_long_md.md)] e versões anteriores podem gerar códigos MSIL diferentes para algumas instruções de opção que contêm casos com falhas.

## <a name="see-also"></a>Consulte também
 [Medindo complexidade e facilidade de manutenção do código gerenciado](../code-quality/code-metrics-values.md)