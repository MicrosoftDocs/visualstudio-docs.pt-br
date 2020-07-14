---
title: Selecionar uma configuração de execução para um teste de carga
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, run settings, active
ms.assetid: ed6ff546-acfa-4dd8-b3a2-6e7455930ca4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8400c5afcb81215078617cca00cef9aa8ce018d6
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287539"
---
# <a name="how-to-select-the-active-run-setting-for-a-load-test"></a>Como selecionar a configuração de execução ativa para um teste de carga

Depois de criar seu teste de carga com o **Novo Assistente de Teste de Carga**, você poderá usar o **Editor de Teste de Carga** para alterar as propriedades de cenários para que eles atendam às suas metas e necessidades de teste.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Um teste de carga pode conter uma ou mais *configurações de execução*, que são um conjunto de propriedades que influenciam como um teste de carga é executado. As configurações de execução são organizadas por categorias na janela **Propriedades**. Quando é executado, um teste de carga usa a configuração de execução definida como ativa no momento.

> [!NOTE]
> Para obter uma lista completa das propriedades de configurações de execução e suas descrições, consulte [Propriedades de configurações de execução de teste de carga](../test/load-test-run-settings-properties.md).

Se o teste de carga contiver apenas um nó de configuração de execução na pasta **Configurações de Execução**, esse nó sempre será o nó ativo. Se o teste de carga contiver vários nós de configurações de execução, você poderá selecionar um para usar ao executar um teste de carga. Consulte [Como adicionar configurações de execução adicionais a um teste de carga](../test/how-to-add-additional-run-settings-to-a-load-test.md).

No **Editor de Teste de Carga**, a configuração de execução ativa é identificada pelo sufixo "[Active]".

## <a name="select-the-active-run-setting"></a>Selecionar a configuração de execução ativa

1. Abra um teste de carga.

2. Expanda a pasta **Configurações de Execução**.

3. Clique com o botão direito do mouse no nó de configurações de execução que você quer que seja o nó ativo e escolha **Definir como ativo**.

     No **Editor de Teste de Carga**, o nó de configuração de execução afetado é atualizado com o sufixo "[Active]".

     A configuração de execução selecionada torna-se ativa, e permanece ativa até que você selecione uma configuração de execução para ser ativa.

> [!NOTE]
> Você pode substituir a configuração de execução ativa definindo uma variável de ambiente denominada `Test.UseRunSetting=<run setting name>`. Isso é útil quando você executa um teste de carga a partir da linha de comando ou de um arquivo em lotes. Isso permite escolher configurações de execução diferentes sem abrir o teste de carga.

## <a name="specify-the-run-setting-to-use-from-the-command-line"></a>Especificar a configuração de execução a ser usada na linha de comando

Você pode substituir as configurações de execução padrão no teste de carga definindo uma variável de ambiente na linha de comando:

**Set Test.UseRunSetting=PreProdEnvironment**

E para executar o teste:

**mstest /testcontainer:loadtest1.loadtest**

## <a name="see-also"></a>Veja também

- [Definir configurações de execução de teste de carga](../test/configure-load-test-run-settings.md)
- [Especificar os conjuntos de contadores e as regras de limite para computadores em um teste de carga](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [Como: adicionar configurações de execução adicionais a um teste de carga](../test/how-to-add-additional-run-settings-to-a-load-test.md)
