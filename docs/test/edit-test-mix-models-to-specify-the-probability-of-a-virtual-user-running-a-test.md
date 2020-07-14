---
title: Editando modelos de combinação de testes
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, scenarios
- load tests, virtual users
ms.assetid: e3b7d952-9012-400a-8131-3444390a6066
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8ce54af89164b1a71c7328d04635c8735eec1b28
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288644"
---
# <a name="edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test"></a>Editar modelos de combinação de testes para especificar a probabilidade de um usuário virtual executar um teste

O *modelo de combinação de testes* especifica a probabilidade de um usuário virtual executar um determinado teste em um cenário de teste de carga. Isso permite a você simular a carga de forma mais realista. Em vez de ter apenas um fluxo de trabalho com seus aplicativos, você pode ter vários fluxos de trabalho, que é uma aproximação de como os usuários finais interagem com seus aplicativos.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="test-mix-model-options"></a>Opções do modelo de combinação de testes

Você pode especificar uma das seguintes opções de modelo da combinação de testes para seu cenário de teste de carga:

- **Baseado no número total de testes:** determina qual teste de desempenho Web ou teste de unidade é executado quando um usuário virtual inicia uma iteração de teste. No final do teste de carga, o número de vezes que um teste específico foi executado corresponde à distribuição de teste atribuída. Use esse modelo da combinação de testes quando você estiver baseando a combinação em porcentagens de transações em um log do IIS ou em dados de produção.

- **Baseado no número de usuários virtuais:** determina o percentual de usuários virtuais que executarão um teste de desempenho Web ou um teste de unidade específico. A qualquer momento do teste de carga, o número usuários que estão executando um teste específico corresponde à distribuição atribuída. Use esse modelo da combinação de testes quando você estiver baseando a combinação na porcentagem de usuários executando um teste específico.

- **Baseado no ritmo do usuário:** no decorrer do teste de carga, cada teste de desempenho Web ou teste de unidade é executado um número especificado de vezes por usuários, por hora. Use esse modelo da combinação de testes quando quiser que os usuários virtuais executem o teste em um determinado ritmo durante o teste de carga.

- **Baseado na ordem sequencial:** cada usuário virtual executa os testes de desempenho Web ou de unidade na ordem em que os testes são definidos no cenário. O usuário virtual continua a alternar entre os testes nesta ordem até que o teste de carga seja concluído.

## <a name="tasks"></a>Tarefas

|Tarefas|Tópicos associados|
|-|-----------------------|
|**Especificando a combinação de testes para o teste de carga:** ao criar um teste de carga, você especifica as configurações do teste de carga no **Novo Assistente de Teste de Carga**. No **Novo Assistente de Teste de Carga**, você escolhe testes de unidade e da Web existentes para adicionar ao cenário inicial. Depois de adicionar testes ao cenário, você especifica a combinação de testes para o cenário.<br /><br /> Você usa opções de modelagem de carga para prever com maior precisão o uso real esperado de um site ou aplicativo que está passando por teste de carga. É importante fazer isso porque um teste de carga não baseado em um modelo de carga preciso pode gerar resultados enganadores.|-   [Emular o uso real esperado de um site ou aplicativo](../test/emulate-real-world-usage-of-a-web-site-in-a-load-test-using-test-mix-models.md)|
|**Edite o modelo de combinação de testes:** Você pode alterar um cenário de teste de carga para usar um dos modelos de combinação de teste usando o **Editor de teste de carga**.||
|**Configurar a definição de atrasos para um modelo de combinação de testes baseado no ritmo do usuário:** se seu cenário de teste de carga for configurado para usar o **modelo de combinação de testes baseado no ritmo do usuário**, você poderá especificar como quer que o atraso de distribuição seja configurado.|-   [Como aplicar a distribuição ao intervalo de ritmo ao usar um modelo de combinação de teste do usuário do ritmo](../test/how-to-apply-distribution-to-pacing-delay-when-using-a-user-pace-test-mix-model.md)|

## <a name="change-the-test-mix-model-in-a-scenario"></a>Alterar o modelo de combinação de testes em um cenário

Depois de criar o teste de carga usando o **novo assistente de teste de carga**, você pode usar o **Editor de teste de carga** para alterar as propriedades de cenários para atender às suas necessidades e metas de teste.

> [!NOTE]
> Para obter uma lista completa das propriedades de configurações de carregamento e suas descrições, consulte [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md).

Usando o **Editor de teste de carga**, você pode alterar o modelo de combinação de teste em um cenário de teste de carga editando a propriedade de **tipo de combinação de teste** na janela **Propriedades** .

### <a name="to-change-the-test-mix-model"></a>Para alterar o modelo de combinação de testes

1. Abra um teste de carga.

     O **Editor de Teste de Carga** é exibido. A árvore do teste de carga é exibida.

2. Na pasta *Cenários* da árvore de teste de carga, escolha o nó do cenário para o qual você deseja especificar o número máximo de iterações de teste.

3. No menu **Exibir**, selecione **Janela de Propriedades**.

     As categorias e as propriedades do cenário são exibidas.

4. Na propriedade **Tipo de combinação de testes**, escolha o botão de reticências (**…**).

     A caixa de diálogo **Editar combinação de testes** é exibida.

5. Escolha a lista suspensa em **Modelo de combinação de testes** e selecione o modelo de combinação de testes que você deseja usar para o cenário.

6. (Opcional) Modifique a combinação de testes usando os botões **Adicionar**, **Remover** e **Distribuir** e os controles deslizantes de distribuição. Para saber mais, confira [Editar a combinação de testes para especificar quais testes incluir em um cenário de teste de carga](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md).

7. (Opcional) Especifique um teste de desempenho na Web e um teste de unidade para inicializar ou encerrar usando as caixas de seleção e selecionando os testes desejados. Para saber mais, confira [Emular o uso real esperado de um site ou aplicativo](../test/emulate-real-world-usage-of-a-web-site-in-a-load-test-using-test-mix-models.md).

8. Escolha **OK**.

     A janela **Propriedades** exibe o novo modelo de combinação de testes para a propriedade **Tipo de combinação de testes**.

9. Depois de alterar a propriedade, escolha **Salvar** no menu **Arquivo**. Assim, você pode executar o teste de carga usando o novo valor de **Tipo de combinação de testes**.

## <a name="see-also"></a>Veja também

- [Editar cenários de teste de carga](../test/edit-load-test-scenarios.md)
- [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md)
