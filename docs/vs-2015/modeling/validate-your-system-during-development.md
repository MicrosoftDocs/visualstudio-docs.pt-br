---
title: Validar o sistema durante o desenvolvimento | Microsoft Docs
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
- layer diagrams
ms.assetid: c9dafb47-7b1d-4c72-9432-d43be3db1799
caps.latest.revision: 39
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 03cac924853f4348faabd773260a9512c2d82b6b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51760982"
---
# <a name="validate-your-system-during-development"></a>Validar o sistema durante o desenvolvimento
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio pode ajudar a manter seu software consistentes com os requisitos de usuários e com a arquitetura do seu sistema.  
  
 Para ver quais versões do Visual Studio dão suporte a cada um desses recursos, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
## <a name="key-tasks"></a>Tarefas-chave  
 Use as seguintes tarefas para validar seu software.  
  
|**Tarefas**|**Tópicos associados**|  
|---------------|---------------------------|  
|**Verifique se que seu modelo é consistente:**<br /><br /> Dependendo de como o seu projeto usa e interpreta os modelos, pode ser útil para não permitir algumas combinações de elementos. Por exemplo, você poderia restringir classes UML para que eles sempre têm [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)]-nomes em conformidade. Você pode definir restrições de como esses em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensões.|-   [Validar o modelo UML](../modeling/validate-your-uml-model.md)<br />-   [Definir restrições de validação para modelos UML](../modeling/define-validation-constraints-for-uml-models.md)|  
|**Verifique se o seu software atenda aos requisitos dos usuários**:<br /><br /> Você pode usar os requisitos e modelos de arquitetura para ajudar você a organizar os testes do seu sistema e seus componentes. Essa prática ajuda a garantir que você teste os requisitos que são importantes para os usuários e outros participantes e ajudá-lo a atualizar os testes rapidamente quando os requisitos são alterados.|-   [Desenvolver testes de um modelo](../modeling/develop-tests-from-a-model.md)|  
|**Certifique-se de que seu software permaneça consistente com o design pretendido do seu sistema:**<br /><br /> Diagramas de camada descrevem as dependências pretendidas entre os componentes do seu aplicativo. Durante o desenvolvimento, você pode verificar que as dependências reais no código em conformidade com o design desejado.|-   [Criar diagramas de camada do seu código](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [Validar o código com diagramas de camada](../modeling/validate-code-with-layer-diagrams.md)|  
  
## <a name="external-resources"></a>Recursos externos  
  
|**Categoria**|**Links**|  
|------------------|---------------|  
|**Vídeos**|![link para vídeo](../data-tools/media/playvideo.gif "PlayVideo") [Channel 9: Doug sete: Noções básicas sobre o código e Design do sistema com o Visual Studio 2010](http://go.microsoft.com/fwlink/?LinkId=216100)<br /><br /> ![link para vídeo](../data-tools/media/playvideo.gif "PlayVideo") [Channel 9: arquitetura de um aplicativo usando um diagrama de camada](http://go.microsoft.com/fwlink/?LinkID=201117)<br /><br /> ![link para vídeo](../data-tools/media/playvideo.gif "PlayVideo") [série MSDN How Do I: como validar códigos usando diagramas de camada](http://go.microsoft.com/fwlink/?LinkID=214405)|  
|**Fóruns**|-   [Visualização do Visual Studio e ferramentas de modelagem](http://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visualização do Visual Studio e modelagem (ferramentas DSL) do SDK](http://go.microsoft.com/fwlink/?LinkId=184721)|  
|**Blogs**|-   [Visual Studio ALM + Blog do Team Foundation Server](http://go.microsoft.com/fwlink/?LinkID=201340)|  
|**Artigos técnicos e diários**|[MSDN Architecture Center](http://go.microsoft.com/fwlink/?LinkId=201343)|  
  
## <a name="see-also"></a>Consulte também  
 [Testando o aplicativo](http://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac)   
 [Estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md)   
 [Requisitos de usuário do modelo](../modeling/model-user-requirements.md)   
 [Análise e modelagem de arquitetura](../modeling/analyze-and-model-your-architecture.md)



