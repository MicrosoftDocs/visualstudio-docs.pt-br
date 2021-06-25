---
title: Implementando Single-File geradores | Microsoft Docs
description: Saiba como usar uma ferramenta personalizada que implementa a interface IVsSingleFileGenerator para estender os sistemas de projeto Visual Basic e Visual C# em Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- custom tools, implementing
- projects [Visual Studio SDK], extensibility
- projects [Visual Studio SDK], managed custom tools
ms.assetid: fe9ef6b6-4690-4c2c-872c-301c980d17fe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 11ce8a69841d18d383e9d8e12c14d7af652d9cb8
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900025"
---
# <a name="implementing-single-file-generators"></a>Implementando geradores de arquivo único
Uma ferramenta personalizada , às vezes chamada de gerador de arquivo único, pode ser usada para estender os sistemas [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] de projeto e no [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Uma ferramenta personalizada é um componente COM que implementa a <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> interface . Usando essa interface, uma ferramenta personalizada transforma um único arquivo de entrada em um único arquivo de saída. O resultado da transformação pode ser o código-fonte ou qualquer outra saída útil. Dois exemplos de arquivos de código personalizados gerados por ferramentas são o código gerado em resposta a alterações em um designer visual e arquivos gerados usando o WSDL (Linguagem de Descrição dos Serviços Web).

 Quando uma ferramenta personalizada é carregada ou o arquivo de entrada é salvo, o sistema de projeto chama o método e passa uma referência a uma interface de retorno de chamada, na qual a ferramenta pode relatar seu progresso para <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsGeneratorProgress> o usuário.

 O arquivo de saída que a ferramenta personalizada gera é adicionado ao projeto com uma dependência no arquivo de entrada. O sistema de projeto determina automaticamente o nome do arquivo de saída, com base na cadeia de caracteres retornada pela implementação da ferramenta personalizada de <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A> .

 Uma ferramenta personalizada deve implementar a <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> interface . Opcionalmente, as ferramentas personalizadas suportam <xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite> a interface para recuperar informações de fontes diferentes do arquivo de entrada. Em qualquer caso, antes de usar uma ferramenta personalizada, você deve registrá-la no sistema ou [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] no registro local. Para obter mais informações sobre como registrar ferramentas personalizadas, consulte [Registrando geradores de arquivo único.](../../extensibility/internals/registering-single-file-generators.md)

## <a name="see-also"></a>Confira também
- [Expondo tipos para designers visuais](../../extensibility/internals/exposing-types-to-visual-designers.md)
