---
title: Manifestos de aplicativo e implantação em soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- manifests [Office development in Visual Studio]
- deployment manifests [Office development in Visual Studio]
- application manifests [Office development in Visual Studio]
- assemblies [Office development in Visual Studio], updating
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: bb4386469e02934045d9f1da45fe515dc9af5da2
ms.sourcegitcommit: 20c0991d737c540750c613c380cd4cf5bb07de51
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53247953"
---
# <a name="application-and-deployment-manifests-in-office-solutions"></a>Manifestos de aplicativo e implantação em soluções do Office
  Um manifesto de aplicativo é um arquivo XML que fornece informações que são usadas por uma solução do Office para localizar e atualizar seus assemblies. Um manifesto de aplicativo pode ser usado com um manifesto de implantação, que é um arquivo XML armazenado no servidor que fornece as informações necessárias para localizar a versão mais atual do manifesto do aplicativo e assemblies.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
## <a name="manifest-structure-for-office-solutions"></a>Estrutura de manifesto para soluções do Office  
 Para soluções do Microsoft Office criadas usando as ferramentas de desenvolvimento do Office no Visual Studio, todos os manifestos são baseados no esquema padrão do ClickOnce. Quando você implanta as soluções do Office, os manifestos do aplicativo para o nível de documento e projetos de suplemento do VSTO estão localizados no cache do ClickOnce. Os manifestos de implantação não são copiados para o computador cliente.  
  
 Para obter informações sobre o conteúdo do aplicativo e manifestos de implantação para projetos do Office, consulte [manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md) e [manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md).  
  
## <a name="create-application-and-deployment-manifests"></a>Criar manifestos de aplicativo e implantação  
 Manifestos de aplicativo são criados automaticamente como parte do processo de compilação. Sempre que você criar um projeto de nível de documento, o local do manifesto de implantação será inserido no documento como uma propriedade de documento personalizado. Para suplementos do VSTO, o local do manifesto de implantação é armazenado no registro.  
  
 Para obter mais informações sobre o **Assistente de publicação**, consulte [implantar uma solução do Office usando o ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md).  
  
 Para obter mais informações sobre como se manifesta trabalhar com soluções do Office, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).  
  
## <a name="see-also"></a>Consulte também  
 [Arquitetura de personalizações no nível do documento](../vsto/architecture-of-document-level-customizations.md)   
 [Arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md)   
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)   
 [Manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)   
 [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)   
 [Manifesto do aplicativo ClickOnce](/visualstudio/deployment/clickonce-application-manifest)   
 [Manifesto de implantação do ClickOnce](/visualstudio/deployment/clickonce-deployment-manifest)  
  
  