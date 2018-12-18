---
title: Como selecionar um repositório de resultados do teste de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.dialog.connectstringmissing
- vs.test.load.dialog.databaseconnectstring
helpviewer_keywords:
- load tests, results repository
- results, load test
- load test results, repository
- Load Test Results Repository
- SQL, Load Test Results Store
ms.assetid: fa0c4dd9-612f-4a57-b8eb-458f129d9cda
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 6c3627b55fa7b4b60193d31fc96be803301ce4c9
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895646"
---
# <a name="how-to-select-a-load-test-results-repository"></a>Como selecionar um repositório de resultados do teste de carga

Você não está limitado a um repositório de resultados local. Geralmente, os testes de carga são executados em um conjunto remoto de computadores de agente. Os agentes, juntamente com um controlador, podem gerar mais carga simulada do que qualquer computador individual. Para obter mais informações, consulte [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md).

Os resultados do teste de seus agentes ou do seu computador local podem ser salvos em qualquer servidor SQL no qual você criou um repositório de resultados de testes de carga. Em ambos os casos, você precisa identificar o local de armazenamento dos resultados do teste de carga usando a janela **Administrar Controladores de Teste**.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="identify-a-results-store-for-load-test-data"></a>Identificar um repositório de resultados para dados de testes de carga

1.  No **Gerenciador de Soluções**, abra o arquivo de teste de carga.

2.  Na barra de ferramentas **Teste de Carga**, selecione **Gerenciar Controladores de Teste**. A caixa de diálogo **Gerenciar Controlador de Teste** é exibida. Se você estiver usando um agente remotamente, selecione um controlador.

     ![Propriedades de conexão de repositório de resultados de teste de carga](../test/media/loadtestconnectionproperties.png) Propriedades de conexão de repositório de resultados de teste de carga

3.  No **Repositório de resultados do teste de carga**, clique em **(…)** para exibir a caixa de diálogo **Propriedades da Conexão**.

4.  Em **Nome do Servidor**, digite o nome do servidor em que você executou os scripts `LoadTest`.

    > [!TIP]
    > Se estiver usando o SQL Express no computador local como repositório de testes de carga, digite \<nomedocomputador>\sqlexpress (for example, **MyComputer\sqlexpress**).

5.  Em **Fazer logon no servidor**, você pode escolher **Usar Autenticação do Windows**. Você pode especificar o nome de usuário e a senha, mas se fizer isso, deverá selecionar a opção **Salvar minha senha**.

6.  Em **Conectar a um banco de dados**, escolha **Selecionar ou digitar um nome de banco de dados**. Selecione **LoadTest** na caixa de listagem suspensa.

7.  Escolha **OK**. Você pode testar a conexão escolhendo **Testar Conexão**.

8.  Escolha **Fechar** na caixa de diálogo **Gerenciar o controlador de teste**.

## <a name="see-also"></a>Consulte também

- [Gerenciar resultados do teste de carga no repositório de Resultados do Teste de Carga](../test/manage-load-test-results-in-the-load-test-results-repository.md)
- [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md)