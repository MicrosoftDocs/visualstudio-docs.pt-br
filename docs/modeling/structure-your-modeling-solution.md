---
title: Estruturar a solução de modelagem
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cc4eba7dc4d185cbd8eb4f1b073fce8b0c9fb07e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545035"
---
# <a name="structure-your-modeling-solution"></a>Estruturar a solução de modelagem

Para usar modelos com eficiência em um projeto de desenvolvimento, os integrantes da equipe devem ser capazes de trabalhar em modelos de partes diferentes do projeto ao mesmo tempo. Este tópico sugere um esquema para dividir o aplicativo em diferentes partes que correspondem às camadas em um diagrama de camadas geral.

Para iniciar em um projeto ou subprojeto rapidamente, é útil ter um modelo de projeto que segue a estrutura do projeto que você escolheu. Este tópico descreve como criar e usar um modelo desse tipo.

Este tópico pressupõe que você está trabalhando em um projeto que é grande o suficiente para exigir vários membros da equipe e talvez tenha várias equipes. O código e os modelos do projeto são armazenados em um sistema de controle do código-fonte, como [!INCLUDE[esprtfs](../code-quality/includes/esprtfs_md.md)] . Pelo menos alguns membros da equipe usam o Visual Studio para desenvolver modelos e outros membros da equipe podem exibir os modelos usando outras versões do Visual Studio.

Para ver quais versões do Visual Studio dão suporte a cada ferramenta e recurso de modelagem, consulte [suporte de versão para ferramentas de arquitetura e modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

## <a name="solution-structure"></a>Estrutura da solução

Em um projeto médio ou grande, a estrutura da equipe é baseada na estrutura do aplicativo. Cada equipe usa uma solução do Visual Studio.

### <a name="to-divide-an-application-into-layers"></a>Para dividir um aplicativo em camadas

1. Baseie a estrutura de suas soluções na estrutura do seu aplicativo, como aplicativo Web, aplicativo de serviço ou aplicativo de área de trabalho. Uma variedade de arquiteturas comuns é discutida em [arquétipos de aplicativo no guia de arquitetura de aplicativos da Microsoft](/previous-versions/msp-n-p/ee658107(v=pandp.10)).

2. Crie uma solução do Visual Studio, que chamaremos de solução de arquitetura. Essa solução será usada para criar o design geral do sistema. Ele conterá modelos, mas sem código.

   Adicione um diagrama de dependência a essa solução. No diagrama de dependência, desenhe a arquitetura que você escolheu para seu aplicativo. Por exemplo, o diagrama pode mostrar essas camadas e as dependências entre elas: apresentação; Lógica de negócios; e dados.

4. Crie uma solução do Visual Studio separada para cada camada no diagrama de dependência da arquitetura.

   Essas soluções serão usadas para desenvolver o código das camadas.

5. Crie modelos que representam os designs das camadas e os conceitos que são comuns a todas as camadas. Organize os modelos para que todos os modelos possam ser vistos na solução de arquitetura e os modelos relevantes possam ser vistos em cada camada.

   Você pode conseguir isso usando qualquer um dos procedimentos a seguir. A primeira alternativa cria um projeto de modelagem separado para cada camada, e a segunda cria um único projeto de modelagem que é compartilhado entre as camadas.

#### <a name="use-a-separate-modeling-project-for-each-layer"></a>Usar um projeto de modelagem separado para cada camada

1. Crie um projeto de modelagem em cada solução de camada.

   Esse modelo conterá diagramas que descrevem os requisitos e o design dessa camada. Ele também pode conter diagramas de dependência que mostram camadas aninhadas.

   Agora você tem um modelo para cada camada, além de um modelo para a arquitetura do aplicativo. Cada modelo está contido em sua própria solução. Isso permite que os membros da equipe trabalhem nas camadas ao mesmo tempo.

2. Para a solução de arquitetura, adicione o projeto de modelagem de cada solução de camada. Para fazer isso, abra a solução de arquitetura. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nó da solução, aponte para adicionar e clique em **projeto existente**. Navegue até o projeto de modelagem (. modelproj) em uma solução de camada.

   Cada modelo agora é visível em duas soluções: sua solução "inicial" e a solução de arquitetura.

3. Para o projeto de modelagem de cada camada, adicione um diagrama de dependência. Comece com uma cópia do diagrama de dependência da arquitetura. Você pode excluir partes que não são dependências do diagrama de dependência.

   Você também pode adicionar diagramas de dependência que representam a estrutura detalhada dessa camada.

   Esses diagramas são usados para validar o código que é desenvolvido nessa camada.

4. Na solução arquitetura, edite os requisitos e modelos de design de todas as camadas usando o Visual Studio.

   Em cada solução de camada, desenvolva o código para essa camada, referindo-se ao modelo. Se você for conteúdo para fazer o desenvolvimento sem usar o mesmo computador para atualizar o modelo, poderá ler o modelo e desenvolver o código usando versões do Visual Studio que não podem criar modelos. Você também pode gerar código do modelo nessas versões.

   Esse método garante que nenhuma interferência será causada por desenvolvedores que editem os modelos de camada ao mesmo tempo.

   No entanto, como os modelos são separados, é difícil se referir a conceitos comuns. Cada modelo deve ter sua própria cópia dos elementos nos quais ele depende de outras camadas e da arquitetura. O diagrama de dependência em cada camada deve ser mantido em sincronia com o diagrama de dependência da arquitetura. É difícil manter a sincronização quando esses elementos são alterados, embora você possa desenvolver ferramentas para fazer isso.

#### <a name="use-a-separate-package-for-each-layer"></a>Usar um pacote separado para cada camada

1. Na solução para cada camada, adicione o projeto de modelagem de arquitetura. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nó da solução, aponte para **Adicionar**e clique em **projeto existente**. O único projeto de modelagem agora pode ser acessado a partir de cada solução: o projeto de arquitetura e o projeto de desenvolvimento para cada camada.

2. No modelo compartilhado, crie um pacote para cada camada: em **Gerenciador de soluções**, selecione o projeto de modelagem. No **Gerenciador de modelos UML**, clique com o botão direito do mouse no nó raiz do modelo, aponte para **Adicionar**e clique em **pacote**.

   Cada pacote conterá diagramas que descrevem os requisitos e o design da camada correspondente.

3. Se necessário, adicione diagramas de dependência local para a estrutura interna de cada camada.

   Esse método permite que os elementos de design de cada camada façam referência direta às camadas e à arquitetura comum da qual ela depende.

   Embora o trabalho simultâneo em pacotes diferentes possa causar alguns conflitos, eles são razoavelmente fáceis de gerenciar, pois os pacotes são armazenados em arquivos separados.

## <a name="create-architecture-templates"></a>Criar modelos de arquitetura

Na prática, você não cria todas as soluções do Visual Studio ao mesmo tempo, mas as adiciona à medida que o projeto progride. Você provavelmente também usará a mesma estrutura de solução em projetos futuros. Para ajudá-lo a criar novas soluções rapidamente, você pode criar um modelo de solução ou de projeto. Você pode capturar o modelo em uma extensão de integração do Visual Studio (VSIX) para que seja fácil de distribuir e instalar em outros computadores.

Por exemplo, se você usa com frequência as soluções que têm camadas de apresentação, de negócios e de dados, você pode configurar um modelo que criará novas soluções que tenham essa estrutura.

### <a name="to-create-a-solution-template"></a>Para criar um modelo de solução

1. [Baixe e instale o assistente de exportação de modelo](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.ExportTemplateWizard).

2. Crie a estrutura da solução que você deseja usar como ponto de partida para projetos futuros.

3. No menu **arquivo** , clique em **Exportar modelo como VSIX**.

   O **Assistente para exportar modelo como VSIX** é aberto.

4. Seguindo as instruções no assistente, selecione os projetos que você deseja incluir no modelo, forneça um nome e uma descrição para o modelo e especifique um local de saída.

## <a name="watch-a-video"></a>Assistir a um vídeo

[Organizar e gerenciar seus modelos](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-9-organizing-and-managing-your-models)

## <a name="see-also"></a>Consulte também

- [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)
- [Orientação de ferramentas de arquitetura do Visual Studio](../modeling/visual-studio-architecture-tooling-guidance.md)
