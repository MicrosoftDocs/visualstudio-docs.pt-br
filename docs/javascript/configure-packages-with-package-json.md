---
title: Configurar pacotes npm com package.json
description: Especifique versões de pacote npm usando package.json
ms.custom: ''
ms.date: 09/06/2018
ms.technology: vs-nodejs
ms.topic: conceptual
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: douge
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 711d7b65eb329e844fedb0148006cacb1c7a0ebf
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219089"
---
# <a name="packagejson-configuration"></a>configuração do package.json

Se você estiver desenvolvendo um aplicativo Node.js com muitos pacotes npm, não é incomum encontrar erros ou avisos quando você compila o projeto se um ou mais pacotes tiverem sido atualizados. Às vezes, ocorre um conflito de versão ou uma versão do pacote foi preterida. Veja algumas dicas rápidas para ajudá-lo a configurar seu arquivo [package.json](https://docs.npmjs.com/files/package.json) e entender o que está acontecendo quando você vê erros ou avisos. Este não é um guia completo de *package.json* e seu foco é apenas o controle de versão do pacote npm.

O sistema de controle de versão do pacote npm tem regras rígidas. O formato da versão é o seguinte:

    [major].[minor].[patch]

Digamos que você tenha um pacote em seu aplicativo com a versão 5.2.1. A versão principal é 5, a versão secundária é 2 e o patch é 1.

* Em uma atualização de versão principal, o pacote inclui novas funcionalidades que são incompatíveis com versões anteriores, ou seja, alterações de falha.
* Em uma atualização de versão secundária, foram adicionados ao pacote novas funcionalidades que são compatíveis com versões anteriores dele.
* Em uma atualização de patch, uma ou mais correções de bug são incluídas. Correções de bug sempre são compatíveis com versões anteriores.

Vale a pena observar que algumas funcionalidades de pacote npm têm dependências. Por exemplo, para usar um novo recurso do pacote do compilador de TypeScript (ts-loader) com webpack, é possível que você também precise atualizar o pacote npm do webpack e o pacote webpack-cli.

Para ajudar a gerenciar o controle de versão do pacote, o npm dá suporte a várias notações que você pode usar em *package.json*. Você pode usar essas notações para controlar o tipo de atualizações de pacote que deseja aceitar em seu aplicativo.

Digamos que você esteja usando o React e precise incluir os pacotes npm **react** e **react-dom**. Você pode especificar isso de várias maneiras em seu arquivo *package.json*. Por exemplo, você pode especificar o uso de uma versão exata de um pacote da seguinte forma.

  ```json
  "dependencies": {
    "react": "16.4.2",
    "react-dom": "16.4.2",
  },
  ```

Usando a notação anterior, o npm sempre obterá a versão exata especificada, 16.4.2.

Você pode usar uma notação especial para limitar as atualizações a atualizações de patch (correções de bug). Neste exemplo:

  ```json
  "dependencies": {
    "react": "~16.4.2",
    "react-dom": "~16.4.2",
  },
  ```

você pode usar o caractere til (~) para instruir o npm a atualizar um pacote somente quando ele for corrigido. Portanto, o npm pode atualizar o react 16.4.2 para 16.4.3 (ou 16.4.4, etc.), mas não aceitará uma atualização da versão principal ou secundária. Portanto, 16.4.2 não será atualizado para 16.5.0.

Você também pode usar o símbolo de acento circunflexo (^) para especificar que o npm pode atualizar o número de versão secundária.

  ```json
  "dependencies": {
    "react": "^16.4.2",
    "react-dom": "^16.4.2",
  },
  ```

Usando essa notação, o npm pode atualizar o react 16.4.2 para 16.5.0 (ou 16.5.1, 16.6.0, etc.), mas não aceitará uma atualização da versão principal. Portanto, 16.4.2 não será atualizado para 17.0.0.

Quando o npm atualiza pacotes, ele gera um arquivo *package-lock.json*, que lista as versões reais do pacote npm usadas em seu aplicativo, incluindo todos os pacotes aninhados. Embora *package.json* controle as dependências diretas de seu aplicativo, ele não controla dependências aninhadas (outros pacotes npm exigidos por um pacote npm específico). Você poderá usar o arquivo *package-lock.json* em seu ciclo de desenvolvimento se precisar garantir que outros desenvolvedores e testadores estejam usando os pacotes exatos que você está usando, incluindo pacotes aninhados. Para obter mais informações, confira [package-lock.json](https://docs.npmjs.com/files/package-lock.json) na documentação do npm.

Para o Visual Studio, o arquivo *package-lock.json* não é adicionado ao seu projeto, mas você pode encontrá-lo na pasta do projeto.
