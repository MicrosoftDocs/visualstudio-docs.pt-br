---
title: Comandos que devem ser executados após a instalação | Microsoft Docs
description: Saiba mais sobre os comandos que devem ser executados como parte da instalação de uma extensão implantada por meio de um arquivo. msi no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- post-install commands
ms.assetid: c9601f2e-2c6e-4da9-9a6e-e707319b39e2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ef557c0c679fad0dff25a51a8529270e4bd7ced2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057137"
---
# <a name="commands-that-must-be-run-after-installation"></a>Comandos que devem ser executados após a instalação
Se você implantar sua extensão por meio de um arquivo *. msi* , deverá executar **devenv/setup** como parte de sua instalação para que o Visual Studio descubra suas extensões.

> [!NOTE]
> As informações neste tópico se aplicam à localização de *devenv.exe* com o Visual Studio 2008 e anterior. Para obter informações sobre como descobrir *devenv.exe* com versões posteriores do Visual Studio, consulte [detectar requisitos do sistema](../../extensibility/internals/detecting-system-requirements.md).

## <a name="find-devenvexe"></a>Localizar devenv.exe
 Você pode localizar as *devenv.exe* de cada versão de valores de registro que os [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] instaladores gravam, usando a tabela RegLocator e as tabelas AppSearch para armazenar os valores do registro como propriedades. Para obter mais informações, consulte [detectar requisitos do sistema](../../extensibility/internals/detecting-system-requirements.md).

### <a name="reglocator-table-rows-to-locate-devenvexe-from-different-versions-of-visual-studio"></a>RegLocator linhas da tabela para localizar devenv.exe de diferentes versões do Visual Studio

|Assinatura|Root|Chave|Nome|Type|
|-----------------|----------|---------|----------|----------|
|RL_DevenvExe_2002|2|SOFTWARE\Microsoft\VisualStudio\7.0\Setup\VS|EnvironmentPath|2|
|RL_DevenvExe_2003|2|SOFTWARE\Microsoft\VisualStudio\7.1\Setup\VS|EnvironmentPath|2|
|RL_DevenvExe_2005|2|SOFTWARE\Microsoft\VisualStudio\8.0\Setup\VS|EnvironmentPath|2|
|RL_DevenvExe_2008|2|SOFTWARE\Microsoft\VisualStudio\9.0\Setup\VS|EnvironmentPath|2|

### <a name="appsearch-table-rows-for-corresponding-reglocator-table-rows"></a>Linhas da tabela AppSearch para linhas da tabela RegLocator correspondentes

|Propriedade|Assinatura|
|--------------|-----------------|
|DEVENV_EXE_2002|RL_DevenvExe_2002|
|DEVENV_EXE_2003|RL_DevenvExe_2003|
|DEVENV_EXE_2005|RL_DevenvExe_2005|
|DEVENV_EXE_2008|RL_DevenvExe_2008|

 Por exemplo, o instalador do Visual Studio grava o valor do registro de **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0\Setup\VS\EnvironmentPath** como *C:\VS2008\Common7\IDE\devenv.exe*, um caminho completo para o executável que o instalador deve executar.

> [!NOTE]
> Como a coluna de tipo da tabela RegLocator é 2, não é necessário especificar informações de versão adicionais na tabela de assinatura.

## <a name="run-devenvexe"></a>Executar devenv.exe
 Depois que a ação AppSearch padrão for executada no instalador, cada propriedade na tabela AppSearch terá um valor que aponta para o arquivo de *devenv.exe* para a versão correspondente do Visual Studio. Se qualquer um dos valores de registro especificados não estiver presente — porque essa versão do Visual Studio não está instalada — a propriedade especificada será definida como NULL.

 O Windows Installer dá suporte à execução de um executável no qual uma propriedade aponta por meio do tipo de ação personalizada 50. A ação personalizada deve incluir as opções de execução em script, `msidbCustomActionTypeInScript` (1024) e `msidbCustomActionTypeCommit` (512), para garantir que o VSPackage tenha sido instalado com êxito antes de integrá-lo ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Para obter mais informações, consulte [tabela de CustomAction](/windows/desktop/msi/customaction-table) e [Opções de execução em script de ação personalizada](/windows/desktop/msi/custom-action-in-script-execution-options).

 Ações personalizadas do tipo 50 especificam a propriedade que contém o executável como o valor da coluna de origem e os argumentos de linha de comando na coluna de destino.

### <a name="customaction-table-rows-to-run-devenvexe"></a>Linhas da tabela CustomAction a serem executadas devenv.exe

|Ação|Type|Fonte|Destino|
|------------|----------|------------|------------|
|CA_RunDevenv2002|1586|DEVENV_EXE_2002|/setup|
|CA_RunDevenv2003|1586|DEVENV_EXE_2003|/setup|
|CA_RunDevenv2005|1586|DEVENV_EXE_2005|/setup|
|CA_RunDevenv2008|1586|DEVENV_EXE_2008|/setup|

 As ações personalizadas devem ser criadas na tabela InstallExecuteSequence para agendá-las para execução durante a instalação. Use a propriedade correspondente em cada linha da coluna condição para impedir que a ação personalizada seja executada se essa versão do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] não estiver instalada no sistema.

> [!NOTE]
> As propriedades com valor nulo são avaliadas `False` quando usadas em condições.

 O valor da coluna de sequência para cada ação personalizada depende de outros valores de sequência em seu pacote de Windows Installer. Os valores de sequência devem ser de modo que o *devenv.exe* ações personalizadas sejam executadas o mais próximo possível imediatamente antes da ação InstallFinalize padrão.

### <a name="installexecutesequence-table-to-schedule-the-devenvexe-custom-actions"></a>Tabela InstallExecuteSequence para agendar as ações personalizadas de devenv.exe

|Ação|Condição|Sequência|
|------------|---------------|--------------|
|CA_RunDevenv2002|DEVENV_EXE_2002|6602|
|CA_RunDevenv2003|DEVENV_EXE_2003|6603|
|CA_RunDevenv2005|DEVENV_EXE_2005|6605|
|CA_RunDevenv2008|DEVENV_EXE_2008|6608|

## <a name="see-also"></a>Confira também
- [Instalar o VSPackages com Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
