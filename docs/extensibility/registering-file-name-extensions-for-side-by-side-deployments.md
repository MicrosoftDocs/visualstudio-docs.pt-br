---
title: Registrando extensões de nome de arquivo para implantações lado a lado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- file extensions, registering for side-by-side
ms.assetid: 9ab046a2-147d-4167-aa14-7d661b1eaaa5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1aa553b5370f637f5a779bbdff432319ce3e0bf4
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39638473"
---
# <a name="register-file-name-extensions-for-side-by-side-deployments"></a>Registrar as extensões de nome de arquivo para implantações lado a lado
VSPackages implantado em um ambiente lado a lado, você deve registrar as extensões de nome de arquivo para associar os arquivos com a versão correta do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. A menos que você use uma extensão de nome de arquivo específicos da versão, o registro permite aos usuários abrir seu projeto e arquivos de item na versão apropriada do projeto [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 [Sobre extensões de nome de arquivo](../extensibility/about-file-name-extensions.md)  
 Discute como extensões de nome de arquivo são registradas.  
  
 [Especificar identificadores de arquivo para extensões de nome de arquivo](../extensibility/specifying-file-handlers-for-file-name-extensions.md)  
 Fornece informações sobre como registrar os aplicativos que podem abrir, editar e assim por diante, uma extensão de nome de arquivo específico.  
  
 [Registrar verbos para extensões de nome de arquivo](../extensibility/registering-verbs-for-file-name-extensions.md)  
 Discute como registrar verbos.  
  
 [Gerenciar associações de arquivo lado a lado](../extensibility/managing-side-by-side-file-associations.md)  
 Discute como lidar com instalações lado a lado em que uma versão específica do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] deve ser invocado para abrir um arquivo.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Suporte a várias versões do Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md)  
 Descreve os problemas relacionados a várias versões do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e o VSPackage durante o desenvolvimento e implantação para os usuários finais.