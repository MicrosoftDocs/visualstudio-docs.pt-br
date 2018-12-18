---
title: Configurar a emulação de rede usando configurações de teste no Visual Studio
ms.date: 10/03/2016
ms.topic: conceptual
helpviewer_keywords:
- test settings, network emulation
ms.assetid: ff275cfb-5df9-4710-9a91-9caabaaad34f
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: d58bf2bc321b3041ffa0958786b976276acf0186
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896296"
---
# <a name="how-to-configure-network-emulation-using-test-settings-in-visual-studio"></a>Como configurar a emulação de rede usando configurações de teste no Visual Studio

Você pode configurar o adaptador de dados de diagnóstico para testar o aplicativo em vários ambientes de rede do Visual Studio. Ele também pode ser configurado para testar uma carga de rede artificial ou gargalo, quando você executa os testes.

> [!WARNING]
> Se você executar seus testes em uma rede real que seja um tipo mais lento do que a rede emulada, o teste ainda será executado na velocidade mais lenta de rede. A emulação só pode reduzir a velocidade do ambiente de rede, e não agilizá-la.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

O procedimento a seguir descreve como configurar a emulação de rede no editor de configuração. Essas etapas se aplicam ao editor de configuração no Microsoft Test Manager e ao Visual Studio.

> [!NOTE]
> O adaptador de dados de diagnóstico de emulação de rede só se aplica às configurações de teste do Visual Studio. Ele não é usado para configurações de teste no Microsoft Test Manager.

Uma conta que tenha privilégios de administrador deve ser usada para a emulação de rede. Se tiver selecionado a emulação de rede para uma função local que executa testes manuais, você deverá iniciar o Microsoft Test Manager usando privilégios de administrador. Se você selecionou a emulação de rede para qualquer outra função, deverá verificar se o agente de teste no computador dessa função usa uma conta de usuário que seja membro do grupo de administradores. Para obter mais informações sobre como configurar a conta para seu agente de teste, consulte [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md).

> [!NOTE]
> A conta do Serviço de Rede, que é a conta padrão para o agente de teste, não é membro do grupo de administradores.

**Emulação de rede verdadeira**

O Visual Studio usa emulação de rede real baseada em software para todos os tipos de testes. Isso inclui testes de carga. A emulação de rede verdadeira simula condições de rede pela manipulação direta de pacotes de rede. O emulador real de rede pode emular o comportamento de redes com fio e sem fio usando um link físico confiável, como Ethernet. Os seguintes atributos de rede são incorporados na emulação de rede verdadeira:

- O tempo da viagem de ida e volta pela rede (latência)

- A quantidade de largura de banda disponível

- Comportamento do enfileiramento

- Perda de pacote

- Reordenação de pacotes

- Propagações de erros.

A emulação de rede verdadeira também fornece flexibilidade em pacotes de rede de filtragem com base em endereços IP ou em protocolos como TCP, UDP e ICMP.

A emulação real de rede pode ser usada por desenvolvedores e testadores na rede para emular um ambiente de teste desejado, avaliar o desempenho, prever o efeito da alteração ou para tomar decisões sobre otimização da tecnologia. Quando comparada com bases de teste de hardware, a emulação de rede verdadeira é uma solução muito mais econômica e flexível.

## <a name="configure-network-emulation-for-your-test-settings"></a>Configurar a emulação de rede para as configurações de teste

Antes de executar as etapas neste procedimento, você deverá abrir as configurações de teste no Visual Studio e selecionar a página **Dados e Diagnósticos**.

### <a name="to-configure-network-emulation-for-your-test-settings"></a>Para configurar a emulação de rede para suas configurações de teste

1.  Selecione a função a ser usada para emular uma rede específica.

    > [!NOTE]
    > Você precisa configurar o adaptador de Emulação de Rede somente na função de cliente ou na função de servidor. Você não precisa usar o adaptador em ambas as funções. O adaptador emula ruídos de rede que afetam a comunicação entre as duas funções para que você não precise usá-lo em ambas. A menos que necessário, você deve escolher uma função de cliente para que o adaptador de Emulação de Rede evite sobrecarga adicional na função de servidor.

2.  Selecione **Emulação de Rede** e escolha **Configurar**.

     A caixa de diálogo para configurar a emulação de rede é exibida.

3.  Escolha a seta ao lado de **Selecione o perfil de rede a ser usado** e selecione o tipo de rede que você deseja emular ao executar um teste (por exemplo, **Cabo-DSL 768Kps**).

    > [!WARNING]
    > Se você executar seus testes em uma rede real que seja um tipo mais lento do que a rede emulada, o teste ainda será executado na velocidade mais lenta de rede. A emulação só pode reduzir a velocidade do ambiente de rede, e não agilizá-la.

4.  Se você incluir o adaptador de dados de diagnóstico de emulação de rede nas configurações de teste e se pretende usar no seu computador local, então também deverá associar o driver de emulação de rede para um dos adaptadores de rede do computador. O driver de emulação de rede é necessário para que o adaptador de dados de diagnóstico de emulação de rede funcione. O driver de emulação de rede é instalado e associado ao seu adaptador de duas maneiras:

    -   **Driver de emulação de rede instalado com o Agente de Teste do Microsoft Visual Studio:** o Agente de Teste do Microsoft Visual Studio pode ser usado em computadores remotos e em seu computador local. Quando você instala o Visual Studio Test Agent, o processo de instalação inclui uma etapa de configuração que associa o driver de emulação de rede em seu cartão de rede. Para obter mais informações, consulte [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md).

    -   **Driver de emulação de rede instalado com o Microsoft Visual Studio Test Professional:** quando você usar a emulação de rede pela primeira vez, será solicitada a associação do driver de emulação de rede a uma placa de rede.

    > [!TIP]
    > Você também pode instalar o driver de emulação de rede de linha de comando em seu computador local sem instalar o agente de teste do Visual Studio, usando o seguinte comando: **VSTestConfig NETWORKEMULATION /install**

## <a name="see-also"></a>Consulte também

- [Coletar informações de diagnóstico usando configurações de teste](../test/collect-diagnostic-information-using-test-settings.md)
- [Executar testes manuais (Azure Test Plans)](/azure/devops/test/run-manual-tests?view=vsts)