---
title: Combinação de testes do navegador para testes de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, web browser types
- load tests, scenarios
- load tests, adding browsers
- load tests, removing browsers
ms.assetid: 47f981d9-3038-45cc-a486-82b9daf9a9a1
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 8999d3acdd9160ea33f6e1fa9d07dc9f69619b01
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896465"
---
# <a name="edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario"></a>Editar a combinação de testes para especificar os tipos de navegadores da Web em um cenário de teste de carga

A *combinação de navegadores* possibilita simular a carga de modo mais realista em um cenário de teste de carga. A carga é gerada usando uma combinação heterogênea de navegadores da Web, em vez de um único navegador da Web. Você cria um cenário mais próximo dos navegadores da Web que serão usados com seus aplicativos.

Uma combinação de navegadores especifica a probabilidade de um usuário virtual executar um tipo específico de navegador da Web em um cenário de teste de carga. Ao criar um teste de carga, talvez seja conveniente simular que a carga é gerada por mais de um navegador da Web. Quando você adiciona um tipo de navegador da Web à combinação do conjunto de navegadores da Web que são fornecidos, um conjunto de cabeçalhos associados para o navegador da Web selecionado é adicionado a cada solicitação HTTP que é enviada a um teste de desempenho na Web.

A combinação de navegadores funciona como outras opções de combinação. Um tipo de navegador da Web é aleatoriamente associado a um usuário virtual, com base na combinação de navegadores. Os testes desse usuário são executados em um navegador da Web específico, com base na probabilidade especificada na combinação.

Depois de especificar uma combinação de navegadores, posteriormente, você poderá adicionar e remover tipos de navegador da Web da combinação. Você também pode alterar a distribuição da combinação de navegadores usando o controle misto. O controle misto permite ajustar facilmente a distribuição de navegadores em um cenário.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="add-new-browsers-to-a-scenario"></a>Adicionar novos navegadores a um cenário

### <a name="to-add-new-browsers-to-a-scenario"></a>Para adicionar novos navegadores a um cenário

1.  Durante o processo de especificar a combinação de navegadores para um cenário, escolha **Adicionar**.

     Uma nova entrada de navegador é adicionada à grade.

    > [!NOTE]
    > Para exibir a caixa de diálogo **Editar combinação de navegadores**, clique com o botão direito do mouse em um cenário existente e escolha **Editar combinação de navegadores**.

2.  Na coluna **Tipo de navegador**, escolha a seta para a nova entrada e escolha o tipo de navegador desejado.

3.  (Opcional) Ajuste o controle misto para especificar a distribuição de teste.

4.  Quando terminar de adicionar os navegadores, escolha **OK**.

##  <a name="remove-browsers-from-a-scenario"></a>Remover navegadores de um cenário

### <a name="to-remove-browsers-from-a-scenario"></a>Para remover navegadores de um cenário

1.  Abra um teste de carga.

2.  Clique com o botão direito do mouse no cenário do qual deseja remover um navegador e escolha **Editar combinação de navegadores**.

     A caixa de diálogo **Editar combinação de navegadores** é exibida.

3.  Selecione o navegador na grade e escolha **Remover**.

4.  (Opcional) Ajuste o controle misto para especificar a distribuição de teste.

5.  Quando terminar de remover os navegadores, escolha **OK**.

## <a name="about-the-mix-control"></a>Sobre o controle misto

 O controle misto permite que você ajuste a porcentagem de carga distribuída entre testes, tipos de navegador ou tipos de rede em um cenário de teste de carga. Você ajusta os valores de porcentagem movendo controles deslizantes. O ajuste da combinação dos tipos de navegador especifica a probabilidade de um usuário virtual executar um tipo de navegador específico em um cenário de teste de carga.

 Quando você move um controle deslizante, os valores de porcentagem de todos os itens disponíveis mudam. Se você tiver mais de dois itens, a quantidade adicionada ou removida será distribuída por igual entre os outros itens. É possível substituir esse comportamento. Se marcar a caixa de seleção na coluna de cadeado de um item específico, você bloqueará o valor de porcentagem especificado do item. Então, quando você mover um controle deslizante, o valor adicionado ou removido só será aplicado aos itens desbloqueados restantes.

 O botão **Distribuir** é usado para alocar igualmente os valores de percentual entre todos os itens. Por exemplo, se você tiver três itens, escolher **Distribuir** define os valores de percentual como 34, 33 e 33.

> [!WARNING]
> O botão **Distribuir** substitui todos os itens bloqueados.

 Também é possível digitar os valores de percentual diretamente na coluna **%** em vez de usar os controles deslizantes. Se você inserir um valor de porcentagem diretamente, os outros itens não serão ajustados automaticamente.

> [!NOTE]
> Os controles deslizantes serão desabilitados quando o total não for 100% ou quando os valores de percentual inseridos na coluna **%** forem decimais.

 Ao inserir valores de porcentagem manualmente, você deve ter certeza de que a soma de todos os itens seja 100%. Ao salvar uma combinação, se a soma não for 100%, você deverá aceitar os valores de porcentagem como estão ou voltar e ajustá-los. Se você optar por aceitá-los como estão, eles serão rateados em 100%.  Por exemplo, se você tiver dois itens e defini-los manualmente como 80% e 40%, o primeiro item será definido como 66,67% (80 dividido por 120) e o segundo item será definido como 33,33% (40 dividido por 120).

## <a name="see-also"></a>Consulte também

- [Editar cenários de teste de carga](../test/edit-load-test-scenarios.md)