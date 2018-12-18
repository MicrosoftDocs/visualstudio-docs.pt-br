---
title: Adicionar configurações de execução em um teste de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, run settings, adding
- load tests, run settings
ms.assetid: 257d2a24-d582-4cfe-8b2b-51f51ba9cc84
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: e894bb0b53240795ad2bf7505ba081dbf479989d
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896608"
---
# <a name="how-to-add-additional-run-settings-to-a-load-test"></a>Como adicionar configurações de execução adicionais a um teste de carga

As configurações de execução de um teste de carga determinam várias outras configurações. Entre elas estão a duração do teste, o nível de detalhes da coleção de resultados e os conjuntos de contadores coletados quando o teste é executado. Você pode criar e armazenar várias configurações de execução para cada teste de carga e selecionar uma configuração específica a ser usada quando executar o teste. Uma configuração inicial de execução é adicionada ao teste de carga quando você cria o teste de carga usando o **Novo Assistente de Teste de Carga**.

Você pode adicionar mais configurações de execução ao teste de carga com configurações de propriedade diferentes para que possa executar o teste de carga em condições diferentes. Por exemplo, você pode adicionar uma nova configuração de teste e usar uma taxa de amostragem diferente ou especificar uma duração de execução mais longa. Você só pode usar uma configuração executada de cada vez e deve especificar qual configuração de execução usar marcando-a como ativa.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-add-another-run-setting"></a>Para adicionar outra configuração de execução

1.  Abra um teste de carga.

2.  (Opcional) Expanda a pasta **Configurações de Execução**.

3.  Clique com o botão direito do mouse na pasta **Configurações de Execução** e selecione **Adicionar Configurações de Execução**.

     Uma nova configuração de execução é adicionada à pasta **Configurações de Execução**.

4.  No menu **Exibir**, escolha **Janela de Propriedades**.

     A Janela **Propriedades** é exibida com as propriedades da configuração de execução selecionada.

5.  Na janela **Propriedades**, use a caixa de texto da propriedade **Nome** para dar à nova configuração de execução um nome que descreva a intenção da configuração de execução (por exemplo, **Configuração da Execução: execução de cinco minutos**).

6.  Use a janela **Propriedades** para alterar as configurações de execução. Por exemplo, altere a duração da execução para **00:05:00** a fim de executar o teste por cinco minutos.

    > [!NOTE]
    > Para obter uma lista completa das propriedades das configurações de execução e suas descrições, confira [Propriedades de configurações de execução de teste de carga](../test/load-test-run-settings-properties.md).

     Agora você pode especificar que deseja usar a configuração de execução adicionada definindo-a como ativa. Para saber mais, consulte [Como selecionar a configuração de execução ativa para um teste de carga](../test/how-to-select-the-active-run-setting-for-a-load-test.md).

## <a name="see-also"></a>Consulte também

- [Definir configurações de execução de teste de carga](../test/configure-load-test-run-settings.md)
- [Especificar os conjuntos de contadores e as regras de limite para computadores em um teste de carga](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)