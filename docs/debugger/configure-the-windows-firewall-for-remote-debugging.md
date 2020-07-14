---
title: Configurar o Firewall do Windows para depuração remota | Microsoft Docs
ms.date: 10/31/2018
ms.topic: how-to
ms.assetid: 66e3230a-d195-4473-bbce-8ca198516014
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0fa5d60d7fe662cff31b54bf3a13c203f4b6d8c9
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350687"
---
# <a name="configure-windows-firewall-for-remote-debugging"></a>Configurar o Firewall do Windows para depuração remota

Em uma rede protegida pelo firewall do Windows, o firewall deve ser configurado para permitir a depuração remota. O Visual Studio e as ferramentas de depuração remota tentam abrir as portas de firewall corretas durante a instalação ou inicialização, mas você também pode precisar abrir portas ou permitir aplicativos manualmente.

Este tópico descreve como configurar o Firewall do Windows para habilitar a depuração remota no Windows 10, 8/8.1 e 7; e os computadores com Windows Server 2012 R2, 2012 e 2008 R2. O Visual Studio e o computador remoto não precisam executar o mesmo sistema operacional. Por exemplo, o computador do Visual Studio pode executar o Windows 10 e o computador remoto pode executar o Windows Server 2012 R2.

>[!NOTE]
>As instruções para configurar o Firewall do Windows diferem ligeiramente em sistemas operacionais diferentes e para versões mais antigas do Windows. As configurações do Windows 8/8.1, Windows 10 e Windows Server 2012 usam o *aplicativo*Word, enquanto o Windows 7 e o windows Server 2008 usam o *programa*Word.

## <a name="configure-ports-for-remote-debugging"></a>Configurar portas para depuração remota

O Visual Studio e o depurador remoto tentam abrir as portas corretas durante a instalação ou inicialização. No entanto, em alguns cenários, como um firewall de terceiros, talvez seja necessário abrir portas manualmente.

**Para abrir uma porta:**

1. No menu **Iniciar** do Windows, procure e abra o **Firewall do Windows com segurança avançada**. No Windows 10, esse é o **Windows Defender firewall com segurança avançada**.

1. Para uma nova porta de entrada, selecione **regras de entrada** e, em seguida, selecione **nova regra**. Para uma regra de saída, selecione **regras de saída** em vez disso.

1. No **Assistente para nova regra de entrada**, selecione **porta**e, em seguida, selecione **Avançar**.

1. Selecione **TCP** ou **UDP**, dependendo do número da porta das tabelas a seguir.

1. Em **portas locais específicas**, insira um número de porta nas tabelas a seguir e selecione **Avançar**.

1. Selecione **permitir a conexão**e, em seguida, selecione **Avançar**.

1. Selecione um ou mais tipos de rede para habilitar, incluindo o tipo de rede para a conexão remota e, em seguida, selecione **Avançar**.

1. Adicione um nome para a regra (por exemplo, **msvsmon**, **IIS**ou **implantação da Web**) e, em seguida, selecione **concluir**.

   A nova regra deve aparecer e ser selecionada na lista **regras de entrada** ou **regras de saída** .

### <a name="ports-on-the-remote-computer-that-enable-remote-debugging"></a>Portas no computador remoto que habilitam a depuração remota

Para a depuração remota, as seguintes portas devem estar abertas no computador remoto:

::: moniker range="vs-2017"

|**Portas**|**Entrada/saída**|**Protocolo**|**Descrição**|
|-|-|-|-|
|4022|Entrada|TCP|Para VS 2017. O número da porta é incrementado em 2 para cada versão do Visual Studio. Para obter mais informações, consulte [atribuições de porta do depurador remoto do Visual Studio](../debugger/remote-debugger-port-assignments.md).|
|4023|Entrada|TCP|Para VS 2017. O número da porta é incrementado em 2 para cada versão do Visual Studio. Essa porta é usada apenas para depurar remotamente um processo de 32 bits de uma versão de 64 bits do depurador remoto. Para obter mais informações, consulte [atribuições de porta do depurador remoto do Visual Studio](../debugger/remote-debugger-port-assignments.md).|
|3702|Saída|UDP|Adicional Necessário para a descoberta de depurador remoto.|

::: moniker-end

::: moniker range=">= vs-2019"

|**Portas**|**Entrada/saída**|**Protocolo**|**Descrição**|
|-|-|-|-|
|4024|Entrada|TCP|Para VS 2019. O número da porta é incrementado em 2 para cada versão do Visual Studio. Para obter mais informações, consulte [atribuições de porta do depurador remoto do Visual Studio](../debugger/remote-debugger-port-assignments.md).|
|4025|Entrada|TCP|Para VS 2019. O número da porta é incrementado em 2 para cada versão do Visual Studio. Essa porta é usada apenas para depurar remotamente um processo de 32 bits de uma versão de 64 bits do depurador remoto. Para obter mais informações, consulte [atribuições de porta do depurador remoto do Visual Studio](../debugger/remote-debugger-port-assignments.md).|
|3702|Saída|UDP|Adicional Necessário para a descoberta de depurador remoto.|

::: moniker-end

Se você selecionar **usar o modo de compatibilidade gerenciado** em **ferramentas**  >  **Opções**  >  **depuração**, abra essas portas adicionais do depurador remoto. O modo de compatibilidade gerenciado do depurador habilita uma versão herdada do Visual Studio 2010 do depurador.

|**Portas**|**Entrada/saída**|**Protocolo**|**Descrição**|
|-|-|-|-|
|135, 139, 445|Saída|TCP|Obrigatórios.|
|137, 138|Saída|UDP|Obrigatórios.|

Se sua política de domínio exigir que a comunicação de rede seja executada por meio do IPSec, você deverá abrir portas adicionais no Visual Studio e nos computadores remotos. Para depurar em um servidor Web IIS remoto, abra a porta 80 no computador remoto.

|**Portas**|**Entrada/saída**|**Protocolo**|**Descrição**|
|-|-|-|-|
|500, 4500|Saída|UDP|Necessário se sua política de domínio exigir que a comunicação de rede seja executada por meio do IPSec.|
|80|Saída|TCP|Necessário para depuração de servidor Web.|

Para permitir aplicativos específicos por meio do firewall do Windows, consulte [Configurar a depuração remota por meio do firewall do Windows](#configure-remote-debugging-through-windows-firewall).

## <a name="configure-remote-debugging-through-windows-firewall"></a>Configurar a depuração remota por meio do firewall do Windows

Você pode instalar as ferramentas de depuração remota no computador remoto ou executá-las de uma pasta compartilhada. Em ambos os casos, o Firewall do computador remoto deve ser configurado corretamente.

Em um computador remoto, as ferramentas de depuração remota estão em:

*\<Visual Studio installation directory\>\\\\Depurador remoto do IDE do Common7 \\\\\<x86*, *x64*, or *Appx*\>

### <a name="allow-and-configure-the-remote-debugger-through-windows-firewall"></a>Permitir e configurar o depurador remoto por meio do firewall do Windows

1. No menu **Iniciar** do Windows, procure e abra o **Firewall do Windows**ou o **Windows Defender firewall**.

1. Selecione **permitir um aplicativo por meio do firewall do Windows**.

1. Se o **depurador remoto** ou **depurador remoto do Visual Studio** não aparecer em **aplicativos e recursos permitidos**, selecione **alterar configurações**e, em seguida, selecione **permitir outro aplicativo**.

1. Se o aplicativo do depurador remoto ainda não estiver listado na caixa de diálogo **Adicionar um aplicativo** , selecione **procurar**e navegue até * \<Visual Studio installation directory\> \\ Common7 \\ \\ do depurador remoto do IDE \\ \<x86*, *x64*, or *Appx*\> , dependendo da arquitetura apropriada para seu aplicativo. Selecione *msvsmon.exe*e, em seguida, selecione **Adicionar**.

1. Na lista de **aplicativos** , selecione o **depurador remoto** que você acabou de adicionar. Selecione **tipos de rede**e, em seguida, selecione um ou mais tipos de rede, incluindo o tipo de rede para a conexão remota.

1. Selecione **Adicionar** e, em seguida, selecione **OK**.

## <a name="troubleshoot-the-remote-debugging-connection"></a><a name="troubleshooting"></a>Solucionar problemas de conexão de depuração remota

Se você não puder anexar ao seu aplicativo com o depurador remoto, verifique se as portas do firewall de depuração remota, os protocolos, os tipos de rede e as configurações do aplicativo estão todos corretos.

- No menu **Iniciar** do Windows, procure e abra o **Firewall do Windows**e selecione **permitir um aplicativo por meio do firewall do Windows**. Verifique se o **depurador remoto** ou **depurador remoto do Visual Studio** aparece na lista de **aplicativos e recursos permitidos** com uma caixa de seleção selecionada e se os tipos de rede corretos estão selecionados. Caso contrário, [adicione os aplicativos e as configurações corretas](#configure-remote-debugging-through-windows-firewall).

- No menu **Iniciar** do Windows, procure e abra o **Firewall do Windows com segurança avançada**. Verifique se o **depurador remoto** ou **depurador remoto do Visual Studio** aparece em **regras de entrada** (e, opcionalmente, regras de **saída**) com um ícone de marca de seleção verde e se todas as configurações estão corretas.

  - Para exibir ou alterar as configurações de regra, clique com o botão direito do mouse no aplicativo do **depurador remoto** na lista e selecione **Propriedades**. Use as guias **Propriedades** para habilitar ou desabilitar a regra, ou alterar os números de porta, protocolos ou tipos de rede.
  - Se o aplicativo do depurador remoto não aparecer na lista de regras, [adicione e configure as portas corretas](#configure-ports-for-remote-debugging).

## <a name="see-also"></a>Veja também

- [Depuração remota](../debugger/remote-debugging.md)
- [Atribuições de porta do depurador remoto do Visual Studio](../debugger/remote-debugger-port-assignments.md)
