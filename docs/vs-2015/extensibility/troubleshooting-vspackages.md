---
title: Solucionar problemas de VSPackages | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- VSPackages, troubleshooting
- debugging, VSPackages
ms.assetid: 274673e7-72e7-476f-a263-3411b5b874be
caps.latest.revision: 23
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: b2c9a7b57a8b15683cb202b71e33e908a1bfd1b5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51764001"
---
# <a name="troubleshooting-vspackages"></a>Solucionando problemas de VSPackages
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A seguir estão os problemas comuns que você pode ter com o VSPackage e dicas para resolver os problemas.  
  
### <a name="to-troubleshoot-a-vspackage-that-keeps-visual-studio-from-starting"></a>Para solucionar problemas de um VSPackage que impede que o Visual Studio iniciando  
  
-   Iniciar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] no modo de segurança.  
  
     Para começar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] no modo de segurança em um prompt de comando, digite **devenv.exe /safemode**.  
  
     Durante esse processo não VSPackages são carregados, exceto os VSPackages que acompanham [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
### <a name="to-troubleshoot-a-vspackage-that-does-not-load"></a>Para solucionar problemas de um VSPackage que não é carregado  
  
1.  Certifique-se de que você está usando a raiz do registro no qual o VSPackage é registrado para ser executado, normalmente, a raiz do registro experimental.  
  
     Para obter mais informações, consulte [a instância Experimental](../extensibility/the-experimental-instance.md).  
  
2.  Se o VSPackage é direcionado para executar na raiz do registro experimental, certifique-se de que você está executando a versão de avaliação do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
     Para executar a versão experimental, digite o seguinte em uma janela de comando: **devenv /rootsuffix exp**.  
  
3.  Verifique as entradas de registro de VSPackage.  
  
     Para obter mais informações, consulte [registrar VSPackages](http://msdn.microsoft.com/en-us/31e6050f-1457-4849-944a-a3c36b76f3dd) e [gerenciar VSPackages](../extensibility/managing-vspackages.md).  
  
4.  Abra o **saída** janela da instância do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] que falha ao carregar o VSPackage. Informações sobre por que o VSPackage falha no carregamento podem ser exibidas nessa janela.  
  
    > [!NOTE]
    >  Se você estiver começando a versão de avaliação do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] inspecionar o ambiente de desenvolvimento integrado (IDE), o **saída** janela de ambas as versões.  
  
5.  Examine o log de atividades.  
  
     Para obter mais informações, consulte [como: usar o Log de atividades](../extensibility/how-to-use-the-activity-log.md).  
  
6.  Para obter mais informações sobre as exceções geradas pelo IDE, clique em **exceções** sobre o **depurar** menu habilitar as exceções. No **exceções** caixa de diálogo Selecionar os tipos de exceções sobre o qual você deseja obter mais informações.  
  
### <a name="to-troubleshoot-a-vspackage-that-does-not-register"></a>Para solucionar problemas de um VSPackage que não registra  
  
1.  Certifique-se de que o assembly de VSPackage reside em um local confiável. RegPkg não é possível registrar assemblies em um local não confiável ou parcialmente confiável, como um compartilhamento de rede na configuração de segurança do .net padrão. Embora um aviso é exibido sempre que um usuário cria um projeto em um local não confiável, a caixa de seleção "não mostrar esta mensagem novamente" pode impedir que esse aviso ocorra.  
  
### <a name="to-troubleshoot-a-command-that-is-not-visible-or-that-generates-an-error-when-you-click-a-command"></a>Para solucionar problemas de um comando que não é visível ou que gera um erro quando você clica em um comando  
  
1.  Mesclar os comandos de menu novos ou alterados e aqueles já no IDE, digitando o seguinte comando na [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Prompt de comando: **devenv /rootsuffix Exp /Setup.**.  
  
2.  Certifique-se de que [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] pode encontrar UI.dll para o VSPackage.  
  
    1.  Localize o CLSID do VSPackage na seção de pacotes do registro:  
  
         Studio HKLM\Software\Microsoft\Visual\\*\<versão >* \packages.  
  
    2.  Verifique se o caminho fornecido pela subchave SatelliteDll está correto.  
  
### <a name="to-troubleshoot-a-vspackage-that-behaves-unexpectedly"></a>Para solucionar problemas de um VSPackage que se comporta de forma inesperada  
  
1.  Defina os pontos de interrupção no seu código.  
  
     Bons pontos de partida para a depuração são o construtor e o método de inicialização. Você também pode definir pontos de interrupção na área que você deseja avaliar, como um comando de menu. Para habilitar os pontos de interrupção, você deve executar sob o depurador.  
  
    1.  No menu **Projeto**, clique em **Propriedades**.  
  
    2.  Sobre o **páginas de propriedades** caixa de diálogo, selecione o **depurar** guia.  
  
    3.  No **argumentos de linha de comando** , digite o sufixo raiz do ambiente de desenvolvimento que os destinos de VSPackage. Por exemplo, para selecionar a compilação experimental, digite: **RootSuffix Exp**.  
  
    4.  Sobre o **Debug** menu, clique em **iniciar depuração** ou pressione F5.  
  
        > [!NOTE]
        >  Se você estiver depurando um projeto, criar ou carregar uma instância existente do seu projeto agora.  
  
2.  Use o log de atividades.  
  
     Rastrear o comportamento de VSPackage gravando informações ao log de atividades em pontos-chave. Essa técnica é especialmente útil quando você executa um VSPackage em um ambiente de varejo. Para obter mais informações, consulte [como: usar o Log de atividades](../extensibility/how-to-use-the-activity-log.md).  
  
3.  Use os símbolos públicos.  
  
     Para melhorar a legibilidade durante a depuração, você pode anexar os símbolos do depurador.  
  
    1.  Dos **Ferramentas/opções** menu, navegue até a **depuração/símbolos** caixa de diálogo.  
  
    2.  Adicione isso **local do arquivo (. PDB) de símbolo**:  
  
         [http://msdl.microsoft.com/download/symbols](http://msdl.microsoft.com/download/symbols)  
  
    3.  Para melhorar o desempenho, especifique uma pasta de cache de símbolo, por exemplo:  
  
        ```  
        C:\symbols  
        ```  
  
### <a name="to-troubleshoot-a-missing-vspackage-or-one-of-its-dependencies"></a>Solucionar problemas de um VSPackage ausente ou uma de suas dependências  
  
1. Para código gerenciado, certifique-se de que os caminhos de referência estão corretos.  
  
   1.  No menu **Projeto**, clique em **Propriedades**.  
  
   2.  Selecione o **referências** guia o **páginas de propriedade** caixa de diálogo e verifique se todos os caminhos estão corretos. Como alternativa, você pode usar o **Pesquisador de objetos** para procurar os objetos referenciados.  
  
        Para código gerenciado, você pode usar o [Fuslogvw.exe (Assembly Binding Log Viewer)](http://msdn.microsoft.com/library/e32fa443-0778-4cc3-bf36-5c8ea297d296) para exibir os detalhes de carregamentos de assembly com falha.  
  
2. Para código não gerenciado, localize o CLSID do VSPackage no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] nó do Registro CLSID:  
  
    Studio HKLM\Software\Microsoft\Visual\\*\<versão >* \CLSID  
  
   Certifique-se de que a entrada InprocServer32 tem o caminho correto da dll VSPackage.  
  
## <a name="see-also"></a>Consulte também  
 [VSPackages](../extensibility/internals/vspackages.md)

