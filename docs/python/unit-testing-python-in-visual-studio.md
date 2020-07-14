---
title: Teste de unidade do código Python
description: A configuração do teste de unidade para o código Python no Visual Studio aproveita ao máximo as funcionalidades do Gerenciador de Testes para descobrir, executar e depurar testes.
ms.date: 09/18/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 2a621cd56f980c8a1404ba8855cdf3544e58d39d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535311"
---
# <a name="set-up-unit-testing-for-python-code"></a>Configurar o teste de unidade para o código do Python

Testes de unidade são partes do código que testam outras unidades de código em um aplicativo, normalmente, funções isoladas, classes e assim por diante. Quando um aplicativo é aprovado em todos os seus testes de unidade, pelo menos, é possível confiar que sua funcionalidade de baixo nível está correta.

O Python usa testes de unidade extensivamente para validar cenários durante a criação de um programa. O suporte do Python no Visual Studio inclui a descoberta, a execução e a depuração de testes de unidade no contexto do processo de desenvolvimento, sem precisar executar os testes separadamente.

Este artigo fornece uma breve descrição das funcionalidades de teste de unidade no Visual Studio com o Python. Para obter mais informações sobre testes de unidade em geral, consulte [Executar um teste de unidade no código](../test/unit-test-your-code.md).

::: moniker range="vs-2017"

[!include[Testing Python code](includes/vs-2017/unit-testing-python.md)]

::: moniker-end

::: moniker range=">= vs-2019"

[!include[Testing Python code](includes/vs-2019/unit-testing-python.md)]

::: moniker-end