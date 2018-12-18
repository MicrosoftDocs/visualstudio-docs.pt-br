---
title: Decisões de Design do controle de origem | Microsoft Docs
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
- source control [Visual Studio SDK], design decisions
ms.assetid: 5f60ec1a-5a74-4362-8293-817a4dd73872
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: a0932d0029ee924d900dead6b80c3ad2d7e555a0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51726079"
---
# <a name="source-control-design-decisions"></a>Decisões de design de controle do código-fonte
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

As seguintes decisões de design devem ser consideradas para projetos ao implementar o controle de origem.  
  
## <a name="will-information-be-shared-or-private"></a>Informações será compartilhado ou particular?  
 A decisão de design mais importante, que você pode fazer é quais informações são compartilháveis e o que é privado. Por exemplo, a lista de arquivos para o projeto é compartilhada, mas dentro dessa lista de arquivos, alguns usuários talvez queira ter arquivos particulares. Configurações do compilador são compartilhadas, mas o projeto de inicialização é geralmente particular. As configurações são puramente compartilhados, compartilhados com uma substituição ou puramente privadas. Por design, itens particulares, como opções de usuário de solução (. suo) de arquivos, não são verificadas em [!INCLUDE[vsvss](../../includes/vsvss-md.md)]. Certifique-se de armazenar informações particulares em arquivos particulares, como o arquivo. suo ou um arquivo privado específico, você cria, por exemplo, um. arquivo csproj no Visual c# ou. vbproj arquivo para o Visual Basic.  
  
 Essa decisão não é abrangente e pode ser feita em uma base de item por item.  
  
## <a name="will-the-project-include-special-files"></a>O projeto incluirá arquivos especiais?  
 Outra decisão de design importante é se a estrutura do projeto usa arquivos especiais. Arquivos especiais são arquivos ocultos que sustenta os arquivos que são caixas de diálogo visível no Gerenciador de soluções e no check-in e check-out. Se você usar arquivos especiais, siga estas diretrizes:  
  
1.  Não associe arquivos especiais no nó raiz do projeto — ou seja, com o projeto de arquivos em si. O arquivo de projeto deve ser um único arquivo.  
  
2.  Quando os arquivos especiais são adicionados, removidos ou renomeados em um projeto apropriado <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> os eventos devem ser disparados com o conjunto de sinalizador que indica que os arquivos são arquivos especiais. Esses eventos são chamados pelo ambiente em resposta ao projeto de chamada apropriada <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> métodos.  
  
3.  Quando o projeto ou o editor chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> para um arquivo, arquivos especiais associados a esse arquivo não são automaticamente checked out. Passe os arquivos especiais no junto com o arquivo pai. O ambiente será detecte a relação entre todos os arquivos que são passados e ocultar adequadamente os arquivos especiais no check-out de interface do usuário.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>   
 [Oferecer suporte ao controle do código-fonte](../../extensibility/internals/supporting-source-control.md)

