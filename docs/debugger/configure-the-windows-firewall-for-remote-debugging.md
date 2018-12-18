---
title: Configurar o Firewall do Windows para depuração remota | Microsoft Docs
ms.date: 10/31/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 66e3230a-d195-4473-bbce-8ca198516014
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: da505c6193dd7d05cc10a8e7cec8383f8ee3adfc
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53058591"
---
# <a name="configure-windows-firewall-for-remote-debugging"></a>Configurar o Firewall do Windows para depuração remota

Em uma rede protegida por Firewall do Windows, o firewall deve ser configurado para permitir a depuração remota. Experimente o Visual Studio e as ferramentas de depuração remotas abrir as portas de firewall corretas durante a instalação ou de inicialização, mas você pode também precisa abrir portas ou permitir que os aplicativos manualmente. 

Este tópico descreve como configurar o firewall do Windows para habilitar a depuração remota no Windows 10, 8/8.1 e 7; e computadores com Windows Server 2012 R2, 2012 e 2008 R2. O Visual Studio e o computador remoto não precisam estar executando o mesmo sistema operacional. Por exemplo, o computador do Visual Studio pode executar o Windows 10 e o computador remoto pode executar o Windows Server 2012 R2.      
  
>[!NOTE]
>As instruções para configurar o firewall do Windows são ligeiramente diferem em diferentes sistemas operacionais e para versões mais antigas do Windows. Configurações do Windows 8/8.1, Windows 10 e Windows Server 2012 usam a palavra *app*, enquanto o Windows 7 e Windows Server 2008 usam a palavra *programa*.  

## <a name="configure-ports-for-remote-debugging"></a>Configurar portas para depuração remota  

Visual Studio e o depurador remoto tentam abrir as portas corretas durante a instalação ou a inicialização. No entanto, em alguns cenários, como um firewall de terceiros, talvez você precise abrir portas manualmente. 

**Para abrir uma porta:**
  
1. No Windows **inicie** menu, procure e abra **Firewall do Windows com segurança avançada**. No Windows 10, isso é **Windows Defender Firewall com segurança avançada**.
   
1. Para uma nova porta de entrada, selecione **regras de entrada** e, em seguida, selecione **nova regra**. Para uma regra de saída, selecione **regras de saída** em vez disso.

1. No **novo Assistente de regra de entrada**, selecione **porta**e, em seguida, selecione **próxima**. 
   
1. Selecione a **TCP** ou **UDP**, dependendo do número da porta nas tabelas a seguir.
   
1. Sob **portas locais específicas**, digite um número de porta entre as tabelas a seguir e selecione **próxima**.
   
1. Selecione **permitir a Conexão**e, em seguida, selecione **próxima**.
   
1. Selecione um ou mais tipos de rede para habilitar, incluindo o tipo de rede para a conexão remota e, em seguida, selecione **próxima**.
   
1. Adicionar um nome para a regra (por exemplo, **msvsmon**, **IIS**, ou **implantação da Web**) e, em seguida, selecione **concluir**.

   A nova regra deve aparecer e ser selecionada a **regras de entrada** ou **regras de saída** lista.

### <a name="ports-on-the-remote-computer-that-enable-remote-debugging"></a>Portas que habilitar a depuração remota no computador remoto

Para depuração remota, as portas a seguir devem estar abertas no computador remoto:

|**Portas**|**Entrada/saída**|**Protocolo**|**Descrição**|   
|-|-|-|-|
|4022|Entrada|TCP|Para VS 2017. O porta número é incrementado por 2 para cada versão do Visual Studio. Para obter mais informações, consulte [atribuições de porta de depurador remoto do Visual Studio](../debugger/remote-debugger-port-assignments.md).|  
|4023|Entrada|TCP|Para VS 2017. O porta número é incrementado por 2 para cada versão do Visual Studio. Essa porta é apenas usada para remoto depurar um processo de 32 bits de uma versão de 64 bits do depurador remoto. Para obter mais informações, consulte [atribuições de porta de depurador remoto do Visual Studio](../debugger/remote-debugger-port-assignments.md).| 
|3702|Saída|UDP|(Opcional) Necessário para a descoberta de depurador remoto.|    
  
Se você selecionar **usar o modo de compatibilidade gerenciado** sob **ferramentas** > **opções** > **depuração**, abra Essas portas adicionais do depurador remoto. Modo de compatibilidade do depurador gerenciado habilita uma herdado, a versão do Visual Studio 2010 do depurador. 

|**Portas**|**Entrada/saída**|**Protocolo**|**Descrição**|  
|-|-|-|-|  
|135, 139, 445|Saída|TCP|Necessário.|  
|137, 138|Saída|UDP|Necessário.|  

Se sua diretiva de domínio requer comunicação de rede a ser executada por meio de IPSec, é necessário abrir portas adicionais nos computadores remotos e Visual Studio. Para depurar em um servidor de web IIS remoto, abra a porta 80 no computador remoto.

|**Portas**|**Entrada/saída**|**Protocolo**|**Descrição**|  
|-|-|-|-|  
|500, 4500|Saída|UDP|Necessário se a sua diretiva de domínio requer comunicação de rede a ser executada por meio de IPSec.|  
|80|Saída|TCP|Necessário para a depuração do servidor web.|

Para permitir que aplicativos específicos por meio do firewall do Windows, consulte [configurar a depuração remota por meio do Firewall do Windows](#configure-remote-debugging-through-windows-firewall). 

## <a name="configure-remote-debugging-through-windows-firewall"></a>Configurar a depuração remota por meio do firewall do Windows

Você pode instalar as ferramentas de depuração remotas no computador remoto ou executá-los de uma pasta compartilhada. Em ambos os casos, o firewall do computador remoto deve ser configurado corretamente. 

Em um computador remoto, as ferramentas de depuração remotas estão em:  
  
*\<Diretório de instalação do Visual Studio\>\\Common7\\IDE\\depurador remoto\\\<x86*, *x64*, ou  *AppX*\> 
  
### <a name="allow-and-configure-the-remote-debugger-through-windows-firewall"></a>Permitir e configurar o depurador remoto por meio do Firewall do Windows 
  
1. No Windows **inicie** menu, procure e abra **Firewall do Windows**, ou **Windows Defender Firewall**. 
  
1. Selecione **permitem que um aplicativo por meio do Firewall do Windows**.  
  
1.  Se **depurador remoto** ou **depurador remoto do Visual Studio** não aparecer sob **aplicativos e recursos permitidos**, selecione **alterar configurações**e, em seguida, selecione **permitir que o outro aplicativo**. 

1.  Se o aplicativo depurador remoto ainda não estiver listado na **adicionar um aplicativo** caixa de diálogo, selecione **procurar**e navegue até  *\<diretório de instalação do Visual Studio\> \\Common7\\IDE\\depurador remoto\\\<x86*, *x64*, ou *Appx* \> , dependendo da arquitetura apropriada para seu aplicativo. Selecione *msvsmon.exe*e, em seguida, selecione **Add**.  
    
1.  No **aplicativos** lista, selecione o **depurador remoto** que você acabou de adicionar. Selecione **tipos de rede**e, em seguida, selecione um ou mais tipos de rede, incluindo o tipo de rede para a conexão remota. 
    
1.  Selecione **Add**e, em seguida, selecione **Okey**.

## <a name="troubleshooting"></a>Solucionar problemas de conexão de depuração remota
  
Se você não é possível anexar ao seu aplicativo com o depurador remoto, verifique se as portas de firewall depuração remota, protocolos, tipos de rede e configurações do aplicativo estão todos corretas. 

- No Windows **inicie** menu, procure e abra **Firewall do Windows**e selecione **permitem que um aplicativo por meio do Firewall do Windows**. Certifique-se **depurador remoto** ou **depurador remoto do Visual Studio** aparece no **aplicativos e recursos permitidos** lista com uma caixa de seleção e os tipos de rede corretos são selecionado. Caso contrário, [adicione as configurações e os aplicativos corretos](#configure-remote-debugging-through-windows-firewall).
  
- No Windows **inicie** menu, procure e abra **Firewall do Windows com segurança avançada**. Certifique-se **1&gt;{2&gt;Iniciando** ou **depurador remoto do Visual Studio** aparece sob **regras de entrada** (e, opcionalmente, **regras de saída**) com um ícone de marca de seleção verde e que todas as configurações estão corretas. 
  
  - Para exibir ou alterar as configurações de regra, clique com botão direito do **depurador remoto** aplicativo na lista e selecione **propriedades**. Use o **propriedades** guias para habilitar ou desabilitar a regra ou alterar tipos de rede, protocolos ou números de porta. 
  - Se o aplicativo depurador remoto não aparecer na lista de regras [adicionar e configurar as portas corretas](#configure-ports-for-remote-debugging). 

## <a name="see-also"></a>Consulte também  
[Depuração remota](../debugger/remote-debugging.md)

[Atribuições de porta do Visual Studio depurador remoto](../debugger/remote-debugger-port-assignments.md)
