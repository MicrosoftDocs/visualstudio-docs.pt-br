---
title: Web Essentials do projeto | Microsoft Docs
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
- web projects, essentials
ms.assetid: ca2f4e43-322c-4431-8680-52da846940bc
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6343860465cc5c8acdefb80a39eac3c33087a36d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51748833"
---
# <a name="web-project-essentials"></a>Conceitos básicos do projeto Web
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Projetos da Web criam aplicativos Web. Você pode usar um projeto da Web para criar um aplicativo Web que tem inteligentes páginas da Web. Uma página da Web inteligente tem o código do lado do servidor que processa a página da Web sob demanda.  
  
 Usando linguagens de programação tradicionais, como [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] ou [!INCLUDE[csprcs](../../includes/csprcs-md.md)], você pode criar páginas de Web inteligentes para coletar e processar informações de um usuário, armazená-lo em um banco de dados e assim por diante.  
  
-   O modelo code-behind associa os arquivos de código fonte dependentes com páginas da Web com o. asmx ou. aspx de extensão de arquivo. Por exemplo, Hello. aspx pode ter o hello.aspx.cs de arquivo de código fonte dependentes.  
  
-   O código de servidor associado a uma página da Web inteligente é compilado em um arquivo executável que está localizado na pasta /bin do site da Web.  
  
-   Arquivos de código de origem adicionais, como classes auxiliares que não estão associados uma página da Web específica, estão localizados na pasta /App_Code site da Web.  
  
    -   Um projeto de site da Web (WSP) gera um arquivo executável para cada página da Web inteligente. Arquivos executáveis adicionais são gerados de arquivos na pasta /App_Code qualquer código-fonte.  
  
    -   Um projeto de aplicativo Web (WAP) produz um único arquivo executável que combina o código para todas as páginas da Web inteligentes, bem como todos os arquivos de origem na pasta /App_Code.  
  
-   O arquivo de solução para um projeto da Web está localizado separadamente do site em si. Por padrão, arquivos de solução estão localizados em \Documents and Settings\\*Suaconta*\My Documents\\*\<Visual Studio # # # >* \Projects\\ *YourWebSite*.  
  
    > [!NOTE]
    >  Se você quiser manter o arquivo de solução com o site da Web, movê-lo lá e reabri-lo.  
  
-   Se você abrir um site que não tiver nenhum arquivo de solução no Visual Studio, um novo arquivo de solução é gerado automaticamente para ele.  
  
-   Projetos da Web não tem nenhum arquivo de projeto. Informações do projeto são armazenadas no arquivo de solução, o arquivo Web. config e em outro lugar.  
  
-   Adicionando propriedades globais para um projeto Web automaticamente cria um arquivo de armazenamento na pasta de solução de projeto da Web.  
  
-   Uma página da Web inteligente pode ser associada uma linguagem de programação do lado do servidor usando a diretiva de página ou o \<script runat = "server" > marca.  
  
-   Além disso, as páginas da Web pode ter qualquer número de blocos de script do lado do cliente escrito em qualquer linguagem de script.  
  
-   Um sistema de projeto de site da Web é implementado pela adição de modelos de projeto e item e o registro para o [!INCLUDE[vwprvw](../../includes/vwprvw-md.md)] projeto.  
  
-   Um sistema WAP é implementado como um subtipo de projeto, também chamado de um tipo de projeto. O [!INCLUDE[vwprvw](../../includes/vwprvw-md.md)] projeto é tipo pelo subtipo do WAP para criar o sistema WAP. Para obter mais informações sobre os subtipos de projeto, consulte [subtipos do projeto](../../extensibility/internals/project-subtypes.md).  
  
-   Uma página da Web inteligente combina o HTML com uma linguagem de programação do lado do servidor. O idioma do lado do servidor é chamado de linguagem independente. Para dar suporte a uma linguagem independente, o sistema de projeto da Web deve implementar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> família de interfaces.  
  
    -   Para dar suporte a linguagem independente em um editor, o serviço de linguagem HTML deve adiar exibindo código independente de linguagem para um serviço de linguagem independente.  
  
    -   Marcadores de erro (vermelho squigglies) sempre devem ser criados no buffer de principal do editor de código.  
  
## <a name="see-also"></a>Consulte também  
 [Projetos Web](../../extensibility/internals/web-projects.md)

