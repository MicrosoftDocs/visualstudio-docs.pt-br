---
title: Comandos que devem ser executados após a instalação | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- post-install commands
ms.assetid: c9601f2e-2c6e-4da9-9a6e-e707319b39e2
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 08e1bcf064a8e94af306230e705f686d2d8037c1
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39510700"
---
# <a name="commands-that-must-be-run-after-installation"></a>Comandos que devem ser executados após a instalação
Se você implantar sua extensão por meio de um *. msi* arquivo, você deve executar **devenv /setup** como parte de sua instalação para Visual Studio descobrir suas extensões.  
  
> [!NOTE]
>  As informações neste tópico se aplica a Localizando *devenv.exe* com o Visual Studio 2008 e versões anteriores. Para obter informações sobre como descobrir *devenv.exe* com versões posteriores do Visual Studio, consulte [detectar os requisitos de sistema](../../extensibility/internals/detecting-system-requirements.md).  
  
## <a name="find-devenvexe"></a>Localizar devenv.exe  
 Você pode localizar cada versão *devenv.exe* do registro de valores que [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] gravam instaladores, usando o RegLocator e AppSearch tabelas para armazenar os valores do registro como propriedades. Para obter mais informações, consulte [detectar os requisitos de sistema](../../extensibility/internals/detecting-system-requirements.md).  
  
### <a name="reglocator-table-rows-to-locate-devenvexe-from-different-versions-of-visual-studio"></a>Linhas da tabela RegLocator localizar devenv.exe de diferentes versões do Visual Studio  
  
|Assinatura|Raiz|Chave|Nome|Tipo|  
|-----------------|----------|---------|----------|----------|  
|RL_DevenvExe_2002|2|SOFTWARE\Microsoft\VisualStudio\7.0\Setup\VS|EnvironmentPath|2|  
|RL_DevenvExe_2003|2|SOFTWARE\Microsoft\VisualStudio\7.1\Setup\VS|EnvironmentPath|2|  
|RL_DevenvExe_2005|2|SOFTWARE\Microsoft\VisualStudio\8.0\Setup\VS|EnvironmentPath|2|  
|RL_DevenvExe_2008|2|SOFTWARE\Microsoft\VisualStudio\9.0\Setup\VS|EnvironmentPath|2|  
  
### <a name="appsearch-table-rows-for-corresponding-reglocator-table-rows"></a>Linhas da tabela AppSearch para linhas correspondentes da tabela RegLocator  
  
|Propriedade|Assinatura|  
|--------------|-----------------|  
|DEVENV_EXE_2002|RL_DevenvExe_2002|  
|DEVENV_EXE_2003|RL_DevenvExe_2003|  
|DEVENV_EXE_2005|RL_DevenvExe_2005|  
|DEVENV_EXE_2008|RL_DevenvExe_2008|  
  
 Por exemplo, o instalador do Visual Studio grava o valor do registro do **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0\Setup\VS\EnvironmentPath** como *C:\VS2008\Common7\IDE\devenv.exe*, um caminho completo para o executável que o instalador deve ser executado.  
  
> [!NOTE]
> Porque a coluna de tipo da tabela RegLocator for 2, não é necessário especificar informações adicionais de versão na tabela de assinatura.  
  
## <a name="run-devenvexe"></a>Executar devenv.exe  
 Após o AppSearch ação padrão é executada no instalador, cada propriedade na tabela AppSearch tem um valor que aponta para o *devenv.exe* arquivo para a versão correspondente do Visual Studio. Se qualquer um dos valores do Registro especificada não estão presentes — porque essa versão do Visual Studio não está instalado, a propriedade especificada está definida como null.  
  
 Windows Installer o dá suporte à execução de um executável para o qual aponta uma propriedade por meio da ação personalizada digite 50. A ação personalizada deve incluir as opções de execução no script `msidbCustomActionTypeInScript` (1024) e `msidbCustomActionTypeCommit` (512), para garantir que o VSPackage foi instalado com êxito antes da integração-o na [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Para obter mais informações, consulte [tabela CustomAction](https://docs.microsoft.com/windows/desktop/msi/customaction-table) e [opções de execução no script de ação personalizado](https://docs.microsoft.com/windows/desktop/msi/custom-action-in-script-execution-options).  
  
 Ações personalizadas de tipo 50 especificam a propriedade que contém o executável como o valor da coluna de origem e argumentos de linha de comando na coluna de destino.  
  
### <a name="customaction-table-rows-to-run-devenvexe"></a>Linhas da tabela CustomAction executar devenv.exe  
  
|Ação|Tipo|Origem|Destino|  
|------------|----------|------------|------------|  
|CA_RunDevenv2002|1586|DEVENV_EXE_2002|/Setup|  
|CA_RunDevenv2003|1586|DEVENV_EXE_2003|/Setup|  
|CA_RunDevenv2005|1586|DEVENV_EXE_2005|/Setup|  
|CA_RunDevenv2008|1586|DEVENV_EXE_2008|/Setup|  
  
 Ações personalizadas devem ser criadas na tabela InstallExecuteSequence agendá-los para execução durante a instalação. Use a propriedade correspondente em cada linha da coluna da condição para impedir que a ação personalizada de ser executado se essa versão do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] não está instalado no sistema.  
  
> [!NOTE]
>  Propriedades de valor nulo são avaliadas como `False` quando usado em condições.  
  
 O valor da coluna de sequência para cada ação personalizada depende de outros valores de sequência em seu pacote do Windows Installer. Valores de sequência devem ser, de modo que o *devenv.exe* ações personalizadas executadas como próximo possível imediatamente antes da ação padrão de InstallFinalize.  
  
### <a name="installexecutesequence-table-to-schedule-the-devenvexe-custom-actions"></a>Tabela InstallExecuteSequence para agendar as ações personalizadas de devenv.exe  
  
|Ação|Condição|Sequência|  
|------------|---------------|--------------|  
|CA_RunDevenv2002|DEVENV_EXE_2002|6602|  
|CA_RunDevenv2003|DEVENV_EXE_2003|6603|  
|CA_RunDevenv2005|DEVENV_EXE_2005|6605|  
|CA_RunDevenv2008|DEVENV_EXE_2008|6608|  
  
## <a name="see-also"></a>Consulte também  
 [Instalar VSPackages com o Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md)