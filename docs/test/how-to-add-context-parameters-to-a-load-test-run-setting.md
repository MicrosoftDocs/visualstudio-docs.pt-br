---
title: Adicionar parâmetros de contexto a uma configuração de execução de teste de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, run settings, context parameters
- load tests, context parameters
ms.assetid: a8a0b97e-8040-4711-85ab-36548b130ed2
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: c351079f0a29176ded3172d6e0e26893a1163354
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52894099"
---
# <a name="how-to-add-context-parameters-to-a-load-test-run-setting"></a>Como adicionar parâmetros de contexto a uma configuração de execução de teste de carga

Depois de criar seu teste de carga usando o **Novo Assistente de Teste de Carga**, você poderá usar o **Editor de Teste de Carga** para alterar as propriedades de cenários para que eles atendam às suas metas e necessidades de teste.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> Para obter uma lista completa das propriedades das configurações de execução e suas descrições, confira [Propriedades de configurações de execução de teste de carga](../test/load-test-run-settings-properties.md).

Você pode criar os parâmetros de contexto a serem usados em uma configuração de execução de teste de carga usando o Editor de testes de carga. Os parâmetros de contexto permitem parametrizar uma cadeia de caracteres.

Suponha que o teste de carga contenha um teste de desempenho na Web que já use uma URL parametrizada do servidor Web usando um parâmetro de contexto. Você pode adicionar um parâmetro de contexto a uma configuração de execução de teste de carga que usa o mesmo valor de nome daquele usado no teste de desempenho na Web. Isso mapeará o teste de desempenho na Web a um servidor diferente quando você executa o teste de carga. Por exemplo, se o teste de carga incluir um teste de desempenho na Web que usa um parâmetro de contexto que é chamado WebServer1 para o nome do servidor Web na URL. Se você especificar um parâmetro de contexto na sua configuração de execução do teste de carga que também é chamado WebServer1, o teste de carga usará o parâmetro de contexto que você atribuiu na configuração de execução de teste de carga. Para esclarecer, se o teste de desempenho na Web no teste de carga usar o mesmo nome de parâmetro de contexto de um parâmetro de contexto do teste de carga, o parâmetro de contexto no teste de carga substituirá o parâmetro de contexto que é usado no teste de desempenho na Web.

> [!WARNING]
> Tenha cuidado para não substituir por acidente o parâmetro de contexto de um teste de desempenho na Web ao usar parâmetros de contexto em uma configuração de execução. Evite usar os mesmos nomes de parâmetro de contexto, a menos que você faça isso intencionalmente.

Se atribuir o valor do parâmetro de contexto Webserver1 como `http://CorporateStagingWebServer`, você poderá usar `WebServer1` durante o teste de carga e, assim, alterar facilmente o valor para um servidor Web diferente a qualquer momento.

Além disso, atribuindo valores diferentes a um parâmetro de contexto usando o mesmo nome em diferentes configurações de execução de teste de carga, você pode executar o teste de carga usando diferentes ambientes:

- Configuração de execução do servidor Web de preparo empresarial: o parâmetro de contexto chamado `WebServer1=http://CorporateStagingWebServer`

- Configuração de execução do servidor Web de produção empresarial: o parâmetro de contexto chamado `WebServer1=http://CorporateProductionWebServer`

  **Alterando a configuração de execução na linha de comando**

  Se você quiser usar configurações de execução diferentes na linha de comando para se beneficiar da estratégia do parâmetro de contexto, use os seguintes comandos:

  **Set Test.UseRunSetting= CorporateStagingWebServer**

  -e-

  **mstest /testcontainer:loadtest1.loadtest**

## <a name="to-add-a-context-parameter-to-a-run-setting"></a>Para adicionar um parâmetro de contexto a uma configuração de execução

1.  Abra um teste de carga.

2.  Expanda a pasta **Configurações de Execução** na árvore de teste de carga no Editor de Teste de Carga.

3.  Clique com o botão direito do mouse na configuração de execução específica à qual você deseja adicionar um parâmetro de contexto e escolha em **Adicionar parâmetro de contexto**.

     Um novo parâmetro de contexto é adicionado à pasta **Parâmetros de contexto** na pasta **Configurações de execução** na árvore de teste de carga.

     -ou-

     Se a configuração de execução já contém uma pasta **Parâmetros de contexto**, você pode clicar com o botão direito do mouse nela e escolher **Adicionar parâmetro de contexto**.

4.  Na janela **Propriedades**, altere o valor de **Nome** conforme apropriado (por exemplo, WebServer1). Na janela **Propriedades**, altere **Valor** para o parâmetro que você deseja usar (por exemplo, `http://CorporateStagingWebServer`).

5.  (Opcional) Repita as etapas 3 a 5 e use uma cadeia de caracteres diferente para a propriedade **Valor** (por exemplo, `http://CorporateProductionWebServer`).

6.  Selecione as configurações de execução que quer que estejam ativas. Abra o menu de atalho nas configurações de execução e selecione **Definir como ativo**.

## <a name="see-also"></a>Consulte também

- [Definir configurações de execução de teste de carga](../test/configure-load-test-run-settings.md)