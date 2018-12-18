---
title: erros de FxCopCmd
ms.date: 10/19/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
helpviewer_keywords:
- FxCopCmd errors
ms.author: gewarren
author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 71e2a39b792dcc5a01eb28611664736f6620bb1f
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2018
ms.locfileid: "47474578"
---
# <a name="fxcopcmd-tool-errors"></a>Erros de ferramenta de FxCopCmd

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

**Erro de análise** é retornado para erros fatais. Ele indica que a análise não pôde ser concluída. Quando aplicável, o código de erro também contém a causa do erro fatal. As condições a seguir geram erros fatais:

- A análise não pôde ser executada devido a entrada insuficiente.

- A análise gerou uma exceção não tratada pelo FxCopCmd.

- O arquivo de projeto especificado não pôde ser encontrado ou está corrompido.

- A opção de saída não foi especificada ou não foi possível gravar o arquivo.

> [!NOTE]
> Código de retorno de FxCopCmd **erro faz referência a Assembly** 0x200 por si só é um aviso em vez de um erro. Esse código de retorno indica que estiverem faltando referências indiretas, mas que FxCopCmd foi capaz de lidar com eles. O aviso significa que há uma possibilidade de que alguns resultados de análise podem ter sido comprometidos. Tratar **erro faz referência a Assembly** como um erro quando ele é combinado com qualquer outro código de retorno.

## <a name="see-also"></a>Consulte também

- [Erros de aplicativo de análise de código](../code-quality/code-analysis-application-errors.md)