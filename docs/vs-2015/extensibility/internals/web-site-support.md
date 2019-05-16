---
title: Suporte de Site | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- web site projects
ms.assetid: ce9f4266-bb64-4c09-be88-4bd6413f60d0
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f1a96504783de466551c6fb9d055b95ba38df760
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687689"
---
# <a name="web-site-support"></a>Suporte a site
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um sistema de projeto de site da Web é um sistema de projeto que cria projetos da Web. Projetos da Web por sua vez criam aplicativos Web. Um projeto de site gera um arquivo executável para cada página da Web que tem o código associado. Arquivos executáveis adicionais são gerados de arquivos de código-fonte na pasta /App_Code.  
  
 Sistemas de projeto de site da Web são criados com a adição de modelos e os atributos do registro para um sistema de projeto existente. Um desses atributos seleciona o provedor do IntelliSense para o idioma. A implementação do provedor IntelliSense trata referências e chama o compilador de linguagem quando uma página da Web inteligente que não é armazenado em cache é solicitada.  
  
 O compilador de linguagem usado para compilar páginas da Web deve ser registrado com [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]. Você pode usar o [ \<compilador > elemento](https://msdn.microsoft.com/library/7a151659-b803-4c27-b5ce-1c4aa0d5a823) em um arquivo Web. config para registrar o compilador, como no exemplo a seguir:  
  
```  
<system.codedom>  <compilers>    <compiler language="py;IronPython" extension=".py"       type="IronPython.CodeDom.PythonProvider, IronPython,       Version=1.0.2391.18146, Culture=neutral,       PublicKeyToken=b03f5f7f11d50a3a" />  </compilers></system.codedom>  
```  
  
## <a name="in-this-section"></a>Nesta seção  
 [Modelos de suporte do site](../../extensibility/internals/web-site-support-templates.md)  
 Lista os modelos que você pode usar para criar novos projetos de site da Web e os itens associados.  
  
 [tributos de suporte do site](../../extensibility/internals/web-site-support-attributes.md)  
 Apresenta os atributos de registro que se conectam a um projeto de site da Web para [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)].  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Projetos Web](../../extensibility/internals/web-projects.md)  
 Apresenta uma visão geral dos dois tipos de projetos da Web, projetos de site da Web e projetos de aplicativos Web.
