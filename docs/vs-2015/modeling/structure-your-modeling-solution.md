---
title: Estruturar a solução de modelagem | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2ba70ba4-2cea-4e01-93c2-055903d59470
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 995192b372b9c1909ad3a7f164474cfaf63f07bc
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51784449"
---
# <a name="structure-your-modeling-solution"></a>Estruturar a solução de modelagem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para usar modelos com eficiência em um projeto de desenvolvimento, os membros da equipe devem ser capazes de trabalhar em modelos de diferentes partes do projeto ao mesmo tempo. Este tópico sugere um esquema para dividir o aplicativo em diferentes partes que correspondem às camadas do geral diagrama da disposição em camadas.  
  
 Para iniciar em um projeto ou subprojeto rapidamente, é útil ter um modelo de projeto que segue a estrutura do projeto que você escolheu. Este tópico descreve como criar e usar um modelo desse tipo.  
  
 Este tópico pressupõe que você está trabalhando em um projeto que seja grande o suficiente para exigir vários membros da equipe e talvez tenha várias equipes. O código e modelos do projeto são armazenados em um sistema de controle do código-fonte, como [!INCLUDE[esprtfs](../includes/esprtfs-md.md)]. Pelo menos alguns membros da equipe usam o Visual Studio para desenvolver modelos e outros membros da equipe podem exibir os modelos por meio de outras versões do Visual Studio.  
  
 Para ver quais versões do Visual Studio dão suporte a cada recurso de modelagem e a ferramenta, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
## <a name="solution-structure"></a>Estrutura da solução  
 Em um projeto de médio ou grande, a estrutura da equipe com base na estrutura do aplicativo. Cada equipe usa uma solução do Visual Studio.  
  
#### <a name="to-divide-an-application-into-layers"></a>Para dividir um aplicativo em camadas  
  
1. A estrutura de suas soluções de base na estrutura do seu aplicativo, como o aplicativo web, aplicativo de serviço ou aplicativo da área de trabalho. Uma variedade de arquiteturas comuns é discutida [arquétipos de aplicativo no guia de arquitetura de aplicativo do Microsoft](http://go.microsoft.com/fwlink/?LinkId=196681).  
  
2. Criar um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solução, que chamaremos a solução de arquitetura. Esta solução será usada para criar o design geral do sistema. Ele conterá os modelos, mas nenhum código.  
  
    Adicione um diagrama de camada para essa solução. No diagrama de camada, desenhe a arquitetura que você escolheu para o seu aplicativo. Por exemplo, o diagrama pode mostrar essas camadas e as dependências entre eles: apresentação; Lógica de negócios; e os dados.  
  
    Você pode criar uma nova solução do Visual Studio e diagrama de camada ao mesmo tempo usando o **UML novo ou diagrama de camada** comando as **arquitetura** menu.  
  
3. Adicione para os diagramas UML de modelo de arquitetura que representam os conceitos de negócios importantes e casos de uso que são chamados no design de todas as camadas.  
  
4. Crie uma solução do Visual Studio separada para cada camada no diagrama da arquitetura de camada.  
  
    Essas soluções serão usadas para desenvolver o código das camadas.  
  
5. Crie modelos UML que representarão os designs das camadas e os conceitos que são comuns a todas as camadas. Organize os modelos de modo que todos os modelos podem ser vistos da solução de arquitetura e os modelos relevantes podem ser vistos em cada camada.  
  
    Você pode fazer isso usando qualquer um dos procedimentos a seguir. A primeira alternativa cria um projeto de modelagem separado para cada camada, e o segundo cria um projeto de modelagem única que é compartilhado entre as camadas.  
  
   ###### <a name="to-use-a-separate-modeling-project-for-each-layer"></a>Para usar um projeto de modelagem separado para cada camada  
  
   1. Crie um projeto de modelagem em cada solução de camada.  
  
       Esse modelo contém diagramas UML que descrevem os requisitos e design dessa camada. Ele também pode conter os diagramas de camada que mostram as camadas aninhadas.  
  
       Agora você tem um modelo para cada camada, além de um modelo para a arquitetura do aplicativo. Cada modelo é contido em sua própria solução. Isso permite que os membros da equipe trabalhar nas camadas ao mesmo tempo.  
  
   2. Para a solução de arquitetura, adicione o projeto de modelagem de cada solução de camada. Para fazer isso, abra a solução de arquitetura. No Gerenciador de soluções, clique com botão direito no nó da solução, aponte para adicionar e, em seguida, clique em **projeto existente**. Navegue até o projeto de modelagem (. modelproj) na solução de uma camada.  
  
       Cada modelo agora está visível em duas soluções: sua solução de "home" e a solução de arquitetura.  
  
   3. Para o projeto de modelagem de cada camada, adicione um diagrama de camada. Comece com uma cópia do diagrama da arquitetura de camada. Você pode excluir as partes que não são as dependências do diagrama de camada.  
  
       Você também pode adicionar diagramas de camada que representam a estrutura detalhada dessa camada.  
  
       Esses diagramas são usados para validar o código que é desenvolvido nessa camada.  
  
   4. Na solução de arquitetura, edite os modelos de design de todas as camadas e os requisitos usando o Visual Studio.  
  
       Em cada solução de camada, desenvolva o código para essa camada, referindo-se ao modelo. Se você for o conteúdo para fazer o desenvolvimento sem usar o mesmo computador para atualizar o modelo, você pode ler o modelo e desenvolver código usando versões do Visual Studio que não é possível criar modelos. Você também pode gerar o código do modelo nessas versões.  
  
      Esse método garante que nenhum interferência será causada pelos desenvolvedores que editar os modelos de camada ao mesmo tempo.  
  
      No entanto, como os modelos são separados, é difícil para se referir a conceitos comuns. Cada modelo deve ter sua própria cópia dos elementos no qual ele é dependente de outras camadas e a arquitetura. O diagrama de camada em cada camada deve ser mantido em sincronia com o diagrama de camada de arquitetura. É difícil de manter a sincronização quando alterar esses elementos, embora você possa desenvolver ferramentas para fazer isso.  
  
   ###### <a name="to-use-a-separate-package-for-each-layer"></a>Para usar um pacote separado para cada camada  
  
   1. Na solução para cada camada, adicione o projeto de modelagem de arquitetura. No Gerenciador de soluções, clique com botão direito no nó da solução, aponte para **Add**e, em seguida, clique em **projeto existente**. O projeto de modelagem único agora pode ser acessado de cada solução: o projeto de arquitetura e o projeto de desenvolvimento para cada camada.  
  
   2. No modelo de UML compartilhado, crie um pacote para cada camada: no Gerenciador de soluções, selecione o projeto de modelagem. No Gerenciador de modelos UML, clique com botão direito no nó de raiz do modelo, aponte para **Add**e, em seguida, clique em **pacote**.  
  
       Cada pacote conterá os diagramas UML que descrevem os requisitos e design da camada correspondente.  
  
   3. Se for necessário, adicione diagramas de camada de local para a estrutura interna de cada camada.  
  
      Esse método permite que os elementos de design de cada camada para referir-se diretamente das camadas e a arquitetura comum dos quais ele depende.  
  
      Embora o trabalho simultâneo em pacotes diferentes pode causar alguns conflitos, eles são muito fáceis de gerenciar porque os pacotes são armazenados em arquivos separados. A grande dificuldade é causada pela exclusão de um elemento que é referenciado em um pacote dependente. Para obter mais informações, consulte [gerenciar modelos e diagramas com controle de versão](../modeling/manage-models-and-diagrams-under-version-control.md).  
  
## <a name="creating-architecture-templates"></a>Criando modelos de arquitetura  
 Na prática, você não criará todas as suas soluções do Visual Studio ao mesmo tempo, mas adicioná-las conforme o andamento do projeto. Você provavelmente também use a mesma estrutura de solução de projetos futuros.  Para ajudar você a criar novas soluções rapidamente, você pode criar um modelo de solução ou projeto. Você pode capturar o modelo em um Visual Studio Integration VSIX (extensão) para que seja fácil de distribuir e instalar em outros computadores.  
  
 Por exemplo, se você frequentemente usa soluções que têm camadas de apresentação, negócios e dados, você pode configurar um modelo que irá criar novas soluções que têm essa estrutura.  
  
#### <a name="to-create-a-solution-template"></a>Para criar um modelo de solução  
  
1.  [Baixe e instale o Assistente para exportar modelo](http://go.microsoft.com/fwlink/?LinkId=196686), se você ainda não tiver feito isso.  
  
2.  Crie a estrutura da solução que você deseja usar como ponto de partida para projetos futuros.  
  
3.  Sobre o **arquivo** menu, clique em **Export Template como VSIX**. O **exportar modelo como o Assistente de VSIX** é aberta.  
  
4.  Seguindo as instruções no assistente, selecione os projetos que você deseja incluir no modelo, forneça um nome e descrição para o modelo e especifique um local de saída.  
  
> [!NOTE]
>  O material neste tópico é abstraído e traduzido do Visual Studio ferramentas diretrizes de arquitetura, escrito pelo Visual Studio ALM Rangers, que é uma colaboração entre Most Valued Professionals (MVPs), o Microsoft Services e o Visual Studio equipe do produto e gravadores. [Clique aqui para baixar o pacote de diretrizes completo.](http://go.microsoft.com/fwlink/?LinkID=191984)  
  
## <a name="related-materials"></a>Materiais relacionados  
 [Organizar e gerenciar seus modelos](http://channel9.msdn.com/posts/clinted/UML-with-VS-2010-Part-9-Organizing-and-Managing-Your-Models/) – vídeo por Clint Edmondson.  
  
 [Guia de ferramentas arquitetura do Visual Studio](../modeling/visual-studio-architecture-tooling-guidance.md) – ainda mais orientações sobre gerenciamento de modelos em uma equipe  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar modelos e diagramas com controle de versão](../modeling/manage-models-and-diagrams-under-version-control.md)   
 [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)



