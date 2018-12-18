---
title: Configurando um Repositório do Subversion
description: Usando o Subversion no Visual Studio para Mac.
author: conceptdev
ms.author: crdun
ms.date: 05/06/2018
ms.assetid: 0D58FB37-530E-495B-BED6-FD499477A9B6
ms.openlocfilehash: 3995db4ef4609f68512dede454855da1f770141f
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295547"
---
# <a name="set-up-a-subversion-repository"></a>Configurar um repositório do Subversion

O Subversion é um _sistema de controle de versão_ centralizado, o que significa que há um único servidor que contém todos os arquivos e as revisões do qual os usuários podem fazer check-out de qualquer versão de qualquer arquivo. Ao fazer check-out de arquivos de um repositório Subversion remoto, o usuário receberá um instantâneo do repositório no momento em questão.

Para usar o Subversion no controle de versão, ele precisa estar instalado no computador. Para verificar se o Subversion está instalado no computador, use o seguinte comando no Terminal:

```bash
svn --version
```

Esse comando retorna o número de versão.

Se o Subversion ainda não está instalado, a maneira mais fácil de obtê-lo é instalar as _Ferramentas de Linha de Comando do Xcode_. Use o comando a seguir para instalar as Ferramentas de Linha de Comando do Xcode e o Subversion.

```bash
xcode-select --install
```

Após instalar o Subversion no computador, siga as etapas a seguir para publicar seu projeto no SVN.

1. Crie um repositório SVN online gratuito. Neste exemplo, [Assembla](https://app.assembla.com/) foi usado. Depois de criado, uma URL será fornecida, que será usada para se conectar ao repositório:

    ![copie a URL do SVN](media/version-control-subversion1-sml.png)

2. Abra ou crie um Projeto do Visual Studio para Mac.

3. Clique com o botão direito do mouse no Projeto e selecione **Controle de versão > Publicar no Controle de versão...**:

    ![Iniciar a publicação do projeto](media/version-control-subversion2.png)

4. Na guia **Conectar-se ao repositório**, selecione **Subversion** na lista suspensa superior.

5. Insira a URL da etapa 1. Após a inserção da URL, os outros campos serão preenchidos por padrão:

    ![Selecione o Repositório e a caixa de diálogo Insira os detalhes](media/version-control-subversion3.png)

7. Clique em **OK** e confirme pressionando **Publicar**.

7. Se solicitado, insira suas credenciais para o site no qual você está criando o repositório, conforme a ilustração abaixo:

    ![Inserir as credenciais do repositório do Subversion](media/version-control-subversion5.png)

8.  Todos os comandos de controle de versão disponíveis agora devem estar visíveis no menu de controle de versão.

## <a name="see-also"></a>Consulte também

- [Trabalhando com o Subversion](working-with-subversion.md)