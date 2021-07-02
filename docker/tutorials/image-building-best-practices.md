---
title: 'Tutorial do Docker – Parte 8: Camadas de imagem'
description: Como examinar e gerenciar camadas de imagem em imagens do Docker.
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 8f669baf6f3275f54c7e4a6ff2b31f9c260b2bb9
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222663"
---
# <a name="image-layering"></a>Camadas de imagem

Você sabia que pode ver o que com torna uma imagem? Usando o `docker image history` comando , você pode ver o comando que foi usado para criar cada camada em uma imagem.

1. Use o `docker image history` comando para ver as camadas na imagem criada `getting-started` anteriormente no tutorial.

    ```bash
    docker image history getting-started
    ```

    Você deve obter uma saída parecida com esta (datas/IDs podem ser diferentes).

    ```plaintext
    IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
    a78a40cbf866        18 seconds ago      /bin/sh -c #(nop)  CMD ["node" "/app/src/ind…   0B                  
    f1d1808565d6        19 seconds ago      /bin/sh -c yarn install --production            85.4MB              
    a2c054d14948        36 seconds ago      /bin/sh -c #(nop) COPY dir:5dc710ad87c789593…   198kB               
    9577ae713121        37 seconds ago      /bin/sh -c #(nop) WORKDIR /app                  0B                  
    b95baba1cfdb        13 days ago         /bin/sh -c #(nop)  CMD ["node"]                 0B                  
    <missing>           13 days ago         /bin/sh -c #(nop)  ENTRYPOINT ["docker-entry…   0B                  
    <missing>           13 days ago         /bin/sh -c #(nop) COPY file:238737301d473041…   116B                
    <missing>           13 days ago         /bin/sh -c apk add --no-cache --virtual .bui…   5.35MB              
    <missing>           13 days ago         /bin/sh -c #(nop)  ENV YARN_VERSION=1.21.1      0B                  
    <missing>           13 days ago         /bin/sh -c addgroup -g 1000 node     && addu…   74.3MB              
    <missing>           13 days ago         /bin/sh -c #(nop)  ENV NODE_VERSION=12.14.1     0B                  
    <missing>           13 days ago         /bin/sh -c #(nop)  CMD ["/bin/sh"]              0B                  
    <missing>           13 days ago         /bin/sh -c #(nop) ADD file:e69d441d729412d24…   5.59MB   
    ```

    Cada uma das linhas representa uma camada na imagem. A exibição aqui mostra a base na parte inferior com a camada mais recente na parte superior. Usando isso, você também pode ver rapidamente o tamanho de cada camada, ajudando a diagnosticar imagens grandes.

1. Você observará que várias das linhas estão truncadas. Se você adicionar o sinalizador, obterá a saída completa (sim, você usará um sinalizador truncado para obter `--no-trunc` uma saída não truncada).

    ```bash
    docker image history --no-trunc getting-started
    ```

## <a name="layer-caching"></a>Cache de camada

Agora que você viu a camada em ação, há uma lição importante para aprender a ajudar a diminuir os tempos de build para suas imagens de contêiner.

> Depois que uma camada é muda, todas as camadas downstream também devem ser recriadas

Vamos ver o Dockerfile que você estava usando mais uma vez...

```dockerfile
FROM node:12-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "/app/src/index.js"]
```

Voltando para a saída do histórico de imagens, você verá que cada comando no Dockerfile se torna uma nova camada na imagem. Você pode se lembrar de que, quando você fez uma alteração na imagem, as dependências do yarn precisaram ser reinstaladas. Há uma maneira de corrigir isso? Não faz muito sentido enviar as mesmas dependências sempre que você cria, certo?

Para corrigir isso, você pode reestruturar seu Dockerfile para ajudar a dar suporte ao cache das dependências. Para aplicativos baseados em Nó, essas dependências são definidas no `package.json` arquivo . Então, e se você copiou apenas esse arquivo em primeiro lugar, instalar as dependências *e,* em seguida, copiar em todo o resto? Em seguida, você só recriará as dependências do yarn se houver uma alteração no `package.json` . Faz sentido?

1. Atualize o Dockerfile para copiar na `package.json` primeira, instale as dependências e copie todo o resto.

    ```dockerfile hl_lines="3 4 5"
    FROM node:12-alpine
    WORKDIR /app
    COPY package.json yarn.lock ./
    RUN yarn install --production
    COPY . .
    CMD ["node", "/app/src/index.js"]
    ```

1. Crie uma nova imagem usando `docker build` .

    ```bash
    docker build -t getting-started .
    ```

    Você deverá ver uma saída como esta...

    ```plaintext
    Sending build context to Docker daemon  219.1kB
    Step 1/6 : FROM node:12-alpine
    ---> b0dc3a5e5e9e
    Step 2/6 : WORKDIR /app
    ---> Using cache
    ---> 9577ae713121
    Step 3/6 : COPY package* yarn.lock ./
    ---> bd5306f49fc8
    Step 4/6 : RUN yarn install --production
    ---> Running in d53a06c9e4c2
    yarn install v1.17.3
    [1/4] Resolving packages...
    [2/4] Fetching packages...
    info fsevents@1.2.9: The platform "linux" is incompatible with this module.
    info "fsevents@1.2.9" is an optional dependency and failed compatibility check. Excluding it from installation.
    [3/4] Linking dependencies...
    [4/4] Building fresh packages...
    Done in 10.89s.
    Removing intermediate container d53a06c9e4c2
    ---> 4e68fbc2d704
    Step 5/6 : COPY . .
    ---> a239a11f68d8
    Step 6/6 : CMD ["node", "/app/src/index.js"]
    ---> Running in 49999f68df8f
    Removing intermediate container 49999f68df8f
    ---> e709c03bc597
    Successfully built e709c03bc597
    Successfully tagged getting-started:latest
    ```

    Você verá que todas as camadas foram refeitas. Perfeitamente bem, já que você alterou bastante o Dockerfile.

1. Agora, faça uma alteração no `src/static/index.html` arquivo (como alterar o `<title>` para dizer "The Awesome Todo App").

1. Crie a imagem do Docker agora usando `docker build` novamente. Desta vez, a saída deve parecer um pouco diferente.

    ```plaintext hl_lines="5 8 11"
    Sending build context to Docker daemon  219.1kB
    Step 1/6 : FROM node:12-alpine
    ---> b0dc3a5e5e9e
    Step 2/6 : WORKDIR /app
    ---> Using cache
    ---> 9577ae713121
    Step 3/6 : COPY package* yarn.lock ./
    ---> Using cache
    ---> bd5306f49fc8
    Step 4/6 : RUN yarn install --production
    ---> Using cache
    ---> 4e68fbc2d704
    Step 5/6 : COPY . .
    ---> cccde25a3d9a
    Step 6/6 : CMD ["node", "/app/src/index.js"]
    ---> Running in 2be75662c150
    Removing intermediate container 2be75662c150
    ---> 458e5c6f080c
    Successfully built 458e5c6f080c
    Successfully tagged getting-started:latest
    ```

    Primeiro, você deve observar que o build foi muito mais rápido! E você verá que todas as etapas de 1 a 4 têm `Using cache` . Portanto, hooray! Você está usando o cache de build. Efetuar o e efetuar o estivar essa imagem e atualizá-la também será muito mais rápido. Viva!

## <a name="multi-stage-builds"></a>Builds de vários estágios

Embora não nos aprobamos muito neste tutorial, os builds de vários estágios são uma ferramenta incrivelmente poderosa para ajudar a usar vários estágios para criar uma imagem. Há várias vantagens para eles:

- Separar dependências de tempo de build de dependências de runtime
- Reduzir o tamanho geral da imagem enviando *apenas* o que seu aplicativo precisa executar

### <a name="maventomcat-example"></a>Exemplo de Maven/Tomcat

Ao criar aplicativos baseados em Java, um JDK é necessário para compilar o código-fonte para o código de byte Java. No entanto, esse JDK não é necessário na produção. Além disso, você pode estar usando ferramentas como Maven ou Gradle para ajudar a criar o aplicativo.
Eles também não são necessários em sua imagem final. Ajuda de builds de vários estágios.

```dockerfile
FROM maven AS build
WORKDIR /app
COPY . .
RUN mvn package

FROM tomcat
COPY --from=build /app/target/file.war /usr/local/tomcat/webapps 
```

Este exemplo usa um estágio (chamado `build` ) para executar o build java real usando o Maven. O segundo estágio (começando em `FROM tomcat` ) copia em arquivos do `build` estágio. A imagem final é apenas o último estágio que está sendo criado (que pode ser substituído usando o `--target` sinalizador ).

### <a name="react-example"></a>React exemplo

Ao criar React aplicativos, você precisa de um ambiente node para compilar o código JS (normalmente JSX), folhas de estilos DE SASS e muito mais em HTML estático, JS e CSS. Se você não estiver fazendo a renderização do lado do servidor, nem precisa de um ambiente node para o build de produção. Por que não enviar os recursos estáticos em um contêiner nginx estático?

```dockerfile
FROM node:12 AS build
WORKDIR /app
COPY package* yarn.lock ./
RUN yarn install
COPY public ./public
COPY src ./src
RUN yarn run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
```

Aqui, você está usando uma imagem para executar o build (maximizando o cache de camada) e copiando a saída `node:12` para um contêiner nginx. Legal, não é?

## <a name="recap"></a>Recapitulação

Ao entender um pouco sobre como as imagens são estruturadas, você pode criar imagens mais rapidamente e enviar menos alterações. Os builds de vários estágios também ajudam a reduzir o tamanho geral da imagem e aumentar a segurança final do contêiner separando as dependências de tempo de build das dependências de runtime.

## <a name="next-steps"></a>Próximas etapas

Continue com o tutorial!

> [!div class="nextstepaction"]
> [Implantando na nuvem](deploy-to-cloud.md)