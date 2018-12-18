---
title: Web Essentials do projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- web projects, essentials
ms.assetid: ca2f4e43-322c-4431-8680-52da846940bc
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: bb69eeb701ed5ce24259d203c0320c2635c96e4a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49934516"
---
# <a name="web-project-essentials"></a>Conceitos básicos do projeto Web
Projetos da Web criam aplicativos Web. Você pode usar um projeto da Web para criar um aplicativo Web que tem inteligentes páginas da Web. Uma página da Web inteligente tem o código do lado do servidor que processa a página da Web sob demanda.  
  
 Usando linguagens de programação tradicionais, como [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] ou [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)], você pode criar páginas de Web inteligentes para coletar e processar informações de um usuário, armazená-lo em um banco de dados e assim por diante.  
  
- O modelo code-behind associa os arquivos de código fonte dependentes com páginas da Web com o. asmx ou. aspx de extensão de arquivo. Por exemplo, Hello. aspx pode ter o hello.aspx.cs de arquivo de código fonte dependentes.  
  
- O código de servidor associado a uma página da Web inteligente é compilado em um arquivo executável que está localizado na pasta /bin do site da Web.  
  
- Arquivos de código de origem adicionais, como classes auxiliares que não estão associados uma página da Web específica, estão localizados na pasta /App_Code site da Web.  
  
  -   Um projeto de site da Web (WSP) gera um arquivo executável para cada página da Web inteligente. Arquivos executáveis adicionais são gerados de arquivos na pasta /App_Code qualquer código-fonte.  
  
  -   Um projeto de aplicativo Web (WAP) produz um único arquivo executável que combina o código para todas as páginas da Web inteligentes, bem como todos os arquivos de origem na pasta /App_Code.  
  
- O arquivo de solução para um projeto da Web está localizado separadamente do site em si. Por padrão, arquivos de solução estão localizados em \Documents and Settings\\*Suaconta*\My Documents\\*\<Visual Studio # # # >* \Projects\\ *YourWebSite*.  
  
  > [!NOTE]
  >  Se você quiser manter o arquivo de solução com o site da Web, movê-lo lá e reabri-lo.  
  
- Se você abrir um site que não tiver nenhum arquivo de solução no Visual Studio, um novo arquivo de solução é gerado automaticamente para ele.  
  
- Projetos da Web não tem nenhum arquivo de projeto. Informações do projeto são armazenadas no arquivo de solução, o arquivo Web. config e em outro lugar.  
  
- Adicionando propriedades globais para um projeto Web automaticamente cria um arquivo de armazenamento na pasta de solução de projeto da Web.  
  
- Uma página da Web inteligente pode ser associada uma linguagem de programação do lado do servidor usando a diretiva de página ou o \<script runat = "server" > marca.  
  
- Além disso, as páginas da Web pode ter qualquer número de blocos de script do lado do cliente escrito em qualquer linguagem de script.  
  
- Um sistema de projeto de site da Web é implementado pela adição de modelos de projeto e item e o registro para o [!INCLUDE[vwprvw](../../extensibility/internals/includes/vwprvw_md.md)] projeto.  
  
- Um sistema WAP é implementado como um subtipo de projeto, também chamado de um tipo de projeto. O [!INCLUDE[vwprvw](../../extensibility/internals/includes/vwprvw_md.md)] projeto é tipo pelo subtipo do WAP para criar o sistema WAP. Para obter mais informações sobre os subtipos de projeto, consulte [subtipos do projeto](../../extensibility/internals/project-subtypes.md).  
  
- Uma página da Web inteligente combina o HTML com uma linguagem de programação do lado do servidor. O idioma do lado do servidor é chamado de linguagem independente. Para dar suporte a uma linguagem independente, o sistema de projeto da Web deve implementar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> família de interfaces.  
  
  -   Para dar suporte a linguagem independente em um editor, o serviço de linguagem HTML deve adiar exibindo código independente de linguagem para um serviço de linguagem independente.  
  
  -   Marcadores de erro (vermelho squigglies) sempre devem ser criados no buffer de principal do editor de código.  
  
## <a name="see-also"></a>Consulte também  
 [Projetos Web](../../extensibility/internals/web-projects.md)