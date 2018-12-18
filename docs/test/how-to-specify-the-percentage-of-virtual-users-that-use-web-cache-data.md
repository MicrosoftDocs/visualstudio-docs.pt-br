---
title: Especificar o percentual de usuários virtuais que usam dados de cache da Web para testes de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, virtual users
ms.assetid: f66d5d43-4121-4487-b27f-d0a0baaf7601
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 1178cd08bf8d12b4fba61e858ca5631d103292c2
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895568"
---
# <a name="how-to-specify-the-percentage-of-virtual-users-that-use-web-cache-data"></a>Como especificar o percentual de usuários virtuais que usam dados de cache da Web

Depois de criar seu teste de carga com o **Novo Assistente de Teste de Carga**, você poderá alterar as propriedades dos cenários de forma a atender suas necessidades e objetivos de teste usando o **Editor de Teste de Carga**. Para obter uma lista completa das propriedades de cenário de teste de carga e suas descrições, confira [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md).

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

A propriedade **Percentual de novos Usuários** é definida na janela **Propriedades**. Edite as propriedades de cenário de teste de carga no **Editor de Teste de Carga**.

A propriedade **Percentual de novos usuários** afeta a maneira como o teste de carga simula o armazenamento em cache que seria executado por um navegador da Web. Por padrão, a propriedade de **Percentual de novos usuários** é definida como 0%. Se o valor da propriedade **Percentual de novos usuários** for definido como 100%, cada execução de teste de desempenho Web em um teste de carga será tratada como um usuário de primeira vez no site que não tem nenhum conteúdo do site no cache de visitas anteriores do navegador. Assim, todas as solicitações do teste na Web, incluindo todas as solicitações dependentes como imagens, são baixadas.

> [!NOTE]
> Quando o mesmo recurso que pode ser armazenado em cache é solicitado mais de uma vez em um teste na Web, as solicitações não são baixadas.

Se você estiver testando a carga de um site que tem um número significativo de usuários de retorno que provavelmente têm imagens e outros conteúdos armazenados em cache localmente, uma configuração de 100% para a propriedade de **Percentual de novos usuários** gerará mais solicitações de download do que aconteceria no uso real. Nesse caso, você deve calcular o percentual de visitas ao site que são de usuários de primeira vez do site e definir a propriedade de **Percentual de novos usuários** adequadamente.

## <a name="to-specify-the-percentage-of-new-users-for-a-scenario"></a>Para especificar a porcentagem de novos usuários para um cenário

1. Abra um teste de carga.

     O **Editor de Teste de Carga** é exibido. A árvore do teste de carga é exibida.

2. Na pasta **Cenários** das árvores de teste de carga, escolha o nó do cenário do qual você queira alterar o novo valor de porcentagem de usuário.

3. No menu **Exibir**, selecione **Janela de Propriedades**.

     As categorias e as propriedades do cenário são exibidas na janela **Propriedades**.

4. Defina o valor da propriedade **Percentual de Novos Usuários** digitando um número para o percentual de novos usuários.

5. Depois de alterar a propriedade, escolha **Salvar** no menu **Arquivo**. Assim, você pode executar o teste de carga usando o novo valor de **Percentual de Novos Usuários**.

## <a name="see-also"></a>Consulte também

- [Editar cenários de teste de carga](../test/edit-load-test-scenarios.md)
- [Passo a passo: criar e executar um teste de carga](../test/walkthrough-create-and-run-a-load-test.md)
- [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md)
- [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md)
- [Editar padrões de carga para modelar atividades de usuário virtual](../test/edit-load-patterns-to-model-virtual-user-activities.md)