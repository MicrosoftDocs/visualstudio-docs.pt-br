---
title: Propriedade de armazenamento de detalhes de tempo para uma configuração de execução de teste de carga
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, properties
- load tests, run settings
ms.assetid: 867a9c21-0909-4963-bc02-d41e9393008c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0225ae23ed141b317d4424da573593d446766f43
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287305"
---
# <a name="how-to-specify-the-timing-details-storage-property-for-a-load-test-run-setting"></a>Como especificar a propriedade de armazenamento de detalhes de tempo para uma configuração de execução de teste de carga

Depois de criar seu teste de carga com o **Novo Assistente de Teste de Carga**, você poderá usar o **Editor de Teste de Carga** para alterar as configurações de forma que elas atendam às suas metas e necessidades de teste.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Você pode editar um valor da propriedade **Armazenamento de detalhes de medição de tempo** das configurações de execução na janela **Propriedades**. A propriedade **Armazenamento de detalhes de medição de tempo** pode ser definida como qualquer uma das seguintes opções:

- **Todos os detalhes de individuais:** coleta e armazena dados de tempo individuais para cada teste, transação e página emitidos durante o teste.

  > [!NOTE]
  > A opção **Todos os detalhes individuais** deve ser selecionada para habilitar informações de dados de usuário virtual em seus resultados de teste de carga. Para saber mais, confira [Análise da atividade de usuário virtual na exibição Detalhes](../test/analyze-load-test-virtual-user-activity-in-the-details-view.md).

- **Nenhum:** não coleta detalhes de medição de tempo individuais. No entanto, os valores médios permanecem disponíveis.

- **Apenas estatísticas:** armazena dados de tempo individuais, mas somente como dados em percentis. Isso economiza recursos de espaço.

  **Considerações sobre a propriedade Armazenamento de detalhes de medição de tempo**

  Se a propriedade **Armazenamento de detalhes de medição de tempo** estiver habilitada, o tempo para execução de cada teste, transação e página individual durante o teste de carga será armazenado no repositório de resultados de testes de carga. Isso permite que os dados 90 º e 95 º percentil sejam mostrados no **analisador de testes de carga** nas tabelas **tests**, **Transactions**e **pages** .

  Se a propriedade **Armazenamento de detalhes de medição de tempo** for habilitada, ao configurar seu valor como **StatisticsOnly** ou **AllIndividualDetails**, todos os testes, páginas e transações individuais serão cronometrados e os dados de percentil serão calculados dos dados de medição de tempo individuais. A diferença é que, com a opção **StatisticsOnly**, depois que os dados de percentil são calculados, os dados de tempo individuais são excluídos do repositório. Isso reduz a quantidade de espaço necessário no repositório quando são usados detalhes de medição de tempo. No entanto, convém processar os dados de detalhes de medição de tempo de outras maneiras usando ferramentas SQL. Nesse caso, a opção **AllIndividualDetails** deve ser usada para que os dados de detalhes de tempo estejam disponíveis para esse processamento. Além disso, se você definir a propriedade como **AllIndividualDetails**, poderá analisar a atividade de usuário virtual usando o **gráfico de atividade de usuário virtual** no **analisador de testes de carga** depois que o teste de carga for concluído em execução. Para saber mais, confira [Análise da atividade de usuário virtual na exibição Detalhes](../test/analyze-load-test-virtual-user-activity-in-the-details-view.md).

  A quantidade de espaço necessário no repositório de resultados de teste de carga para armazenar os dados dos detalhes de tempo pode ser muito grande, especialmente para testes de carga mais longos. Além disso, o tempo para armazenar esses dados no repositório de resultados de teste de carga no final do teste é mais longo porque esses dados são armazenados nos agentes de teste de carga até que o teste de carga termine, e esse é o momento em que os dados são armazenados no repositório. A propriedade **Armazenamento de detalhes de medição de tempo** é habilitada por padrão. Se isso for um problema para seu ambiente de teste, você poderá definir o **Armazenamento de detalhes de medição de tempo** como **Nenhum**.

  Os dados dos detalhes de tempo são armazenados no arquivo *LoadTestItemResults.dat* durante a execução e são enviados de volta ao controlador depois que o teste de carga é concluído. Para um teste de carga em execução por muito tempo, o tamanho do arquivo será grande. Se não houver espaço em disco suficiente no computador do agente, isso será um problema.

  Se você estiver atualizando um projeto de uma versão anterior do teste de carga do Visual Studio, use o seguinte procedimento para habilitar a coleta de detalhes completos.

## <a name="to-configure-the-timing-details-storage-property-in-a-load-test"></a>Para configurar a propriedade de armazenamento de detalhes de medição de tempo em um teste de carga

1. Abra um teste de carga no Editor de testes de carga.

2. Expanda o nó **Configurações de execução** no teste de carga.

3. Escolha as configurações de execução que deseja definir, por exemplo **Configurações de Execução1[Ativas]**.

4. Abra a janela **Propriedades** . No menu **Exibir**, selecione **Janela de Propriedades**.

5. Na categoria **Resultados**, escolha a propriedade **Armazenamento de detalhes de medição de tempo** e selecione **Todos os detalhes individuais**.

     Depois de definir a configuração de **todos os detalhes individuais** para a propriedade de **armazenamento de detalhes de tempo** , você pode executar o teste de carga e exibir o gráfico de atividade de **usuário virtual**. Para obter mais informações, consulte [como: analisar o que os usuários virtuais estão fazendo durante um teste de carga](../test/how-to-analyze-virtual-user-activity-during-a-load-test.md).

## <a name="see-also"></a>Veja também

- [Analisando a atividade do usuário virtual na exibição Detalhes](../test/analyze-load-test-virtual-user-activity-in-the-details-view.md)
- [Walkthrough: usando o gráfico de atividade de usuário virtual para isolar problemas](../test/walkthrough-use-the-virtual-user-activity-chart-to-isolate-issues.md)
