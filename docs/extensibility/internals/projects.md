---
title: Projetos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- custom tools [Visual Studio SDK]
- project subtypes [Visual Studio SDK]
- projects [Visual Studio SDK]
- project types [Visual Studio SDK]
ms.assetid: 237742e4-a638-4d5b-a9b3-6a69d627763c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b2ca4edabcee9f561dea51ea4b579ce194d13fa8
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31130995"
---
# <a name="projects"></a>Projetos
No Visual Studio, os projetos são os contêineres que os desenvolvedores usam para organizar arquivos de código fonte e outros recursos que aparecem em **Gerenciador de soluções**. Normalmente, os projetos são arquivos (por exemplo, um arquivo. csproj para um projeto c#) que armazenam referências aos arquivos de código fonte e recursos, como arquivos de bitmap. Projetos permitem organizar, compilar, depurar e implantar o código-fonte, as referências a serviços Web e bancos de dados e outros recursos. VSPackages pode estender o sistema de projeto do Visual Studio de três maneiras principais: *tipos de projeto*, *projeto subtipos*, e *ferramentas personalizadas*.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Tipos de projeto](../../extensibility/internals/project-types.md)  
 *Tipos de projeto* adicionar suporte para novos tipos de projetos, como linguagens de programação. Por exemplo, cada idioma com suporte para Visual Studio tem seu próprio tipo de projeto, e o exemplo de integração de IronPython inclui um tipo de projeto para o idioma de IronPython. Você deve criar um tipo de projeto para idiomas diferentes do c# ou Visual Basic para personalizar como os itens são criados, depurados, implantados e exibidos no **Gerenciador de soluções**. Para obter mais informações, consulte [tipos de projeto](../../extensibility/internals/project-types.md).  
  
 [Subtipos de projeto](../../extensibility/internals/project-subtypes.md)  
 *Projeto subtipos* são baseados nos tipos de projeto e pode ser usado para personalizar a forma como os projetos são criados, depurados e implantados. O Visual Studio usa subtipos de projeto com projetos de dispositivo inteligente; eles personalizar implantação copiando um programa recentemente criado de um computador de desenvolvimento para o dispositivo de destino. O c# e tipos de projeto do Visual Basic podem ser usados como base para os subtipos de projeto. Tipos de projeto do C++ não é possível. Seus próprios tipos de projeto também podem ser usados como base para os subtipos de projeto. Para obter mais informações, consulte [subtipos de projeto](../../extensibility/internals/project-subtypes.md).  
  
 [Projetos Web](../../extensibility/internals/web-projects.md)  
 Explica o projeto da Web, que por sua vez, criam aplicativos da Web.  
  
 [Nova geração de projeto: Nos bastidores, parte 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md) e [nova geração de projeto: nos bastidores, segunda parte](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)  
 Explica o que realmente ocorre quando você cria um novo projeto.  
  
 [Exemplos de VSSDK](http://aka.ms/vs2015sdksamples)  
 Contém os exemplos de VSSDK que lidam com projetos e soluções.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Dentro do SDK do Visual Studio](../../extensibility/internals/inside-the-visual-studio-sdk.md)  
 Explica os diferentes aspectos de extensibilidade do Visual Studio.