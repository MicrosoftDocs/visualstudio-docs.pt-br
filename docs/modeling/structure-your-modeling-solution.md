---
title: Estruturar a solução de modelagem
description: Aprenda um esquema de modelagem para dividir o aplicativo em partes diferentes que correspondem às camadas em um diagrama de camadas geral.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 54275c55d3d7a80dc2df1721585bc6c39ba8b06e
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385481"
---
# <a name="structure-your-modeling-solution"></a>Estruturar a solução de modelagem

Para usar modelos efetivamente em um projeto de desenvolvimento, os membros da equipe devem ser capazes de trabalhar em modelos de diferentes partes do projeto ao mesmo tempo. Este tópico sugere um esquema para dividir o aplicativo em partes diferentes que correspondem às camadas em um diagrama de camadas geral.

Para começar rapidamente em um projeto ou subprojeto, é útil ter um modelo de projeto que siga a estrutura do projeto que você escolheu. Este tópico descreve como criar e usar esse modelo.

Este tópico pressu que você está trabalhando em um projeto grande o suficiente para exigir vários membros da equipe e talvez tenha várias equipes. O código e os modelos do projeto são armazenados em um sistema de controle do código-fonte, como [!INCLUDE[esprtfs](../code-quality/includes/esprtfs_md.md)] . Pelo menos alguns membros da equipe usam Visual Studio para desenvolver modelos e outros membros da equipe podem exibir os modelos usando outras Visual Studio versões.

Para ver quais versões do Visual Studio suporte a cada ferramenta e recurso de modelagem, consulte Suporte de versão para ferramentas de [arquitetura e modelagem](../modeling/analyze-and-model-your-architecture.md#VersionSupport).

## <a name="solution-structure"></a>Estrutura da solução

Em um projeto médio ou grande, a estrutura da equipe é baseada na estrutura do aplicativo. Cada equipe usa uma Visual Studio solução.

### <a name="to-divide-an-application-into-layers"></a>Para dividir um aplicativo em camadas

1. Basear a estrutura de suas soluções na estrutura do aplicativo, como aplicativo Web, aplicativo de serviço ou aplicativo da área de trabalho. Uma variedade de arquiteturas comuns é discutida em [Arquétipos de Aplicativo no Guia de Arquitetura de Aplicativos da Microsoft.](/previous-versions/msp-n-p/ee658107(v=pandp.10))

2. Crie uma Visual Studio, que chamaremos de solução de arquitetura. Essa solução será usada para criar o design geral do sistema. Ele conterá modelos, mas nenhum código.

   Adicione um diagrama de dependência a essa solução. No diagrama de dependência, desenhe a arquitetura que você escolheu para seu aplicativo. Por exemplo, o diagrama pode mostrar essas camadas e as dependências entre elas: Apresentação; Lógica de negócios; e Dados.

4. Crie uma solução Visual Studio separada para cada camada no diagrama de dependência da arquitetura.

   Essas soluções serão usadas para desenvolver o código das camadas.

5. Crie modelos que representam os designs das camadas e os conceitos que são comuns a todas as camadas. Organize os modelos para que todos os modelos possam ser vistos na solução arquitetura e os modelos relevantes possam ser vistos de cada camada.

   Você pode fazer isso usando qualquer um dos procedimentos a seguir. A primeira alternativa cria um projeto de modelagem separado para cada camada e a segunda cria um único projeto de modelagem compartilhado entre as camadas.

#### <a name="use-a-separate-modeling-project-for-each-layer"></a>Usar um projeto de modelagem separado para cada camada

1. Crie um projeto de modelagem em cada solução de camada.

   Esse modelo conterá diagramas que descrevem os requisitos e o design dessa camada. Ele também pode conter diagramas de dependência que mostram camadas aninhadas.

   Agora você tem um modelo para cada camada, além de um modelo para a arquitetura do aplicativo. Cada modelo está contido em sua própria solução. Isso permite que os membros da equipe trabalhem nas camadas ao mesmo tempo.

2. Para a solução arquitetura, adicione o projeto de modelagem de cada solução de camada. Para fazer isso, abra a solução Arquitetura. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó da solução, aponte para Adicionare clique **em Projeto Existente**. Navegue até o projeto de modelagem (.modelproj) em uma solução de camada.

   Cada modelo agora está visível em duas soluções: sua solução "home" e a solução arquitetura.

3. Ao projeto de modelagem de cada camada, adicione um diagrama de dependência. Comece com uma cópia do diagrama de dependência arquitetura. Você pode excluir partes que não são dependências do diagrama de dependência.

   Você também pode adicionar diagramas de dependência que representam a estrutura detalhada dessa camada.

   Esses diagramas são usados para validar o código desenvolvido nessa camada.

4. Na solução Arquitetura, edite os requisitos e os modelos de design de todas as camadas usando Visual Studio.

   Em cada solução de camada, desenvolva o código para essa camada, fazendo referência ao modelo. Se você estiver conteúdo para fazer o desenvolvimento sem usar o mesmo computador para atualizar o modelo, poderá ler o modelo e desenvolver código usando versões do Visual Studio que não podem criar modelos. Você também pode gerar código do modelo nessas versões.

   Esse método garante que nenhuma interferência será causada por desenvolvedores que editam os modelos de camada ao mesmo tempo.

   No entanto, como os modelos são separados, é difícil se referir a conceitos comuns. Cada modelo deve ter sua própria cópia dos elementos dos quais depende de outras camadas e da arquitetura. O diagrama de dependência em cada camada deve ser mantido em sincronia com o diagrama de dependência arquitetura. É difícil manter a sincronização quando esses elementos mudam, embora você possa desenvolver ferramentas para fazer isso.

#### <a name="use-a-separate-package-for-each-layer"></a>Usar um pacote separado para cada camada

1. Na solução para cada camada, adicione o projeto modelagem de arquitetura. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó da solução, aponte para Adicionar e clique **em Projeto Existente**. O único projeto de modelagem agora pode ser acessado de cada solução: o projeto de arquitetura e o projeto de desenvolvimento para cada camada.

2. No modelo compartilhado, crie um pacote para cada camada: **no Gerenciador de Soluções**, selecione o projeto de modelagem. No **Explorador de Modelos UML,** clique com o botão direito do mouse no nó raiz do modelo, aponte para **Adicionar** e clique em **Pacote**.

   Cada pacote conterá diagramas que descrevem os requisitos e o design da camada correspondente.

3. Se necessário, adicione diagramas de dependência local para a estrutura interna de cada camada.

   Esse método permite que os elementos de design de cada camada se refiram diretamente àqueles das camadas e da arquitetura comum da qual ela depende.

   Embora o trabalho simultâneo em pacotes diferentes possa causar alguns conflitos, eles são bastante fáceis de gerenciar porque os pacotes são armazenados em arquivos separados.

## <a name="create-architecture-templates"></a>Criar modelos de arquitetura

Na prática, você não cria todas as suas soluções Visual Studio ao mesmo tempo, mas as adiciona à medida que o projeto progride. Provavelmente, você também usará a mesma estrutura de solução em projetos futuros. Para ajudá-lo a criar novas soluções rapidamente, você pode criar uma solução ou modelo de projeto. Você pode capturar o modelo em um VSIX (Visual Studio Integration Extension) para que seja fácil distribuir e instalar em outros computadores.

Por exemplo, se você usar frequentemente soluções que têm camadas de Apresentação, Negócios e Dados, poderá configurar um modelo que criará novas soluções que têm essa estrutura.

### <a name="to-create-a-solution-template"></a>Para criar um modelo de solução

1. [Baixe e instale o Assistente para Exportar Modelo.](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.ExportTemplateWizard)

2. Crie a estrutura de solução que você deseja usar como ponto de partida para projetos futuros.

3. No menu **Arquivo,** clique em **Exportar Modelo como VSIX.**

   O **Assistente para Exportar Modelo como VSIX é** aberto.

4. Seguindo as instruções no assistente, selecione os projetos que você deseja incluir no modelo, forneça um nome e uma descrição para o modelo e especifique um local de saída.

## <a name="watch-a-video"></a>Assistir a um vídeo

[Organizar e gerenciar seus modelos](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-9-organizing-and-managing-your-models)

## <a name="see-also"></a>Confira também

- [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)
