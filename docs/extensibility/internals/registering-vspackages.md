---
title: Registrando VSPackages | Microsoft Docs
description: Um arquivo. pkgdef tem informações que, de outra forma, seriam adicionadas ao registro do sistema. Saiba como o Visual Studio usa arquivos. pkgdef para descrever/localizar um VSPackage.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, registering
- registration, managed VSPackages
ms.assetid: 79b9424e-7e9b-4fc8-9b9f-00212674573c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9e2ed8d7c376f7d9f23e06786fefc1a955ebea3a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069459"
---
# <a name="registering-vspackages"></a>Registrando VSPackages
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depende de arquivos. pkgdef para descrever e localizar um VSPackage. Um arquivo. pkgdef contém todas as informações de registro que, de outra forma, seriam adicionadas ao registro do sistema. Os VSPackages gerenciados são registrados pela adição de atributos ao código-fonte e, em seguida, pela execução do [utilitário CreatePkgDef](../../extensibility/internals/createpkgdef-utility.md) no assembly resultante para gerar um arquivo. pkgdef.

## <a name="in-this-section"></a>Nesta seção
- [Especificando o local do arquivo do VSPackage para o Shell do VS](../../extensibility/internals/specifying-vspackage-file-location-to-the-vs-shell.md)

 Descreve o caminho de carregamento para VSPackages.

- [Registrar e cancelar o registro de VSPackages](../../extensibility/registering-and-unregistering-vspackages.md)

 Explica como registrar um VSPackage.
