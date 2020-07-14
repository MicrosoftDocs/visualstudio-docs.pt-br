---
title: Configurar o Firewall do Windows para depuração remota | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 66e3230a-d195-4473-bbce-8ca198516014
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f232446ed699bd7cc034e4b6d6148b665830cf2d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535519"
---
# <a name="configure-the-windows-firewall-for-remote-debugging"></a>Configurar o Firewall do Windows para depuração remota
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como configurar o firewall para habilitar a depuração remota em computadores que executam os seguintes sistemas operacionais:  
  
- Windows 7  
  
- Windows 8/8.1  
  
- Windows 10  
  
- Windows Server 2008 (R2)  
  
- Windows Server 2012  
  
- Windows Server 2012 R2  
  
  Se a rede na qual você está depurando não estiver protegida por um firewall, essa configuração será desnecessária. Caso contrário, o computador que hospeda o Visual Studio e o computador remoto que será depurado exigirá alterações na configuração do firewall.  
  
  **IPSec** Se sua rede exigir que a comunicação seja executada usando o IPSec, você deverá abrir portas adicionais no computador host do Visual Studio e no computador remoto.  
  
  **Servidor Web** Se estiver depurando um servidor Web remoto, você deverá abrir uma porta adicional no computador remoto.  
  
  Observe que os dois computadores não precisam executar o mesmo sistema operacional. Por exemplo, o computador do Visual Studio pode executar o Windows 10 e o computador remoto pode executar o Windows Server 2012 R2.  
  
## <a name="to-configure-windows-firewall-on-the-visual-studio-computer"></a>Para configurar o Firewall do Windows no computador do Visual Studio  
 As instruções para configurar o Firewall do Windows diferem ligeiramente em sistemas operacionais diferentes. No Windows 7 ou no Windows Server 2008, o **programa** Word é usado; no Windows 8/8.1, Windows 10 e Windows Server 2012, o **aplicativo** Word é usado.  Nas etapas a seguir, usaremos o **aplicativo**Word.  
  
1. Abra a página Firewall do Windows. (Na caixa de pesquisa do menu **Iniciar** , digite **Firewall do Windows**).  
  
2. Clique em **Permitir um aplicativo ou recurso pelo Firewall do Windows**.  
  
3. Na lista **aplicativos e recursos permitidos** , procure **depurador remoto do Visual Studio descoberta**. Se estiver listado, verifique se ele está selecionado e se um ou mais tipos de rede também estão selecionados.  
  
4. Se **depurador remoto do Visual Studio descoberta** não estiver listada, clique em **permitir outro aplicativo**. Se você ainda não o vir na janela **Adicionar um aplicativo** , clique em **procurar** e navegue até ** \<Visual Studio installation directory> \Common7\IDE\Remote Debugger**. Localize a pasta apropriada para o aplicativo (x86, x64, AppX) e, em seguida, selecione **msvsmon.exe**. Clique em **Adicionar**.  
  
5. Na lista **aplicativos e recursos permitidos** , selecione **Visual Studio monitor de depuração remota**. Verifique um ou mais tipos de rede (**domínio, início/trabalho (privado), público**) com os quais você deseja que o monitor de depuração remota se comunique. Os tipos devem incluir a rede à qual o computador do Visual Studio está conectado.  
  
## <a name="to-open-a-port-on-the-visual-studio-computer-to-enable-discovery"></a>Para abrir uma porta no computador do Visual Studio para habilitar a descoberta  
 Você deve permitir a entrada da porta UDP 3702 para permitir a descoberta do (s) computador (es) que executam o depurador remoto. Para adicioná-lo, consulte como configurar portas em um firewall.  
  
## <a name="to-configure-the-windows-firewall-of-the-remote-computer-for-remote-debugging"></a>Para configurar o Firewall do Windows do computador remoto para depuração remota  
 Os componentes de depuração remota podem ser instalados no computador remoto ou executados a partir de um diretório compartilhado. O Firewall do computador remoto deve ser configurado em ambos os casos. Os componentes de depuração remota estão localizados em:  
  
 **\<Visual Studio installation directory>Depurador do \Common7\IDE\Remote**  
  
 As instruções para configurar o Firewall do Windows diferem ligeiramente em sistemas operacionais diferentes. No Windows 7 ou no Windows Server 2008, o **programa** Word é usado; no Windows 8/8.1, Windows 10 e Windows Server 2012, o **aplicativo** Word é usado.  Nas etapas a seguir, usaremos o **aplicativo**Word.  
  
1. Abra a página Firewall do Windows. (Na caixa de pesquisa do menu **Iniciar** , digite **Firewall do Windows**.)  
  
2. Clique em **Permitir um aplicativo ou recurso pelo Firewall do Windows**.  
  
3. Na lista de **aplicativos e recursos permitidos** , procure o **Visual Studio monitor de depuração remota**. Se estiver listado, verifique se ele está selecionado e se um ou mais tipos de rede também estão selecionados.  
  
4. Se o **Visual Studio monitor de depuração remota** não estiver listado, clique em **permitir outro aplicativo**. Se você ainda não o vir na **janela Adicionar um aplicativo**, clique em **procurar** e navegue até ** \<Visual Studio installation directory> \Common7\IDE\Remote Debugger**. Localize a pasta apropriada para o aplicativo (x86, x64, AppX) e, em seguida, selecione **msvsmon.exe**. Clique em **Adicionar**.  
  
5. Na lista de **aplicativos permitidos** , selecione **Visual Studio monitor de depuração remota**. Verifique um ou mais tipos de rede (**domínio, início/trabalho (privado), público**) com os quais você deseja que o monitor de depuração remota se comunique. Os tipos devem incluir a rede à qual o computador do Visual Studio está conectado.  
  
## <a name="ports-on-the-remote-computer-that-enable-remote-debugging"></a>Portas no computador remoto que habilitam a depuração remota  
  
|**Portas**|**Entrada/saída**|**Protocolo**|**Descrição**|  
|-|-|-|-|
|3702|Saída|UDP|Necessário para a descoberta de depurador remoto.|  
|4020||TCP|Para VS 2015. O número da porta é incrementado por 2 para cada versão do Visual Studio. Para obter mais informações, consulte Depurador Remoto do Visual Studio atribuições de porta.|  
|4021||TCP|Para VS 2015. O número da porta é incrementado por 2 para cada versão do Visual Studio. Para obter mais informações, consulte Depurador Remoto do Visual Studio atribuições de porta.|  
  
## <a name="ports-on-the-remote-computer-that-enable-remote-debugging-with-managed-or-native-compatibility-mode"></a>Portas no computador remoto que habilitam a depuração remota com modo de compatibilidade gerenciado ou nativo  
  
|**Portas**|**Entrada/saída**|**Protocolo**|**Descrição**|  
|-|-|-|-|  
|135, 139, 445|Saída|TCP|Obrigatórios.|  
|137, 138|Saída|UDP|Obrigatórios.|  
|500, 4500|Saída|UDP|Necessário se sua política de domínio exigir que a comunicação de rede seja executada por meio do IPSec.|  
|80|Saída|TCP|Necessário para depuração de servidor Web.|  
  
## <a name="how-to-configure-ports-in-windows-firewall"></a>Como configurar portas no firewall do Windows  
  
1. No menu **Iniciar** , procure por **Firewall do Windows com segurança avançada**.  
  
2. Clique em **regras de entrada** ou de **saída** e, em seguida, clique em **nova regra** na lista **ações** .  
  
3. Na página **tipo de regra** , selecione **porta** e clique em **Avançar**.  
  
4. Na página **protocolo e portas** , selecione o protocolo de porta (TCP ou UDP). Selecione **portas locais específicas** e insira um ou mais números de porta que você deseja habilitar para o protocolo. Separe os números com vírgulas. Em seguida, clique em **Próximo**.  
  
5. Na página **ação** , selecione **permitir a conexão** e clique em **Avançar**.  
  
6. Na página **perfil** , selecione um ou mais tipos de rede a serem habilitados para a porta. O tipo selecionado deve incluir a rede à qual o computador remoto está conectado. Em seguida, clique em **Próximo**.  
  
7. Na página **nome** , digite um nome para a regra e clique em **concluir**.  
  
8. Você deve ver sua nova regra na lista **regras de entrada** ou **regras de saída** .  
  
## <a name="see-also"></a>Consulte Também  
 [Depuração remota](../debugger/remote-debugging.md)
