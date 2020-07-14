---
title: Usar uma política de check-in de análise de código
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- code analysis, check-in policies
ms.assetid: d1b3b04f-4dd9-40e6-b2d4-b414d33fb647
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 883b5e231036c446c1cbf1fbc2fc125a01b3de62
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371853"
---
# <a name="how-to-enforce-maintainable-code-with-a-code-analysis-check-in-policy"></a>Como impor código passível de manutenção com uma política de check-in de análise de código

Os desenvolvedores podem usar a ferramenta de métricas de código para medir a complexidade e a manutenção de seu código, mas você não pode invocar as métricas de código como parte de uma política de check-in. No entanto, você pode habilitar regras de análise de código que verificam a conformidade do seu código com padrões de métricas de código e impõem as regras por meio de políticas de check-in. Para obter mais informações sobre métricas de código, consulte [valores de métricas de código](../code-quality/code-metrics-values.md).

Você pode habilitar a profundidade de herança, acoplamento de classes, índice de manutenção e regras de complexidade para impor o código passível de manutenção por meio de uma política de check-in de análise de código. Todas as quatro regras são encontradas na categoria "regras de manutenção" no editor de política de análise de código.

Os administradores do controle de versão do Team Foundation podem adicionar as regras de manutenção da análise de código aos requisitos da política de check-in. Essas políticas de check-in exigem que os desenvolvedores executem a análise de código com base nessas alterações de regra antes de iniciar um check-in.

## <a name="to-open-the-code-analysis-policy-editor"></a>Para abrir o editor de políticas de análise de código

1. Em **Team Explorer**, clique com o botão direito do mouse no projeto, clique em **configurações do projeto**e clique em **controle do código-fonte**.

     A caixa de diálogo **controle do código-fonte** é exibida.

2. Na guia **política de check-in** e clique em **Adicionar**.

     A caixa de diálogo **Adicionar política de check-in** é exibida.

3. Na lista **política de check-in** , marque a caixa de seleção **análise de código** e clique em **OK**.

     A caixa de diálogo **Editor de políticas de análise de código** é exibida.

## <a name="to-enable-code-analysis-maintainability-rules"></a>Para habilitar regras de manutenção da análise de código

1. Na caixa de diálogo **Editor de políticas de análise de código** , em configurações de **regra**, expanda o nó **regras de manutenção** .

2. Marque as caixas de seleção para as seguintes regras:

   - Profundidade de herança: **CA1501 AvoidExcessiveInheritance** -Threshold: aviso em mais de 5 níveis de profundidade

   - Complexidade: **CA1502 AvoidExcessiveComplexity** -Threshold: aviso em mais de 25

   - Índice de facilidade de manutenção: **CA1505 AvoidUnmaintainableCode** -Threshold: aviso em menos de 20

   - Acoplamento de classe: **CA1506 AvoidExcessiveClassCoupling** -Threshold: aviso em mais de 80 para uma classe e mais de 30 para um método

     Além disso, se você quiser uma violação de regra para impedir uma compilação bem-sucedida, marque a caixa de seleção **tratar aviso como um erro** ao lado da descrição da regra.

3. Clique em **OK**. A nova política de check-in agora se aplica a check-ins futuros.

## <a name="see-also"></a>Veja também

- [Valores de métricas de código](../code-quality/code-metrics-values.md)
- [Criando e usando políticas de check-in de análise de código](../code-quality/how-to-create-or-update-standard-code-analysis-check-in-policies.md)
