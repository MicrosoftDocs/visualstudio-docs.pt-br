---
title: 'Como: definir comandos de implantação do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 060acd0164ff7819d2abfb8d92f2394b4bcc0672
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118553"
---
# <a name="how-to-set-sharepoint-deployment-commands"></a>Como: comandos de implantação do SharePoint de conjunto
  Você pode personalizar o processo de implantação, definindo comandos pré e pós-implantação. Esses comandos são executados antes e depois de outras ações de implantação quando você depura soluções do SharePoint no Visual Studio.  
  
### <a name="to-add-a-pre-deployment-command"></a>Para adicionar um comando de pré-implantação  
  
1.  Na barra de menus, escolha **Project** > **\<*ProjectName*> propriedades**.  
  
2.  Escolha o **SharePoint** guia.  
  
3.  No **linha de comando de pré-implantação** texto, digite os comandos do MS-DOS ou MSBuild para personalizar esta etapa.  
  
     Por exemplo, para listar o conteúdo do diretório antes da conclusão da implantação, insira **dir**.  
  
### <a name="to-add-a-post-deployment-command"></a>Para adicionar um comando de pós-implantação  
  
1.  Na barra de menus, escolha **Project** > **\<*ProjectName*> propriedades**.  
  
2.  Escolha o **SharePoint** guia.  
  
3.  No **linha de comando de pós-implantação** texto, digite os comandos do MS-DOS ou MSBuild para personalizar esta etapa.  
  
     Por exemplo, para listar o conteúdo do diretório após a conclusão da implantação, insira **dir**. Para usar uma variável do MSBuild para copiar o assembly do diretório de compilação, digite **copiar $ (TargetPath) c:\DeploymentDirectory**.  
  
## <a name="see-also"></a>Consulte também
 [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)  
  
