---
title: Suporte do Site da Web | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- web site projects
ms.assetid: ce9f4266-bb64-4c09-be88-4bd6413f60d0
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 6d3da310c6695598eef36998cc562f6d477eff29
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31139845"
---
# <a name="web-site-support"></a>Suporte do Site da Web
Um sistema de projeto de site da Web é um sistema de projeto que cria projetos da Web. Projetos da Web por sua vez criam aplicativos da Web. Um projeto de site gera um arquivo executável para cada página da Web que tem o código associado. Arquivos executáveis adicionais são gerados a partir de arquivos de código-fonte na pasta /App_Code.  
  
 Sistemas de projeto de site da Web são criados com a adição de modelos e atributos de registro para um sistema de projeto existente. Um desses atributos seleciona o provedor do IntelliSense para o idioma. A implementação de provedor de IntelliSense trata referências e chama o compilador de linguagem quando uma página da Web inteligente que não estão em cache é solicitada.  
  
 O compilador de idioma usado para compilar páginas da Web deve ser registrado com [!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)]. Você pode usar o [ \<compilador > elemento](/dotnet/framework/configure-apps/file-schema/compiler/compiler-element) em um arquivo Web. config para registrar o compilador, como no exemplo a seguir:  
  
```  
<system.codedom>  <compilers>    <compiler language="py;IronPython" extension=".py"       type="IronPython.CodeDom.PythonProvider, IronPython,       Version=1.0.2391.18146, Culture=neutral,       PublicKeyToken=b03f5f7f11d50a3a" />  </compilers></system.codedom>  
```  
  
## <a name="in-this-section"></a>Nesta seção  
 [Modelos de suporte do site](../../extensibility/internals/web-site-support-templates.md)  
 Lista os modelos que você pode usar para criar novos projetos de site da Web e itens associados.  
  
 [tributos de suporte do site](../../extensibility/internals/web-site-support-attributes.md)  
 Apresenta os atributos de registro que se conectam a um projeto de site da Web para [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] e [!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)].  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Projetos Web](../../extensibility/internals/web-projects.md)  
 Apresenta uma visão geral dos dois tipos de projetos da Web, projetos de site da Web e projetos de aplicativo Web.