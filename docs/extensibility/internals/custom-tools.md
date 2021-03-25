---
title: Ferramentas personalizadas | Microsoft Docs
description: Saiba como criar ferramentas personalizadas no Visual Studio que associem uma ferramenta a um item em um projeto e executem essa ferramenta sempre que o arquivo for salvo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, custom tools
- tools [Visual Studio], custom
- custom tools
ms.assetid: d669f154-9b23-48b6-b9f6-7419c8dd61a6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d714822605178382ec2ef3574db617f7986cf888
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091039"
---
# <a name="custom-tools"></a>Ferramentas personalizadas
As *ferramentas personalizadas* permitem associar uma ferramenta a um item em um projeto e executar essa ferramenta sempre que o arquivo é salvo. Algumas ferramentas personalizadas, às vezes chamadas de *geradores de arquivo único*, são usadas frequentemente para implementar tradutores que geram código a partir de dados e vice-versa. Por exemplo, geradores de arquivo único criam [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] e [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] código-fonte fora dos arquivos *. Settings* e *. resx* . O código-fonte gerado fornece acesso fortemente tipado aos dados nos arquivos *. Settings* e *. resx* . Os [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] tipos de projeto e oferecem suporte a ferramentas personalizadas; os [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] tipos de projeto não. Seus próprios tipos de projeto também podem oferecer suporte a ferramentas personalizadas.

 As ferramentas personalizadas são componentes registrados que implementam a `IVsSingleFileGenerator` interface.

 As ferramentas personalizadas são associadas a um `ProjectItem` objeto de interface e são como designers e editores. Uma ferramenta personalizada usa o arquivo representado por um `ProjectItem` como entrada e grava um novo arquivo cujo nome de arquivo é fornecido pelo `DefaultExtension` método.

## <a name="in-this-section"></a>Nesta seção
- [Implementar geradores de arquivo único](../../extensibility/internals/implementing-single-file-generators.md)

 Descreve como usar a <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> interface para implementar uma ferramenta personalizada.

- [Registrar geradores de arquivo único](../../extensibility/internals/registering-single-file-generators.md)

 Fornece descrições para todas as entradas de registro para uma ferramenta personalizada.

- [Expor tipos a designers visuais](../../extensibility/internals/exposing-types-to-visual-designers.md)

 Explica como os sistemas de projeto oferecem suporte a designers visuais para acessar classes e tipos gerados por meio de arquivos executáveis temporários (PE).

- [Persistir a propriedade de um item de projeto](../../extensibility/persisting-the-property-of-a-project-item.md)

 Mostra como manter uma propriedade de item de projeto, como o autor de um arquivo de origem, no arquivo de projeto.

## <a name="reference"></a>Referência
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> Fornece detalhes sobre o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> , que transforma um único arquivo de entrada em um único arquivo de saída que pode ser compilado ou adicionado a um projeto.

 <xref:EnvDTE.ProjectItem> Explica a `ProjectItem` interface, que representa um item em um projeto.

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A> Fornece detalhes sobre o `DefaultExtension` método, que recupera a extensão de nome de arquivo que é fornecida ao nome do arquivo de saída.

## <a name="related-sections"></a>Seções relacionadas
- [Estender projetos](../../extensibility/extending-projects.md)

 Descreve como usar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] projetos e soluções para organizar arquivos de código e arquivos de recursos e como implementar o controle do código-fonte.
