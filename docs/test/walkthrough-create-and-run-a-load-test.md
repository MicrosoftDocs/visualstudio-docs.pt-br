---
title: Criar e executar um teste de carga no Visual Studio
ms.date: 10/01/2016
ms.topic: conceptual
helpviewer_keywords:
- unit tests, in load tests
- unit tests, load test walkthrough
- load tests, walkthrough
ms.assetid: bbf075a5-96d5-48ed-a03c-330f0fc04748
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 649fe84b716355f5c7228e371fa88d80937f24af
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895373"
---
# <a name="walkthrough-create-and-run-a-load-test-that-contains-unit-tests"></a>Passo a passo: Criar e executar um teste de carga que contém testes de unidade

Nesta explicação passo a passo você cria um teste de carga que contém testes de unidade.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Esta explicação passo a passo orienta você na criação e execução de um teste de carga usando o Visual Studio Enterprise. Um teste de carga é um contêiner de testes de desempenho na Web e de testes de unidade. Crie testes de carga com o **Novo Assistente de Teste de Carga**.

Um teste de carga também expõe muitas propriedades de tempo de execução que podem ser alteradas para gerar a simulação desejada de carga. Neste passo a passo, você usará o **Novo Assistente de Teste de Carga** para adicionar testes de unidade a um teste de carga.

Nesta explicação passo a passo, você concluirá as seguintes tarefas:

-   Criar um teste de carga que usa testes de unidade.

-   Alterar algumas configurações do teste de carga.

-   Executar um teste de carga.

-   Execute as etapas de [Passo a passo: Criando e executando testes de unidade para código gerenciado](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md) para criar uma biblioteca de classes C# simples que contém um projeto de desempenho Web e de teste de carga com alguns testes de unidade.

## <a name="create-a-load-test-containing-unit-tests-using-the-new-load-test-wizard"></a>Criar um teste de carga que contém testes de unidade usando o Novo Assistente de Teste de Carga

### <a name="to-start-the-new-load-test-wizard"></a>Para iniciar o Novo assistente de teste de carga

1.  Abra a solução Bank criada em [Passo a passo: Criando e executando testes de unidade para código gerenciado](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md).

2.  No **Gerenciador de Soluções**, abra o menu de atalho do nó da solução de Banco, escolha **Adicionar** e **Novo Projeto**.

     A caixa de diálogo **Adicionar Novo Projeto** é exibida.

3.  Na caixa de diálogo **Adicionar Novo Projeto**, expanda **Visual C#** e escolha **Teste**. Na lista de modelos, escolha **Projeto de teste de carga e desempenho da Web** e, no campo **Nome**, digite `BankLoadTest`. Escolha **OK**.

     O projeto de teste de desempenho na Web e de carga BankLoadTest é adicionado à solução.

4.  Abra o menu de atalho do novo projeto de teste de desempenho Web e de carga BankLoadTest, escolha **Adicionar** e **Teste de Carga**.

5.  O **Novo Assistente de Teste de Carga** é iniciado.

6.  A página **Bem-vindo** do **Novo Assistente de Teste de Carga** é a primeira página.

7.  Escolha **Avançar**.

### <a name="to-edit-settings-for-load-test-scenario"></a>Para editar as configurações do cenário de teste de carga

1.  Na caixa de texto **Digite um nome para o cenário de teste de carga**, digite **ScenarioSample**.

     Um *cenário* é um mecanismo de agrupamento. Consiste em um conjunto de testes e as propriedades para executar esses testes sob carga.

2.  Defina o **Perfil de tempo de processamento** como `Use normal distribution centered on recorded think times`. Os tempos de raciocínio representam o tempo que um usuário refletiria sobre uma página da Web antes de passar para a próxima página.

1.  Escolha **Avançar** quando terminar.

### <a name="to-edit-load-pattern-setting-for-test-scenario"></a>Para editar a configuração de padrão de carga para um cenário de teste

1.  Escolha **Carga por etapa**.

    > [!NOTE]
    > Você pode escolher entre dois tipos de padrões de carga: constante e etapa. Cada tipo tem sua função no teste de carga, mas neste passo a passo, escolha **Carga por etapa**.

2.  Defina **Iniciar a contagem de usuários** como 10 usuários.

3.  Defina **Duração da etapa** como 10 segundos.

4.  Defina **Contagem de usuário em etapas** como 10 usuários/etapa.

5.  Defina **Contagem máxima de usuários** como 100 usuários.

6.  Escolha **Avançar**.

### <a name="to-select-test-mix-model-for-the-scenario"></a>Para selecionar o modelo de combinação de testes para o cenário

1.  Em **Como a combinação de testes deve ser modelada?**, selecione **Baseado no número total de testes**.

2.  Escolha **Avançar**.

### <a name="to-add-unit-tests-to-the-scenario"></a>Para adicionar testes de unidade ao cenário

1.  A próxima etapa é **Adicionar testes a um cenário de teste de carga e editar a combinação de testes**.

2.  Escolha **Adicionar** para selecionar testes.

3.  Escolha os testes de unidade **CreditTest** listados no painel **Testes Disponíveis**, que lista todos os testes de desempenho Web e os testes de unidade no projeto de teste de desempenho Web e de carga.

4.  Escolha a seta para adicionar o teste de unidade **CreditTest** ao painel **Testes Selecionados**.

5.  Repita as etapas 3 e 4 para os testes de unidade **DebitTest** e **FreezeAccountTest**.

6.  Quando você tiver terminado de adicionar os três testes de unidade, escolha **OK**.

     Você recebe a combinação de testes.

7.  Mova o controle deslizante em **Distribuição** para **CreditTest** ligeiramente para a direita para ajustar a distribuição de teste. Observe que os outros controles deslizantes se movem para a esquerda automaticamente, de forma que a distribuição permaneça em 100%.

8.  Escolha **Avançar**.

### <a name="to-select-network-mix-for-test-scenario"></a>Para selecionar a combinação de redes para o cenário de teste

1.  Selecione o tipo de conexão LAN a ser adicionado à combinação de largura de banda de rede.

     Você pode adicionar mais tipos de rede. Use os controles deslizantes para ajustar a distribuição e a relevância do teste.

2.  Escolha **Avançar**.

### <a name="to-specify-computers-to-monitor-with-counter-sets-during-load-test-run"></a>Para especificar computadores para monitorar com conjuntos de contadores durante a execução do teste de carga

1.  Escolha **Avançar**.

     Para obter mais informações sobre conjuntos de contadores, confira [Especificar os conjuntos de contadores e as regras de limite para computadores em um teste de carga](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md).

### <a name="to-edit-run-setting-for-load-test"></a>Para editar a configuração de execução do teste de carga

1.  Selecione **Duração do teste de carga** e defina **Duração da execução** como 2 minutos para criar um *smoke test* de seu teste de carga.

     Quando você compila seus testes de carga, é uma boa prática validar que tudo esteja configurado corretamente e sendo executado como esperado executando um breve teste de carga leve. Esse processo é conhecido como *smoke testing*.

2.  Escolha **Concluir**. Seu teste de carga será aberto no **Editor de Teste de Carga**.

## <a name="run-the-load-test"></a>Executar o teste de carga
 Após você criar o teste de carga, execute-o para ver como seu aplicativo de banco responde à simulação de carga. Enquanto um teste de carga está sendo executado, consulte a janela **Analisador de Teste de Carga**.

### <a name="to-run-the-load-test"></a>Para executar o teste de carga

1.  Com um teste de carga aberto no **Editor de Teste de Carga**, escolha o botão verde **Executar Teste** na barra de ferramentas. Seu teste de carga começa a ser executado.

2.  Se a simulação de teste exceder qualquer limite, ícones serão exibidos nos nós de controle da árvore para indicar uma violação de limite. Erros têm uma sobreposição de círculo vermelho, e os avisos têm uma sobreposição de triângulo amarelo. Você pode localizar um contador que excede o limite e o representa graficamente arrastando o ícone no gráfico. Você pode fazer isso quando o teste está sendo executado.

## <a name="see-also"></a>Consulte também

- [Editar a combinação de testes para especificar quais testes incluir em um cenário de teste de carga](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md)
- [Especificar tipos de rede virtual](../test/specify-virtual-network-types-in-a-load-test-scenario.md)
- [Editar cenários de teste de carga](../test/edit-load-test-scenarios.md)
- [Editar padrões de carga para modelar atividades de usuário virtual](../test/edit-load-patterns-to-model-virtual-user-activities.md)
- [Editar modelos de combinação de testes para especificar a probabilidade de um usuário virtual executar um teste](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md)