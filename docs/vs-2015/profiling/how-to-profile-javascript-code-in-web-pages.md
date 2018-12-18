---
title: Como analisar código JavaScript em páginas da Web | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- JavaScript performance profiling
- Profiling Tools,JavaScript
- web site performance profiling
ms.assetid: 37d02aad-ca4d-4eb0-bf66-ca3ecef31fbe
caps.latest.revision: 32
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8f9def923e0cc012a37c02d24b67e807668ae976
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51792106"
---
# <a name="how-to-profile-javascript-code-in-web-pages"></a>Como analisar código JavaScript em páginas da Web
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] podem coletar dados de desempenho para o código JavaScript que é executado em um aplicativo Web do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)], em uma página da Web arbitrária ou em um aplicativo JavaScript usando o método de criação de perfil de instrumentação.  
  
 **Requisitos**  
  
-   [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
-   Internet Explorer 8 ou posterior.  
  
> [!WARNING]
>  Para analisar JavaScript em aplicativos da Windows Store, consulte um dos seguintes tópicos:  
> 
> - [Temporização de função JavaScript](http://msdn.microsoft.com/library/b2bf49fc-aea7-4d9c-8fcf-cff8b8dd0c03) [temporização de função JavaScript em um dispositivo remoto](http://msdn.microsoft.com/library/d78812b6-a97e-46dc-8d99-e724d1d725d8)  
>   -   [Analisar dados de temporização de função JavaScript](http://msdn.microsoft.com/library/b5aea8d8-36df-47ba-a7ca-95406700ca9b)  
>   -  
  
 Você pode usar o Assistente de Criação de Perfil para criar uma sessão de desempenho. Especifique o método de instrumentação e, em seguida, especifique a opção de criação de perfil JavaScript na página de Instrumentação da caixa de diálogo de propriedades da sessão de desempenho.  
  
 Ao especificar criação de perfil JavaScript, o código JavaScript que é executado no navegador e o código do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] que é executado no servidor serão analisados.  
  
-   Para um aplicativo Web do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)], o código JavaScript que é executado no navegador e o código do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] que é executado no servidor serão analisados.  
  
-   Para uma página da Web arbitrária, o código JavaScript que é executado no navegador é analisado.  
  
### <a name="to-profile-javascript-in-an-aspnet-web-application-project"></a>Para analisar JavaScript em um projeto de aplicativo Web ASP .NET  
  
1.  No [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], abra o projeto Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)].  
  
2.  No menu **Analisar**, clique em **Iniciar o Assistente de Desempenho**.  
  
3.  Na primeira página do Assistente de Desempenho, especifique o método de criação de perfil **Instrumentação** e, em seguida, clique em **Avançar**.  
  
4.  Na segunda página do assistente, verifique se o projeto atual está selecionado na lista de destinos e, em seguida, clique em **Avançar.**  
  
5.  Na terceira página do assistente, selecione a caixa de seleção **Perfil JavaScript** e, em seguida, clique em **Avançar**.  
  
6.  Na quarta página do assistente, clique em **Concluir** para iniciar o aplicativo Web no navegador.  
  
7.  Execute a funcionalidade que você deseja analisar.  
  
8.  Para encerrar a sessão de criação de perfil, feche o navegador.  
  
### <a name="to-profile-javascript-in-individual-web-pages-or-a-javascript-applications"></a>Para analisar JavaScript em páginas da Web individuais ou em aplicativos JavaScript  
  
1.  Abra [!INCLUDE[vsPreShort](../includes/vspreshort-md.md)].  
  
2.  No menu **Analisar**, clique em **Iniciar o Assistente de Desempenho**.  
  
3.  Na primeira página do Assistente de Desempenho, especifique o método de criação de perfil **Instrumentação** e, em seguida, clique em **Avançar**.  
  
4.  Na segunda página do assistente, clique em um aplicativo ASP.NET ou JavaScript e, em seguida, clique em **Avançar.**  
  
5.  Na terceira página do assistente:  
  
    1.  Digite a URL da página na caixa **Qual URL ou caminho executará seu aplicativo**.  
  
    2.  Selecione a caixa de seleção **Perfil JavaScript** e, em seguida, clique em **Avançar**.  
  
6.  Na quarta página do assistente, clique em **Concluir** para iniciar a página da Web no navegador.  
  
7.  Execute a funcionalidade que você deseja analisar.  
  
8.  Para encerrar a sessão de criação de perfil, feche o navegador.



