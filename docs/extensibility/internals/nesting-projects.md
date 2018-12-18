---
title: Projetos de aninhamento | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project nesting
- nested projects
- projects [Visual Studio SDK], child projects
- projects [Visual Studio SDK], nesting
ms.assetid: 12cce037-9840-4761-845e-5abd5fb317b0
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 35d0f4f8906acc08733894d1c24b6d8c2199e1f7
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31131154"
---
# <a name="nesting-projects"></a>Projetos de aninhamento
Os desenvolvedores de aplicativos de empresa que usam o pacote do VS convenientemente podem agrupar tipos semelhantes de projetos de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] usando *aninhamento de projeto*. Por exemplo, o projeto de modelo da empresa usa projetos aninhados para projetos de grupo em categorias. Projetos de fachada de negócios, projetos de interface de usuário da Web e assim por diante são agrupados juntos em uma categoria.  
  
 Neste cenário, não há nenhum limite para o número de projetos, que o desenvolvedor pode aninhar em cada projeto pai, embora o desenvolvedor pode fornecer programaticamente limites. Esse tipo de agrupamento pode ser feito também recursivo, caso em que os projetos do mesmo tipo como um projeto filho podem ser aninhados em filho para se tornar um subprojeto do filho, que é um subprojeto do pai.  
  
 Aninhamento de projeto não é uma parte intrínseca da [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Você precisa escrever o código para habilitar o aninhamento e subprojeto aninhamento dentro de projetos de filho. O projeto principal é um VSPackage especial, ou o tipo de projeto, criado e registrado com seu próprio GUID que inclui o código que é necessário para implementar o aninhamento de projeto.  
  
 Você pode encontrar um exemplo de projetos aninhados no exemplo do c# Example.Nested projeto.  
  
## <a name="nested-projects-example"></a>Exemplo de projetos aninhados  
 ![Aninhados projetos solução](../../extensibility/internals/media/vsnestedprojects.gif "vsNestedProjects")  
Exemplo de projetos aninhados  
  
## <a name="see-also"></a>Consulte também  
 [Como: implementar projetos aninhados](../../extensibility/internals/how-to-implement-nested-projects.md)   
 [Considerações para descarregar e recarregando projetos aninhados](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)   
 [Suporte do Assistente para projetos aninhados](../../extensibility/internals/wizard-support-for-nested-projects.md)   
 [Registro de modelos de projeto e Item](../../extensibility/internals/registering-project-and-item-templates.md)   
 [Implementando o tratamento de projetos aninhados de comando](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)   
 [A caixa de diálogo AddItem de filtragem para projetos aninhados](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)   
 [Lista de verificação: Criar novos tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [Parâmetros de contexto](../../extensibility/internals/context-parameters.md)   
 [Arquivo do assistente (.Vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)