---
title: Personalizando o IntelliSense para RequireJS | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2be07ef8-9c08-444b-a21a-22a4fe6386a3
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 7b1c32d0096742c2364e5ac3b8afe59b39152b2b
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49246708"
---
# <a name="customizing-intellisense-for-requirejs"></a>Personalizando o IntelliSense para RequireJS
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Começando com o Visual Studio 2013 atualização 4, para o arquivo de RequireJS JavaScript popular e o carregador modular há suporte. RequireJS torna mais fácil de definir dependências entre os módulos de código e carregar dinamicamente os módulos apenas quando necessário. Ao escrever código JavaScript que usa o RequireJS, sugestões do IntelliSense serão fornecidas para os módulos que você já referenciado em sua definição de módulo ou referenciados usando chamadas para `require()` de dentro de seu código.  
  
 Por padrão, o Visual Studio dá suporte a uma configuração muito básica para dar suporte a RequireJS, mas é uma prática comum para configurar suas próprias configurações de configuração personalizada (ou seja, definir aliases para bibliotecas). Este tópico descreve as diferentes maneiras que você pode personalizar o Visual Studio para trabalhar com a instalação de exclusivo do seu projeto.  
  
 Este tópico descreve como:  
  
-   Personalizar o RequireJS em projetos do ASP.NET  
  
-   Personalizar o RequireJS em projetos de JSProj, que são usados para criar aplicativos do Apache Cordova, aplicativos da Windows Store e aplicativos HTML do LightSwitch  
  
## <a name="customize-requirejs-in-aspnet-projects"></a>Personalizar o RequireJS em projetos do ASP.NET  
 Suporte para RequireJS é habilitado automaticamente quando um arquivo chamado Require é referenciado por seu arquivo JavaScript atual (para obter mais informações, consulte a seção de determinar o contexto do IntelliSense no [JavaScript IntelliSense](../ide/javascript-intellisense.md)). Em projetos do ASP.NET, referenciar Require normalmente é feito usando um / / / \<referência / > diretiva dentro de um arquivo _references.js.  
  
### <a name="configure-the-data-main-attribute-in-an-aspnet-project"></a>Configurar o atributo principal de dados em um projeto ASP.NET  
 Para simular com precisão o funcionamento de seu aplicativo quando você executá-lo, o editor do JavaScript precisa saber qual arquivo a ser carregado pela primeira vez durante a configuração Require. Isso normalmente é configurado no seu aplicativo HTML usando o `data-main` atributo do elemento de script que faz referência a Require, conforme mostrado aqui.  
  
```html  
<script src="js/require.js" data-main="js/app.js"></script>  
```  
  
 Neste exemplo, o script referenciado pelo principal de dados (js/app.js) é carregado imediatamente após Require. O arquivo que é carregado imediatamente é o melhor lugar para configurar primeiro o uso do RequireJS (usando `require.config()`). Para informar o editor do JavaScript que arquivo a ser usado para `data-main` em seu aplicativo, adicione uma `data-main` do atributo e, em seguida, modifique um / / / \<referência / > diretiva que faz referência a Require em seu aplicativo. Por exemplo, você pode usar esta diretiva:  
  
```javascript  
/// <reference path="js/require.js" data-main="js/app.js" />  
```  
  
### <a name="configure-the-application-start-page-in-an-aspnet-project"></a>Configurar página inicial do aplicativo em um projeto ASP.NET  
 Quando o aplicativo é executado, RequireJS supõe que relativo caminhos para arquivos (por exemplo, "... \\"caminhos) são relativo ao arquivo HTML que carregou a biblioteca Require. Conforme você escreve o código no editor do Visual Studio para um projeto do ASP.NET, esta página de início é desconhecida e você precisará informar ao editor do qual iniciar a página a ser usada ao usar caminhos de arquivo relativos. Para fazer isso, adicione uma `start-page` de atributo para o / / / \<referência / > diretiva.  
  
```javascript  
/// <reference path="js/require.js" data-main="js/app.js" start-page="/app/index.html" />  
```  
  
 O `start-page` atributo especifica a URL da página que você veria-lo em um navegador ao executar seu aplicativo.  
  
## <a name="customize-requirejs-in-jsproj-projects"></a>Personalizar o RequireJS em projetos JSProj  
 JSProj projetos (arquivos de projeto que terminam em uma extensão. jsproj) são usados para criar aplicativos para aplicativos do Apache Cordova, com base em HTML aplicativos do Windows Store ou HTML do LightSwitch. Diferentemente dos projetos do ASP.NET, esses projetos ler referências aos arquivos. js dos arquivos HTML que existem no projeto. Por isso, ao editar o JavaScript em um projeto JSProj, você verá o suporte para RequireJS estará habilitado se o arquivo JavaScript que está sendo editada é referenciado em outro arquivo HTML que também referencia Require.  
  
 As etapas de personalização necessárias para projetos do ASP.NET não são necessários em um arquivo de projeto JSProj. Ou seja, os arquivos usados por do script de `data-main` atributo na marca de script que faz referência a Require são carregados automaticamente para configurar Require. O arquivo HTML referenciando Require também é usado como a página inicial para o aplicativo.  
  
## <a name="see-also"></a>Consulte também  
 [JavaScript IntelliSense](../ide/javascript-intellisense.md)



