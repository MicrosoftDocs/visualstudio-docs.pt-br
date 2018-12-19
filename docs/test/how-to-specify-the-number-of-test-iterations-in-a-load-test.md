---
title: Especificar o número de iterações de teste em uma configuração de execução de teste de carga
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, properties
- load tests, run settings
ms.assetid: 45a625db-b3e7-4d64-beda-b9a76248096d
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: e250096a99cfc272cd23b58bf0f7b70eeb3a7c9d
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53059834"
---
# <a name="how-to-specify-the-number-of-test-iterations-in-a-load-test-run-setting"></a>Como: Especificar o número de iterações de teste em uma configuração de execução de teste de carga

Depois de criar seu teste de carga com o **Novo Assistente de Teste de Carga**, você poderá usar o **Editor de Teste de Carga** para alterar as propriedades de cenários para que eles atendam às suas metas e necessidades de teste. Para obter mais informações, confira [Passo a passo: Criar e executar um teste de carga](../test/walkthrough-create-and-run-a-load-test.md).

Usando o **Editor de Teste de Carga**, você pode editar a propriedade **Iterações do Teste** de um valor das configurações de execução na janela **Propriedades**. A propriedade **Iterações de teste** especifica o número de iterações a serem executadas em todos os testes de unidade e desempenho Web em todos os cenários em um teste de carga usando o **Editor de Teste de Carga**.

> [!NOTE]
> Para obter uma lista completa das propriedades de configurações de execução e suas descrições, confira [Propriedades de configurações de execução de teste de carga](../test/load-test-run-settings-properties.md).

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-specify-the-number-of-test-iterations-in-a-run-setting"></a>Para especificar o número de iterações de teste em uma configuração de execução

1.  Abra um teste de carga.

     O **Editor de Teste de Carga** aparece e exibe a árvore de teste de carga.

2.  Na árvore de teste de carga, na pasta **Configurações de Execução**, escolha uma configuração de execução.

3.  No menu **Exibição**, selecione a **Janela de Propriedades** para exibir as categorias e as propriedades da configuração de execução de carga.

4.  Defina a propriedade **Usar iterações de teste** como **Verdadeiro**.

5.  Na propriedade **Iterações de teste**, insira um número que indica o número de iterações de teste a serem executadas durante o teste de carga.

6.  Depois de alterar a propriedade, escolha **Salvar** no menu **Arquivo**. Assim, você pode executar o teste de carga usando o novo valor de **Iterações de teste**.

## <a name="see-also"></a>Consulte também

- [Definir configurações de execução de teste de carga](../test/configure-load-test-run-settings.md)
- [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md)