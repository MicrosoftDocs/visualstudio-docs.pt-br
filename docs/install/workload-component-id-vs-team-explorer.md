---
title: IDs de carga de trabalho e de componente do Team Explorer para Visual Studio 2017
titleSuffix: ''
description: Usar IDs de carga de trabalho e de componente do Visual Studio para fornecer ferramentas de teste integradas para testadores em geral
keywords: ''
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.date: 11/13/2018
ms.prod: visual-studio-dev15
ms.topic: reference
helpviewer_keywords:
- workload ID, Visual Studio
- component ID, Visual Studio
- install Visual Studio, administrator guide
ms.assetid: c6ef9a3b-d13d-49b4-9faa-51fa06b21e1f
ms.workload:
- multiple
monikerRange: vs-2017
ms.openlocfilehash: f5b9d6b449a2f551e96132e07c0997455388fa82
ms.sourcegitcommit: 23feea519c47e77b5685fec86c4bbd00d22054e3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56841501"
---
# <a name="visual-studio-team-explorer-2017-component-directory"></a>Diretório de componentes do Team Explorer para Visual Studio 2017

As tabelas desta página listam as IDs que podem ser usadas para instalar o Visual Studio usando a linha de comando ou que podem ser especificadas como uma dependência em um manifesto do VSIX. Observe que adicionaremos outros componentes conforme atualizações forem liberadas para o Visual Studio.

Além disso, observe o seguinte sobre a página:

* Cada carga de trabalho tem sua própria seção, seguida pela ID da carga de trabalho e por uma tabela dos componentes que estão disponíveis para a carga de trabalho.
* Por padrão, os componentes **Obrigatórios** serão instalados durante a instalação da carga de trabalho.
* Se preferir, também será possível instalar os componentes **Recomendados** e **Opcionais**.
* Também adicionamos uma seção que lista os componentes adicionais que não são afiliados a nenhuma carga de trabalho.

Ao definir dependências no manifesto do VSIX, é necessário especificar somente IDs de Componente. Use as tabelas desta página para determinar nossas dependências mínimas de componente. Em alguns cenários, isso pode significar que somente um componente de uma carga de trabalho é especificado. Em outros cenários, isso pode significar que vários componentes de uma única carga de trabalho ou que vários componentes de várias cargas de trabalho são especificados. Para obter mais informações, confira a página [Como: Migrar projetos de extensibilidade para o Visual Studio 2017](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md).

Para obter mais informações sobre como usar essas IDs, consulte a página [Usar parâmetros de linha de comando para instalar o Visual Studio 2017](use-command-line-parameters-to-install-visual-studio.md). Além disso, para obter uma lista de IDs de carga de trabalho e de componente para outros produtos, consulte a página [IDs de carga de trabalho e de componente do Visual Studio 2017](workload-and-component-ids.md).

## <a name="visual-studio-core-editor-included-with-visual-studio-team-explorer-2017"></a>Editor de núcleo do Visual Studio (incluído no Team Explorer para Visual Studio 2017)

**ID:** Microsoft.VisualStudio.Workload.CoreEditor

**Descrição:** A experiência do shell do núcleo do Visual Studio, incluindo edição de código com reconhecimento de sintaxe, controle do código-fonte e gerenciamento de itens de trabalho.

### <a name="components-included-by-this-workload"></a>Componentes incluídos por essa carga de trabalho

ID do componente | Nome | Versão | Tipo de dependência
--- | --- | --- | ---
Microsoft.VisualStudio.Component.CoreEditor | Editor do Visual Studio Core | 15.8.27729.1 | Necessária
Microsoft.VisualStudio.Component.StartPageExperiment.Cpp | Página inicial do Visual Studio para usuários C++ | 15.0.27128.1 | Opcional

## <a name="unaffiliated-components"></a>Componentes não afiliados

Estes são os componentes que não são incluídos com nenhuma carga de trabalho, mas que podem ser selecionados como um componente individual.

ID do componente | Nome | Versão
--- | --- | ---
N/D | N/D | N/D

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Consulte também

* [Carga de trabalho do Visual Studio e IDs do componente](workload-and-component-ids.md)
* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
  * [Exemplos de parâmetro de linha de comando](command-line-parameter-examples.md)
* [Criar uma instalação offline do Visual Studio](create-an-offline-installation-of-visual-studio.md)
