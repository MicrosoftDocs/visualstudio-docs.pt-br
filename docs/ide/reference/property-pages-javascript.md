---
title: Páginas de Propriedade, JavaScript
ms.date: 06/21/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- javascript.project.property.debugging.debuggertype
- javascript.project.property.debugging.requireauthentication
- javascript.project.property.outputpath
- javascript.project.property.debugging.launchapplication
- javascript.project.property.defaultlanguage
- javascript.project.property.debugging.machinename
- javascript.project.property.debugging.allowlocalnetworkloopback
ms.assetid: a05ab01f-3d5d-4675-a845-eab51807d3a3
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a35ee6d086153adc718a1616c0c8f0c8c606fbb7
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220024"
---
# <a name="property-pages-javascript"></a>Páginas de Propriedade, JavaScript
As **Páginas de Propriedades** fornecem acesso às configurações do projeto. Você pode usar as páginas que aparecem nas **Páginas de Propriedade** para alterar as propriedades do projeto.

Para acessar as propriedades do projeto, selecione um nó do projeto no **Gerenciador de Soluções**. No menu **Projeto**, clique em **Propriedades**.

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

As opções e páginas a seguir aparecem nas **Páginas de Propriedade**.

## <a name="configuration-and-platform-page"></a>Página de plataforma e configuração
 Use as seguintes opções para selecionar a configuração e a plataforma a exibir ou modificar.

 **Configuração**

 Especifica as definições de configuração a exibir ou modificar. As configurações são **Depurar** (padrão), **Versão**, **Todas as Configurações de** ou uma configuração definida pelo usuário. Para obter mais informações, consulte [How to: Set debug and release configurations in Visual Studio](../../debugger/how-to-set-debug-and-release-configurations.md) (Como definir configurações de depuração e versão no Visual Studio).

 **Plataforma**

 Especifica as configurações de plataforma a exibir ou modificar. As configurações são **Qualquer CPU** (padrão para aplicativos [!INCLUDE[win8_appname_long](../../debugger/includes/win8_appname_long_md.md)]), **x64**, **ARM**, **x86** ou uma plataforma definida pelo usuário. Para obter mais informações, consulte [How to: Set debug and release configurations in Visual Studio](../../debugger/how-to-set-debug-and-release-configurations.md) (Como definir configurações de depuração e versão no Visual Studio).

## <a name="general-page"></a>Página geral
 Use as seguintes opções para configurar propriedades gerais do projeto.

> [!NOTE]
> Algumas opções estão disponíveis somente em aplicativos UWP.


 **Caminho de Saída**

 Especifica o local dos arquivos de saída para a configuração do projeto. O caminho é relativo; se você inserir um caminho absoluto, o caminho absoluto será salvo no projeto. O caminho padrão é bin\Debug.

 Quando você usa configurações de build simplificadas, o sistema do projeto determina se é necessário compilar uma versão de depuração ou de liberação. Quando você clica em **Depurar**, **Iniciar Depuração** (ou pressiona F5), o build é colocado no local de depuração, independentemente do **Caminho de saída** especificado. No entanto, o comando **Compilar Solução** no menu **Criar** a coloca no local especificado. Para habilitar as configurações de build avançadas, na barra de menus, escolha **Ferramentas**, **Opções**. Na caixa de diálogo **Opções**, expanda **Projetos e Soluções**, selecione **Geral** e desmarque a caixa de seleção **Mostrar configurações de build avançadas**. Isso lhe dá controle manual sobre todos os valores de configuração e de se uma versão de depuração ou liberação é compilada.

 **Idioma padrão**

 Especifica o idioma padrão para o projeto. A opção de idioma selecionada em **Relógio, Idioma e Região** no Painel de Controle especifica o idioma preferencial do usuário. Ao especificar um idioma padrão para o projeto, certifique-se de que os recursos de idioma padrão especificado sejam usados se o idioma preferencial do usuário não corresponder aos recursos de idioma fornecidos no aplicativo.

## <a name="debug-page"></a>Página de depuração
 Use as seguintes opções para definir propriedades para o comportamento de depuração no projeto.

> [!NOTE]
> Algumas opções estão disponíveis somente em aplicativos UWP.


 **Depurador a ser iniciado**

 Especifica o host padrão para o depurador.

-   Selecione **Computador Local** para iniciar o aplicativo no computador de host do Visual Studio. Para obter mais informações, consulte [Executando aplicativos no computador local](../../debugger/run-windows-store-apps-on-the-local-machine.md).

-   Selecione **Simulador** para iniciar o aplicativo no Simulador. Para obter mais informações, consulte [Executando aplicativos no simulador](../../debugger/run-windows-store-apps-in-the-simulator.md).

-   Selecione **Computador Remoto** para iniciar o aplicativo em um computador remoto. Para obter mais informações sobre a depuração remota, consulte [Executando aplicativos em um computador remoto](../../debugger/run-windows-store-apps-on-a-remote-machine.md).

**Iniciar Aplicativo**

Especifica se o aplicativo deve ser iniciado quando você pressiona F5 ou clica em **Depurar**, **Iniciar Depuração**. Selecione **Sim** para iniciar o aplicativo; caso contrário, selecione **Não**. Se você selecionar **Não**, ainda poderá depurar o aplicativo se você usar um método diferente para iniciá-lo.

**Tipo de Depurador**

Especifica os tipos de código a depurar. Selecione **Somente Script** para depurar o código JavaScript. Selecione **Somente Gerenciado** para depurar código gerenciado pelo Common Language Runtime. Selecione **Somente Nativo** para depurar código C++. Selecione **Nativo com Script** para depurar C++ e JavaScript. Selecione **Misto (Gerenciado e Nativo)** para depurar código gerenciado e C++.

**Permitir Loopback de Rede Local**

Especifica se o acesso ao endereço IP de loopback é permitido para testes de aplicativos. Selecione **Sim** para permitir o uso do endereço de loopback se o aplicativo cliente estiver no mesmo computador em que o aplicativo para servidores está em execução; caso contrário, selecione **Não**. Essa propriedade estará disponível somente se a propriedade **Depurador a Iniciar** estiver definida como **Computador Remoto**.

**Nome do Computador**

Especifica o nome do computador remoto no qual hospedar o depurador. Essa propriedade estará disponível somente se **Depurador a Iniciar** estiver definido como **Computador Remoto**.

**Exigir Autenticação**

Especifica se o computador remoto exige autenticação. Essa propriedade estará disponível somente se **Depurador a Iniciar** estiver definido como **Computador Remoto**.
