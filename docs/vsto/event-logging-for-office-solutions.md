---
title: Log de eventos para soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], event viewer
- ClickOnce deployment [Office development in Visual Studio], event viewer
- deploying applications [Office development in Visual Studio], event viewer
- Office development in Visual Studio, event viewer
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 267d3e06e9f0d4733a7985f65aa81f368c3f5413
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49925104"
---
# <a name="event-logging-for-office-solutions"></a>Log de eventos para soluções do Office
  Você pode usar o Visualizador de eventos no Windows para ver mensagens de exceção que são capturadas pelo [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ao instalar ou desinstalar soluções do Office. Você pode usar essas mensagens do agente de log de eventos para solucionar problemas de implantação e instalação.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
## <a name="read-the-event-log"></a>Ler o Log de eventos  
 Abra **Visualizador de eventos** e filtrar os eventos que você deseja ver.  
  
### <a name="to-read-the-event-log-in-windows-server-2003-and-windows-xp"></a>Para ler o Log de eventos no Windows Server 2003 e Windows XP  
  
1.  No painel de controle, abra **ferramentas administrativas**.  
  
2.  Inicie **Visualizador de eventos**.  
  
3.  Na lista de logs de eventos, selecione **aplicativo**.  
  
4.  Sobre o **modo de exibição** menu, clique em **filtro**.  
  
5.  No **origem do evento** lista, selecione **VSTO 4.0**.  
  
6.  Para eventos de instalação nos **ID do evento** , digite **4096**.  
  
7.  Clique em **Okey** para ver a exibição filtrada.  
  
### <a name="to-read-the-event-log-in-windows-7-windows-vista-and-windows-server-2008"></a>Para ler o Log de eventos no Windows 7, Windows Vista e Windows Server 2008  
  
1. No painel de controle, abra **ferramentas administrativas**.  
  
2. Inicie **Visualizador de eventos**.  
  
3. Expandir **Logs do Windows**.  
  
4. Na lista de logs de eventos, selecione **aplicativo**.  
  
5. Sobre o **ação** menu, clique em **Filtrar Log atual**.  
  
6. No **origem do evento** lista, selecione **VSTO 4.0**.  
  
7. Para eventos de instalação nos **ID do evento** , digite **4096**.  
  
8. Clique em **Okey** para ver a exibição filtrada.  
  
   O Visualizador de eventos inclui as seguintes informações:  
  
- O local do manifesto de implantação para a solução.  
  
- Uma mensagem que descreve a causa do erro ou exceção.  
  
  Essas mensagens de exceção podem ajudá-lo a determinar o motivo para um problema de instalação, como um certificado não confiável, um local do documento não confiável ou um manifesto de implantação inválido.  
  
  Depois que uma solução do Office é desinstalada, as mensagens de exceção permanecem no log de eventos.  
  
  Para mostrar ou registrar em log mensagens de exceção quando uma solução do Office está em execução, consulte [projetos do Office Debug](../vsto/debugging-office-projects.md) e [projetos do Office depurar](../vsto/debugging-office-projects.md).  
  
### <a name="localization"></a>Localização  
 O idioma da mensagem de exceção é determinado pelo Visual Studio Tools para Office runtime language. Por exemplo, se o computador do usuário final com o pacote de idioma japonês instalado, a mensagem de exceção é gravada no log de eventos em japonês.  
  
## <a name="disable-the-event-logger"></a>Desabilitar o agente de log de eventos  
 Por padrão, o agente de log de eventos é habilitado quando você instala ou desinstala as soluções do Office. Você pode desabilitar o agente de log de eventos, definindo a variável de ambiente VSTO_EVENTLOGDISABLED como "1" (um).  
  
### <a name="to-disable-the-event-log"></a>Para desabilitar o Log de eventos  
  
1.  No painel de controle, abra **sistema**.  
  
2.  Sobre o **Advanced** , clique em **variáveis de ambiente**.  
  
3.  No **variáveis do sistema** painel, clique em **New**.  
  
4.  No **nova variável do sistema** caixa de diálogo, digite **VSTO_EVENTLOGDISABLED** no **nome da variável** caixa.  
  
5.  No **valor da variável** , digite **1**.  
  
6.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)   
 [Solucionar problemas de implantação de solução do Office](../vsto/troubleshooting-office-solution-deployment.md)  
  
  