---
title: -Upgrade (devenv.exe) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- /upgrade Devenv switch
- Devenv, /upgrade switch
- upgrade Devenv switch
ms.assetid: 3468045c-5cc9-4157-9a9d-622452145d27
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 79a00da92ac2da6eb37fa1eef90fa112598d23f3
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49264936"
---
# <a name="upgrade-devenvexe"></a>/Upgrade (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Atualiza o arquivo de solução e todos os seus arquivos de projeto, ou o arquivo de projeto especificado, para os formatos [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] atuais para esses arquivos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
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
  
 Usar a opção `/upgrade` não inicia [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Os resultados da atualização podem ser vistos no Relatório de Atualização da linguagem de desenvolvimento da solução ou projeto. Nenhuma informação de erro ou de uso é retornada. Para obter mais informações sobre como atualizar projetos em [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], consulte [Como solucionar problemas de atualizações de projeto do Visual Studio malsucedidas](../../porting/how-to-troubleshoot-unsuccessful-visual-studio-project-upgrades.md).  
  
## <a name="example"></a>Exemplo  
 Este exemplo atualiza um arquivo de solução chamado "MyProject.sln" na pasta padrão para soluções [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
```  
devenv "MyProject.sln" /upgrade  
```  
  
## <a name="see-also"></a>Consulte também  
 [Como solucionar problemas de atualizações de projeto do Visual Studio malsucedidas](../../porting/how-to-troubleshoot-unsuccessful-visual-studio-project-upgrades.md)   
 [Opções de linha de comando devenv](../../ide/reference/devenv-command-line-switches.md)



