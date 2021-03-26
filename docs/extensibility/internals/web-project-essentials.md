---
title: Conceitos básicos do projeto Web | Microsoft Docs
description: Aprenda os detalhes internos sobre como os projetos Web funcionam no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web projects, essentials
ms.assetid: ca2f4e43-322c-4431-8680-52da846940bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9442dcdd460e1213c3c07ee87a5ea2e0d7099072
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085696"
---
# <a name="web-project-essentials"></a>Conceitos básicos do projeto Web
Projetos da Web criam aplicativos Web. Você pode usar um projeto Web para criar um aplicativo Web que tenha páginas da Web inteligentes. Uma página da Web inteligente tem um código do lado do servidor que renderiza a página da Web sob demanda.

 Usando linguagens de programação tradicionais, como [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] ou [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] , você pode criar páginas da Web inteligentes para coletar e processar informações de um usuário, armazená-las em um banco de dados e assim por diante.

- O modelo code-behind associa arquivos de código-fonte dependentes com páginas da Web que têm a extensão de arquivo. aspx ou. asmx. Por exemplo, Hello. aspx pode ter o arquivo de código-fonte dependente Hello. aspx. cs.

- O código do lado do servidor associado a uma página da Web inteligente é compilado em um arquivo executável localizado na pasta/bin do site da Web.

- Arquivos de código-fonte adicionais, como as classes auxiliares que não estão associadas a uma página da Web específica, estão localizados na pasta site/App_Code.

  - Um WSP (projeto de site da Web) gera um arquivo executável para cada página da Web inteligente. Arquivos executáveis adicionais são gerados de qualquer arquivo de código-fonte na pasta/App_Code.

  - Um WAP (projeto de aplicativo Web) produz um único arquivo executável que combina o código para todas as páginas da Web inteligentes, bem como todos os arquivos de origem na pasta/App_Code.

- O arquivo de solução para um projeto Web está localizado separadamente do site da Web. Por padrão, os arquivos de solução estão localizados em \Documents and Settings \\ *suaconta*\Meus documentos \\ *\<Visual Studio ####>* \projects \\ *YourWebSite*.

  > [!NOTE]
  > Se você quiser manter o arquivo da solução com o site, basta movê-lo e reabri-lo.

- Se você abrir um site que não tem nenhum arquivo de solução no Visual Studio, um novo arquivo de solução será gerado automaticamente para ele.

- Projetos da Web não têm arquivos de projeto. As informações do projeto são armazenadas no arquivo da solução, no arquivo de web.config e em outro lugar.

- A adição de propriedades globais a um projeto Web cria automaticamente um arquivo de armazenamento na pasta de solução do projeto Web.

- Uma página da Web inteligente pode ser associada a uma linguagem de programação do lado do servidor usando a diretiva Page ou a \<script runat="server"> marca.

- Além disso, as páginas da Web podem ter qualquer número de blocos de script do lado do cliente escritos em qualquer linguagem de script.

- Um sistema de projeto de site é implementado adicionando modelos de projeto e item e registro ao [!INCLUDE[vwprvw](../../extensibility/internals/includes/vwprvw_md.md)] projeto.

- Um sistema WAP é implementado como um subtipo de projeto, também chamado de tipo de projeto. O [!INCLUDE[vwprvw](../../extensibility/internals/includes/vwprvw_md.md)] projeto é recriado pelo subtipo WAP para criar o sistema WAP. Para obter mais informações sobre subtipos de projeto, consulte [subtipos de projeto](../../extensibility/internals/project-subtypes.md).

- Uma página da Web inteligente combina HTML com uma linguagem de programação no servidor. O idioma do lado do servidor é chamado de idioma contido. Para dar suporte a um idioma contido, o sistema de projeto da Web deve implementar a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> família de interfaces.

  - Para dar suporte ao idioma contido em um editor, o serviço de linguagem HTML deve adiar a exibição do código de idioma contido em um serviço de linguagem independente.

  - Marcadores de erro (ondulados vermelho) sempre devem ser criados no buffer primário do editor de código.

## <a name="see-also"></a>Confira também
- [Projetos Web](../../extensibility/internals/web-projects.md)
