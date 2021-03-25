---
title: Usando e fornecendo serviços | Microsoft Docs
description: Saiba mais sobre os serviços que o IDE do Visual Studio oferece para o VSPackages fornecer e usar. Estes artigos descrevem como obter e fornecer serviços.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- examples [Visual Studio SDK], services
- Visual Studio, services
- services
ms.assetid: c0b415ba-b825-4da0-9faf-8a60a663e302
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b3f5e99b946514ebd3064441e9d2265be31e968a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060189"
---
# <a name="using-and-providing-services"></a>Usando e fornecendo serviços
Um serviço é um contrato entre duas VSPackages. Uma VSPackage oferece um conjunto específico de interfaces para que outra VSPackage consuma. Por exemplo, [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] o oferece o <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> serviço para qualquer VSPackage que ele carrega. Esse serviço fornece a <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> interface, que pode ser usada para gravar no log de atividades. Para obter mais informações, consulte [como: usar o log de atividades](../extensibility/how-to-use-the-activity-log.md).

 O VSPackages pode oferecer serviços próprios usando a <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> interface.

 O Visual Studio oferece serviços importantes, como o seguinte:

|Serviço IDE|Descrição|
|-----------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>|Fornece acesso aos serviços do IDE lidando com a funcionalidade básica, VSPackages e o registro.|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|Fornece janela básica e funcionalidade relacionada à interface do usuário no IDE, como a capacidade de criar ferramentas e janelas de documentos.|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|Fornece funcionalidade básica relacionada à solução, como a capacidade de enumerar projetos, criar novos projetos e monitorar alterações no projeto.|

## <a name="in-this-section"></a>Nesta seção
- [Noções básicas do serviço](../extensibility/internals/service-essentials.md) Apresenta os elementos importantes de um serviço do Visual Studio.

- [Como: obter um serviço](../extensibility/how-to-get-a-service.md) Discute como solicitar (consumir) um serviço.

- [Como: fornecer um serviço](../extensibility/how-to-provide-a-service.md) Discute como fornecer um serviço.

- [Como: fornecer um serviço assíncrono do Visual Studio](../extensibility/how-to-provide-an-asynchronous-visual-studio-service.md) Discute como fornecer um serviço assíncrono.

- [Como: solucionar problemas de serviços](../extensibility/how-to-troubleshoot-services.md) Discute problemas comuns e apresenta soluções para eles.

## <a name="related-sections"></a>Seções relacionadas
- [SDK do Visual Studio](../extensibility/visual-studio-sdk.md)
