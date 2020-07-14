---
title: Solucionando problemas de VSPackages | Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
helpviewer_keywords:
- VSPackages, troubleshooting
- debugging, VSPackages
ms.assetid: 274673e7-72e7-476f-a263-3411b5b874be
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2141d2fd7d046f61ba6febecc427066d7a09ba18
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904483"
---
# <a name="troubleshooting-vspackages"></a>Solucionando problemas de VSPackages
Veja a seguir os problemas comuns que você pode ter com seu VSPackage e dicas para resolver os problemas.

### <a name="to-troubleshoot-a-vspackage-that-keeps-visual-studio-from-starting"></a>Para solucionar um VSPackage que impede o Visual Studio de iniciar

- Inicie o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] no modo de segurança.

   Para iniciar [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] no modo de segurança, em um prompt de comando, digite **devenv.exe/safemode**.

   Durante esse processo, nenhum VSPackages é carregado, exceto os VSPackages incluídos no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

### <a name="to-troubleshoot-a-vspackage-that-does-not-load"></a>Para solucionar problemas de um VSPackage que não é carregado

1. Verifique se você está usando a raiz do registro na qual o VSPackage está registrado para ser executado, geralmente a raiz do registro experimental.

    Para obter mais informações, consulte [a instância experimental](../extensibility/the-experimental-instance.md).

2. Se a VSPackage for destinada a executar na raiz do registro experimental, verifique se você está executando a versão experimental do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

    Para executar a versão experimental, digite o seguinte em uma janela de comando: **devenv/rootsuffix exp**.

3. Verifique suas entradas de registro do VSPackage.

    Para obter mais informações, consulte [registrando VSPackages](registering-and-unregistering-vspackages.md) e [Gerenciando VSPackages](../extensibility/managing-vspackages.md).

4. Abra a janela de **saída** da instância do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] que está falhando ao carregar o VSPackage. As informações sobre o motivo da falha do carregamento do VSPackage podem ser exibidas nessa janela.

   > [!NOTE]
   > Se você estiver iniciando a versão experimental do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE (ambiente de desenvolvimento integrado), inspecione a janela de **saída** de ambas as versões.

5. Examine o log de atividades.

    Para obter mais informações, consulte [como: usar o log de atividades](../extensibility/how-to-use-the-activity-log.md).

6. Para obter mais informações sobre exceções geradas pelo IDE, clique em **exceções** no menu **depurar** para habilitar as exceções. Na caixa de diálogo **exceções** , selecione os tipos de exceções sobre os quais você deseja obter mais informações.

### <a name="to-troubleshoot-a-vspackage-that-does-not-register"></a>Para solucionar problemas de um VSPackage que não se registra

1. Verifique se o assembly VSPackage reside em um local confiável. RegPkg não pode registrar assemblies em um local não confiável ou parcialmente confiável, como um compartilhamento de rede na configuração de segurança padrão do .net. Embora um aviso apareça sempre que um usuário cria um projeto em um local não confiável, a caixa de seleção "não mostrar esta mensagem novamente" pode impedir que esse aviso ocorra novamente.

### <a name="to-troubleshoot-a-command-that-is-not-visible-or-that-generates-an-error-when-you-click-a-command"></a>Para solucionar problemas de um comando que não está visível ou que gera um erro quando você clica em um comando

1. Mescle os comandos de menu novos ou alterados e aqueles já existentes no IDE digitando o seguinte no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] prompt de comando: **devenv/rootsuffix exp/setup**.

2. Certifique-se de que [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] o possa encontrar UI.dll para seu VSPackage.

   1. Localize o CLSID do VSPackage na seção pacotes do registro:

        \Packages HKLM\Software\Microsoft\Visual Studio \\ *\<version>*

   2. Verifique se o caminho fornecido pela subchave SatelliteDll está correto.

### <a name="to-troubleshoot-a-vspackage-that-behaves-unexpectedly"></a>Para solucionar problemas de um VSPackage que se comporta inesperadamente

1. Defina os pontos de interrupção no seu código.

     Bons pontos de partida para depuração são o construtor e o método de inicialização. Você também pode definir pontos de interrupção na área que deseja avaliar, como um comando de menu. Para habilitar pontos de interrupção, você deve executar sob o depurador.

    1. No menu **Projeto** , clique em **Propriedades**.

    2. Na caixa de diálogo **páginas de propriedades** , selecione a guia **depurar** .

    3. Na caixa **argumentos de linha de comando** , digite o sufixo raiz do ambiente de desenvolvimento ao qual seu VSPackage se destina. Por exemplo, para selecionar a compilação experimental, digite: **/RootSuffix exp**.

    4. No menu **depurar** , clique em **Iniciar Depuração** ou pressione F5.

        > [!NOTE]
        > Se você estiver depurando um projeto, crie ou carregue uma instância existente do seu projeto agora.

2. Use o log de atividades.

     Rastreie o comportamento de VSPackage gravando informações no log de atividades em pontos-chave. Essa técnica é especialmente útil quando você executa um VSPackage em um ambiente de varejo. Para obter mais informações, consulte [como: usar o log de atividades](../extensibility/how-to-use-the-activity-log.md).

3. Use símbolos públicos.

     Para melhorar a legibilidade durante a depuração, você pode anexar símbolos ao depurador.

    1. No menu **ferramentas/opções** , navegue até a caixa de diálogo **depuração/símbolos** .

    2. Adicionar este **arquivo de símbolo (. pdb) local**:

         `https://msdl.microsoft.com/download/symbols`

    3. Para melhorar o desempenho, especifique uma pasta de cache de símbolos, por exemplo:

        ```
        C:\symbols
        ```

### <a name="to-troubleshoot-a-missing-vspackage-or-one-of-its-dependencies"></a>Para solucionar um VSPackage ausente ou uma de suas dependências

1. Para código gerenciado, verifique se os caminhos de referência estão corretos.

   1. No menu **Projeto** , clique em **Propriedades**.

   2. Selecione a guia **referências** na caixa de diálogo **páginas de propriedades** e verifique se todos os caminhos estão corretos. Como alternativa, você pode usar o **pesquisador de objeto** para procurar os objetos referenciados.

        Para código gerenciado, você pode usar a [Fuslogvw.exe (Visualizador de log de associação de assembly)](/dotnet/framework/tools/fuslogvw-exe-assembly-binding-log-viewer) para exibir os detalhes das cargas de assembly com falha.

2. Para código não gerenciado, localize o CLSID do VSPackage no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] nó do Registro CLSID:

    \CLSID HKLM\Software\Microsoft\Visual Studio \\ *\<version>*

   Verifique se a entrada InprocServer32 tem o caminho correto da dll VSPackage.

## <a name="see-also"></a>Confira também
- [VSPackages](../extensibility/internals/vspackages.md)
