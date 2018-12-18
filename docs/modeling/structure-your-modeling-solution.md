---
title: Estruturar a solução de modelagem
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 2c279da9aed4a11799004a38004f8b82dca65174
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50966707"
---
# <a name="structure-your-modeling-solution"></a>Estruturar a solução de modelagem

Para usar modelos com eficiência em um projeto de desenvolvimento, os membros da equipe devem ser capazes de trabalhar em modelos de diferentes partes do projeto ao mesmo tempo. Este tópico sugere um esquema para dividir o aplicativo em diferentes partes que correspondem às camadas do geral diagrama da disposição em camadas.

Para iniciar em um projeto ou subprojeto rapidamente, é útil ter um modelo de projeto que segue a estrutura do projeto que você escolheu. Este tópico descreve como criar e usar um modelo desse tipo.

Este tópico pressupõe que você está trabalhando em um projeto que seja grande o suficiente para exigir vários membros da equipe e talvez tenha várias equipes. O código e modelos do projeto são armazenados em um sistema de controle do código-fonte, como [!INCLUDE[esprtfs](../code-quality/includes/esprtfs_md.md)]. Pelo menos alguns membros da equipe usam o Visual Studio para desenvolver modelos e outros membros da equipe podem exibir os modelos por meio de outras versões do Visual Studio.

Para ver quais versões do Visual Studio dão suporte a cada recurso de modelagem e a ferramenta, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

## <a name="solution-structure"></a>Estrutura da solução

Em um projeto de médio ou grande, a estrutura da equipe com base na estrutura do aplicativo. Cada equipe usa uma solução do Visual Studio.

### <a name="to-divide-an-application-into-layers"></a>Para dividir um aplicativo em camadas

1. A estrutura de suas soluções de base na estrutura do seu aplicativo, como o aplicativo web, aplicativo de serviço ou aplicativo da área de trabalho. Uma variedade de arquiteturas comuns é discutida [arquétipos de aplicativo no guia de arquitetura de aplicativo do Microsoft](http://go.microsoft.com/fwlink/?LinkId=196681).

2. Crie uma solução do Visual Studio, que chamaremos a solução de arquitetura. Esta solução será usada para criar o design geral do sistema. Ele conterá os modelos, mas nenhum código.

   Adicione um diagrama de dependência para esta solução. No diagrama de dependência, desenhe a arquitetura que você escolheu para o seu aplicativo. Por exemplo, o diagrama pode mostrar essas camadas e as dependências entre eles: apresentação; Lógica de negócios; e os dados.

4. Crie uma solução do Visual Studio separada para cada camada no diagrama de dependência de arquitetura.

   Essas soluções serão usadas para desenvolver o código das camadas.

5. Crie modelos que representam os designs das camadas e os conceitos que são comuns a todas as camadas. Organize os modelos de modo que todos os modelos podem ser vistos da solução de arquitetura e os modelos relevantes podem ser vistos em cada camada.

   Você pode fazer isso usando qualquer um dos procedimentos a seguir. A primeira alternativa cria um projeto de modelagem separado para cada camada, e o segundo cria um projeto de modelagem única que é compartilhado entre as camadas.

#### <a name="use-a-separate-modeling-project-for-each-layer"></a>Usar um projeto de modelagem separado para cada camada

1. Crie um projeto de modelagem em cada solução de camada.

   Esse modelo contém diagramas que descrevem os requisitos e design dessa camada. Ele também pode conter os diagramas de dependência que mostram as camadas aninhadas.

   Agora você tem um modelo para cada camada, além de um modelo para a arquitetura do aplicativo. Cada modelo é contido em sua própria solução. Isso permite que os membros da equipe trabalhar nas camadas ao mesmo tempo.

2. Para a solução de arquitetura, adicione o projeto de modelagem de cada solução de camada. Para fazer isso, abra a solução de arquitetura. Na **Gerenciador de soluções**, clique com botão direito no nó da solução, aponte para adicionar e, em seguida, clique em **projeto existente**. Navegue até o projeto de modelagem (. modelproj) na solução de uma camada.

   Cada modelo agora está visível em duas soluções: sua solução de "home" e a solução de arquitetura.

3. Para o projeto de modelagem de cada camada, adicione um diagrama de dependência. Comece com uma cópia do diagrama da arquitetura de dependência. Você pode excluir as partes que não são as dependências do diagrama de dependência.

   Você também pode adicionar diagramas de dependência que representam a estrutura detalhada dessa camada.

   Esses diagramas são usados para validar o código que é desenvolvido nessa camada.

4. Na solução de arquitetura, edite os modelos de design de todas as camadas e os requisitos usando o Visual Studio.

   Em cada solução de camada, desenvolva o código para essa camada, referindo-se ao modelo. Se você for o conteúdo para fazer o desenvolvimento sem usar o mesmo computador para atualizar o modelo, você pode ler o modelo e desenvolver código usando versões do Visual Studio que não é possível criar modelos. Você também pode gerar o código do modelo nessas versões.

   Esse método garante que nenhum interferência será causada pelos desenvolvedores que editar os modelos de camada ao mesmo tempo.

   No entanto, como os modelos são separados, é difícil para se referir a conceitos comuns. Cada modelo deve ter sua própria cópia dos elementos no qual ele é dependente de outras camadas e a arquitetura. O diagrama de dependência em cada camada deve ser mantido em sincronia com o diagrama de dependência de arquitetura. É difícil de manter a sincronização quando alterar esses elementos, embora você possa desenvolver ferramentas para fazer isso.

#### <a name="use-a-separate-package-for-each-layer"></a>Usar um pacote separado para cada camada

1. Na solução para cada camada, adicione o projeto de modelagem de arquitetura. Na **Gerenciador de soluções**, clique com botão direito no nó da solução, aponte para **Add**e, em seguida, clique em **projeto existente**. O projeto de modelagem único agora pode ser acessado de cada solução: o projeto de arquitetura e o projeto de desenvolvimento para cada camada.

2. No modelo compartilhado, crie um pacote para cada camada: nos **Gerenciador de soluções**, selecione o projeto de modelagem. Na **Gerenciador de modelos UML**, clique com botão direito no nó de raiz do modelo, aponte para **Add**e, em seguida, clique em **pacote**.

   Cada pacote contém diagramas que descrevem os requisitos e design da camada correspondente.

3. Se for necessário, adicione diagramas de dependência de local para a estrutura interna de cada camada.

   Esse método permite que os elementos de design de cada camada para referir-se diretamente das camadas e a arquitetura comum dos quais ele depende.

   Embora o trabalho simultâneo em pacotes diferentes pode causar alguns conflitos, eles são muito fáceis de gerenciar porque os pacotes são armazenados em arquivos separados.

## <a name="create-architecture-templates"></a>Criar modelos de arquitetura

Na prática, você não cria todas as suas soluções do Visual Studio ao mesmo tempo, mas adicioná-las conforme o andamento do projeto. Você provavelmente também use a mesma estrutura de solução de projetos futuros. Para ajudar você a criar novas soluções rapidamente, você pode criar um modelo de solução ou projeto. Você pode capturar o modelo em um Visual Studio Integration VSIX (extensão) para que seja fácil de distribuir e instalar em outros computadores.

Por exemplo, se você frequentemente usa soluções que têm camadas de apresentação, negócios e dados, você pode configurar um modelo que irá criar novas soluções que têm essa estrutura.

### <a name="to-create-a-solution-template"></a>Para criar um modelo de solução

1. [Baixe e instale o Assistente para exportar modelo](http://go.microsoft.com/fwlink/?LinkId=196686).

2. Crie a estrutura da solução que você deseja usar como ponto de partida para projetos futuros.

3. Sobre o **arquivo** menu, clique em **Export Template como VSIX**.

   O **exportar modelo como o Assistente de VSIX** é aberta.

4. Seguindo as instruções no assistente, selecione os projetos que você deseja incluir no modelo, forneça um nome e descrição para o modelo e especifique um local de saída.

## <a name="watch-a-video"></a>Assista a um vídeo

[Organizar e gerenciar seus modelos](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-9-organizing-and-managing-your-models)

## <a name="see-also"></a>Consulte também

- [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)
- [Diretrizes de ferramentas de arquitetura do Visual Studio](../modeling/visual-studio-architecture-tooling-guidance.md)
