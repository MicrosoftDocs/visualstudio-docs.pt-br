---
title: Configurações de inicialização das ferramentas de contêiner do Visual Studio
author: ghogen
description: Visão geral do processo de Build das ferramentas de contêiner
ms.author: ghogen
ms.date: 08/15/2019
ms.technology: vs-azure
ms.topic: reference
ms.openlocfilehash: 07dd9dd4c5c61014eecf245719b142cdbaecbc38
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283327"
---
# <a name="container-tools-launch-settings"></a>Configurações de inicialização das ferramentas de contêiner

Na pasta *Propriedades* em um projeto ASP.NET Core, você pode encontrar o launchSettings.jsno arquivo, que contém configurações que controlam como seu aplicativo Web é iniciado em seu computador de desenvolvimento. Para obter informações detalhadas sobre como esse arquivo é usado no desenvolvimento do ASP.NET, consulte [usar vários ambientes no ASP.NET Core](/aspnet/core/fundamentals/environments?view=aspnetcore-2.2). No *launchSettings.jsno*, as configurações na seção **Docker** estão relacionadas ao modo como o Visual Studio lida com aplicativos em contêineres.

::: moniker range="vs-2017"
```json
    "Docker": {
      "commandName": "Docker",
      "launchBrowser": true,
      "launchUrl": "{Scheme}://{ServiceHost}:{ServicePort}"
    }
```

::: moniker-end
::: moniker range=">=vs-2019"

```json
    "Docker": {
      "commandName": "Docker",
      "launchBrowser": true,
      "launchUrl": "{Scheme}://{ServiceHost}:{ServicePort}",
      "environmentVariables": {
        "ASPNETCORE_URLS": "https://+:443;http://+:80",
        "ASPNETCORE_HTTPS_PORT": "44360"
      },
      "httpPort": 51803,
      "useSSL": true,
      "sslPort": 44360
    }
```

::: moniker-end

A configuração commandName identifica que esta seção se aplica a ferramentas de contêiner. A tabela a seguir mostra as propriedades que podem ser definidas nesta seção:

::: moniker range="vs-2017"

|Nome da configuração|Versão|Exemplo|Descrição|
|------------|-------|-------|---------------|
|launchBrowser|Visual Studio 2017|"launchBrowser": verdadeiro|Indica se o navegador deve ser iniciado após a inicialização bem-sucedida do projeto.|
|launchUrl|Visual Studio 2017|"launchUrl": "{Scheme}://{ServiceHost}: {ServicePortal}"|Essa URL é usada ao iniciar o navegador.  Os tokens de substituição com suporte para esta cadeia de caracteres são:<br>   {Scheme}-substituído por "http" ou "https", dependendo de o SSL ser usado.<br>   {ServiceHost} – geralmente substituído por "localhost". No entanto, ao direcionar contêineres do Windows no Windows 10 RS3 ou mais antigo, ele é substituído pelo IP do contêiner.<br>   {ServicePortal} – geralmente substituído por porta SSL ou httpPort, dependendo se o SSL é usado.  No entanto, ao direcionar contêineres do Windows no Windows 10 RS3 ou mais antigo, ele é substituído por "443" ou "80", dependendo se o SSL é usado.|

::: moniker-end

::: moniker range=">=vs-2019"

| Nome da configuração         | Exemplo                                               | Descrição                                                                                                             |
| -------------------- | ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| commandLineArgs      | "commandLineArgs": "--mydefinition myValue"              | Esses argumentos de linha de comando para iniciar seu aplicativo são usados ao iniciar o projeto no contêiner.                                     |
| environmentVariables | "environmentVariables": {                             | Esses valores de variáveis de ambiente são passados para o processo quando ele é iniciado no contêiner.                       |
|                      | "ASPNETCORE_URLS": " https://+:443 ; http://+:80 ",       |                                                                                                                         |
|                      | "ASPNETCORE_HTTPS_PORT": "44381"                      |                                                                                                                         |
|                      | }                                                     |                                                                                                                         |
| httpPort             | "httpPort": 24051                                     | Essa porta no host é mapeada para a porta do contêiner 80 ao iniciar o contêiner.                                |
|                      |                                                       | Se não for especificado, o valor será obtido do valor iisSettings.                                                          |
| launchBrowser        | "launchBrowser": verdadeiro                                 | Indica se o navegador deve ser iniciado após a inicialização bem-sucedida do projeto.                                       |
| launchUrl            | "launchUrl": "{Scheme}://{ServiceHost}: {ServicePortal}" | Essa URL é usada ao iniciar o navegador. Os tokens de substituição com suporte para esta cadeia de caracteres são:                          |
|                      |                                                       | -{Scheme} – substituído por "http" ou "https", dependendo de o SSL ser usado.                                   |
|                      |                                                       | -{ServiceHost} – geralmente substituído por "localhost".                                                                    |
|                      |                                                       | No entanto, ao direcionar contêineres do Windows no Windows 10 RS3 ou mais antigo, ele é substituído pelo IP do contêiner.           |
|                      |                                                       | -{ServicePortal} – geralmente substituído por porta SSL ou httpPort, dependendo se o SSL é usado.                   |
|                      |                                                       | No entanto, ao direcionar contêineres do Windows no Windows 10 RS3 ou mais antigo, ele é substituído por "443" ou "80",         |
|                      |                                                       | dependendo se o SSL é usado.                                                                                       |
| Porta SSL              | "porta SSL": 44381                                      | Essa porta no host é mapeada para a porta do contêiner 443 ao iniciar o contêiner.                               |
|                      |                                                       | Se não for especificado, o valor será obtido do valor iisSettings.                                                          |
| useSSL               | "useSSL": verdadeiro                                        | Indica se o SSL deve ser usado ao iniciar o projeto. Se useSSL não for especificado, o SSL será usado quando porta SSL > 0. |

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Configure seu projeto definindo as [ferramentas de contêiner Propriedades de compilação](container-msbuild-properties.md).

## <a name="see-also"></a>Veja também

[Docker Compose Propriedades de compilação](docker-compose-properties.md)
