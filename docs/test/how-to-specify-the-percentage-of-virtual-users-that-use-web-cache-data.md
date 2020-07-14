---
title: 'Teste de carga: definir porcentagem de usuário virtual usando dados de cache da Web'
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, virtual users
ms.assetid: f66d5d43-4121-4487-b27f-d0a0baaf7601
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0a31ea50cdedbeb825d03de38a89200b6e8e5200
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287396"
---
# <a name="how-to-specify-the-percentage-of-virtual-users-that-use-web-cache-data"></a>Como especificar o percentual de usuários virtuais que usam dados de cache da Web

Depois de criar seu teste de carga com o **Novo Assistente de Teste de Carga**, você poderá alterar as propriedades dos cenários de forma a atender suas necessidades e objetivos de teste usando o **Editor de Teste de Carga**. Para obter uma lista completa das propriedades de cenário de teste de carga e suas descrições, confira [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md).

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

A propriedade **percentual de novos usuários** é definida na janela **Propriedades** . Edite as propriedades de cenário de teste de carga no **Editor de Teste de Carga**.

A propriedade **porcentagem de novos usuários** afeta a maneira como o teste de carga simula o cache que seria executado por um navegador da Web. Por padrão, a propriedade de **Percentual de novos usuários** é definida como 0%. Se o valor da propriedade **Percentual de novos usuários** for definido como 100%, cada execução de teste de desempenho Web em um teste de carga será tratada como um usuário de primeira vez no site que não tem nenhum conteúdo do site no cache de visitas anteriores do navegador. Assim, todas as solicitações do teste na Web, incluindo todas as solicitações dependentes como imagens, são baixadas.

> [!NOTE]
> Quando o mesmo recurso que pode ser armazenado em cache é solicitado mais de uma vez em um teste na Web, as solicitações não são baixadas.

Se você estiver testando a carga de um site que tem um número significativo de usuários de retorno que provavelmente têm imagens e outros conteúdos armazenados em cache localmente, uma configuração de 100% para a propriedade de **Percentual de novos usuários** gerará mais solicitações de download do que aconteceria no uso real. Nesse caso, você deve calcular o percentual de visitas ao site que são de usuários de primeira vez do site e definir a propriedade de **Percentual de novos usuários** adequadamente.

## <a name="to-specify-the-percentage-of-new-users-for-a-scenario"></a>Para especificar a porcentagem de novos usuários para um cenário

1. Abra um teste de carga.

     O **Editor de Teste de Carga** é exibido. A árvore do teste de carga é exibida.

2. Na pasta **Cenários** das árvores de teste de carga, escolha o nó do cenário do qual você queira alterar o novo valor de porcentagem de usuário.

3. No menu **Exibir**, selecione **Janela de Propriedades**.

     As categorias e as propriedades do cenário são exibidas na janela **Propriedades**.

4. Defina o valor da propriedade **porcentagem de novos usuários** inserindo um número para a porcentagem de novos usuários.

5. Depois de alterar a propriedade, escolha **Salvar** no menu **Arquivo**. Em seguida, você pode executar o teste de carga usando o novo valor **percentual do novo usuário** .

## <a name="see-also"></a>Veja também

- [Editar cenários de teste de carga](../test/edit-load-test-scenarios.md)
- [Passo a passo: Criar e executar um teste de carga](../test/walkthrough-create-and-run-a-load-test.md)
- [Controladores de teste e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md)
- [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md)
- [Editar padrões de carga para modelar atividades de usuário virtual](../test/edit-load-patterns-to-model-virtual-user-activities.md)
