---
title: Aninhando projetos | Microsoft Docs
description: Saiba mais sobre como aninhar projetos, que permite aos desenvolvedores de aplicativos que usam seu VSPackage para agrupar tipos semelhantes de projetos no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project nesting
- nested projects
- projects [Visual Studio SDK], child projects
- projects [Visual Studio SDK], nesting
ms.assetid: 12cce037-9840-4761-845e-5abd5fb317b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 30b562cac794b7ab960f055fe67a5d0cc4ec871f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063209"
---
# <a name="nesting-projects"></a>Aninhando projetos
Os desenvolvedores de aplicativos empresariais que usam o pacote do VS podem, de forma conveniente, agrupar tipos semelhantes de projetos no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] usando o *aninhamento de projetos*. Por exemplo, o projeto de modelo empresarial usa projetos aninhados para agrupar projetos em categorias. Projetos de fachada de negócios, projetos de interface do usuário da Web e assim por diante são agrupados em uma categoria.

 Nesse cenário, não há nenhum limite para o número de projetos que o desenvolvedor pode aninhar em cada projeto pai, embora o desenvolvedor possa fornecer limites programaticamente. Esse tipo de agrupamento também pode ser recursivo, caso em que os projetos do mesmo tipo que um projeto filho podem ser aninhados sob o filho para se tornar um subprojeto do filho, que é um subprojeto do pai.

 O aninhamento de projetos não é uma parte intrínseca do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Você precisa escrever o código para habilitar o aninhamento e aninhamento de subprojetos em projetos filho. O projeto pai é um VSPackage especial, ou tipo de projeto, criado e registrado com seu próprio GUID que inclui o código necessário para implementar o aninhamento de projetos.

 Você pode encontrar um exemplo de como aninhar projetos no [How to: Implement aninhated Projects](../../extensibility/internals/how-to-implement-nested-projects.md).

## <a name="nested-projects-example"></a>Exemplo de projetos aninhados
 ![Solução de projetos aninhados](../../extensibility/internals/media/vsnestedprojects.gif "vsNestedProjects") Exemplo de projetos aninhados

## <a name="see-also"></a>Confira também
- [Considerações para descarregar e recarregar projetos aninhados](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)
- [Suporte do assistente para projetos aninhados](../../extensibility/internals/wizard-support-for-nested-projects.md)
- [Registrando modelos de projeto e item](../../extensibility/internals/registering-project-and-item-templates.md)
- [Implementando a manipulação de comando para projetos aninhados](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)
- [Filtrando a caixa de diálogo AddItem para projetos aninhados](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)
- [Lista de verificação: Criando tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)
- [Parâmetros de contexto](../../extensibility/internals/context-parameters.md)
- [Arquivo do assistente (.Vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)
