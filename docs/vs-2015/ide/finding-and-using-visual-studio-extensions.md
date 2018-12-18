---
title: Localizando e usando extensões | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.ExtensionManager
helpviewer_keywords:
- install extensions
- install packages
- managing extensions visual studio
ms.assetid: 4ca92d93-31b9-47ef-8109-4a429d9e2ca3
caps.latest.revision: 47
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 8de9a0394c72043bc54dd6fa0632d3ed3e6edfd5
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53062794"
---
# <a name="finding-and-using-visual-studio-extensions"></a>Encontrando e usando extensões do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As extensões do Visual Studio são pacotes de código executados dentro do Visual Studio e fornecem recursos novos ou aprimorados do Visual Studio. Você pode encontrar mais informações sobre extensões do Visual Studio aqui: [SDK do Visual Studio](../extensibility/visual-studio-sdk.md)

 É possível usar a caixa de diálogo **Extensões e Atualizações** para instalar as extensões e amostras do Visual Studio de sites e outros locais e habilitá-las, desabilitá-las, atualizá-las ou desinstalá-las. (**Ferramentas/Extensões e Atualizações** ou digite ou **Extensões** na janela **Início Rápido**). A caixa de diálogo também mostra atualizações para amostras e extensões instaladas. Também é possível baixar extensões de sites ou obtê-las de outros desenvolvedores.

> [!NOTE]
>  A partir do Visual Studio 2015, as extensões hospedadas na Galeria do Visual Studio serão atualizadas automaticamente.  É possível alterar essa configuração por meio da caixa de diálogo **Extensões e Atualizações**.  Consulte a seção **Atualizações automáticas de extensões** abaixo para obter detalhes.

## <a name="finding-visual-studio-extensions"></a>Localizando extensões do Visual Studio
 É possível instalar extensões da [Galeria do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=178891) ou da [Galeria de Amostras](http://go.microsoft.com/fwlink/?LinkId=245175) no site da Microsoft. As extensões podem ser controles, exemplos, modelos, ferramentas ou outros componentes que adicionam funcionalidades ao Visual Studio. O Visual Studio dá suporte a extensões no formato do pacote VSIX, o que inclui modelos de projeto, modelos de item, itens da **Caixa de Ferramentas**, componentes MEF (Managed Extension Framework) e VSPackages. Também é possível baixar e instalar extensões baseadas em MSI, mas a caixa de diálogo **Extensões e Atualizações** não pode habilitá-las nem desabilitá-las. A Galeria do Visual Studio contém extensões VSIX e MSI.

## <a name="installing-or-uninstalling-visual-studio-extensions"></a>Instalando ou desinstalando extensões do Visual Studio
 Em **Extensões e Atualizações**, localize a extensão que você deseja instalar. (Se você souber o nome ou parte do nome da extensão, será possível pesquisar na janela **Pesquisar na Galeria do Visual Studio**.) Clique em **Baixar**, em seguida, em **Instalar**. É necessário reiniciar o Visual Studio para carregar a extensão.

 Se você tentar instalar uma extensão que tenha dependências, o instalador verificará se elas já foram instaladas. Se elas não tiverem sido instaladas, a caixa de diálogo **Extensões e Atualizações** listará as dependências que devem ser instaladas para que seja possível instalar a extensão.

 Se desejar parar de usar uma extensão, você poderá desabilitá-la ou desinstalá-la. A desabilitação de uma extensão a mantém instalada, mas descarregada. É possível desabilitar somente extensões VSIX; as extensões que foram instaladas usando um MSI só podem ser desinstaladas. Localize a extensão e clique em **Desinstalar** ou **Desabilitar**. É necessário reiniciar o Visual Studio para descarregar uma extensão desabilitada.

## <a name="per-user-and-administrative-extensions"></a>Extensões administrativas e por usuário
 A maioria das extensões são extensões por usuário e são instaladas na pasta **%LocalAppData%\Microsoft\VisualStudio\\<Visual Studio version\>\Extensions\\** folder. Algumas extensões são extensões administrativas e são instaladas na **\<pasta de instalação do Visual Studio>\Common7\IDE\Extensions\\**.

 Para proteger seu sistema contra extensões que possam conter erros ou código mal-intencionado, é possível restringir que as extensões por usuário sejam carregadas somente quando o Visual Studio estiver em execução com permissões de usuário normal. Isso significa que as extensões por usuário são desabilitadas quando o Visual Studio é executado com permissões de usuário administrativo. Para fazer isso, vá para a página de opções **Extensões e Atualizações** (**Ferramentas/Opções**, **Ambiente**, **Extensões e Atualizações** ou simplesmente digite **Extensão** na janela **Início Rápido**). Desmarque a caixa de seleção **Carregar extensões por usuário ao executar como administrador** e reinicie o Visual Studio.

## <a name="automatic-extension-updates"></a>Atualizações automáticas de extensão
 As extensões por usuário são atualizadas automaticamente quando uma nova versão está disponível na Galeria do Visual Studio.  A nova versão da extensão é detectada e instalada na tela de fundo e na próxima reinicialização do Visual Studio, a nova versão da extensão será executada.

 Somente as extensões por usuário podem ser atualizadas automaticamente.  As extensões administrativas instaladas para todos os usuários não serão atualizadas e você ainda instalará manualmente as novas versões por meio do nó **Atualizações** da caixa de diálogo **Extensões e Atualizações**. É possível ver quais extensões serão atualizadas automaticamente no painel de detalhes da extensão da caixa de diálogo **Extensões e Atualizações**.

 Se você desejar desabilitar as atualizações automáticas, será possível desabilitar o recurso para todas as extensões ou somente para extensões específicas.

-   Para desabilitar as atualizações automáticas para todas as extensões, clique no link **Alterar as configurações de Extensões e Atualizações** na caixa de diálogo **Extensões e Atualizações** e desmarque **Atualizar extensões automaticamente**.

-   Para desabilitar as atualizações automáticas de uma extensão específica, desmarque a opção **Atualizar automaticamente essa extensão** no painel de detalhes da extensão do lado direito da caixa de diálogo **Extensões e Atualizações**.

> [!NOTE]
>  A partir do Visual Studio 2015 Atualização 2, é possível especificar (em **Ferramentas/Opções/Ambiente/Extensões e Atualizações**) se você deseja atualizações automáticas para extensões por usuário, todas as extensões do usuário ou ambas (a configuração padrão).

## <a name="sample-master-copies-and-working-copies"></a>Cópias mestras e cópias funcionais de amostras
 Quando você instala um exemplo online, a solução é armazenada em dois locais:

- Uma cópia funcional é armazenada no local especificado na caixa de diálogo **Novo Projeto**.

- Uma cópia mestra separada é armazenada em seu computador.

  É possível usar a caixa de diálogo **Extensões e Atualizações** para executar estas tarefas relacionadas a amostras:

- Listar as cópias mestras dos exemplos que você instalou.

- Desabilitar ou desinstalar a cópia mestra de um exemplo.

- Instale os Pacotes de Exemplos, que são coleções de exemplos que se relacionam a uma tecnologia ou um recurso.

- Instalar exemplos online individuais. (Também é possível fazer isso na caixa de diálogo **Novo Projeto**.)

- Exibir notificações de atualização quando as alterações do código-fonte são publicadas para exemplos instalados.

- Atualize a cópia mestra de uma amostra instalada quando houver uma notificação de atualização.

## <a name="installing-without-using-the-extensions-and-updates-dialog-box"></a>Instalando sem usar a caixa de diálogo Extensões e Atualizações
 As extensões que foram empacotadas em arquivos .vsix podem estar disponíveis em outros locais, e não na Galeria do Visual Studio. A caixa de diálogo **Extensões e Atualizações** não pode detectar esses arquivos, mas é possível instalar um arquivo .vsix clicando duas vezes no arquivo ou selecionando-o e pressionando a tecla ENTER. Depois disso, basta seguir as instruções. Depois que a extensão for instalada, será possível usar a caixa de diálogo **Extensões e Atualizações** para habilitá-la, desabilitá-la ou desinstalá-la.

## <a name="extension-types-not-supported-by-the-extensions-and-updates-dialog-box"></a>A caixa de diálogo Extensões e Atualizações não dá suporte aos tipos de extensão
 O Visual Studio continua dando suporte a extensões instaladas pelo MSI (Microsoft Installer), mas não por meio da caixa de diálogo **Extensões e Atualizações** sem modificação.

> [!TIP]
>  Se uma extensão baseada em MSI incluir um arquivo extension.vsixmanifest, a extensão será exibida na caixa de diálogo **Extensões e Atualizações**.
