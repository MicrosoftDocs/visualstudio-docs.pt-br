---
title: -Upgrade (devenv.exe)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: reference
helpviewer_keywords:
- /upgrade Devenv switch
- Devenv, /upgrade switch
- upgrade Devenv switch
ms.assetid: 3468045c-5cc9-4157-9a9d-622452145d27
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 46e549dfdc661819dac00d0aa965616462130ad0
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53944717"
---
# <a name="upgrade-devenvexe"></a>/Upgrade (devenv.exe)
Atualiza o arquivo de solução e todos os seus arquivos de projeto, ou o arquivo de projeto especificado, para os formatos [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] atuais para esses arquivos.

## <a name="syntax"></a>Sintaxe

```cmd
devenv SolutionFile | ProjectFile /upgrade
```

## <a name="arguments"></a>Arguments
 `SolutionFile`

 Necessário se você estiver atualizando uma solução inteira e seus projetos. O caminho e o nome de um arquivo de solução. Você pode inserir apenas o nome do arquivo de solução, ou um caminho completo e o nome do arquivo de solução. Se a pasta ou o arquivo nomeado ainda não existir, ele será criado.

 `ProjectFile`

 Necessário se você estiver atualizando um único projeto. O caminho e o nome de um arquivo de projeto na solução. Você pode inserir apenas o nome do arquivo de projeto, ou um caminho completo e o nome do arquivo de projeto. Se a pasta ou o arquivo nomeado ainda não existir, ele será criado.

## <a name="remarks"></a>Comentários
 Backups são criados e copiados automaticamente para um diretório chamado Backup, que é criado no diretório atual.

 É necessário fazer o check-out de projetos ou soluções controlados pelo código-fonte para que eles possam ser atualizados.

 Usar a opção `/upgrade` não inicia [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Os resultados da atualização podem ser vistos no Relatório de Atualização da linguagem de desenvolvimento da solução ou projeto. Nenhuma informação de erro ou de uso é retornada. Para obter mais informações sobre como atualizar projetos no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], consulte [Portar, migrar e atualizar projetos do Visual Studio](../../porting/port-migrate-and-upgrade-visual-studio-projects.md).

## <a name="example"></a>Exemplo
 Este exemplo atualiza um arquivo de solução chamado "MyProject.sln" na pasta padrão para soluções [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].

```cmd
devenv "MyProject.sln" /upgrade
```

## <a name="see-also"></a>Consulte também

- [Opções de linha de comando do Devenv](../../ide/reference/devenv-command-line-switches.md)