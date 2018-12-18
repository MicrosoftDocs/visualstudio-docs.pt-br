---
title: Erros de FxCopCmd | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FxCopCmd errors
ms.assetid: bb614ed0-1b7c-4b56-99ae-da50ef6cfef9
caps.latest.revision: 12
ms.author: mikejo
manager: douge
ms.openlocfilehash: 828805e0746fb985ea310b755cdaaa252e215a07
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51751724"
---
# <a name="fxcopcmd-errors"></a>Erros (FxCopCmd)
FxCopCmd não considera todos os erros fatais. Se o FxCopCmd tem informações suficientes para executar uma análise parcial, ele executa as análise e relatórios de erros que ocorreram. O código de erro, que é um inteiro de 32 bits, contém uma combinação bit a bit de valores numéricos que correspondem aos erros.  
  
 A tabela a seguir descreve os códigos de erro retornados pelo FxCopCmd:  
  
|Erro|Valor numérico|  
|-----------|-------------------|  
|Nenhum erro|0x0|  
|Erro de análise|0x1|  
|Exceções de regra|0x2|  
|Erro ao carregar projeto|0x4|  
|Erro de carregamento de assembly|0x8|  
|Erro ao carregar biblioteca regra|0x10|  
|Erro de importação de carga de relatório|0x20|  
|Erro de saída|0x40|  
|Erro de opção de linha de comando|0x80|  
|Erro de inicialização|0x100|  
|Erro de referências de assembly|0x200|  
|BuildBreakingMessage|0x400|  
|Erro desconhecido|0x1000000|  
  
 O erro de análise é retornado para erros fatais. Ele indica que a análise não pôde ser concluída. Quando aplicável, o código de erro também contém a causa do erro fatal. As condições a seguir geram erros fatais:  
  
-   A análise não pôde ser executada provocadas por entrada insuficiente.  
  
-   A análise gerou uma exceção não tratada pelo FxCopCmd.  
  
-   O arquivo de projeto especificado não pôde ser encontrado ou está corrompido.  
  
-   A opção de saída não foi especificada ou não foi possível gravar o arquivo.  
  
    > [!NOTE]
    >  O FxCopCmd retornar o código de "Erro de referências de Assembly" 0x200 por si só é um aviso em vez de um erro. Esse código de retorno indica que referências indiretas ausentes foram encontradas, mas que FxCopCmd foi capaz de lidar com eles. É um aviso de que há uma possibilidade de que alguns resultados de análise podem ter sido comprometidos. Considere o código de retorno de "Erro de referências de Assembly" como um erro quando ele é combinado com qualquer outro código de retorno.  
  
## <a name="see-also"></a>Consulte também  
 [Erros de aplicativo de análise de código](../code-quality/code-analysis-application-errors.md)