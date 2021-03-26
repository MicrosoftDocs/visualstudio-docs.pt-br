---
title: Gerenciando associações de arquivos lado a lado | Microsoft Docs
description: Se o seu VSPackage fornece associações de arquivos, decida como lidar com instalações lado a lado nas quais uma versão específica do Visual Studio abre um arquivo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- verbs, setting default
ms.assetid: 9b6df3bc-d15c-4a5d-9015-948a806193b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 083eef2454a9e805b1cb8b3e85a6d7d81263a0dd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073047"
---
# <a name="manage-side-by-side-file-associations"></a>Gerenciar associações de arquivos lado a lado

Se o seu VSPackage fornece associações de arquivos, você deve decidir como lidar com instalações lado a lado nas quais uma versão específica do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] deve ser chamada para abrir um arquivo. Formatos de arquivo incompatíveis compõem o problema.

Os usuários esperam que uma nova versão de um produto seja compatível com as versões anteriores, para que os arquivos existentes possam ser carregados em uma nova versão sem perder dados. O ideal é que seus VSPackage possam carregar e salvar os formatos de arquivo de versões anteriores. Se isso não for verdadeiro, você deverá oferecer para atualizar o formato de arquivo para a nova versão do seu VSPackage. A desvantagem dessa abordagem é que o arquivo atualizado não pode ser aberto na versão anterior.

Para evitar esse problema, você pode alterar as extensões quando os formatos de arquivo se tornarem incompatíveis. Por exemplo, a versão 1 de seu VSPackage poderia usar a extensão, *. mypkg10* e a versão 2 poderia usar a extensão, *. mypkg20*. Essa diferença identifica o VSPackage que abre um arquivo específico. Se você adicionar VSPackages mais recentes à lista de programas associados a uma extensão antiga, os usuários poderão clicar com o botão direito do mouse no arquivo e optar por abri-lo em um VSPackage mais recente. Nesse ponto, seu VSPackage pode oferecer para atualizar o arquivo para o novo formato ou abrir o arquivo e manter a compatibilidade com versões anteriores do VSPackage.

> [!NOTE]
> Você pode combinar essas abordagens. Por exemplo, você pode oferecer compatibilidade com versões anteriores carregando um arquivo mais antigo e oferecer para atualizar o formato de arquivo quando o usuário salvá-lo.

## <a name="face-the-problem"></a>Enfrentar o problema

Se você quiser que vários VSPackages lado a lado usem a mesma extensão, deverá escolher a versão do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] que está associada à extensão. Aqui estão duas alternativas:

- Abra o arquivo na versão mais recente do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] instalada no computador de um usuário.

   Nessa abordagem, o instalador é responsável por determinar a versão mais recente do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e incluir isso na entrada do registro gravada para a associação de arquivo. Em um pacote Windows Installer, você pode incluir ações personalizadas para definir uma propriedade que indica a versão mais recente do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

  > [!NOTE]
  > Neste contexto, "mais recente" significa "versão mais recente com suporte". Essas entradas do instalador não irão detectar automaticamente uma versão subsequente do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . As entradas na [detecção de requisitos do sistema](../extensibility/internals/detecting-system-requirements.md) e em [comandos que devem ser executados após a instalação](../extensibility/internals/commands-that-must-be-run-after-installation.md) são semelhantes àquelas apresentadas aqui e são necessárias para dar suporte a versões adicionais do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

   As linhas a seguir na tabela CustomAction definem a propriedade DEVENV_EXE_LATEST como uma propriedade definida pelas tabelas AppSearch e RegLocator discutidas em [comandos que devem ser executados após a instalação](../extensibility/internals/commands-that-must-be-run-after-installation.md). As linhas na tabela InstallExecuteSequence agendam as ações personalizadas logo no início da sequência de execução. Os valores na coluna condição fazem a lógica funcionar:

  - O Visual Studio .NET 2002 é a versão mais recente se for a única versão presente.

  - O Visual Studio .NET 2003 é a versão mais recente somente se estiver presente e [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] não estiver presente.

  - [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] é a versão mais recente se for a única versão presente.

    O resultado líquido é que DEVENV_EXE_LATEST contém o caminho da versão mais recente do devenv.exe.

  **Linhas da tabela CustomAction que determinam a versão mais recente do Visual Studio**

  |Ação|Type|Fonte|Destino|
  |------------|----------|------------|------------|
  |CA_SetDevenvLatest_2002|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2002]|
  |CA_SetDevenvLatest_2003|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2003]|
  |CA_SetDevenvLatest_2005|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2005]|

  **Linhas da tabela InstallExecuteSequence que determinam a versão mais recente do Visual Studio**

  |Ação|Condição|Sequência|
  |------------|---------------|--------------|
  |CA_SetDevenvLatest_2002|DEVENV_EXE_2002 E NÃO (DEVENV_EXE_2003 OU DEVENV_EXE_2005)|410|
  |CA_SetDevenvLatest_2003|DEVENV_EXE_2003 E NÃO DEVENV_EXE_2005|420|
  |CA_SetDevenvLatest_2005|DEVENV_EXE_2005|430|

   Você pode usar a propriedade DEVENV_EXE_LATEST na tabela de registro do pacote Windows Installer para gravar o valor padrão da chave do **HKEY_CLASSES_ROOT *ProgID* ShellOpenCommand** , [DEVENV_EXE_LATEST] "%1"

- Execute um programa iniciador compartilhado que possa fazer a melhor escolha das versões disponíveis do VSPackage.

   Os desenvolvedores de [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] escolheram essa abordagem para lidar com os requisitos complexos dos vários formatos de soluções e projetos que resultam de muitas versões do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . Nessa abordagem, você registra um programa iniciador como o manipulador de extensão. O iniciador examina o arquivo e decide qual versão do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e seu VSPackage podem manipular esse arquivo específico. Por exemplo, se um usuário abrir um arquivo que foi salvo pela última vez por uma versão específica do seu VSPackage, o iniciador poderá iniciar o VSPackage na versão correspondente do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . Além disso, um usuário pode configurar o iniciador para sempre iniciar a versão mais recente. Um iniciador também pode solicitar que um usuário atualize o formato do arquivo. Se o formato do arquivo incluir um número de versão, o iniciador poderá informar um usuário se o formato de arquivo for de uma versão posterior a um ou mais dos VSPackages instalados.

   O iniciador deve estar em um componente Windows Installer que é compartilhado com todas as versões do seu VSPackage. Esse processo garante que a versão mais recente esteja sempre instalada e não seja removida até que todas as versões do seu VSPackage sejam desinstaladas. Dessa forma, as associações de arquivo e outras entradas de registro do componente iniciador são preservadas mesmo que uma versão do VSPackage seja desinstalada.

## <a name="uninstall-and-file-associations"></a>Desinstalar e associações de arquivos

A desinstalação de um VSPackage que grava entradas de registro para associações de arquivo Remove as associações de arquivo. Portanto, a extensão não tem programas associados. Windows Installer não "recuperar" as entradas do registro que foram adicionadas quando o VSPackage foi instalado. Aqui estão algumas maneiras de corrigir as associações de arquivo de um usuário:

- Use um componente iniciador compartilhado conforme descrito anteriormente.

- Instrua o usuário a executar um reparo da versão do VSPackage que o usuário deseja que tenha a associação de arquivo.

- Forneça um programa executável separado que reescreve as entradas de registro apropriadas.

- Forneça uma página de opções de configuração ou caixa de diálogo que permite aos usuários escolher associações de arquivo e recuperar associações perdidas. Instrua os usuários a executá-lo após a desinstalação.

## <a name="see-also"></a>Confira também

- [Registrar extensões de nome de arquivo para implantações lado a lado](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)
- [Registrar verbos para extensões de nome de arquivo](../extensibility/registering-verbs-for-file-name-extensions.md)
