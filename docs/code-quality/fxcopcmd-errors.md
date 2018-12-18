---
title: erros de FxCopCmd
ms.date: 10/19/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
helpviewer_keywords:
- FxCopCmd errors
ms.assetid: bb614ed0-1b7c-4b56-99ae-da50ef6cfef9
ms.author: gewarren
author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 657e650f9244fb97d4990e04a60b9e1f93794af4
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31924255"
---
# <a name="fxcopcmd-tool-errors"></a>Erros de ferramenta (fxcopcmd)

FxCopCmd não considera todos os erros para ser fatal. Se FxCopCmd tem informações suficientes para executar uma análise parcial, ele executa as análise e relatórios de erros que ocorreram. O código de erro, que é um inteiro de 32 bits, contém uma combinação bit a bit de valores numéricos que correspondem a erros.

A tabela a seguir descreve os códigos de erro retornados por FxCopCmd:

|Erro|Valor numérico|
|-----------|-------------------|
|Sem erros|0x0|
|Erro de análise|0x1|
|Exceções de regra|0x2|
|Erro ao carregar projeto|0x4|
|Erro ao carregar assembly|0x8|
|Erro ao carregar biblioteca regra|0x10|
|Erro de carregamento do relatório de importação|0x20|
|Erro de saída|0x40|
|Erro de chave de linha de comando|0x80|
|Erro de inicialização|0x100|
|Erro de referências de assembly|0x200|
|BuildBreakingMessage|0x400|
|Erro desconhecido|0x1000000|

**Erro de análise** é retornada para erros fatais. Ele indica que não foi possível concluir a análise. Quando aplicável, o código de erro também contém a causa do erro fatal. As condições a seguir geram erros fatais:

- Não foi possível executar a análise devido à entrada insuficiente.

- A análise gerou uma exceção não tratada pelo FxCopCmd.

- O arquivo de projeto especificado não pôde ser encontrado ou está corrompido.

- A opção de saída não foi especificada ou não foi possível gravar o arquivo.

> [!NOTE]
> Código de retorno de FxCopCmd **erro as referências a Assembly** 0x200 por si só é um aviso em vez de um erro. O código de retorno indica que há ausentes referências indiretas, mas que FxCopCmd foi capaz de lidar com eles. O aviso significa que há uma possibilidade de que alguns resultados de análise podem ter sido comprometidos. Tratar **erro as referências a Assembly** como um erro quando ele é combinado com qualquer outro código de retorno.

## <a name="see-also"></a>Consulte também

- [Erros de aplicativo de análise de código](../code-quality/code-analysis-application-errors.md)