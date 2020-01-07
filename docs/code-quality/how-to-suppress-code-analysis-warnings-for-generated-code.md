---
title: Suprimir violações de análise de código para código gerado
ms.date: 05/13/2019
ms.topic: conceptual
ms.assetid: 3a96434e-d419-43a7-81ba-95cccac835b8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9ab2ffce28103059414cef8f1b556152485a12ff
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2020
ms.locfileid: "75587427"
---
# <a name="how-to-suppress-code-analysis-warnings-for-generated-code"></a>Como: suprimir avisos de análise de código para código gerado

O código gerado inclui o código que é adicionado ao seu projeto por compiladores de código gerenciado ou por ferramentas de terceiros. Talvez você queira ver as violações de regra que a análise de código descobre no código gerado. No entanto, como não é possível exibir e manter o código que contém as violações, talvez você não queira vê-las.

A caixa de seleção **suprimir resultados do código gerado** na página de propriedades análise de código de um projeto permite que você selecione se deseja mostrar avisos de análise de código do código gerado por uma ferramenta de terceiros.

> [!NOTE]
> Essa opção não suprime erros de análise de código e avisos do código gerado quando os erros e avisos que aparecem em formulários e modelos. Você pode exibir e manter o código-fonte de um formulário ou de um modelo.

### <a name="to-suppress-warnings-for-generated-code-in-a-project"></a>Para suprimir avisos de código gerado em um projeto

1. Clique com o botão direito do mouse no projeto em **Gerenciador de soluções** e clique em **Propriedades**.

2. Escolha a guia **análise de código** .

3. Marque a caixa de seleção **suprimir resultados do código gerado** .

> [!IMPORTANT]
> Você só pode suprimir avisos da análise herdada. A página de propriedades com a configuração foi preterida e será removida em uma versão futura do produto. No momento, não é possível suprimir avisos de análise de código de [analisadores](roslyn-analyzers-overview.md).
