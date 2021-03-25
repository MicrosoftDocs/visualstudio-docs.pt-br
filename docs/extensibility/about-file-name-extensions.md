---
title: Sobre extensões de nome de arquivo | Microsoft Docs
description: Saiba como registrar extensões de nome de arquivo para VSPackages e associá-las a uma versão específica do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions
- file name extensions
ms.assetid: 99f4f9ff-fb84-4258-9787-6890f308a57f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f38bee1b62340f7d557ac2e5190fc5c48d9268fe
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060140"
---
# <a name="about-file-name-extensions"></a>Sobre extensões de nome de arquivo
Ao registrar uma extensão de arquivo de um VSPackage, você o associa a uma versão do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . Isso é importante se mais de uma versão do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] estiver instalada em um computador.

 As extensões de arquivo para VSPackages são registradas em **HKEY_CLASSES_ROOT** chave com um valor padrão que aponta para o identificador de programação (ProgID) associado.

 O exemplo a seguir mostra informações de registro para a extensão de arquivo *. vcproj* :

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)=" VisualStudio.vcproj.8.0"
```

 Os arquivos associados a [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] devem ter um ProgID com versão, como `VisualStudio.vcproj.8.0` . Um ProgID com versão permite instalações lado a lado do produto para manter as associações de extensão de arquivo entre as versões do produto. Um ProgID específico da versão também permite que você use verbos padrão, como abrir, editar e assim por diante, sem a preocupação de substituir ou ser substituído por outros aplicativos ou versões do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

 Em determinados casos, o ProgID associado a uma extensão de arquivo não deve ser alterado. Por exemplo, o ProgID para a extensão de arquivo *. htm* (ProgID = HTMLFILE) é embutido em código em vários locais no sistema operacional e é amplamente conhecido e usado em associação com arquivos *. htm* e *. html* .

## <a name="see-also"></a>Confira também
- [Registrar extensões de nome de arquivo para implantações lado a lado](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)
- [Especificar manipuladores de arquivo para extensões de nome de arquivo](../extensibility/specifying-file-handlers-for-file-name-extensions.md)
