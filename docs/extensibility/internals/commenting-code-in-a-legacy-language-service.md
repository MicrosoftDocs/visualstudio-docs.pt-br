---
title: Comentando o código em um serviço de linguagem herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- comments, supporting in language services [managed package framework]
- language services [managed package framework], commenting code
ms.assetid: 9600d6f0-e2b6-4fe0-b935-fb32affb97a4
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3a4215d3ea841f8e7c7c9f057535d9585682dcfa
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39510417"
---
# <a name="comment-code-in-a-legacy-language-service"></a>Comentar o código em um serviço de linguagem herdado
Linguagens de programação normalmente fornecem um meio de anotações ou comentários de código. Um comentário é uma seção de texto que fornece informações adicionais sobre o código, mas é ignorada durante a compilação ou interpretação.  
  
 As classes do framework (MPF) de pacote gerenciado dão 1&gt;{2&gt;suporte a inserção e texto selecionado.  
  
## <a name="comment-styles"></a>Estilos de comentário  
Há dois estilos gerais de comentário:  
   
1.  Comentários de linha, em que o comentário é em uma única linha.  
  
2.  Comentários do bloco, em que o comentário pode incluir várias linhas.  
  

Comentários de linha geralmente têm um caractere (ou caracteres iniciais), enquanto os comentários do bloco têm caracteres iniciais e finais. Por exemplo, no c#, um comentário de linha começa com `//`, e um comentário de bloco começa com `/*` e termina com `*/`.  
  
Quando o usuário seleciona o comando **seleção de comentário** da **editar** > **avançado** menu, o comando é roteado para o <xref:Microsoft.VisualStudio.Package.Source.CommentSpan%2A> método no <xref:Microsoft.VisualStudio.Package.Source> classe. Quando o usuário seleciona o comando **seleção Descomente**, o comando é roteado para o <xref:Microsoft.VisualStudio.Package.Source.UncommentSpan%2A> método.  
  
## <a name="support-code-comments"></a>Comentários de código de suporte  
 Você pode ter seus comentários de código do idioma serviço suporte por meio do `EnableCommenting` chamado de parâmetro do <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> . Isso define a <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCommenting%2A> propriedade do <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe. Para obter mais informações sobre como definir recursos do serviço de linguagem, consulte [registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md).  
  
 Você também deve substituir a <xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A> método para retornar um <xref:Microsoft.VisualStudio.Package.CommentInfo> estrutura com os caracteres de comentário para o seu idioma. C#-caracteres de comentário de linha de estilo são o padrão.  
  
### <a name="example"></a>Exemplo  
 Aqui está um exemplo de implementação do <xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A> método.  
  
```csharp  
using Microsoft.VisualStudio.Package;  
  
namespace MyLanguagePackage  
{  
    class MySource : Source  
    {  
        public override CommentInfo GetCommentFormat() {  
            CommentInfo info = new CommentInfo();  
            info.LineStart       = "//";  
            info.BlockStart      = "/*";  
            info.BlockEnd        = "*/";  
            info.UseLineComments = true;  
            return info;  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-features1.md)   
 [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)