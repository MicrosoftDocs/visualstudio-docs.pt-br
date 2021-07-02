---
title: Experiências conectadas no Visual Studio
description: Uma experiência conectada conecta-se à Internet de um computador cliente e fornece um serviço para o cliente.
ms.date: 05/20/2021
ms.topic: conceptual
helpviewer_keywords: ''
author: SayyedaM
ms.author: sayyedamussa
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.openlocfilehash: 689fc40be8aee959023777a3fac6d9134ee979ea
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222884"
---
# <a name="connected-experiences-in-visual-studio"></a>**Experiências conectadas no Visual Studio** #

a Visual Studio consiste em aplicativos de software cliente e experiências conectadas projetadas para permitir que você codifique com mais eficiência. a atualização de um pacote de [NuGet](/nuget/consume-packages/install-use-packages-visual-studio) , a seleção de uma sugestão de [IntelliCode](/visualstudio/intellicode/overview) e a colaboração com outro desenvolvedor por meio de [Live Share](/visualstudio/liveshare/quickstart/share) são exemplos de experiências conectadas. 

## <a name="choose-whether-these-connected-experiences-are-available-to-use"></a>Escolha se essas experiências conectadas estão disponíveis para uso ##

Você pode escolher quais experiências conectadas usar. o uso de certas experiências conectadas exige contrato para termos diferentes e adicionais para o Visual Studio EULA. Essas experiências podem ser de propriedade da Microsoft serviços online e/ou serviços pertencentes a terceiros. por exemplo, quando você usa GitHub experiências conectadas, a [declaração de privacidade GitHub](https://docs.github.com/github/site-policy/github-privacy-statement) e [GitHub termos de serviço](https://docs.github.com/github/site-policy/github-terms-of-service), [GitHub termos de serviço corporativos](https://docs.github.com/github/site-policy/github-corporate-terms-of-service)e/ou [termos de produtos adicionais](https://docs.github.com/github/site-policy/github-additional-product-terms) serão aplicados. Se você [relatar um problema](/visualstudio/ide/how-to-report-a-problem-with-visual-studio), você concorda com os [termos de uso da Microsoft](https://www.microsoft.com/legal/terms-of-use) e a [política de privacidade da Microsoft](https://privacy.microsoft.com/en-us/privacystatement). se você usar o serviço de NuGet, você concorda com os [NuGet termos de uso](https://www.nuget.org/policies/Terms) e a [política de privacidade da Microsoft](https://privacy.microsoft.com/en-us/privacystatement). 

ao instalar o Visual Studio, [você pode, opcionalmente, selecionar cargas de trabalho e componentes a serem instalados](/visualstudio/install/install-visual-studio). Cargas de trabalho e componentes podem aproveitar software de terceiros e podem habilitar experiências conectadas, dependendo de sua funcionalidade. Por exemplo, [baixar a carga de trabalho de desenvolvimento do Azure permite que você publique seus aplicativos de nuvem no Azure](https://visualstudio.microsoft.com/vs/features/azure/). Com base nas seleções de instalação, você também pode usar o menu ferramentas e opções para se conectar, configurar e usar experiências conectadas. Por exemplo, você pode se conectar a um servidor, adicionar a autenticação de serviços do Azure ou alterar as configurações de IntelliCode ou LiveShare.  

Você também pode usar [as configurações de firewall](/visualstudio/install/install-and-use-visual-studio-behind-a-firewall-or-proxy-server) da sua organização para habilitar ou desabilitar a conexão com os serviços. observe que desabilitar a conexão com um ponto de extremidade pode afetar negativamente ou desabilitar o desempenho de recursos de Visual Studio relacionados. 

por fim, o Visual Studio Marketplace oferece extensões que podem permitir experiências conectadas de primeira ou de terceiros. Visual Studio o marketplace está sujeito aos [termos de uso Visual Studio Marketplace](https://cdn.vsassets.io/v/M146_20190123.39/_content/Microsoft-Visual-Studio-Marketplace-Terms-of-Use.pdf) e à [política de privacidade da Microsoft](https://privacy.microsoft.com/en-us/privacystatement). Cada extensão requer contrato para determinados termos de uso e a política de privacidade associada a essa oferta.  


## <a name="required-service-data"></a>Dados de serviço necessários ##

Os dados de serviço necessários podem incluir informações relacionadas à operação da experiência conectada necessária para manter o serviço subjacente seguro, atualizado e executando conforme o esperado. Se você optar por usar uma experiência conectada que analise seu conteúdo, por exemplo, IntelliCode, o código que você selecionou para seu modelo também será enviado e processado para fornecer a você a experiência conectada. os dados de serviço necessários também podem incluir informações necessárias por uma experiência conectada para executar sua tarefa, atualizando um pacote de NuGet. Você pode gerenciar os dados de serviço necessários escolhendo se deseja ou não usar um serviço específico. Se você não usar um serviço, nenhum dado de serviço necessário será coletado. 

Os dados de serviço necessários são diferentes dos dados de diagnóstico porque os dados de diagnóstico estão relacionados ao software em execução no seu dispositivo. sua escolha se deseja participar do [Visual Studio Programa de Aperfeiçoamento da Experiência do Usuário (VSCEIP) controla as configurações de privacidade dos dados de diagnóstico](/visualstudio/ide/visual-studio-experience-improvement-program), mas essa configuração não afeta se os dados de serviço necessários são enviados. 

## <a name="diagnostic-data-collection"></a>Coleta de dados de diagnóstico ##

os dados de diagnóstico são usados para manter Visual Studio seguro e atualizado, detectar, diagnosticar e corrigir problemas e também melhorar as melhorias do produto. os dados de diagnóstico são coletados e enviados à Microsoft sobre Visual Studio software cliente em execução no dispositivo do usuário.

Ao recusar, você está recusando a coleta de dados de diagnóstico opcional. uma coleta de dados de diagnóstico é necessária para garantir que Visual Studio seja seguro, atualizada e executada conforme o esperado. A coleta de dados de diagnóstico necessária não será afetada por sua escolha para recusar o [VSCEIP](/visualstudio/ide/visual-studio-experience-improvement-program). 
