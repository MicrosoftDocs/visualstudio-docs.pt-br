---
title: Sobre extensões de nome de arquivo | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- file extensions
- file name extensions
ms.assetid: 99f4f9ff-fb84-4258-9787-6890f308a57f
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 866a30279ca2c79f4a490a040f76bc3a86c6a6e1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68148029"
---
# <a name="about-file-name-extensions"></a>Sobre as extensões de nome de arquivo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você registra uma extensão de arquivo de um VSPackage, associá-la com uma versão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Isso é importante se mais de uma versão de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é instalado em um computador.  
  
 Extensões de arquivo para os VSPackages são registradas na chave HKEY_CLASSES_ROOT com um valor padrão que aponta para o identificador associado programático (ProgID).  
  
 Este é um exemplo das informações de registro para a extensão de arquivo. vcproj:  
  
```  
HKEY_CLASSES_ROOT\  
   .vcproj\  
      (default)=" VisualStudio.vcproj.8.0"   
```  
  
 Arquivos associados [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] devem ter um ProgID com controle de versão, como `VisualStudio.vcproj.8.0`, para permitir instalações lado a lado do produto para manter as associações de extensão de arquivo entre as versões do produto. Um ProgID específico da versão também permite que você use verbos padrão, como abrir, editar e assim por diante, sem a preocupação de substituir ou ser substituído por outros aplicativos ou versões do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 Em alguns casos, o ProgID associado com uma extensão de arquivo não deve ser alterado. Por exemplo, o ProgID para a extensão de arquivo. htm (progid = htmlfile) é embutido em um número de locais no sistema operacional e é amplamente conhecida e usada em associação com arquivos htm e.  
  
## <a name="see-also"></a>Consulte também  
 [Registrando extensões de nome de arquivo para implantações lado a lado](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)   
 [Especificar identificadores de arquivo para extensões de nome de arquivo](../extensibility/specifying-file-handlers-for-file-name-extensions.md)
