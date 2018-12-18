---
title: Tempos de processamento para teste de carga
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, think times
- load tests, adding delays
- load tests, changing think times
ms.assetid: 8e03bee5-ab7b-4b40-9497-9dbe91ccb90e
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 236b6dffa3885928b48b7d6ea044f2494e7d7b28
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895906"
---
# <a name="edit-think-times-to-simulate-website-human-interaction-delays-in-load-tests-scenarios"></a>Editar tempos de processamento para simular atrasos de interação humana no site em cenários de testes de carga

Os tempos de processamento são usados para simular o comportamento humano que faz com que as pessoas esperem entre as interações com um site. Os tempos de processamento ocorrem entre as solicitações em um teste de desempenho na Web e entre as iterações de teste em um cenário de teste de carga. Usar tempos de processamento em um teste de carga pode ser útil ao criar simulações de carga mais precisas. Você pode alterar se os tempos de processamento serão usados ou ignorados em testes de carga. Você altera se os tempos de processamento são usados nos testes de carga no **Editor de Teste de Carga**.

O *perfil de processamento* é uma configuração que se aplica a um cenário em um teste de carga. A configuração determina se os tempos de processamento que são salvos nos testes de desempenho na Web individuais serão usados durante o teste de carga. Se você quiser usar tempos de processamento em alguns testes de desempenho na Web, mas não em outros, será necessário inseri-los em cenários diferentes. Para saber mais sobre cenários, confira [Editar cenários de teste de carga](../test/edit-load-test-scenarios.md).

Inicialmente, você define se quer usar tempos de processamento em seus testes de carga quando cria o teste de carga usando o **Novo Assistente de Teste de Carga**. Para saber mais, confira [Editar cenários de teste de carga](../test/edit-load-test-scenarios.md).

As opções de **Perfil de Processamento** são descritas na lista a seguir:

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

**Off**

Os tempos de processamento serão ignorados. Use essa configuração se você quiser gerar a carga máxima para forçar extremamente seu servidor Web. Não a use quando você estiver tentando criar interações mais realistas do usuário com um servidor Web.

**On**

Os tempos de processamento são usados exatamente como foram registrados no teste de desempenho na Web. Simula vários usuários que executam testes de desempenho na Web exatamente como registrados. Como um teste de carga simula vários usuários, usar o mesmo tempo de processamento poderia criar um padrão não natural de carga de usuários virtuais sincronizados.

**Distribuição Normal**

Os tempos de processamento são usados, mas variados em uma curva normal. Fornece uma simulação mais realista de usuários virtuais variando ligeiramente o tempo de pensamento entre solicitações.

> [!NOTE]
> Para obter uma lista completa das propriedades do cenário de teste de carga e suas descrições, confira [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md).

## <a name="change-the-think-profile"></a>Alterar o perfil de processamento

### <a name="to-change-a-think-profile-in-a-load-test-scenario"></a>Para alterar um perfil de processamento em um cenário de teste de carga

1.  No projeto de teste de carga e de desempenho na Web, abra um teste de carga.

2.  No **Editor de Teste de Carga**, escolha o nó do cenário em que deseja alterar o **Perfil de Processamento**. O **Perfil de Processamento** é exibido na janela **Propriedades**. Pressione **F4** para exibir a janela **Propriedades**.

3.  Altere a propriedade de **Perfil de Processamento** na janela **Propriedades**.

4.  Depois de alterar as propriedades, escolha **Salvar** no menu **Arquivo**. Você pode executar o teste de carga com o novo perfil de processamento.

## <a name="see-also"></a>Consulte também

- [Editar cenários de teste de carga](../test/edit-load-test-scenarios.md)