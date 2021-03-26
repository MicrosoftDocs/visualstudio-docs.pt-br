---
title: Suporte a site | Microsoft Docs
description: Saiba mais sobre os sistemas de projeto de site, que são criados pela adição de modelos e atributos de registro a um sistema de projeto existente.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web site projects
ms.assetid: ce9f4266-bb64-4c09-be88-4bd6413f60d0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 16de0fdc2c4e65dfe6c2ae2c6dc3cdc6902fa8b0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069082"
---
# <a name="web-site-support"></a>Suporte a site
Um sistema de projeto de site é um sistema de projeto que cria projetos Web. Os projetos da Web, por sua vez, criam aplicativos Web. Um projeto de site gera um arquivo executável para cada página da Web com código associado. Arquivos executáveis adicionais são gerados a partir dos arquivos de código-fonte na pasta/App_Code.

 Os sistemas de projeto de site são criados adicionando modelos e atributos de registro a um sistema de projeto existente. Um desses atributos seleciona o provedor IntelliSense para o idioma. A implementação do provedor do IntelliSense manipula referências e chama o compilador de linguagem quando uma página da Web inteligente que não é armazenada em cache é solicitada.

 O compilador de linguagem usado para compilar páginas da Web deve ser registrado com [!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)] . Você pode usar o [ \<compiler> elemento](/dotnet/framework/configure-apps/file-schema/compiler/compiler-element) em um arquivo de Web.config para registrar o compilador, como no exemplo a seguir:

```
<system.codedom>  <compilers>    <compiler language="py;IronPython" extension=".py"       type="IronPython.CodeDom.PythonProvider, IronPython,       Version=1.0.2391.18146, Culture=neutral,       PublicKeyToken=b03f5f7f11d50a3a" />  </compilers></system.codedom>
```

## <a name="in-this-section"></a>Nesta seção
- [Modelos de suporte a site](../../extensibility/internals/web-site-support-templates.md)

 Lista os modelos que você pode usar para criar novos projetos de site e itens associados.

- [Atributos de suporte a site](../../extensibility/internals/web-site-support-attributes.md)

 Apresenta os atributos de registro que conectam um projeto de site ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] e ao [!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)] .

## <a name="related-sections"></a>Seções relacionadas
- [Projetos Web](../../extensibility/internals/web-projects.md)

 Apresenta uma visão geral dos dois tipos de projetos da Web, projetos de sites e projetos de aplicativos Web.
