---
title: Tempo de rampa de etapa para um padrão de carga de etapa em teste de carga
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, load patterns
ms.assetid: 4a69e857-f93b-4907-9a01-fd1b66291205
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5ae00c3d9d647eff6f9df448c1681ae1d6c54bcb
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287318"
---
# <a name="how-to-specify-the-step-ramp-time-property-for-a-step-load-pattern"></a>Como especificar a propriedade de tempo de rampa de etapa para um padrão de carga de etapa

Depois de criar seu teste de carga com o **Novo Assistente de Teste de Carga**, você poderá usar o **Editor de Teste de Carga** para alterar as propriedades de cenários para que eles atendam às suas metas e necessidades de teste. Para obter mais informações, consulte [Passo a passo: criar e executar um teste de carga](../test/walkthrough-create-and-run-a-load-test.md).

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> Para obter uma lista completa das propriedades de cenário de teste de carga e suas descrições, confira [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md).

A propriedade **time da rampa de etapas** é definida na janela **Propriedades** . Edite as propriedades de cenário de teste de carga no **Editor de Teste de Carga**.

A propriedade **Tempo de rampa de etapa** é usada apenas com um padrão de carga de etapa. Para obter mais informações, confira [Editar padrões de carga para modelar atividades de usuário virtual](../test/edit-load-patterns-to-model-virtual-user-activities.md).

O padrão de carga em etapa é usado para aumentar a carga nos servidores à medida que o teste de carga é executado, de modo que você possa ver como o desempenho varia à medida que a carga de usuários aumenta. Por exemplo, para ver como será o desempenho dos servidores à medida que a carga de usuário aumenta para 2.000 usuários, você pode executar um teste de carga de 10 horas usando um padrão de carga em etapa com as seguintes propriedades:

- Contagem inicial de usuários: 100

- Contagem máxima de usuários: 2000

- Duração da etapa (segundos): 1800

- Tempo de rampa de etapa (segundos): 20

- Contagem de usuário em etapas: 100

Essas configurações têm o teste de carga em execução por 30 minutos (1.800 segundos) nas cargas de 100, 200, 300, até 2.000 usuários.

> [!NOTE]
> A propriedade **time da rampa de etapas** é a única dessas propriedades que não está disponível para escolher na **nova assistente de teste de carga**.

A propriedade **Tempo de rampa de etapa** permite que o aumento de uma etapa para a seguinte (por exemplo, de 100 para 200 usuários) seja gradual e não imediata. No exemplo, a carga de usuário seria aumentada de 100 para 200 usuários durante um período de 20 segundos (um aumento de cinco usuários por segundo).

## <a name="to-edit-the-step-ramp-time-property-for-a-step-load-pattern"></a>Para editar a propriedade de tempo de rampa de etapa para um padrão de carga de etapa

1. Abra um teste de carga.

     O **Editor de Teste de Carga** é exibido. A árvore do teste de carga é exibida.

2. Na pasta **Cenários** das árvores de teste de carga, abra o nó do cenário para o qual deseja especificar o tempo de rampa de etapa.

3. Selecione o nó **Padrão de carga de etapa**.

    > [!NOTE]
    > O padrão de carga para o cenário deve ser um padrão de carga em etapa. Caso contrário, o padrão de carga exibirá o tipo de padrão de carga que está atualmente associado ao cenário. Para obter mais informações, confira [Editar padrões de carga para modelar atividades de usuário virtual](../test/edit-load-patterns-to-model-virtual-user-activities.md).

4. No menu **Exibir**, selecione **Janela de Propriedades**.

     As categorias e as propriedades do cenário são exibidas na janela **Propriedades**.

5. Defina o valor para a propriedade **Tempo de rampa de etapa** inserindo um número para os segundos usados em cada etapa para adicionar gradualmente os usuários especificados pela propriedade **Contagem de usuário em etapas**.

6. Depois de alterar a propriedade, escolha **Salvar** no menu **Arquivo**. Em seguida, você pode executar o teste de carga usando o novo valor de **Tempo de rampa de etapa**.

## <a name="see-also"></a>Veja também

- [Editar cenários de teste de carga](../test/edit-load-test-scenarios.md)
- [Controladores de teste e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md)
- [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md)
- [Editar padrões de carga para modelar atividades de usuário virtual](../test/edit-load-patterns-to-model-virtual-user-activities.md)
