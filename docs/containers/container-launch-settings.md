---
title: Visual Studio configurações de início das Ferramentas de Contêiner
author: ghogen
description: Saiba mais sobre as configurações de lançamento das Ferramentas de Contêiner relacionadas à Visual Studio lida com aplicativos em contêineres.
ms.author: ghogen
ms.date: 08/15/2019
ms.technology: vs-azure
ms.topic: reference
ms.openlocfilehash: e50935145913bcd1f3c4457f4704376a0ac0f6ef
ms.sourcegitcommit: 162be102d2c22a1c4ad2c447685abd28e0e85d15
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2021
ms.locfileid: "109973233"
---
# <a name="container-tools-launch-settings"></a>Configurações de início das Ferramentas de Contêiner

Na pasta *Propriedades* em um projeto ASP.NET Core, você pode encontrar o arquivo launchSettings.js, que contém configurações que controlam como seu aplicativo Web é iniciado no computador de desenvolvimento. Para obter informações detalhadas sobre como esse arquivo é usado ASP.NET desenvolvimento, consulte Usar vários [ambientes no ASP.NET Core](/aspnet/core/fundamentals/environments?view=aspnetcore-2.2&preserve-view=true). No *launchSettings.jsno*, as configurações na seção do **Docker** estão relacionadas a como Visual Studio lida com aplicativos em contêineres.

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

A configuração commandName identifica que esta seção se aplica às Ferramentas de Contêiner. A tabela a seguir mostra as propriedades que podem ser definidas nesta seção:

::: moniker range="vs-2017"

|Nome da configuração|Versão|Exemplo|Descrição|
|------------|-------|-------|---------------|
|launchBrowser|Visual Studio 2017|"launchBrowser": true|Indica se o navegador deve ser lançado após iniciar o projeto com êxito.|
|launchUrl|Visual Studio 2017|"launchUrl": "{Scheme}://{ServiceHost}:{ServicePort}"|Essa URL é usada ao iniciar o navegador.  Os tokens de substituição com suporte para essa cadeia de caracteres são:<br>   {Scheme} – substituído por "http" ou "https", dependendo se o SSL é usado.<br>   {ServiceHost} – geralmente substituído por "localhost". No entanto, ao direcionar contêineres do Windows Windows 10 RS3 ou mais antigo, ele é substituído pelo IP do contêiner.<br>   {ServicePort} – geralmente substituído por sslPort ou httpPort, dependendo se o SSL é usado.  No entanto, ao direcionar contêineres do Windows no Windows 10 RS3 ou mais antigo, ele é substituído por "443" ou "80", dependendo se o SSL é usado.|

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
|                      |                                                       | No entanto, ao direcionar contêineres do Windows Windows 10 RS3 ou mais antigo, ele é substituído pelo IP do contêiner.           |
|                      |                                                       | - {ServicePort} - geralmente substituído por sslPort ou httpPort, dependendo se o SSL é usado.                   |
|                      |                                                       | No entanto, ao direcionar contêineres do Windows Windows 10 RS3 ou mais antigo, ele é substituído por "443" ou "80",         |
|                      |                                                       | dependendo se o SSL é usado.                                                                                       |
| sslPort              | "sslPort": 44381                                      | Essa porta no host é mapeada para a porta 443 do contêiner ao iniciar o contêiner.                               |
|                      |                                                       | Se não for especificado, o valor será retirado do valor iisSettings.                                                          |
| Usessl               | "useSSL": true                                        | Indica se o SSL deve ser usado ao iniciar o projeto. Se useSSL não for especificado, o SSL será usado quando sslPort > 0. |

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Configure seu projeto definindo as propriedades [de build das Ferramentas de Contêiner .](container-msbuild-properties.md)

## <a name="see-also"></a>Confira também

- [Docker Compose de build](docker-compose-properties.md)
- [Gerenciar perfis de lançamento para Docker Compose](launch-profiles.md)
