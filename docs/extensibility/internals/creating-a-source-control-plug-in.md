---
title: Criando um plug-in de controle do código-fonte | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- plug-ins, source control
- source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: c7e69fa4-150e-469a-a6fc-fa1260bdbb07
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9e0d9dc54a61cabe7bdd5c21c10abf0def34ff6a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80709182"
---
# <a name="create-a-source-control-plug-in"></a>Criar um plug-in de controle do código-fonte
O SDK do Visual Studio fornece recursos que permitem que você adicione a funcionalidade de controle do código-fonte ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE (ambiente de desenvolvimento integrado). Ele permite que você use qualquer DLL de plug-in que esteja em conformidade com a API de plug-in de controle do código-fonte descrita nesta documentação.

## <a name="in-this-section"></a>Nesta seção
- [Introdução](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)

 Descreve como instalar um plug-in de controle do código-fonte e realça as versões da API de plug-in de controle do código-fonte disponíveis no momento.

- [Arquitetura](../../extensibility/internals/source-control-plug-in-architecture.md)

 Usa um diagrama de arquitetura para explicar a integração de um plug-in de controle do código-fonte com o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE.

- [Guia de teste](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)

 Fornece orientação sobre como testar a instalação e a operação de um plug-in de controle do código-fonte.

## <a name="related-sections"></a>Seções relacionadas
- [Criar um controle do código-fonte VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)

 Discute como criar um VSPackage de controle do código-fonte que não só fornece funcionalidade de controle de origem, mas substitui a [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] interface do usuário do controle do código-fonte.

- [Plug-ins de controle do código-fonte](../../extensibility/source-control-plug-ins.md)

 Fornece uma listagem completa de todos os elementos na API de plug-in de controle do código-fonte.

- [Controle do código-fonte](../../extensibility/internals/source-control.md)

 Discute as opções para implementar o controle do código-fonte como um recurso integrado do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .
