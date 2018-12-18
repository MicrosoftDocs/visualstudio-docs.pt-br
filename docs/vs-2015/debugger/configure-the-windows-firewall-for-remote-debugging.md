---
title: Configurar o Firewall do Windows para depuração remota | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 66e3230a-d195-4473-bbce-8ca198516014
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 39854b47bd31660fdc523bfd122363d5958df8e2
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51734592"
---
# <a name="configure-the-windows-firewall-for-remote-debugging"></a>Configurar o Firewall do Windows para depuração remota
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como configurar o firewall para habilitar a depuração remota em computadores que executam sistemas operacionais a seguir:  
  
- Windows 7  
  
- Windows 8/8.1  
  
- Windows 10  
  
- Windows Server 2008 (R2)  
  
- Windows Server 2012  
  
- Windows Server 2012 R2  
  
  Se a rede na qual você está depurando não estiver protegida por um firewall, essa configuração é desnecessária. Caso contrário, o computador que hospeda o Visual Studio e o computador remoto a ser depurado exigem alterações à configuração do firewall.  
  
  **IPSec** se sua rede exigir que a comunicação ser realizadas usando o IPSec, você deve abrir portas adicionais no computador host do Visual Studio e o computador remoto.  
  
  **Servidor Web** se você estiver depurando um servidor Web remoto, você deve abrir uma porta adicional no computador remoto.  
  
  Observe que ambos os computadores não é preciso executar o mesmo sistema operacional. Por exemplo, o computador do Visual Studio pode executar o Windows 10 e o computador remoto pode executar o Windows Server 2012 R2.  
  
## <a name="to-configure-windows-firewall-on-the-visual-studio-computer"></a>Para configurar o Firewall do Windows no computador do Visual Studio  
 As instruções para configurar o firewall do Windows é um pouco diferem em diferentes sistemas operacionais. No Windows 7 ou Windows Server 2008, a palavra **programa** é usado; no Windows 8/8.1, Windows 10 e Windows Server 2012, a palavra **aplicativo** é usado.  Nas etapas a seguir, usaremos a palavra **aplicativo**.  
  
1.  Abra a página do Firewall do Windows. (Na **inicie** caixa Pesquisar do menu, digite **Firewall do Windows**).  
  
2.  Clique em **permitir um aplicativo ou recurso pelo Firewall do Windows**.  
  
3.  No **aplicativos e recursos permitidos** lista, procure **descoberta do depurador do Visual Studio remota**. Se estiver listado, certifique-se de que ele está selecionado e que um ou mais tipos de rede também são selecionados.  
  
4.  Se **descoberta do depurador do Visual Studio remota** não é listado, clique em **permitir que o outro aplicativo**. Se você ainda não estiver visível na **adicionar um aplicativo** janela, clique em **procurar** e navegue até  **\<diretório de instalação do Visual Studio > \Common7\IDE\Remotedodepurador**. Localize a pasta apropriada para o aplicativo (x86, x64, Appx) e, em seguida, selecione **msvsmon.exe**. Em seguida, clique em **adicionar**.  
  
5.  No **aplicativos e recursos permitidos** lista, selecione **Visual Studio Remote Debugging Monitor**. Verificar um ou mais tipos de rede (**domínio, Home/Work (privada), público**) que você deseja que o monitor de depuração remota para se comunicar com. Os tipos devem incluir a rede à qual o computador do Visual Studio está conectado.  
  
## <a name="to-open-a-port-on-the-visual-studio-computer-to-enable-discovery"></a>Para abrir uma porta no computador do Visual Studio para habilitar a descoberta  
 Você deve permitir a porta UDP 3702 entrada permitir a descoberta de computadores executando o depurador remoto. Para adicioná-lo, consulte como configurar portas no Firewall.  
  
## <a name="to-configure-the-windows-firewall-of-the-remote-computer-for-remote-debugging"></a>Para configurar o firewall do Windows do computador remoto para depuração remota  
 Os componentes de depuração remotos podem ser instalados no computador remoto ou executar a partir de um diretório compartilhado. O firewall do computador remoto deve ser configurado em ambos os casos. Os componentes de depuração remotos estão localizados em:  
  
 **\<Diretório de instalação do Visual Studio > \Common7\IDE\Remote depurador**  
  
 As instruções para configurar o firewall do Windows é um pouco diferem em diferentes sistemas operacionais. No Windows 7 ou Windows Server 2008, a palavra **programa** é usado; no Windows 8/8.1, Windows 10 e Windows Server 2012, a palavra **aplicativo** é usado.  Nas etapas a seguir, usaremos a palavra **aplicativo**.  
  
1.  Abra a página do Firewall do Windows. (Na **inicie** caixa Pesquisar do menu, digite **Firewall do Windows**.)  
  
2.  Clique em **permitir um aplicativo ou recurso pelo Firewall do Windows**.  
  
3.  No **aplicativos e recursos permitidos** lista, procure **Visual Studio Remote Debugging Monitor**. Se estiver listado, certifique-se de que ele está selecionado e que um ou mais tipos de rede também são selecionados.  
  
4.  Se **Visual Studio Remote Debugging Monitor** não é listado, clique em **permitir que o outro aplicativo**. Se você ainda não estiver visível na **adicionar uma janela de aplicativo**, clique em **procurar** e navegue até  **\<diretório de instalação do Visual Studio > \Common7\IDE\Remotedodepurador**. Localize a pasta apropriada para o aplicativo (x86, x64, Appx) e, em seguida, selecione **msvsmon.exe**. Em seguida, clique em **adicionar**.  
  
5.  No **aplicativos permitidos** lista, selecione **Visual Studio Remote Debugging Monitor**. Verificar um ou mais tipos de rede (**domínio, Home/Work (privada), público**) que você deseja que o monitor de depuração remota para se comunicar com. Os tipos devem incluir a rede à qual o computador do Visual Studio está conectado.  
  
## <a name="ports-on-the-remote-computer-that-enable-remote-debugging"></a>Portas que habilitar a depuração remota no computador remoto  
  
|||||  
|-|-|-|-|  
|**Portas**|**Entrada/saída**|**Protocolo**|**Descrição**|  
|3702|Saída|UDP|Necessário para a descoberta de depurador remoto.|  
|4020||TCP|Para VS 2015. O número da porta é incrementado em 2 para cada versão do Visual Studio. Para obter mais informações, consulte o Visual Studio Remote Debugger atribuições de porta.|  
|4021||TCP|Para VS 2015. O número da porta é incrementado em 2 para cada versão do Visual Studio. Para obter mais informações, consulte o Visual Studio Remote Debugger atribuições de porta.|  
  
## <a name="ports-on-the-remote-computer-that-enable-remote-debugging-with-managed-or-native-compatibility-mode"></a>Portas no computador remoto que habilitar a depuração remota com o modo de compatibilidade gerenciado ou nativo  
  
|||||  
|-|-|-|-|  
|**Portas**|**Entrada/saída**|**Protocolo**|**Descrição**|  
|135, 139, 445|Saída|TCP|Necessário.|  
|137, 138|Saída|UDP|Necessário.|  
|500, 4500|Saída|UDP|Necessário se a sua diretiva de domínio requer comunicação de rede a ser executada por meio de IPSec.|  
|80|Saída|TCP|Necessário para a depuração de servidor Web.|  
  
## <a name="how-to-configure-ports-in-windows-firewall"></a>Como configurar portas no Firewall do Windows  
  
1.  Sobre o **inicie** menu, procure **Firewall do Windows com segurança avançada**.  
  
2.  Clique em **regras de entrada** ou **regras de saída** e, em seguida, clique em **nova regra** no **ações** lista.  
  
3.  Sobre o **tipo de regra** página, selecione **porta** e, em seguida, clique em **próxima**.  
  
4.  Sobre o **protocolo e portas** , selecione o protocolo de porta (TCP ou UDP). Selecione **portas locais específicas** e insira um ou mais números de porta que você deseja habilitar para o protocolo. Números separados por vírgulas. Clique em **Avançar**.  
  
5.  Sobre o **ação** página, selecione **permitir a conexão** e, em seguida, clique em **próxima**.  
  
6.  Sobre o **perfil** , selecione um ou mais tipos de rede para habilitar para a porta. O tipo selecionado deve incluir a rede à qual o computador remoto está conectado. Clique em **Avançar**.  
  
7.  Sobre o **nome** página, digite um nome para a regra e, em seguida, clique em **concluir**.  
  
8.  Você deve ver sua nova regra na **regras de entrada** ou **regras de saída** lista.  
  
## <a name="see-also"></a>Consulte também  
 [Depuração remota](../debugger/remote-debugging.md)



