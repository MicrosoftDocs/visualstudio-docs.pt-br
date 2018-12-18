---
title: Guia do administrador do Help Viewer | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4340c69f-b96b-4932-bb82-38b16a5ab149
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f470c55b08cc559e481ed75e962fda4f0e625a5c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49871284"
---
# <a name="help-viewer-administrator-guide"></a>Guia do administrador do Help Viewer
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Visualizador da Ajuda permite que você gerencie instalações da ajuda local para ambientes de rede com ou sem acesso à internet. O conteúdo da Ajuda local é configurado por máquina. Por padrão, os usuários devem ter direitos de administrador para atualizar a instalação da Ajuda local.  
  
 Se o seu ambiente de rede permitir que clientes acessem a Internet, o Visualizador da Ajuda permitirá que você use scripts de linha de comando para implantar conteúdo da Ajuda local da Internet.  
  
 Se o seu ambiente de rede não permitir que clientes acessem a Internet, o Visualizador da Ajuda poderá implantar conteúdo da Ajuda local da intranet ou de um compartilhamento de rede. Você também pode desabilitar as opções da ajuda do IDE do Visual Studio, como ajuda online/offline, instalação de conteúdo no primeiro lançamento do IDE, especificação de um serviço de conteúdo da Intranet, gerenciamento de conteúdo e uso de substituições de chaves do registro.  
  
 A sintaxe básica é a seguinte:  
  
 \<*caminho para*>\HlpCtntmgr.exe /operation \<*argumento*> /catalogname \<*nome*> /locale \<*localidade*> /sourceuri \<*caminho .msha ou URL*>  
  
 Para obter mais informações sobre a sintaxe de linha de comando HlpCtntMgr.exe, consulte [Argumentos da linha de comando para o Gerenciador de Conteúdo da Ajuda](../ide/command-line-arguments-for-the-help-content-manager.md).  
  
 Para obter mais informações sobre como criar conteúdo, criar um ponto de extremidade de serviço de Intranet e tipos de atividades semelhantes, consulte o SDK do Visualizador da Ajuda.  
  
## <a name="deploying-local-help-content-from-the-internet"></a>Implantando o conteúdo da ajuda local da Internet  
 Você pode usar o serviço de empacotamento de conteúdo do MSDN para implantar o conteúdo da ajuda local da Internet para computadores do cliente. Use a seguinte sintaxe:  
  
 \\<*caminho para*>\v2.2\HlpCtntmgr.exe /operation \<*nome*> /catalogname \<*nome de catálogo*> /locale \<*localidade*>  
  
 Para obter mais informações sobre a sintaxe de linha de comando HlpCtntMgr.exe, consulte [Argumentos da linha de comando para o Gerenciador de Conteúdo da Ajuda](../ide/command-line-arguments-for-the-help-content-manager.md).  
  
 Requisitos:  
  
- Os computadores cliente devem ter acesso à Internet.  
  
- Os usuários devem ter direitos de administrador para atualizar, adicionar, ou remover o conteúdo da ajuda local depois que foi instalado.  
  
  Restrições:  
  
- A fonte padrão para a ajuda ainda será online.  
  
  > [!TIP]
  >  Você pode alterar a fonte padrão da Ajuda modificando a chave do Registro HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\14.0\help\UseOnlineHelp. Para obter mais informações, consulte [Substituições do Gerenciador de Conteúdo da Ajuda](../ide/help-content-manager-overrides.md).  
  
- Os clientes serão solicitados ainda a instalar o conteúdo da ajuda básica na primeira inicialização do Visual Studio. Você pode desabilitar esse prompt alterando a chave do Registro HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VisualStudio\14.0\Help\DisableFirstRunHelpSelection.  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir instala o conteúdo do inglês para o Visual Studio para um computador cliente.  
  
##### <a name="to-install-english-content-from-the-internet"></a>Para instalar o conteúdo em inglês da Internet  
  
1.  Escolha **Iniciar** e **Executar**.  
  
2.  Digite o seguinte:  
  
     C:\Program Files (x86)\Microsoft Help Viewer\v2.2\hlpctntmgr.exe /operation install /catalogname VisualStudio14 /locale en-us  
  
3.  Pressione ENTER.  
  
## <a name="deploying-pre-installed-local-help-content-on-client-computers"></a>Implantando o conteúdo pré-instalado da Ajuda Local em computadores cliente  
 Você pode instalar um conjunto de conteúdo online em um computador, e então copiar o conjunto de conteúdo instalado em outros computadores.  
  
 Requisitos:  
  
- O computador que você instala o conjunto de conteúdo deve ter acesso à Internet.  
  
- Os usuários devem ter direitos de administrador para atualizar, adicionar, ou remover o conteúdo da ajuda local depois que foi instalado.  
  
  > [!TIP]
  >  Se os usuários não tiverem direitos de administrador, é recomendável que você desabilite a guia Gerenciar Conteúdo no Visualizador da Ajuda. Para obter mais informações, consulte [Substituições do Gerenciador de Conteúdo da Ajuda](../ide/help-content-manager-overrides.md).  
  
  Restrições:  
  
- Se os usuários não tiverem direitos de administrador, é recomendável que você desabilite a guia Gerenciar Conteúdo no Visualizador da Ajuda. Para obter mais informações, consulte [Substituições do Gerenciador de Conteúdo da Ajuda](../ide/help-content-manager-overrides.md).  
  
- A fonte padrão para a ajuda ainda será online.  
  
- Os clientes serão solicitados ainda a instalar o conteúdo da ajuda básica na primeira inicialização do Visual Studio. Para obter mais informações, consulte [Substituições do Gerenciador de Conteúdo da Ajuda](../ide/help-content-manager-overrides.md).  
  
### <a name="create-the-content-set"></a>Crie o conjunto de conteúdo  
 Antes de criar o conjunto de conteúdo básico, primeiro você deve desinstalar todo o conteúdo local do Visual Studio no computador de destino.  
  
##### <a name="to-uninstall-local-help"></a>Para desinstalar a ajuda local  
  
1. No Help Viewer, escolha a guia **Gerenciar Conteúdo**.  
  
2. Em **Documentação Disponível**, navegue até o conjunto de documentos do Visual Studio.  
  
3. Escolha **Remover** ao lado de cada subitem.  
  
4. Escolha **Iniciar** para desinstalar  
  
5. Navegue para *n*:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio12 e verifique se a pasta contém somente o arquivo catalogType.xml.  
  
   Depois que remover todo conteúdo da Ajuda do Visual Studio local, você estará pronto para fazer download da ajuda do Visual Studio local, você está pronto para baixar o conjunto de conteúdo básico.  
  
##### <a name="to-download-the-content"></a>Para baixar o conteúdo  
  
1. No Help Viewer, escolha a guia **Gerenciar Conteúdo**.  
  
2. Em **Documentação Disponível**, navegue até os conjuntos de documentação que você deseja baixar e escolha **Adicionar**.  
  
3. Escolha **Iniciar**.  
  
   Em seguida, você precisará empacotar o conteúdo para que ele seja implantado em computadores clientes.  
  
##### <a name="to-package-the-content"></a>Para criar um pacote com o conteúdo  
  
1.  Crie uma pasta para copiar o conteúdo para uma implantação posterior.  
  
     Por exemplo: c:\VS12Help.  
  
2.  Abra cmd.exe com permissões de administrador.  
  
3.  Navegue até a pasta que você criou na etapa 1.  
  
4.  Digite o seguinte:  
  
     Xcopy %SYSTEMDRIVE%\ProgramData\Microsoft\HelpLibrary2 \<*nome da pasta*>\ /y /e /k /o  
  
     Por exemplo: `Xcopy %SYSTEMDRIVE%\ProgramData\Microsoft\HelpLibrary2 c:\VS12Help\ /y /e /k /o`  
  
### <a name="deploying-the-content"></a>Implantando o conteúdo  
  
##### <a name="to-deploy-the-content"></a>Para implantar o conteúdo  
  
1.  Crie um compartilhamento de rede e copie o conteúdo da ajuda três para esse local.  
  
     Por exemplo, copie o conteúdo em c:\VS12Help para \\\myserver\VS12Help.  
  
2.  Crie um arquivo .bat para conter o script de implantação do conteúdo da ajuda. Como o cliente provavelmente tenha um bloqueio de leitura em alguns dos arquivos que estão sendo excluídos como parte do envio, você deve encerrar cliente antes de enviar atualizações.  
  
     Por exemplo:  
  
    ```  
    REM - copy pre-ripped content to ProgramData  
    Xcopy %~dp0HelpLibrary2 %SYSTEMDRIVE%\ProgramData\Microsoft\HelpLibrary2\ /y /e /k /o  
    if ERRORLEVEL 1 ECHO *** ERROR COPYING Help Library files to Programdata (%ERRORLEVEL%)  
  
    REM - get processor type and create/run registry update file  
    IF "%PROCESSOR_ARCHITECTURE%"=="AMD64" GOTO AMD64  
  
    @echo Architecture type is x86  
  
    ECHO Windows Registry Editor Version 5.00 > x86.reg  
  
    ECHO [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.2\Catalogs] >> x86.reg  
    ECHO "ContentStore"="%SYSTEMDRIVE%\\ProgramData\\Microsoft\\HelpLibrary2\\Catalogs\\" >> x86.reg  
  
    ECHO [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.2\Catalogs\VisualStudio12] >> x86.reg  
    ECHO "LocationPath"="%SYSTEMDRIVE%\\ProgramData\\Microsoft\\HelpLibrary2\\Catalogs\\VisualStudio12\\"  >> x86.reg  
    ECHO "FirstTimeRun"="False"  >> x86.reg  
  
    ECHO [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.2\Catalogs\VisualStudio12\en-US]  >> x86.reg  
    ECHO "ContentStore"="%SYSTEMDRIVE%\\ProgramData\\Microsoft\\HelpLibrary2\\Catalogs\\VisualStudio12\\"  >> x86.reg  
    ECHO "catalogName"="Visual Studio version Help Documentation"  >> x86.reg  
  
    ECHO [HKEY_LOCAL_MACHINE\Software\Microsoft\VSWinExpress\14.0\help]  >> x86.reg  
    ECHO "UseOnlineHelp"=dword:00000000  >> x86.reg  
  
    regedit.exe /s x86.reg  
    if ERRORLEVEL 1 ECHO *** ERROR inserting the x86 reg (%ERRORLEVEL%)  
  
    GOTO CONTINUE  
  
    :AMD64  
    @echo Architecture type is AMD64  
  
    ECHO Windows Registry Editor Version 5.00 > x64.reg  
  
    ECHO [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.2\Catalogs] >> x64.reg  
    ECHO "ContentStore"="%SYSTEMDRIVE%\\ProgramData\\Microsoft\\HelpLibrary2\\Catalogs\\" >> x64.reg  
  
    ECHO [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.2\Catalogs\VisualStudio14] >> x64.reg  
    ECHO "LocationPath"="%SYSTEMDRIVE%\\ProgramData\\Microsoft\\HelpLibrary2\\Catalogs\\VisualStudio14\\"  >> x64.reg  
    ECHO "FirstTimeRun"="False"  >> x64.reg  
  
    ECHO [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.2\Catalogs\VisualStudio14\en-US]  >> x64.reg  
    ECHO "ContentStore"="%SYSTEMDRIVE%\\ProgramData\\Microsoft\\HelpLibrary2\\Catalogs\\VisualStudio12\\en-US\\"  >> x64.reg  
    ECHO "catalogName"="Visual Studio version Help Documentation"  >> x64.reg  
  
    ECHO [HKEY_LOCAL_MACHINE\Software\Wow6432Node\Microsoft\VSWinExpress\14.0\help]  >> x64.reg  
    ECHO "UseOnlineHelp"=dword:00000000  >> x64.reg  
  
    regedit.exe /s x64.reg  
    if ERRORLEVEL 1 ECHO *** ERROR inserting the x64 reg (%ERRORLEVEL%)  
  
    :CONTINUE  
    ```  
  
3.  Execute o arquivo bat em computadores locais em que o conteúdo da ajuda deve estar instalado.  
  
## <a name="see-also"></a>Consulte também  
 [Argumentos da linha de comando para o Gerenciador de Conteúdo da Ajuda](../ide/command-line-arguments-for-the-help-content-manager.md)   
 [Substituições do Gerenciador de Conteúdo da Ajuda](../ide/help-content-manager-overrides.md)



