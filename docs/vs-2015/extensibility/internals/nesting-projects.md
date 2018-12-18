---
title: Aninhar projetos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- project nesting
- nested projects
- projects [Visual Studio SDK], child projects
- projects [Visual Studio SDK], nesting
ms.assetid: 12cce037-9840-4761-845e-5abd5fb317b0
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: b4ccf51dd492a32990718ffe84bfe78cd736a42c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51805191"
---
# <a name="nesting-projects"></a>Aninhando projetos
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Os desenvolvedores de aplicativos corporativos que usam o seu pacote VS convenientemente podem agrupar tipos semelhantes de projetos juntos em [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] por meio *aninhamento de projeto*. Por exemplo, o projeto de modelo empresarial usa projetos aninhados para projetos de grupo em categorias. Projetos de fachada de negócios, projetos de interface do usuário Web e assim por diante são agrupados em uma categoria.  
  
 Nesse cenário, não há nenhum limite para o número de projetos, que o desenvolvedor pode aninhar em cada projeto pai, embora o desenvolvedor por meio de programação pode fornecer limites. Esse tipo de agrupamento pode ser feito também recursivo, caso em que os projetos do mesmo tipo como um projeto filho podem ser aninhados sob o filho para se tornar um subprojeto do filho, que é um subprojeto do pai.  
  
 Aninhamento de projeto não é uma parte intrínseca da [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Você precisa escrever o código para habilitar o aninhamento e subprojeto de aninhamento dentro de projetos filho. O projeto pai é um VSPackage especial, ou o tipo de projeto, criado e registrado com seu próprio GUID que inclui o código que é necessário para implementar o aninhamento de projeto.  
  
 Você pode encontrar um exemplo de projetos aninhados no exemplo de c# Example.Nested projeto.  
  
## <a name="nested-projects-example"></a>Exemplo de projetos aninhados  
 ![Aninhado projetos de solução](../../extensibility/internals/media/vsnestedprojects.gif "vsNestedProjects")  
Exemplo de projetos aninhados  
  
## <a name="see-also"></a>Consulte também  
 [Como: implementar projetos aninhados](../../extensibility/internals/how-to-implement-nested-projects.md)   
 [Considerações para descarregar e recarregados projetos aninhados](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)   
 [Suporte do Assistente para projetos aninhados](../../extensibility/internals/wizard-support-for-nested-projects.md)   
 [Registrar modelos de projeto e Item](../../extensibility/internals/registering-project-and-item-templates.md)   
 [Implementar manipulação de comando para projetos aninhados](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)   
 [A caixa de diálogo Adicionar item de filtragem para projetos aninhados](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)   
 [Lista de verificação: Criar novos tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [Parâmetros de contexto](../../extensibility/internals/context-parameters.md)   
 [Arquivo do assistente (.Vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)

