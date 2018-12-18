---
title: Gerenciar pacotes npm
description: O Visual Studio ajuda você a gerenciar pacotes usando o npm (gerenciador de pacotes do Node.js)
ms.custom: seodec18
ms.date: 06/06/2018
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
ms.openlocfilehash: 297bad186c7f3412e56a5a59f65b82ab9cd35a03
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53049646"
---
# <a name="manage-npm-packages-in-visual-studio"></a>Gerenciar pacotes de npm no Visual Studio

O npm permite que você instale e gerencie pacotes a serem usados em seus aplicativos Node.js. Se você não conhece o npm e quer saber mais, acesse a [documentação do npm](https://docs.npmjs.com/).

O Visual Studio facilita a interação com o npm e emite comandos do npm diretamente ou por meio da interface do usuário. Você pode usar um dos seguintes métodos:
* [Instalar os pacotes usando o Gerenciador de Soluções](#npmInstallWindow)
* [Gerenciar pacotes instalados usando o Gerenciador de Soluções](#solutionExplorer)
* [Usar o comando `.npm` na janela interativa do Node.js](#interactive)

Esses recursos funcionam juntos e são sincronizados com o sistema de projeto e o arquivo *package.json* no projeto.

## <a name="npmInstallWindow"></a> Instalar os pacotes usando o Gerenciador de Soluções

A maneira mais fácil de instalar pacotes npm é por meio da janela de instalação de pacote do npm. Para acessar essa janela, clique com o botão direito do mouse no nó do **npm** no projeto e selecione **Instalar Novos Pacotes do npm**.

![Instalar o novo pacote do npm usando o Gerenciador de Soluções](../javascript/media/solution-explorer-install-package.png)

Nessa janela, você pode procurar por um pacote, especificar as opções e instalar. 

![Pesquisar pacote do npm](../javascript/media/search-package.png)

* **Tipo de dependência** – escolha entre os pacotes **Padrão**, **Desenvolvimento** e **Opcional**. Padrão especifica que o pacote é uma dependência de tempo de execução, enquanto Desenvolvimento especifica que o pacote só é necessário durante o desenvolvimento.
* **Adicionar ao package.json** – essa opção foi preterida
* **Versão selecionada** – selecione a versão do pacote que você deseja instalar.
* **Outros argumentos do npm** – especifique outros argumentos padrão do npm. Por exemplo, você pode inserir um valor de versão como `@~0.8` para instalar uma versão específica que não está disponível na lista de versões.

Veja o progresso da instalação na guia de npm na Janela de Saída. Isso pode levar algum tempo.

> [!TIP]
> É possível pesquisar pacotes com escopo acrescentando a consulta de pesquisa com o escopo desejado, por exemplo, digite `@types/mocha` para procurar por arquivos de definição de TypeScript para moca. Além disso, ao instalar as definições de tipo para o TypeScript, você pode especificar a versão do TypeScript para a qual está direcionando adicionando `@ts2.6` no campo de argumento do npm.

## <a name="solutionExplorer"></a>Gerenciar pacotes instalados no Gerenciador de Soluções

Os pacotes do npm são mostrados no Gerenciador de Soluções. As entradas no nó **npm** imitam as dependências do arquivo *package.json*.

![Pesquisar pacote do npm](../javascript/media/solution-explorer-status.png)

### <a name="package-status"></a>Status do pacote
* ![Pacote instalado](../javascript/media/installed-npm.png) – Instalado e listado no package.json
* ![Pacote desconhecido](../javascript/media/extraneous-npm.png) – instalado, mas não listado explicitamente no package.json
* ![Pacote ausente](../javascript/media/missing-npm.png) – Não instalado, mas listado no package.json

Clique com o botão direito do mouse em um nó de pacote ou no nó do **npm** para executar uma das seguintes ações:
* **Instalar pacotes ausentes** listados em *package.json*
* **Atualizar pacotes** para a versão mais recente
* **Desinstalar um pacote** e remover do *package.json*

## <a name="interactive"></a>Use o comando .npm na janela interativa do Node.js

Você também pode usar o comando `.npm` na janela interativa do Node.js para executar comandos do npm. Para abrir a janela, clique com o botão direito do mouse no projeto no Gerenciador de Soluções e escolha **Abrir Janela Interativa do Node.js**.

Na janela, você pode usar comandos como o seguinte para instalar um pacote:

`.npm install azure@4.2.3`
 
 > [!Tip]
 > Por padrão, o npm será executado no diretório inicial do projeto. Se houver vários projetos na solução, especifique o nome ou o caminho do projeto entre colchetes. 
 > `.npm [MyProjectNameOrPath] install azure@4.2.3`

 > [!Tip]
 > Se seu projeto não contiver um arquivo package.json, use `.npm init -y` para criar um novo arquivo package.json com as entradas padrão. 