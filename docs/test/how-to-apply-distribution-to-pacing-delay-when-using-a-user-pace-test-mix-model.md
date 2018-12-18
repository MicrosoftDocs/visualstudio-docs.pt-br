---
title: Aplicar distribuição aos atrasos de ritmo para testes de carga
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, test mix model
ms.assetid: ae8b35f9-d465-4d72-8d7d-7b56ae6ffd22
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 19634186e13574c322c2e9bcc636dda3a823b158
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896180"
---
# <a name="how-to-apply-distribution-to-pacing-delay-for-a-user-pace-test-mix-model"></a>Como aplicar distribuição à definição dos atrasos durante o uso de um modelo de combinação de testes

Depois de criar seu teste de carga usando o **Novo Assistente de Teste de Carga**, você poderá usar o Editor de Teste de Carga para alterar as propriedades de cenários para que eles atendam às suas metas e necessidades de teste.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

A propriedade **Aplicar Distribuição à Definição dos Atrasos** é definida usando a janela **Propriedades**. As propriedades do cenário de teste de carga são modificadas usando o Editor de testes de carga.

> [!NOTE]
> A propriedade **Aplicar distribuição à definição dos atrasos** se aplica apenas se a *combinação de testes de carga* for configurada com base no ritmo do usuário. Para saber mais, veja [Editar modelos de combinação de texto para especificar a probabilidade de um usuário virtual executar um teste](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md).

O valor de **Aplicar distribuição à definição dos atrasos** pode ser definido como verdadeiro ou falso:

- **Verdadeiro**: o cenário aplica atrasos de distribuição estatística normal que são especificados pelo valor na coluna **Testes por usuário por hora** na caixa de diálogo **Editar combinação de testes**. Para saber mais, veja [Editar modelos de combinação de texto para especificar a probabilidade de um usuário virtual executar um teste](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md).

     Por exemplo, vamos supor que você tenha o valor de **Testes por Usuário por Hora** na caixa de diálogo **Editar Combinação de Testes** definido como dois usuários por hora. Se a propriedade de **Aplicar distribuição à definição dos atrasos** for definida como **Verdadeiro**, uma distribuição estatística normal será aplicada ao tempo de espera entre os testes. Os testes ainda serão executados duas vezes por hora, mas não haverá necessariamente um atraso de 30 minutos entre eles. O primeiro teste pode ser executado depois de quatro minutos e o segundo teste, depois de 45 minutos.

- **Falso**: os testes são executados no ritmo que você especificou para o valor na coluna **Testes por usuário por hora** na caixa de diálogo **Editar Combinação de Testes**. Para saber mais, veja [Editar modelos de combinação de texto para especificar a probabilidade de um usuário virtual executar um teste](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md).

     Por exemplo, vamos supor que você tenha o valor de **Testes por Usuário por Hora** na caixa de diálogo **Editar Combinação de Testes** definido como dois usuários por hora. Se a propriedade de **Aplicar distribuição à definição dos atrasos** for definida como **Falso**, não haverá intervalo na execução dos testes. O teste será executado a cada 30 minutos. Isso garante que você execute dois testes por hora.

## <a name="to-specify-the-apply-distribution-to-pacing-delay-property-setting-for-a-scenario"></a>Para especificar a propriedade Aplicar distribuição à definição dos atrasos para um cenário

1. Abra um teste de carga.

   O **Editor de Teste de Carga** é exibido. A árvore do teste de carga é exibida.

2. Na pasta **Cenários** da árvore de teste de carga, escolha o nó de cenário ao qual você deseja aplicar a distribuição de adequação.

3. No menu **Exibir**, selecione **Janela de Propriedades**.

   As categorias e as propriedades do cenário são exibidas na janela **Propriedades**.

4. No valor da propriedade **Aplicar distribuição à definição dos atrasos**, selecione **Verdadeiro** ou **Falso**.

5. Selecione **Arquivo** > **Salvar**. Agora, você pode executar o teste de carga usando o novo valor de **Aplicar Distribuição à Definição dos Atrasos**.

## <a name="see-also"></a>Consulte também

- [Editar cenários de teste de carga](../test/edit-load-test-scenarios.md)
- [Passo a passo: criar e executar um teste de carga](../test/walkthrough-create-and-run-a-load-test.md)
- [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md)
- [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md)