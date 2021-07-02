---
title: 'Tutorial: introdução ao Docker & Visual Studio Code'
description: Um tutorial de várias etapas que aborda as noções básicas de como trabalhar com o Docker com o Visual Studio Code.
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: tutorial
ms.workload:
- azure
next_page: app.md
ms.openlocfilehash: 75a51f478e4e58700f6025dd6a87fcc38439ed87
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222650"
---
# <a name="tutorial-get-started-with-docker"></a>Tutorial: introdução ao Docker

Neste tutorial, você aprenderá a criar e implantar aplicativos do Docker, incluindo o uso de vários contêineres com um banco de dados e o uso de Docker Compose. Você também implantará seu aplicativo em contêineres no Azure.

## <a name="start-the-tutorial"></a>Iniciar o tutorial

Se você já executou o comando para começar a usar o tutorial, parabéns!  Caso contrário, abra um prompt de comando ou uma janela de bash e execute o comando:

```cli
docker run -d -p 80:80 docker/getting-started
```

Você observará alguns sinalizadores sendo usados. Veja mais algumas informações sobre elas:

- `-d` -executar o contêiner no modo desanexado (em segundo plano)
- `-p 80:80` -mapear a porta 80 do host para a porta 80 no contêiner
- `docker/getting-started` -a imagem a ser usada

> [!TIP]
> Você pode combinar sinalizadores de caractere único para encurtar o comando completo.
> Por exemplo, o comando acima poderia ser escrito como:
>
> ```cli
> docker run -dp 80:80 docker/getting-started
> ```

## <a name="the-vs-code-extension"></a>a extensão VS Code

antes de ir muito, desejamos realçar a extensão de VS Code do docker, que fornece uma exibição rápida dos contêineres em execução em seu computador. Ele fornece acesso rápido aos logs de contêiner, permite que você obtenha um shell dentro do contêiner e permite gerenciar facilmente o ciclo de vida do contêiner (parar, remover e assim por diante).

Para acessar a extensão, siga as instruções [aqui](https://code.visualstudio.com/docs/containers/overview). Use o ícone do Docker à esquerda para abrir o modo de exibição do Docker. Se você abrir a extensão agora, verá este tutorial em execução! O nome do contêiner ( `angry_taussig` abaixo) é um nome criado aleatoriamente. Portanto, você provavelmente terá um nome diferente.

![Contêiner de tutorial em execução na extensão do Docker](media/vs-tutorial-in-extension.png)

## <a name="what-is-a-container"></a>O que é um contêiner

Agora que você executou um contêiner, o que *é* um contêiner? Em síntese, um contêiner é simplesmente outro processo em seu computador que foi isolado de todos os outros processos no computador host. Esse isolamento utiliza [namespaces de kernel e cgroups](https://medium.com/@saschagrunert/demystifying-containers-part-i-kernel-space-2c53d6979504), recursos que estão no Linux há muito tempo. O Docker trabalhou para tornar esses recursos mais poderosos e fáceis de usar.

> [!NOTE]
> **Criando contêineres do zero** Se você quiser ver como os contêineres são criados a partir do zero, o arroz Liz da segurança da água tem um vídeo no qual cria um contêiner do zero em trânsito:
>
> [!VIDEO https://www.youtube-nocookie.com/embed/8fi7uSYlOdc]

## <a name="what-is-a-container-image"></a>O que é uma imagem de contêiner

Ao executar um contêiner, ele usa um sistema de arquivos isolado. Esse sistema de arquivos personalizado é fornecido por uma **imagem de contêiner**. Como a imagem contém o sistema de arquivos do contêiner, ela deve conter tudo o que é necessário para executar um aplicativo-todas as dependências, a configuração, os scripts, os binários e assim por diante. A imagem também contém outra configuração para o contêiner, como variáveis de ambiente, um comando padrão a ser executado e outros metadados.

Vamos nos aprofundar em imagens posteriormente, abordando tópicos como camadas, práticas recomendadas e muito mais.

> [!NOTE]
> Se você estiver familiarizado com `chroot` o, imagine um contêiner como uma versão estendida do `chroot` . O sistema de arquivos é simplesmente proveniente da imagem. No entanto, um contêiner adiciona isolamento adicional não disponível ao simplesmente usar chroot.

## <a name="next-steps"></a>Próximas etapas

Continue com o tutorial!

> [!div class="nextstepaction"]
> [O aplicativo](your-application.md)
