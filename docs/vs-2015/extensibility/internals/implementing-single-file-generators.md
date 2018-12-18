---
title: Implementando geradores de arquivo único | Microsoft Docs
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
- custom tools, implementing
- projects [Visual Studio SDK], extensibility
- projects [Visual Studio SDK], managed custom tools
ms.assetid: fe9ef6b6-4690-4c2c-872c-301c980d17fe
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 36aa6df6c0b904ad11f0027c4e01368a9c864b8a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51781655"
---
# <a name="implementing-single-file-generators"></a>Implementando geradores de arquivo único
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Uma ferramenta personalizada — também conhecido como um gerador de arquivo único — podem ser usados para estender a [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] e [!INCLUDE[csprcs](../../includes/csprcs-md.md)] sistemas de projeto [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Uma ferramenta personalizada é um componente COM que implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> interface. Usando esta interface, uma ferramenta personalizada transforma um único arquivo de entrada em um arquivo de saída única. O resultado da transformação pode ser o código-fonte, ou qualquer outra saída que é útil. Dois exemplos de arquivos de código personalizados gerados por ferramenta são o código gerado em resposta a alterações em um designer visual e os arquivos gerados usando a descrição de linguagem WSDL (Web Services).  
  
 Quando uma ferramenta personalizada é carregada, ou o arquivo de entrada é salva, o sistema de projeto chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> método e passa uma referência a um <xref:Microsoft.VisualStudio.Shell.Interop.IVsGeneratorProgress> interface de retorno de chamada, no qual a ferramenta pode relatar o progresso ao usuário.  
  
 O arquivo de saída que gera a ferramenta personalizada é adicionado ao projeto com uma dependência no arquivo de entrada. O sistema de projeto determina automaticamente o nome do arquivo de saída, com base em cadeia de caracteres retornada pela implementação da ferramenta personalizada de <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A>.  
  
 Uma ferramenta personalizada deve implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> interface. Opcionalmente, dar suporte a ferramentas personalizadas a <xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite> interface para recuperar informações de fontes diferentes do arquivo de entrada. Em qualquer caso, antes de usar uma ferramenta personalizada, você deve registrá-lo com o sistema ou no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registro local. Para obter mais informações sobre como registrar ferramentas personalizadas, consulte [registrar geradores de arquivo único](../../extensibility/internals/registering-single-file-generators.md).  
  
## <a name="see-also"></a>Consulte também  
 [Determinando o Namespace padrão de um projeto](../../misc/determining-the-default-namespace-of-a-project.md)   
 [Expor tipos aos designers visuais](../../extensibility/internals/exposing-types-to-visual-designers.md)

