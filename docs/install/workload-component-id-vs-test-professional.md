---
title: IDs de carga de trabalho e de componente do Visual Studio Test Professional
titleSuffix: ''
description: Usar IDs de carga de trabalho e de componente do Visual Studio para fornecer ferramentas de teste integradas para testadores em geral
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.date: 03/16/2020
ms.topic: reference
helpviewer_keywords:
- workload ID, Visual Studio
- component ID, Visual Studio
- install Visual Studio, administrator guide
ms.assetid: 70c03438-8434-4921-ada0-c172519af431
ms.prod: visual-studio-windows
ms.technology: vs-installation
monikerRange: vs-2017
ms.openlocfilehash: ececc1815ebc578076d059b00ade1a5fde4552a4
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2020
ms.locfileid: "79437341"
---
# <a name="visual-studio-test-professional-component-directory"></a>Diretório de componentes do Visual Studio Test Professional

As tabelas desta página listam as IDs que podem ser usadas para instalar o Visual Studio usando a linha de comando ou que podem ser especificadas como uma dependência em um manifesto do VSIX. Observe que adicionaremos outros componentes conforme atualizações forem liberadas para o Visual Studio.

Além disso, observe o seguinte sobre a página:

* Cada carga de trabalho tem sua própria seção, seguida pela ID da carga de trabalho e por uma tabela dos componentes que estão disponíveis para a carga de trabalho.
* Por padrão, os componentes **Obrigatórios** serão instalados durante a instalação da carga de trabalho.
* Se você escolher, você também pode instalar os componentes **Recomendado** e **Opcional.**
* Também adicionamos uma seção que lista os componentes adicionais que não são afiliados a nenhuma carga de trabalho.

Ao definir dependências no manifesto do VSIX, é necessário especificar somente IDs de Componente. Use as tabelas desta página para determinar nossas dependências mínimas de componente. Em alguns cenários, isso pode significar que somente um componente de uma carga de trabalho é especificado. Em outros cenários, isso pode significar que vários componentes de uma única carga de trabalho ou que vários componentes de várias cargas de trabalho são especificados. Para obter mais informações, consulte a página [Como migrar projetos de extensibilidade para o Visual Studio 2017](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md).

Para obter mais informações sobre como usar essas IDs, consulte a página [Usar parâmetros de linha de comando para instalar o Visual Studio 2017](use-command-line-parameters-to-install-visual-studio.md). Além disso, para obter uma lista de IDs de carga de trabalho e de componente para outros produtos, consulte a página [IDs de carga de trabalho e de componente do Visual Studio 2017](workload-and-component-ids.md).

## <a name="test-professional"></a>Test Professional

**ID:** Microsoft.VisualStudio.Workload.TestProfessional

**Descrição:** o Test Professional fornece ferramentas de teste integradas destinadas a testadores em geral, o que os ajuda a impulsionar suas necessidades de teste em todo o ciclo de vida do teste.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.VisualStudio.Component.TestTools.FeedbackClient | Microsoft Feedback Client | 15.6.27406.0 | Obrigatório
Microsoft.VisualStudio.Component.TestTools.MicrosoftTestManager | Microsoft Test Manager | 15.6.27406.0 | Obrigatório

## <a name="unaffiliated-components"></a>Componentes não afiliados

Estes são os componentes que não são incluídos com nenhuma carga de trabalho, mas que podem ser selecionados como um componente individual.

ID do componente | Nome | Versão
--- | --- | ---
n/d | n/d | n/d

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [IDs de carga de trabalho e de componente do Visual Studio](workload-and-component-ids.md)
* [Guia de administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Use parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
  * [Exemplos de parâmetro de linha de comando](command-line-parameter-examples.md)
* [Crie uma instalação offline do Visual Studio](create-an-offline-installation-of-visual-studio.md)
