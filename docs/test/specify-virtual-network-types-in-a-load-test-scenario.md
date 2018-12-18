---
title: Especificando tipos de rede virtuais em um cenário de teste de carga
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, scenarios
- load tests, adding networks
- load tests, removing networks
- load tests, virtual networks
- network mix
ms.assetid: 3c4f7874-081a-4ec4-9510-4d6d7d863a11
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 586038d325f17d37167166a361ee214d959ba2ab
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52894671"
---
# <a name="specify-virtual-network-types-in-a-load-test-scenario"></a>Especificar tipos de rede virtual em um cenário de teste de carga

A *combinação de redes* oferece uma maneira de simular carga de modo mais realista em um cenário de teste de carga. A carga é gerada usando uma combinação heterogênea de tipos de rede, em vez de um único tipo de rede. Você cria uma situação mais parecida com a forma que os usuários finais interagem com seus aplicativos.

Uma combinação de redes especifica a probabilidade de um usuário virtual executar um determinado *perfil de rede*. Um perfil de rede é uma simulação da largura de banda da rede na camada de aplicativo. Ele não simula a latência.

Ao criar um teste de carga, talvez seja conveniente simular que a carga está sendo gerada por mais de um tipo de conexão de rede. A combinação de redes oferece vários tipos de rede. As diferentes redes são simuladas. Quando você escolhe uma opção como `Cable-DSL 1.5Mbps`, os tempos de espera são injetados no teste para simular a largura de banda selecionada.

A combinação de redes funciona como outras opções de combinação. Um tipo de rede é selecionado e aleatoriamente associado a um usuário virtual, com base na combinação de redes. Os testes desse usuário são executados usando um tipo de rede específico, com base na probabilidade especificada na combinação.

Depois de especificar uma combinação de redes, você pode adicionar e remover tipos de rede. Também é possível alterar a distribuição da combinação de redes usando o controle misto.

O controle misto permite ajustar facilmente a distribuição de redes em um cenário.

Para saber mais, confira [Sobre o controle misto](../test/specify-virtual-network-types-in-a-load-test-scenario.md).

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="true-network-emulation"></a>Emulação de rede verdadeira

O Visual Studio usa emulação de rede verdadeira baseada em software para todos os tipos de teste, inclusive testes de carga. A emulação de rede verdadeira simula condições de rede pela manipulação direta de pacotes de rede. O emulador real de rede pode emular o comportamento de redes com fio e sem fio usando um link físico confiável, como Ethernet. Os seguintes atributos de rede são incorporados na emulação de rede verdadeira:

-   O tempo da viagem de ida e volta pela rede (latência)

-   A quantidade de largura de banda disponível

-   Comportamento do enfileiramento

-   Perda de pacote

-   Reordenação de pacotes

-   Propagações de erros.

A emulação de rede verdadeira também fornece flexibilidade em pacotes de rede de filtragem com base em endereços IP ou em protocolos como TCP, UDP e ICMP.

A emulação de rede verdadeira pode ser usada por desenvolvedores e testadores de aplicativos baseados em rede para emular um ambiente de teste desejado, avaliar desempenho, prever o impacto da alteração ou tomar decisões sobre otimização da tecnologia. Quando comparada com bases de teste de hardware, a emulação de rede verdadeira é uma solução muito mais econômica e flexível.

## <a name="to-add-new-networks-to-a-scenario"></a>Para adicionar novas redes a um cenário

1.  Durante o processo de especificar a combinação de redes para um cenário, escolha **Adicionar**.

     Uma nova entrada de rede é adicionada à grade.

    > [!NOTE]
    > Para exibir a caixa de diálogo **Editar combinação de redes**, clique com o botão direito do mouse em um cenário existente e escolha **Editar combinação de redes**.

2.  Na coluna **Tipo de rede**, escolha a seta para a nova entrada. Escolha o tipo de rede desejado.

3.  (Opcional) Ajuste o controle misto para especificar a distribuição de teste. Para saber mais, confira [Sobre o controle misto](../test/specify-virtual-network-types-in-a-load-test-scenario.md).

4.  Quando terminar de adicionar redes, escolha **OK**.

## <a name="to-remove-networks-from-a-scenario"></a>Para remover redes de um cenário

1.  Abra um teste de carga.

2.  Clique com o botão direito do mouse no cenário do qual deseja remover uma rede e escolha **Editar combinação de redes**. A caixa de diálogo **Editar combinação de redes** é exibida.

3.  Selecione a rede na grade e escolha **Remover**.

4.  (Opcional) Ajuste o controle misto para especificar a distribuição de teste. Para saber mais, confira [Sobre o controle misto](../test/specify-virtual-network-types-in-a-load-test-scenario.md).

5.  Quando terminar de remover redes, escolha **OK**.

## <a name="about-the-mix-control"></a>Sobre o controle misto

 O controle misto permite que você ajuste a porcentagem de carga distribuída entre testes, tipos de navegador ou tipos de rede em um cenário de teste de carga. Para ajustar os valores da porcentagem, mova os controles deslizantes. O ajuste da combinação dos tipos de rede especifica a probabilidade de um usuário virtual executar um perfil de rede específico em um cenário de teste de carga.

 Quando você move um controle deslizante, os valores de porcentagem de todos os itens disponíveis mudam. Se você tiver mais de dois itens, a quantidade adicionada ou removida será distribuída por igual entre os outros itens. É possível substituir esse comportamento. Se marcar a caixa de seleção na coluna de cadeado de um item específico, você bloqueará o valor de porcentagem especificado do item. Então, quando você mover um controle deslizante, o valor adicionado ou removido só será aplicado aos itens desbloqueados restantes.

 O botão **Distribuir** é usado para alocar igualmente os valores de percentual entre todos os itens. Por exemplo, se você tiver três itens, escolher **Distribuir** define os valores de percentual como 34, 33 e 33.

> [!WARNING]
> O botão **Distribuir** substitui todos os itens bloqueados.

 Também é possível digitar os valores de percentual diretamente na coluna **%** em vez de usar os controles deslizantes. Se você inserir um valor de porcentagem diretamente, os outros itens não serão ajustados automaticamente.

> [!NOTE]
> Os controles deslizantes serão desabilitados quando o total não for 100% ou quando os valores de percentual inseridos na coluna **%** forem decimais.

Ao inserir valores de porcentagem manualmente, você deve ter certeza de que a soma de todos os itens seja 100%. Ao salvar uma combinação, se a soma não for 100%, você deverá aceitar os valores de porcentagem como estão ou voltar e ajustá-los. Se você optar por aceitá-los como estão, eles serão rateados em 100%.  Por exemplo, se você tiver dois itens e defini-los manualmente como 80% e 40%, o primeiro item será definido como 66,67% (80 dividido por 120) e o segundo item será definido como 33,33% (40 dividido por 120).