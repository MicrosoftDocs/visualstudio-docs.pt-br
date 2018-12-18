---
title: Estender diagramas de camada | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-techdebt
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- layer diagrams, creating extensions
- layer models
ms.assetid: 83fca301-b008-485a-87eb-218050e71451
caps.latest.revision: 41
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 20d84c91ef30ae549b8fa59893d439a06467ed33
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51766923"
---
# <a name="extend-layer-diagrams"></a>Estender diagramas de camada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode escrever código para criar e atualizar diagramas de camada e também para validar a estrutura do código do programa em relação a diagramas de camada no Visual Studio. Você pode adicionar comandos que aparecem no menu de atalho (contexto) dos diagramas, personalizar gestos de arrastar e soltar e acessar o modelo de camada de modelos de texto. Você pode empacotar essas extensões em um Visual Studio Integration VSIX (extensão) e distribuí-los a outros usuários do Visual Studio.  
  
 Para obter mais informações sobre diagramas de camada, consulte:  
  
-   [Diagramas de camada: referência](../modeling/layer-diagrams-reference.md)  
  
-   [Diagramas de camada: diretrizes](../modeling/layer-diagrams-guidelines.md)  
  
-   [Criar diagramas de camada por meio de código](../modeling/create-layer-diagrams-from-your-code.md)  
  
-   [Validar o código com diagramas de camada](../modeling/validate-code-with-layer-diagrams.md)  
  
##  <a name="prereqs"></a> Requisitos  
 Você deve ter os seguintes itens instalados no computador em que você deseja desenvolver suas extensões em camadas:  
  
- Visual Studio  
  
- [SDK do Visual Studio](../extensibility/visual-studio-sdk.md)  
  
- [SDK de modelagem para Visual Studio 2015](http://www.microsoft.com/download/details.aspx?id=48148)  
  
  Você deve ter uma versão adequada do Visual Studio instalado no computador em que você deseja executar suas extensões em camadas. Para obter mais informações, consulte [implantar uma extensão de modelo de camada](../modeling/deploy-a-layer-model-extension.md).  
  
  Para ver quais versões do Visual Studio dão suporte a diagramas de camada, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Adicionar comandos e gestos a diagramas de camada](../modeling/add-commands-and-gestures-to-layer-diagrams.md)  
  
 [Adicionar validação de arquitetura personalizada a diagramas de camada](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)  
  
 [Adicionar propriedades personalizadas a diagramas de camada](../modeling/add-custom-properties-to-layer-diagrams.md)  
  
 [Navegar e atualizar modelos de camada no código do programa](../modeling/navigate-and-update-layer-models-in-program-code.md)  
  
 [Implantar uma extensão de modelo de camada](../modeling/deploy-a-layer-model-extension.md)  
  
 [Solucionar problemas de extensões para diagramas de camada](../modeling/troubleshoot-extensions-for-layer-diagrams.md)  
  
## <a name="see-also"></a>Consulte também  
 [Definir e instalar uma extensão de modelagem](../modeling/define-and-install-a-modeling-extension.md)   
 [Diagramas de camada: referência](../modeling/layer-diagrams-reference.md)   
 [Diagramas de camada: diretrizes](../modeling/layer-diagrams-guidelines.md)   
 [Criar diagramas de camada do seu código](../modeling/create-layer-diagrams-from-your-code.md)   
 [Validar o código com diagramas de camada](../modeling/validate-code-with-layer-diagrams.md)   
 [Gerar arquivos de um modelo UML](../modeling/generate-files-from-a-uml-model.md)   
 [Abrir um modelo UML usando a API do Visual Studio](../modeling/open-a-uml-model-by-using-the-visual-studio-api.md)



