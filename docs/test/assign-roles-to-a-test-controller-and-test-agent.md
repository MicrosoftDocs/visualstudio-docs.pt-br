---
title: Atribuir Funções a um Controlador de teste e Agente de teste para Testes automatizados
ms.date: 10/20/2016
ms.topic: conceptual
helpviewer_keywords:
- testing, walkthroughs, test controller and test agents
- test agent, walkthrough
- walkthroughs [Visual Studio ALM] testing
- test controller, walkthrough
- walkthroughs, test controller and test agents
ms.assetid: 57ed43ae-4e67-4139-8aec-3e9fceb0a745
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 021693266278bd705678c22d2c3f07e534901e5a
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895334"
---
# <a name="assign-roles-to-a-test-controller-and-test-agent"></a>Atribuir funções a um controlador de teste e a um agente de teste

Este passo a passo demonstra como criar e definir uma configuração de teste que usa um controlador de teste e um agente de teste para distribuir testes em vários computadores usando o Visual Studio. Além disso, esta explicação passo a passo demonstra como adicionar adaptadores de diagnóstico e dados à configuração de teste.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="prerequisites"></a>Pré-requisitos

-   Crie testes de unidade ou testes de IU codificados para executar com a configuração de teste.

-   Instale um controlador de teste e agentes de teste. Para obter informações de como instalar um controlador de teste e agentes de teste, confira [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md).

## <a name="to-create-and-configure-a-test-setting"></a>Para criar e configurar uma configuração de teste

1.  Na **Gerenciador de Soluções**, clique com o botão direito do mouse em **Itens da Solução**, aponte para **Adicionar** e clique em **Novo Item**.

     A caixa de diálogo **Adicionar Novo Item** é exibida.

2.  No painel **Modelos Instalados**, escolha **Configurações de Teste**.

3.  Na caixa **Nome**, digite **TestSettingDistributedTestWalkthrough**.

4.  Escolha **Adicionar**.

     O novo arquivo de teste *TestSettingDistributedTestWalkthrough.testsettings* aparece no **Gerenciador de Soluções**, na pasta **Itens da Solução**.

     A caixa de diálogo **Configurações de Teste** é exibida. A página **Geral** está selecionada.

     Agora você pode editar e salvar valores das configurações de teste.

    > [!NOTE]
    > Cada configuração de teste que você cria é listada como uma escolha para as opções **Selecionar Configurações de Teste Ativo** e **Editar Configurações de Teste** no menu **Teste**.

5.  Em **Nome**, digite o nome para as configurações de teste.

6.  Em **Descrição**, digite **Configurações de teste distribuído**.

7.  Deixe **Esquema de nomenclatura padrão** selecionado.

## <a name="to-assign-roles-to-a-test-controller-and-test-agents"></a>Para atribuir funções a um controlador de teste e agentes de teste

1.  Escolha **Funções**.

     A página **Funções** é exibida.

2.  Para executar o teste remotamente, use a lista suspensa **Método de execução do teste** e selecione **Execução remota**.

3.  Na lista suspensa **Controlador**, digite o nome do computador do [seu controlador de teste](../test/lab-management/install-configure-test-agents.md).

    > [!NOTE]
    > Se essa for a primeira vez que você está adicionando um controlador, não haverá controladores listados na lista suspensa. A lista é populada por controladores anteriores que você especificou em outras configurações de teste.

4.  Em **Funções**, escolha **Adicionar**.

5.  Na linha realçada na coluna **Nome**, digite **Teste distribuído**.

## <a name="to-assign-a-diagnostic-and-data-adapter-to-your-test-setting"></a>Para atribuir um adaptador de diagnóstico e dados à sua configuração de teste

1.  Escolha **Dados e Diagnósticos**.

     A página **Dados e Diagnósticos** é exibida.

2.  Em **Função**, verifique se a função **Teste distribuído** está selecionada.

3.  Em **Dados e Diagnósticos para função selecionada**, selecione os adaptadores **IntelliTrace** e **Informações do Sistema**.

     Para obter informações sobre esses adaptadores e outros adaptadores que você pode usar em uma configuração de teste, consulte [Configurar testes de unidade](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md).

4.  Escolha **Hosts**.

5.  (Opcional) Se o computador estiver executando uma versão de 64 bits do Microsoft Windows e você tiver compilado seu teste usando a configuração **Qualquer CPU**, use a lista suspensa **Executar teste em processo de 32 bits ou 64 bits** e selecione **Executar testes em processo de 64 bits no computador de 64 bits**.

    > [!TIP]
    > Para a máxima flexibilidade, você deve compilar seus projetos de teste com a configuração **Qualquer CPU**. Em seguida, você poderá executar os agentes de 32 bits e de 64 bits. Não há vantagem em compilar projetos de teste com a configuração de **64 bits**.

6.  Para salvar as novas configurações de teste, escolha **Aplicar**.

7.  Escolha **Fechar**.

8.  No menu Teste, escolha **Selecionar configurações de teste ativo** e, em seguida, selecione **TestSettingDistributedTestWalkthrough.testsettings**.

9. Execute o teste normalmente.

     Quando o controlador de teste processa testes de unidade e testes IU codificados, o controlador de teste divide os testes em grupos de 100 e os envia a um computador do agente de teste. Por exemplo, se você tiver 250 testes de unidade e três agentes de teste, os 100 primeiros testes de unidade serão enviados ao agente 1, os próximos 100 testes de unidade serão enviados ao agente 2 e os 50 testes de unidade restantes serão enviados ao agente 3.

## <a name="see-also"></a>Consulte também

- [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md)