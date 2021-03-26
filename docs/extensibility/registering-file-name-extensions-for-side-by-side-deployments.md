---
title: Registrar extensões de nome de arquivo para IDEs lado a lado
description: Saiba mais sobre como registrar extensões de nome de arquivo para implantações lado a lado, que permite aos usuários abrir arquivos na versão apropriada do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions, registering for side-by-side
ms.assetid: 9ab046a2-147d-4167-aa14-7d661b1eaaa5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ad6b5715b767729715403d064cd46b4556fa17e3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056552"
---
# <a name="register-file-name-extensions-for-side-by-side-deployments"></a>Registrar extensões de nome de arquivo para implantações lado a lado
Para o VSPackages implantado em um ambiente lado a lado, você deve registrar extensões de nome de arquivo para associar os arquivos com a versão correta do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . A menos que você use uma extensão de nome de arquivo específica de versão, o registro permite que os usuários abram o projeto e os arquivos de item de projeto na versão apropriada do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

## <a name="in-this-section"></a>Nesta seção
- [Sobre extensões de nome de arquivo](../extensibility/about-file-name-extensions.md) Discute como as extensões de nome de arquivo são registradas.

- [Especificar manipuladores de arquivo para extensões de nome de arquivo](../extensibility/specifying-file-handlers-for-file-name-extensions.md) Fornece informações sobre como registrar os aplicativos que podem abrir, editar e assim por diante, uma extensão de nome de arquivo específica.

- [Registrar verbos para extensões de nome de arquivo](../extensibility/registering-verbs-for-file-name-extensions.md) Discute como registrar verbos.

- [Gerenciar associações de arquivos lado a lado](../extensibility/managing-side-by-side-file-associations.md) Discute como lidar com instalações lado a lado nas quais uma versão específica do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] deve ser chamada para abrir um arquivo.

## <a name="related-sections"></a>Seções relacionadas
- [Suporte a várias versões do Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md) Descreve problemas relacionados a várias versões do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e seu VSPackage durante o desenvolvimento e a implantação para os usuários finais.
