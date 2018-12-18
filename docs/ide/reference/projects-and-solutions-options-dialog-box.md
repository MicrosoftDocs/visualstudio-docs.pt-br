---
title: Soluções e Projetos, caixa de diálogo Opções
ms.date: 07/14/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Projects.General
- VS.ToolsOptionsPages.Projects.Locations
helpviewer_keywords:
- Projects and Solutions Options dialog box
- Options dialog box, Projects and Solutions
ms.assetid: 2801f24e-a138-488a-ae3c-e1f99a678ac0
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 09881462b0723dc1e601c908efeabc317ed70b69
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52388943"
---
# <a name="projects-and-solutions-page-options-dialog-box"></a>Página de projetos e soluções, caixa de diálogo Opções

Define o comportamento do Visual Studio relacionado a projetos e soluções. Para acessar essas opções, selecione **Ferramentas** > **Opções**, expanda **Projetos e Soluções** e, em seguida, selecione **Geral**.

Os caminhos padrão para as pastas de projeto e de modelo são definidos por meio da guia **Locais** na mesma caixa de diálogo.

## <a name="general-page"></a>Página geral

As seguintes opções estão disponíveis na página **Geral**.

### <a name="always-show-error-list-if-build-finishes-with-errors"></a>Sempre mostrar a Lista de Erros se o build for concluído com erros

Abre a janela **Lista de Erros** após a conclusão do build, somente se houve falha de build de um projeto. Os erros que ocorrem durante o processo de build são exibidos. Quando essa opção estiver desmarcada, os erros ainda ocorrerão, mas a janela não será aberta quando o build for concluído. Essa opção é habilitada por padrão.

### <a name="track-active-item-in-solution-explorer"></a>Acompanhar item ativo no Gerenciador de Soluções

Quando essa opção estiver selecionada, o **Gerenciador de Soluções** será aberto automaticamente e o item ativo será selecionado. O item selecionado é alterado conforme você trabalha com arquivos diferentes em um projeto ou uma solução, ou com componentes diferentes em um designer. Quando essa opção estiver desmarcada, a seleção no **Gerenciador de Soluções** não será alterada automaticamente. Essa opção é habilitada por padrão.

### <a name="show-advanced-build-configurations"></a>Mostrar configurações de build avançadas

Quando estiverem marcadas, as opções de configuração de build serão exibidas nas caixas de diálogo **Páginas de Propriedades do Projeto** e **Páginas de Propriedades da Solução**. Quando desmarcada, as opções de configuração de build não aparecem nas caixas de diálogo **Páginas de Propriedades do Projeto** e **Páginas de Propriedade da Solução** para projetos do Visual Basic e do C# que contêm uma configuração ou as duas configurações de depuração e versão. Se um projeto tiver uma configuração definida pelo usuário, as opções de configuração de build serão mostradas.

Quando estiverem desmarcados, os comandos do menu **Build**, como **Compilar Solução**, **Recompilar Solução** e **Limpar Solução** serão executados na configuração de Versão e os comandos do menu **Depurar**, como **Iniciar Depuração** e **Iniciar Sem Depuração**, serão executados na configuração de Depuração.

### <a name="always-show-solution"></a>Sempre mostrar solução

Quando essa opção estiver selecionada, a solução e todos os comandos que atuam em soluções sempre serão mostrados no IDE. Quando estiver desmarcada, todos os projetos serão criados como projetos independentes e você não verá a solução no Gerenciador de Soluções nem os comandos que atuam em soluções no IDE se a solução contiver apenas um projeto.

### <a name="save-new-projects-when-created"></a>Salvar novos projetos quando criados

Quando essa opção estiver selecionada, será possível especificar um local para o projeto na caixa de diálogo **Novo Projeto**. Quando estiver desmarcada, todos os novos projetos serão criados como projetos temporários. Quando você estiver trabalhando com projetos temporários, poderá criar e testar um projeto sem a necessidade de especificar um local de disco.

### <a name="warn-user-when-the-project-location-is-not-trusted"></a>Avisar o usuário quando o local do projeto não é confiável

Se você tentar criar um novo projeto ou abrir um projeto existente em um local que não é totalmente confiável (por exemplo, em um caminho UNC ou um caminho HTTP), uma mensagem será exibida. Use essa opção para especificar se a mensagem será exibida sempre que você tentar criar ou abrir um projeto em um local que não é totalmente confiável.

### <a name="show-output-window-when-build-starts"></a>Mostrar a Janela de Saída quando o build é iniciado

Exibe automaticamente a [Janela de Saída](../../ide/reference/output-window.md) no IDE desde o início dos builds da solução.

### <a name="prompt-for-symbolic-renaming-when-renaming-files"></a>Prompt para renomeação simbólica ao renomear arquivos

Quando selecionada, o Visual Studio exibe uma caixa de mensagem perguntando se ele também deve renomear todas as referências no projeto com o elemento de código.

### <a name="prompt-before-moving-files-to-a-new-location"></a>Prompt antes de mover arquivos para um novo local

Quando selecionada, o Visual Studio exibe uma caixa de mensagem de confirmação antes que os locais de arquivos sejam alterados pelas ações no **Gerenciador de Soluções**.

### <a name="reopen-documents-on-solution-load"></a>Reabrir documentos no carregamento da solução

**Novo no Visual Studio 2017 versão 15.8 versão prévia 2 e posterior**

Quando selecionada, os documentos que foram deixados abertos na última vez em que a solução foi fechada são abertos automaticamente quando a solução é aberta.

Reabrir certos tipos de arquivos ou designers pode atrasar o carregamento da solução. Desmarque essa opção para [melhorar o desempenho do carregamento da solução](../../ide/visual-studio-performance-tips-and-tricks.md#disable-automatic-file-restore) se você não quiser restaurar o contexto de anterior da solução.

## <a name="locations-page"></a>Página locais

As seguintes opções estão disponíveis na página **Locais**.

### <a name="projects-location"></a>Local dos projetos

Especifica o local padrão em que o Visual Studio cria novos projetos e pastas da solução. Várias caixas de diálogo também usam o local definido nessa opção para os pontos iniciais da pasta. Por exemplo, a caixa de diálogo **Abrir Projeto** usa esse local para o atalho **Meus Projetos**.

### <a name="user-project-templates-location"></a>Local dos modelos de projeto do usuário

Especifica o local padrão usado pela caixa de diálogo **Novo Projeto** para criar a lista de **Meus Modelos**. Para obter mais informações, consulte [Como localizar e organizar modelos](../../ide/how-to-locate-and-organize-project-and-item-templates.md).

### <a name="user-item-templates-location"></a>Local de modelos de item do usuário

Especifica o local padrão usado pela caixa de diálogo **Adicionar Novo Item** para criar a lista de **Meus Modelos**. Para obter mais informações, consulte [Como localizar e organizar modelos](../../ide/how-to-locate-and-organize-project-and-item-templates.md).

## <a name="see-also"></a>Consulte também

- [Caixa de diálogo Opções, Projetos e Soluções, Compilar e Executar](../../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md)
- [Caixa de diálogo Opções, Projetos e Soluções, Projetos Web](../../ide/reference/options-dialog-box-projects-and-solutions-web-projects.md)
