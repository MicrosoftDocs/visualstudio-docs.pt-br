---
title: Elementos de um modelo de projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], implementation considerations
- project models
- projects [Visual Studio SDK], elements
ms.assetid: a1dbe0dc-68da-45d7-8704-5b43ff7e4fc4
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 9eab0627184ac887aacfdfb2f275f0e8d9d30df7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49912650"
---
# <a name="elements-of-a-project-model"></a>Elementos de um modelo de projeto
As interfaces e implementações de todos os projetos em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] compartilham uma estrutura básica: o modelo de projeto para o tipo de projeto. Em seu modelo de projeto, que é o VSPackage que você está desenvolvendo, você cria objetos que estão em conformidade com suas decisões de design e trabalham em conjunto com a funcionalidade global fornecida pelo IDE. Embora você controla como um item de projeto é persistido, por exemplo, você não controlar notificação que um arquivo deve ser persistente. Quando um usuário coloca o foco em um item de projeto aberto e escolhe **salvar** na **arquivo** menu o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] menu de barras, o código do tipo de projeto deve interceptar o comando a partir do IDE, manter o arquivo, e Envie notificação de volta para o IDE que o arquivo não é alterado.  
  
 O VSPackage interage com o IDE por meio de serviços que fornecem acesso às interfaces do IDE. Por exemplo, por meio de serviços específicos, você monitor e rotear comandos e fornece informações de contexto para seleções feitas no projeto. Toda a funcionalidade IDE global necessária para o VSPackage é fornecida pelos serviços. Para obter mais informações sobre serviços, consulte [como: obter um serviço](../../extensibility/how-to-get-a-service.md).  
  
 Outras considerações de implementação:  
  
- Um modelo de projeto único pode conter mais de um tipo de projeto.  
  
- Tipos de projeto e as fábricas do Assistente do projeto são registradas independentemente com GUIDs.  
  
- Cada projeto deve ter um arquivo de modelo ou o Assistente para inicializar o novo arquivo de projeto quando um usuário cria um novo projeto por meio de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] interface do usuário. Por exemplo, o [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] modelos inicializar o que eventualmente se tornarem arquivos. vcproj.  
  
  A ilustração a seguir mostra as interfaces principais, serviços e objetos que compõem uma implementação típica do projeto. Você pode usar o aplicativo auxiliar, `HierUtil7`, para criar os objetos subjacentes e outro clichê de programação. Para obter mais informações sobre o `HierUtil7` auxiliar de aplicativo, consulte [HierUtil7 Use classes do projeto para implementar um tipo de projeto (C++)](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346).  
  
  ![Gráfico de modelo de projeto do Visual Studio](../../extensibility/internals/media/vsprojectmodel.gif "vsProjectModel")  
  Modelo de projeto  
  
  Para obter mais informações sobre as interfaces e serviços listados no diagrama anterior e outras interfaces opcionais não incluídos no diagrama, consulte [componentes principais do modelo de projeto](../../extensibility/internals/project-model-core-components.md).  
  
  Projetos pode dar suporte a comandos e, portanto, deve implementar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface participem de roteamento de comando por meio do contexto do comando GUIDs.  
  
## <a name="see-also"></a>Consulte também  
 [Lista de verificação: Criar novos tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [Usar classes do projeto HierUtil7 para implementar um tipo de projeto (C++)](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)   
 [Componentes de núcleo do modelo de projeto](../../extensibility/internals/project-model-core-components.md)   
 [Criar instâncias de projetos usando fábricas de projeto](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)   
 [Como: obter um serviço](../../extensibility/how-to-get-a-service.md)   
 [Criar tipos de projeto](../../extensibility/internals/creating-project-types.md)
