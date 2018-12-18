---
title: Perguntas Frequentes sobre as Ferramentas do R para Visual Studio
description: Perguntas frequentes sobre R no Visual Studio.
ms.date: 12/04/2017
ms.prod: visual-studio-dev15
ms.technology: vs-rtvs
ms.topic: reference
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- data-science
ms.openlocfilehash: 832d581a4147b8b050da16b1a1f72d8a3909fc35
ms.sourcegitcommit: f685fa5e2df9dc307bf1230dd9dc3288aaa408b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36235176"
---
# <a name="frequently-asked-questions"></a>Perguntas frequentes

## <a name="visual-studio-support"></a>Suporte a Visual Studio

**P. As RTVS funciona no OS X ou no Linux?**

R. Atualmente, as RTVS se baseiam no Visual Studio, que é uma implementação somente do Windows. A Microsoft está analisando o suporte no Visual Studio Code e no Visual Studio para Mac. Consulte a [edição nº 1295 do RTVS](https://github.com/Microsoft/RTVS/issues/1295).

**P. As RTVS funcionam com edições do Visual Studio Express?**

R. Nº

**P. Posso usar extensões do Visual Studio com as RTVS?**

R. Com certeza. Na verdade, aqui estão algumas opções que são comuns para pessoas que trabalham com o R.

- [VsVim para associações de chave vim](https://marketplace.visualstudio.com/items?itemName=JaredParMSFT.VsVim)
- [GitHub](https://marketplace.visualstudio.com/items?itemName=GitHub.GitHubExtensionforVisualStudio)
- [Editor de markdown com visualização em tempo real](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.MarkdownEditor)

Veja o [Visual Studio Marketplace](https://marketplace.visualstudio.com/) para saber mais.

**P. Como as RTVS estão no Visual Studio, isso significa que o R pode ser facilmente usado com o C#, C++ e outras linguagens da Microsoft?**

R. Nº As RTVS são uma ferramenta para desenvolver código R e usa os intérpretes nativos de R padrão. Atualmente, não há suporte para interoperabilidade entre o R e outras linguagens.

**P. O RTVS funciona com uma localidade diferente do inglês?**

R. A versão 1.0 do RTVS será somente em inglês. A versão 1.1 será localizado para o mesmo conjunto de idiomas do Visual Studio. Enquanto isso, use o [Pacote do idioma inglês para o Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=48157) ou, no Visual Studio 2017, execute o instalador e selecione inglês na guia **Pacotes de idiomas**.

![Configurações internacionais do Visual Studio 2017](media/FAQ-international-settings.png)

**P. Eu gosto muito das minhas configurações atuais do Visual Studio, mas desejo testar as novas configurações de Ciência de Dados. O que devo fazer?**

R. Salve suas configurações atuais do Visual Studio usando **Ferramentas** > **Importar e Exportar Configurações** e, em seguida, mude para as configurações da Ciência de Dados. Para restaurar as configurações salvas, use o comando **Importar e Exportar Configurações** novamente.

**P. Posso armazenar meu projeto do Visual Studio em um compartilhamento de rede?**

R. Não, o Visual Studio não dá suporte ao carregamento de projetos de um compartilhamento de rede.

## <a name="r-interpretersintegration"></a>Interpretadores/integração do R

**P. Com quais intérpretes do R as RTVS funcionam?**

R. [CRAN R](https://cran.r-project.org/), [Microsoft R Client e Microsoft Machine Learning Server](/machine-learning-server/)

**P. Onde posso baixar esses intérpretes?**

R. Veja [Instalação](installing-r-tools-for-visual-studio.md).

P. **O que é o Microsoft R Server?**

R. R Server é o antigo nome do [Microsoft Machine Learning Server](/machine-learning-server/what-is-machine-learning-server).

**P. As RTVS funcionarão com as edições de 32 bits do R?**

R. Não, as RTVS só dão suporte às edições de 64 bits do R em execução em edições de 64 bits do Windows.

**P. As RTVS funcionam com meu sistema de controle do código-fonte?**

R. Sim, você pode usar qualquer sistema de controle do código-fonte que esteja integrado ao Visual Studio.

**P. Quais são as configurações de *.gitignore* recomendadas para um projeto das RTVS?**

R. O GitHub mantém um repositório mestre de arquivos *.gitignore* recomendados. Você pode vê-lo aqui: [.gitignore do R](https://github.com/github/gitignore/blob/master/R.gitignore)

## <a name="remote-services"></a>Serviços remotos

P. **O que são os Serviços Remotos no Visual Studio?**

R. Os Serviços Remotos do R para Visual Studio permitem configurar um computador Windows ou Linux e, em seguida, conectar-se a ele por meio do RTVS. Veja [Configurar espaços de trabalho remotos](setting-up-remote-r-workspaces.md).

P. **As RTVS podem se conectar ao Microsoft Machine Learning Server?**

R. Não, porque o Microsoft ML Server é uma tecnologia diferente e não fornece o mesmo mecanismo de conectividade que as RTVS exigem.

P. **O RTVS pode se conectar a uma VM criada usando a imagem de VM de ciência de dados no Azure?**

R. Sim, a imagem [VM de ciência de dados – Windows 2016](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/) vem pré-instalada com os Serviços R Remotos para Visual Studio.

P. **O RTVS pode se conectar a um computador remoto com R instalado?**

Para executar código R em um computador remoto, deve haver algum serviço de escuta para as solicitações, recebendo o código e enviando os resultados de volta para o computador cliente. É isto que os Serviços Remotos do R para Visual Studio fazem. Veja [Configurar espaços de trabalho remotos](setting-up-remote-r-workspaces.md).

P. **O que é a sessão remota?**

R. Consulte o artigo [Executar no servidor remoto](/machine-learning-server/r/how-to-execute-code-remotely) na documentação do Machine Learning Server.

## <a name="rtvs-development-and-features"></a>Recursos e desenvolvimento do RTVS

**P. O recurso X está ausente, mas o RStudio o tem!**

R. O RStudio é um IDE fantástico e maduro para R que vem sendo desenvolvido há vários anos. As RTVS procuram ter todos os recursos mais importantes que você precisa para ser bem-sucedido. Ajude a priorizar futuros trabalhos participando da [Pesquisa de RTVS](https://www.surveymonkey.com/r/RTVS1) e problemas de arquivo no [GitHub](https://github.com/Microsoft/RTVS/issues/).

**P. Posso contribuir para RTVS?**

R. Claro! O código-fonte reside no [Github](https://github.com/microsoft/RTVS). Use o rastreador de problemas para enviar bugs e comentar sobre aqueles já arquivados.

Você também pode contribuir com esta documentação &mdash; basta selecionar o comando **Editar** no canto superior direito de qualquer página. Os comentários sobre os documentos também são bem-vindos, os quais você pode adicionar à parte inferior de qualquer página.
