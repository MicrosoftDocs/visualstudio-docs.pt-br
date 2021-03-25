---
title: Elementos de design VSPackage de controle do código-fonte | Microsoft Docs
description: Saiba mais sobre a estrutura que o VSPackage de controle do código-fonte deve implementar e as interfaces e os serviços que o VSPackage de controle do código-fonte pode implementar.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, design elements
ms.assetid: edd3f2ff-ca32-4465-8ace-4330493b67bb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1e3e8d70d721e77e0ed7b93dda3be5defdbf7dd9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064054"
---
# <a name="source-control-vspackage-design-elements"></a>Elementos de design do VSPackage de controle do código-fonte
Os tópicos nesta seção descrevem a estrutura que o VSPackage de controle do código-fonte deve implementar para integração profunda. Ele também lista as interfaces e os serviços que o VSPackage de controle do código-fonte pode implementar e as interfaces e serviços que o controle do código-fonte VSPackage pode usar de outros [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] componentes para dar suporte a seu modelo de controle do código-fonte e funcionalidade.

## <a name="in-this-section"></a>Nesta seção
- [Estrutura de VSPackage](../../extensibility/internals/vspackage-structure-source-control-vspackage.md)

 Define a estrutura do controle do código-fonte VSPackage.

- [Interfaces e serviços relacionados](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)

 Lista os serviços e interfaces relacionadas ao pacote de controle do código-fonte.

- [Serviços fornecidos](../../extensibility/internals/services-provided-source-control-vspackage.md)

 Descreve o serviço de controle do código-fonte fornecido pelo VSPackage de controle do código-fonte.

## <a name="related-sections"></a>Seções relacionadas
- [Criar um VSPackage de controle do código-fonte](../../extensibility/internals/creating-a-source-control-vspackage.md)

 Discute como criar um VSPackage de controle do código-fonte que não só fornece funcionalidade de controle do código-fonte, mas pode ser usado para personalizar a [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] interface do usuário do controle do código-fonte.
