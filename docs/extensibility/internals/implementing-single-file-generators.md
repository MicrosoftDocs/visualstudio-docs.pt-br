---
title: Implementando geradores de arquivo único | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- custom tools, implementing
- projects [Visual Studio SDK], extensibility
- projects [Visual Studio SDK], managed custom tools
ms.assetid: fe9ef6b6-4690-4c2c-872c-301c980d17fe
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ce8bca614d0af9c7b0557d5b5979797f127a47af
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62860363"
---
# <a name="implementing-single-file-generators"></a>Implementando geradores de arquivo único
Uma ferramenta personalizada — também conhecido como um gerador de arquivo único — podem ser usados para estender a [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] e [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] sistemas de projeto [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Uma ferramenta personalizada é um componente COM que implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> interface. Usando esta interface, uma ferramenta personalizada transforma um único arquivo de entrada em um arquivo de saída única. O resultado da transformação pode ser o código-fonte, ou qualquer outra saída que é útil. Dois exemplos de arquivos de código personalizados gerados por ferramenta são o código gerado em resposta a alterações em um designer visual e os arquivos gerados usando a descrição de linguagem WSDL (Web Services).

 Quando uma ferramenta personalizada é carregada, ou o arquivo de entrada é salva, o sistema de projeto chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> método e passa uma referência a um <xref:Microsoft.VisualStudio.Shell.Interop.IVsGeneratorProgress> interface de retorno de chamada, no qual a ferramenta pode relatar o progresso ao usuário.

 O arquivo de saída que gera a ferramenta personalizada é adicionado ao projeto com uma dependência no arquivo de entrada. O sistema de projeto determina automaticamente o nome do arquivo de saída, com base em cadeia de caracteres retornada pela implementação da ferramenta personalizada de <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A>.

 Uma ferramenta personalizada deve implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> interface. Opcionalmente, dar suporte a ferramentas personalizadas a <xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite> interface para recuperar informações de fontes diferentes do arquivo de entrada. Em qualquer caso, antes de usar uma ferramenta personalizada, você deve registrá-lo com o sistema ou no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] registro local. Para obter mais informações sobre como registrar ferramentas personalizadas, consulte [registrar geradores de arquivo único](../../extensibility/internals/registering-single-file-generators.md).

## <a name="see-also"></a>Consulte também
- [Expor tipos aos designers visuais](../../extensibility/internals/exposing-types-to-visual-designers.md)