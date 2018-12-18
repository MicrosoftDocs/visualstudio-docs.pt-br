---
title: Usando o gráfico de atividade de usuário virtual em testes de carga
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, virtual user activity chart
- virtual user activity chart, isolating performance issues
ms.assetid: d1c10fb9-cfeb-4e7f-9991-2d1e1103699e
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 8e4584d386cb61aaf7809c8bb5ab748e49543c7e
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895919"
---
# <a name="walkthrough-using-the-virtual-user-activity-chart-to-isolate-issues"></a>Passo a passo: Usando o Gráfico de Atividade de Usuário Virtual para isolar problemas

Neste passo a passo, você aprenderá a usar o Gráfico de Atividade de Usuário Virtual para isolar os erros que ocorreram para os usuários virtuais individuais que executaram seu teste de carga.

O Gráfico de Atividade de Usuário Virtual permite visualizar a atividade de usuário virtual que está associada ao teste de carga. Cada linha do gráfico representa um usuário virtual individual. O Gráfico de Atividade de Usuário Virtual mostra exatamente o que cada usuário virtual executou durante o teste. Isso permite isolar problemas de desempenho vendo padrões de atividade de usuário, padrões de carga, correlação de testes reprovados ou lentos, e ver as solicitações com outra atividade de usuário virtual. O Gráfico de Atividade de Usuário Virtual está disponível apenas depois da conclusão da execução do teste de carga.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="prerequisites"></a>Pré-requisitos

-   Visual Studio Enterprise

-   Complete esses procedimentos:

    -   [Gravar e executar um teste de desempenho Web](/azure/devops/test/load-test/run-performance-tests-app-before-release#recordtests).

    -   [Criar e executar um teste de carga](/azure/devops/test/load-test/run-performance-tests-app-before-release#create-a-load-test)

## <a name="open-the-colorwebapp-solution-created-in-the-previous-walkthroughs"></a>Abrir a solução ColorWebApp criada nos passo a passo anteriores

1.  Inicie o Visual Studio.

2.  Abra a solução **ColorWebApp** que contém o *LoadTest1.loadtest*. Este teste de carga é resultado da execução das etapas nas três explicações passo a passo listadas no início deste tópico na seção de pré-requisitos.

     As etapas restantes deste passo a passo pressupõem a existência de um aplicativo Web chamado ColorWebApp, um teste de desempenho Web chamado *ColorWebAppTest.webtest* e um teste de carga chamado *LoadTest1.loadtest*.

## <a name="run-the-load-test"></a>Executar o teste de carga

Execute o teste de carga para coletar dados da atividade de usuário virtual.

-   No **Editor de Teste de Carga**, escolha o botão **Executar** na barra de ferramentas. A execução de LoadTest1 iniciará.

## <a name="isolate-issues-in-the-virtual-user-activity-chart"></a>Isolar problemas no Gráfico de Atividade de Usuário Virtual

Após a execução do teste de carga e a coleta dos dados de atividade de usuário virtual, você poderá ver os dados nos resultados do teste de carga usando a exibição Detalhes do **Analisador de Teste de Carga** no **Gráfico de Atividade de Usuário Virtual**. Além disso, você pode usar o **Gráfico de Atividade de Usuário Virtual** para ajudar a isolar problemas de desempenho no teste de carga.

### <a name="to-use-the-virtual-user-activity-chart-in-your-load-test-results"></a>Para usar o Gráfico de Atividade de Usuário Virtual nos resultados do teste de carga

1.  Após a execução do teste de carga, a página **Resumo** dos resultados do teste de carga é exibida no **Analisador de Teste de Carga**. Escolha o botão **Gráficos** na barra de ferramentas.

     A exibição Gráficos será mostrada.

2.  No gráfico **Tempo de Resposta de Página**, clique com o botão direito do mouse em um dos ícones de violação de limite e selecione **Ir para detalhe do usuário**.

    > [!NOTE]
    > Use também o botão **Detalhes** na barra de ferramentas do **Editor de Teste de Carga** para abrir o gráfico de Atividade do Usuário. No entanto, se você usar a opção **Ir para detalhe do usuário**, o **Gráfico de Atividade de Usuário Virtual** ampliará automaticamente a parte do teste em que você clicou com o botão direito do mouse no grafo.

     A exibição Detalhes é exibida com o **Gráfico de atividade do usuário virtual** focado no período em que as violações de limite ocorreram.

     No eixo y, os traços horizontais representam usuários virtuais individuais. O eixo x exibe a linha do tempo da execução do teste de carga.

3.  Na ferramenta **Zoom para o período de tempo** abaixo do **Gráfico de atividade do usuário virtual**, ajuste os controles deslizantes à esquerda e à direita até que ambos estejam próximos ao ícone de violação de limite. Isso altera a escala de tempo no **Gráfico de atividade do usuário virtual**

4.  Na **Legenda de detalhes**, marque a caixa de seleção **(Realçar de erros)**. Observe que o usuário virtual que causou a violação de limite está realçado.

5.  No painel **Filtrar resultados**, desmarque as caixas de seleção **Mostrar resultados bem-sucedidos** e **HttpError**, mas deixe a caixa de seleção **ValidationRuleError** marcada.

     O **Gráfico de Atividade de Usuário Virtual** exibe apenas os usuários virtuais que passaram mais de 3 segundos na página *Red.aspx*, conforme especificado pela violação de limite configurada no passo a passo anterior.

6.  Coloque o ponteiro do mouse na linha horizontal que representa o usuário virtual com o erro da regra de validação da violação de limite.

7.  Uma dica de ferramenta é exibida com as seguintes informações:

    -   **ID de usuário**

    -   **Cenário**

    -   **Teste**

    -   **Resultado**

    -   **Network**

    -   **Hora de início**

    -   **Duração**

    -   **Agente**

    -   **Log de teste**

8.  Observe que **Log de teste** é um link. Escolha o link **Log de teste**.

9. O teste de desempenho Web ColorWebTest associado ao log é aberto no **Visualizador de Resultados de Teste de Desempenho Web**. Isso permite isolar onde as violações de limite ocorreram.

     É possível usar várias configurações nos painéis **Legenda de detalhes** e **Filtrar resultados** para ajudar a isolar problemas de desempenho e erros nos testes de carga. Experimente essas configurações e a ferramenta **Zoom para o período de tempo** para ver como os dados do usuário virtual são apresentados no **Gráfico de atividade do usuário virtual**.

## <a name="see-also"></a>Consulte também

- [Analisando a atividade do usuário virtual na exibição Detalhes](../test/analyze-load-test-virtual-user-activity-in-the-details-view.md)
- [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md)
- [Como criar uma configuração de teste para um teste de carga distribuída](../test/how-to-create-a-test-setting-for-a-distributed-load-test.md)
- [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md)
- [Coletar informações de diagnóstico usando configurações de teste](../test/collect-diagnostic-information-using-test-settings.md)
