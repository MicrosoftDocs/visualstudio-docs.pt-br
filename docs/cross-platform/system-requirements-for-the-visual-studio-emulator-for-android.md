---
title: Requisitos do sistema para o emulador do Visual Studio para Android | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-mobile
ms.topic: conceptual
ms.assetid: 35e766ad-269f-41e4-ba23-74a556c315f3
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1ea73057992447016b1b9ac68c98b79b68f70c17
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49881606"
---
# <a name="system-requirements-for-the-visual-studio-emulator-for-android"></a>Requisitos do sistema para o Emulador do Visual Studio para Android
O Emulador do Visual Studio para Android é executado como uma máquina virtual no Hyper-V, a tecnologia de virtualização para o Windows 8 e versões posteriores. Para executar o emulador, o computador deve atender aos requisitos para executar o Hyper-V, conforme descrito neste tópico.  
  
 O programa de instalação tenta configurar esses pré-requisitos para você silenciosamente durante a instalação do emulador. Quando a instalação configurar os pré-requisitos com êxito, o emulador funcionará apenas como esperado. Caso contrário, talvez você precise habilitar esses pré-requisitos manualmente. Se você precisar configurar os pré-requisitos manualmente, as etapas e ferramentas serão as mesmas etapas descritas [aqui](/previous-versions/windows/apps/jj863509\(v=vs.105\)) para o Emulador do Windows Phone.  
  
> [!IMPORTANT]
>  O programa de instalação do emulador verifica os pré-requisitos para executar o Emulador do Visual Studio para Android. Exibirá avisos se os pré-requisitos não estiverem presentes, mas não os exige.  
  
 Este tópico contém as seções a seguir.  
  
-   [Lista de verificação rápida](#Checklist)  
  
-   [Requisitos do sistema](#System)  
  
-   [Requisitos de rede](#Network)  
  
-   [Requisitos do Hyper-V](#HyperV)  
  
-   [Não há suporte para a execução do emulador por meio de um VHD inicializável](#BootableVHD)  
  
-   [O Hyper-V exige arquivos descompactados e não criptografados](#Files)  
  
##  <a name="Checklist"></a> Lista de verificação rápida  
 Esta é uma lista de verificação rápida dos requisitos para executar o Emulador do Visual Studio para Android. Para obter informações mais detalhadas, consulte as próximas seções neste tópico.  
  
 Requisitos do sistema  
  
- Suporte ao Hyper-V (consulte os requisitos do Hyper-V abaixo)  
  
- 6 GB ou mais de RAM.  
  
- versão de 64 bits da edição Pro do Windows 8, Windows 8.1, Windows 10 ou superior  
  
- Um processador que dá suporte ao SSSE3 ou posterior.  
  
  Requisitos de rede  
  
- DHCP  
  
- Definições de gateway e DNS configuradas automaticamente  
  
  Requisitos do Hyper-V  
  
- No BIOS, os seguintes recursos devem ter suporte:  
  
  -   Virtualização assistida por hardware  
  
  -   SLAT (Conversão de Endereços de Segundo Nível)  
  
  -   DEP (Prevenção de Execução de Dados) baseada em hardware  
  
- No Windows, o Hyper-V deve estar habilitado e em execução.  
  
- Você precisa ser um membro do grupo local Administradores do Hyper-V.  
  
##  <a name="System"></a> Requisitos do sistema  
 O computador deve atender aos seguintes requisitos:  
  
- Suporte ao Hyper-V (consulte [Requisitos do Hyper-V](#HyperV))  
  
- 6 GB ou mais de RAM.  
  
- versão de 64 bits da edição Pro do Windows 8, Windows 8.1, Windows 10 ou superior.  
  
  Para verificar os requisitos de RAM e do Windows, no Painel de Controle, escolha Sistema e Segurança e, em seguida, Sistema.  
  
  ![Verificar os requisitos do sistema](../cross-platform/media/android_emu_system_requirements.png "Android_Emu_System_Requirements")  
  
##  <a name="Network"></a> Requisitos de rede  
 A rede deve atender aos seguintes requisitos:  
  
- DHCP  
  
   O emulador exige o DHCP, pois configura a si mesmo como um dispositivo separado na rede com seu próprio endereço IP.  
  
- Definições de gateway e DNS configuradas automaticamente  
  
   Não é possível definir as configurações de gateway e DNS manualmente para o emulador.  
  
  Para solucionar problemas de rede no emulador, consulte os seguintes tópicos:  
  
- [Solução de problemas do emulador do Visual Studio para Android](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md)  
  
##  <a name="HyperV"></a> Requisitos do Hyper-V  
 Requisitos do Hyper-V no BIOS  
  
 O BIOS do computador deve dar suporte aos seguintes requisitos e eles devem estar habilitados:  
  
- Virtualização assistida por hardware  
  
- SLAT (Conversão de Endereços de Segundo Nível)  
  
- DEP (Prevenção de Execução de Dados) baseada em hardware  
  
  Requisitos do Hyper-V no Windows  
  
  Quando definições do computador e do BIOS já estiverem configuradas para dar suporte ao Hyper-V, o programa de instalação habilitará e iniciará o Hyper-V. Caso contrário, talvez você precise habilitar esses requisitos manualmente.  
  
|Requisito|Como verificar e habilitar esse requisito|  
|-----------------|----------------------------------------------|  
|O Hyper-V deve ser instalado|Siga as mesmas instruções usadas para [habilitar o Hyper-V para o emulador do Windows Phone](https://docs.microsoft.com/previous-versions/windows/apps/jj863509(v=vs.105)).<br /><br /> Verifique o status do serviço **Gerenciamento de Máquinas Virtuais do Hyper-V** no snap-in Serviços.|  
|O Hyper-V deve estar em execução.|Para obter mais informações sobre como gerenciar serviços, consulte os seguintes tópicos:<br /><br /> -   [Iniciar, interromper, pausar, retomar ou reiniciar um serviço](https://technet.microsoft.com/library/cc736564\(v=WS.10\).aspx)<br />-   [Configurar o modo de inicialização de um serviço](https://technet.microsoft.com/%20library/cc739213\(v=ws.10\))|  
  
 Você precisa ser um membro do grupo local Administradores do Hyper-V.  
  
 Para executar o Emulador do Visual Studio para Android sem um prompt recorrente para elevar seus direitos, você precisa ser membro do grupo local Administradores do Hyper-V. Se você já for um administrador local no computador quando você instalar o SDK, o programa de instalação do SDK o adicionará ao grupo Administradores do Hyper-V. Caso contrário, talvez você precise habilitar esse requisito manualmente.  
  
 Ao executar o emulador, se você ainda não for membro do grupo Administradores do Hyper-V, será necessário ingressar no grupo (a caixa de diálogo refere-se ao Emulador do Windows Phone). Ingressar no grupo exige direitos de administrador.  
  
> [!IMPORTANT]
> Depois de ingressar no grupo, faça logoff ou reinicie o computador para que as alterações tenham efeito.  
  
 ![Ingressar no grupo de segurança Administradores do Hyper&#45;V](../cross-platform/media/android_emu_hyperv_admin.png "Android_Emu_HyperV_Admin")  
  
 Para adicionar você mesmo a um grupo manualmente, abra o snap-in Usuários e Grupos Locais.  
  
##  <a name="BootableVHD"></a> Não há suporte para a execução do emulador por meio de um VHD inicializável  
 Se você tentar executar um aplicativo no Emulador do Visual Studio para Android enquanto estiver executando o Windows por meio de um VHD inicializável, normalmente, o emulador levará vários minutos para ser iniciado ou não será iniciado. Quando o emulador falha ao iniciar, você recebe a seguinte mensagem: Falha na implantação do aplicativo. Tente novamente.  
  
 Essa configuração não tem suporte. Para obter informações sobre problemas relacionados, confira [Solução de problemas do Emulador do Visual Studio para Android](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md).  
  
##  <a name="Files"></a> O Hyper-V exige arquivos descompactados e não criptografados  
 Em um disco rígido configurado com o sistema de arquivos NTFS, os arquivos do disco rígido virtual usados pelo Hyper-V devem ser descompactados e descriptografados. Verifique se os seguintes diretórios não estão compactados nem criptografados:  
  
- %localappdata%\Microsoft\XDE  
  
- C:\Program Files (x86)\Microsoft Emulator Manager  
  
- C:\Program Files (x86)\Microsoft Visual Studio Emulator for Android  
  
- %localappdata%\Microsoft\VisualStudioEmulator  
  
  No sistema de arquivos ReFS, os arquivos do disco rígido virtual não devem ter o bit de integridade definido.  
  
## <a name="hardware-graphics-forwarding-opengl-es-support-requirements"></a>Requisitos do encaminhamento de elementos gráficos de hardware (suporte ao OpenGL ES)  
 Para que o emulador emule chamadas à GPU, como aquelas usadas pelo OpenGL ES, o computador deve ter uma GPU compatível com DirectX com drivers DirectX apropriados instalados.  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas do Emulador do Visual Studio para Android](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md)
