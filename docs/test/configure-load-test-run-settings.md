---
title: Definindo configurações de execução de teste de carga no Visual Studio
ms.date: 10/03/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, configuring run settings
ms.assetid: 0c86918b-cd63-4468-8f49-6d547a1276dc
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 9c20a56ce2d78ab5ba3c3fdcde19af573a830fc5
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895620"
---
# <a name="configure-load-test-run-settings"></a>Definir configurações de execução de teste de carga

*Configurações de execução* são um conjunto de propriedades que influenciam a maneira como um teste de carga é executado. As configurações de execução são organizadas por categorias na janela **Propriedades**.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Você pode ter mais de uma configuração de execução em um teste de carga. No entanto, somente uma das configurações de execução pode estar ativa por execução. As outras configurações de execução oferecem uma maneira rápida de selecionar uma configuração alternativa a ser usada em execuções de teste subsequentes.

A configuração de execução inicial é criada quando você cria um teste de carga usando o **Novo Assistente de Teste de Carga**.

![Carregar configurações de execução de teste](../test/media/loadtestrunsettings.png)

## <a name="tasks"></a>Tarefas

|Tarefas|Tópicos associados|
|-|-|
|**Adicionar mais configurações de execução ao teste de carga:** além da configuração de execução criada quando você executa o **Novo Assistente de Teste de Carga**, é possível adicionar mais configurações de execução ao teste de carga para que ele possa ser executado em diferentes condições.|-   [Como adicionar configurações de execução adicionais a um teste de carga](../test/how-to-add-additional-run-settings-to-a-load-test.md)|
|**Especificar a configuração de execução ativa a ser usada com o teste de carga:** você pode selecionar a configuração de execução que deseja usar com o teste de carga usando o Editor de Teste de Carga. A configuração de execução ativa é identificada pelo sufixo "[Active]".|-   [Como selecionar a configuração de execução ativa para um teste de carga](../test/how-to-select-the-active-run-setting-for-a-load-test.md)|
|**Editar propriedades da configuração da execução:** você pode editar suas propriedades de configuração de execução para coisas como registrar opções em log (veja mais abaixo), determinar a duração do teste, a duração de aquecimento, o número máximo de detalhes do erro relatados, a taxa de amostragem, o modelo de conexão (somente testes de desempenho Web), o tipo de armazenamento de resultados, o nível de validação e rastreamento SQL. As configurações de execução devem refletir as metas do teste de carga.|-   [Propriedades das configurações de execução de teste de carga](../test/load-test-run-settings-properties.md)<br />-   [Alterando as propriedades da configuração de execução](../test/load-test-run-settings-properties.md#change-run-setting-properties)|
|**Especificar a contagem de iteração de teste em configurações de execução de teste de carga:** você pode especificar o número de vezes em que todos os testes de unidade e desempenho e na Web devem ser executados em todos os cenários dos testes de carga configurando a propriedade **Iterações do teste**.|-   [Como especificar o número de iterações de teste em uma configuração de execução](../test/how-to-specify-the-number-of-test-iterations-in-a-load-test.md)|
|**Especificar a taxa de amostragem para uma configuração de execução de teste de carga:** você pode especificar com que frequência o teste de carga coleta dados do contador de desempenho configurando a propriedade **Taxa de amostragem**.|-   [Como especificar a taxa de amostragem](../test/how-to-specify-the-sample-rate-for-a-load-test.md)|
|**Especificar a opção de armazenamento dos detalhes de tempo:** você pode especificar como deseja que os detalhes do teste de carga sejam salvos configurando a propriedade **Armazenamento de detalhes de medição de tempo**.|-   [Como especificar a propriedade de armazenamento de detalhes de tempo](../test/how-to-specify-the-timing-details-storage-property-for-a-load-test.md)|
|**Especificar o período de retenção de recurso de teste:** acelerar o teste > corrigir > testar o ciclo novamente, mantendo os recursos de teste por um período especificado, definindo a propriedade **Tempo de retenção de recursos**.|-   [Manter os recursos para acelerar o teste de carga](/azure/devops/test/load-test/getting-started-with-performance-testing?view=vsts)|
|**Usar parâmetros de contexto:** você pode usar parâmetros de contexto para parametrizar uma cadeia de caracteres. Por exemplo, quando o teste de carga contém um teste de desempenho Web que usa um servidor Web parametrizado, você pode adicionar um parâmetro de contexto às configurações de execução que seja mapeado para um servidor diferente.|-   [Como adicionar parâmetros de contexto a uma configuração de execução](../test/how-to-add-context-parameters-to-a-load-test-run-setting.md)|
|**Configurando as propriedades do registro em log do teste:** você pode configurar com que frequência os dados são gravados no log associado às configurações de execução de teste de carga. Isso pode ser importante quando você está executando um teste de carga grande ou complexo porque o log poderia ter vários gigabytes.<br /><br /> Você também pode configurar o arquivo de log a ser salvo automaticamente quando o teste de carga não ajuda na depuração e na análise do aplicativo.|-   [Modificando as configurações de registro em log do teste de carga](../test/modify-load-test-logging-settings.md)|