---
title: Combinação de testes para um cenário de teste de carga
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, adding tests
- test mix
- load tests, test mix
- load tests, removing tests
ms.assetid: 303e1d70-5d98-424a-b51e-e0898e16d3f8
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 3b3bd0ae4df657d7234a77413003b18d5db86138
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895984"
---
# <a name="edit-the-test-mix-to-specify-which-web-performance-unit-and-coded-ui-tests-to-include-in-a-load-test-scenario"></a>Editar a combinação de testes para especificar quais testes de IU codificados, de desempenho Web e de unidade incluir em um cenário de teste de carga

A *combinação de testes* de um cenário é uma combinação da seleção dos testes de unidade e de desempenho Web contidos no cenário e da distribuição desses testes no cenário. A distribuição é uma configuração que você pode especificar para a probabilidade de um teste específico ser selecionado por um usuário virtual durante uma execução do teste de carga.

Depois que você adiciona um conjunto de testes a um teste de carga, a *combinação de testes* funciona como qualquer outra opção de combinação. Um usuário virtual seleciona aleatoriamente um teste, com base na probabilidade que você especificou na combinação. Por exemplo, se você tiver dois testes, cada 50 por cento na combinação, um novo usuário único virtual optará por executar o primeiro teste aproximadamente na metade do tempo. Em uma combinação 50/50, se um teste for longo e o outro for curto, mais carga virá do teste longo.

Depois de adicionar testes à combinação, você poderá removê-los. Você também pode alterar a distribuição da combinação de testes usando o controle misto. O controle misto permite ajustar facilmente a distribuição de testes em um cenário.

> [!NOTE]
> Distribuição é uma medida da probabilidade de um teste específico ser selecionado por um usuário virtual durante uma execução do teste de carga. A distribuição é expressa como uma porcentagem. Consequentemente, a soma dos números de distribuição para todos os testes contidos em um cenário é 100. Por exemplo, se um cenário contiver apenas um teste, a distribuição desse teste será 100 por cento.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="add-new-tests-to-a-test-mix-in-an-existing-scenario"></a>Adicionar novos testes a uma combinação de testes em um cenário existente

Ao criar um novo cenário usando o **Novo Assistente de Teste de Carga**, você pode especificar os testes de unidade e desempenho na Web a serem adicionados ao teste misto do novo cenário.

Você pode adicionar mais testes de unidade e desempenho na Web à combinação de texto do cenário usando o **Editor de Teste de Carga**.

![Adicionando um teste a um teste de carga existente](../test/media/ltest_addingtests.png)

### <a name="to-add-more-tests-to-an-existing-scenario"></a>Para adicionar mais testes a um cenário existente

1.  Abra um teste de carga.

2.  No **Editor de Teste de Carga**, clique com o botão direito do mouse em um cenário existente e escolha **Adicionar testes**.

     A caixa de diálogo **Adicionar testes** é exibida. Todos os testes de desempenho na Web, unidade, e de IU codificados na solução que ainda não estejam em seu cenário estão disponíveis para adição ao cenário.

3.  No painel **Testes disponíveis**, selecione os testes de desempenho Web, de unidade e de IU codificados que você deseja adicionar. Escolha a seta para a direita para adicionar os testes ao painel **Testes selecionados**.

4.  Quando terminar de adicionar os testes, escolha **OK**.

     Os testes são adicionados à combinação de testes. Uma nova distribuição é atribuída automaticamente aos testes na combinação de testes.

5.  (Opcional) Ajuste o controle misto para especificar a distribuição de teste. Para saber mais, confira [Sobre o controle misto](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md).

##  <a name="remove-tests-from-a-scenario"></a>Remover testes de um cenário
 ![Removendo um teste de um teste de carga existente](../test/media/ltest_removetest.png)

### <a name="to-remove-tests-from-a-scenario"></a>Para remover testes de um cenário

1.  Abra um teste de carga.

2.  No **Editor de Teste de Carga**, na árvore de teste de carga, clique com o botão direito do mouse no cenário do qual você deseja remover um teste e selecione **Editar combinação de testes**. A caixa de diálogo **Editar combinação de testes** é exibida.

3.  Selecione o teste de desempenho Web, de unidade ou de IU codificado na grade e escolha **Remover**.

    > [!NOTE]
    > Depois de remover o teste, ajuste a combinação de testes de acordo com sua distribuição preferencial.

4.  Quando terminar a remoção dos testes, escolha **OK**.

##  <a name="EditingTestMixAboutMixControl"></a> Sobre o controle misto
 O controle misto permite que você ajuste a porcentagem de carga distribuída entre testes, tipos de navegador ou tipos de rede em um cenário de teste de carga. Você ajusta os valores de porcentagem movendo controles deslizantes. O ajuste da combinação de testes especifica a probabilidade de um usuário virtual executar um teste específico em um cenário de teste de carga.

 Quando você move um controle deslizante, os valores de porcentagem de todos os itens disponíveis mudam. Se você tiver mais de dois itens, a quantidade adicionada ou removida será distribuída por igual entre os outros itens. É possível substituir esse comportamento. Se marcar a caixa de seleção na coluna de cadeado de um item específico, você bloqueará o valor de porcentagem especificado do item. Então, quando você mover um controle deslizante, o valor adicionado ou removido só será aplicado aos itens desbloqueados restantes.

 O botão **Distribuir** é usado para alocar igualmente as porcentagens entre todos os itens. Por exemplo, se você tiver três itens, escolher **Distribuir** define os valores de percentual como 34, 33 e 33.

> [!WARNING]
> O botão **Distribuir** substitui todos os itens bloqueados.


 Também é possível digitar os valores de percentual diretamente na coluna **%** em vez de usar os controles deslizantes. Se você inserir um valor de porcentagem diretamente, os outros itens não serão ajustados automaticamente.

> [!NOTE]
> Os controles deslizantes serão desabilitados quando o total não for 100% ou quando os valores de percentual inseridos na coluna **%** forem decimais.


 Ao inserir valores de porcentagem manualmente, você deve ter certeza de que a soma de todos os itens seja 100%. Ao salvar uma combinação, se a soma não for 100%, você deverá aceitar os valores de porcentagem como estão ou voltar e ajustá-los. Se você optar por aceitá-los como estão, eles serão rateados em 100%.  Por exemplo, se você tiver dois itens e defini-los manualmente como 80% e 40%, o primeiro item será definido como 66,67% (80 dividido por 120) e o segundo item será definido como 33,33% (40 dividido por 120).

## <a name="see-also"></a>Consulte também

- [Editando cenários de teste de carga](../test/edit-load-test-scenarios.md)