---
title: Como exibir, salvar e configurar arquivos de log de build |Microsoft Docs
ms.date: 08/28/2019
ms.technology: vs-ide-compile
ms.topic: how-to
ms.assetid: 75d38b76-26d6-4f43-bbe7-cbacd7cc81e7
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4acf8ca4e116bfb0ab990f1b0aed66bef95820ad
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283899"
---
# <a name="how-to-view-save-and-configure-build-log-files"></a>Como exibir, salvar e configurar arquivos de log de build

Depois de compilar um projeto no Visual Studio IDE, é possível exibir informações sobre sse build na Janela de **Saída**. Usando essas informações, é possível, por exemplo, solucionar problemas de uma falha de build.

- Para projetos C++, você também pode exibir as mesmas informações em um arquivo de log que é criado e salvo quando você cria um projeto. 

- Para projetos de código gerenciado, você pode clicar na janela saída de compilação e pressionar **Ctrl** + **S**. O Visual Studio solicita um local para salvar as informações da janela de **saída** em um arquivo de log.

Também é possível usar o IDE para especificar que tipos de informações você deseja exibir sobre cada build.

Se você criar qualquer tipo de projeto usando o MSBuild, poderá criar um arquivo de log para salvar informações sobre a compilação. Para obter mais informações, consulte [Obtendo logs de build](../msbuild/obtaining-build-logs-with-msbuild.md).

## <a name="to-view-the-build-log-file-for-a-c-project"></a>Para exibir o arquivo de log de build para um projeto C++

1. No **Windows Explorer** ou **Explorador de arquivos**, abra o seguinte arquivo (relativo à pasta raiz do projeto): *versão* \\ <ProjectName> \> . Log * ou *Debug \\<ProjectName \> . log*

## <a name="to-create-a-build-log-file-for-a-managed-code-project"></a>Para criar um arquivo de log de build para um projeto de código gerenciado

1. Na barra de menus, escolha **Compilar**compilar  >  **solução**.

2. Na janela de **Saída**, clique em algum lugar no texto.

3. Pressione **Ctrl** + **S**.

   O Visual Studio solicitará um local para salvar a saída de build.

Você também pode gerar logs executando o MSBuild diretamente na linha de comando, usando a opção de linha de comando `-fileLogger` (`-fl`). Confira [Obter logs de build com o MSBuild](../msbuild/obtaining-build-logs-with-msbuild.md).

## <a name="to-change-the-amount-of-information-included-in-the-build-log"></a>Para alterar a quantidade de informações incluídas no log de build

1. Na barra de menus, escolha **ferramentas**  >  **Opções**.

2. Na página **Projetos e Soluções**, escolha a página **Compilar e Executar**.

3. Na lista **Detalhamento da saída de build do projeto no MSBuild**, escolha um dos seguintes valores e, em seguida, escolha o botão **OK**.

    |Nível de detalhes|Descrição|
    | - |-----------------|
    |**Quiet**|Exibe apenas um resumo do build.|
    |**Mínimo**|Exibe um resumo do build e dos erros, avisos e mensagens categorizadas como altamente importantes.|
    |**Normal**|Exibe um resumo do build; erros, avisos e mensagens categorizados como altamente importantes; e as principais etapas do build. Use esse nível de detalhes com mais frequência.|
    |**Detalhado**|Exibe um resumo do build; erros, avisos e mensagens categorizados como altamente importantes; todas as etapas do build; e as mensagens categorizadas com base na importância normal.|
    |**Diagnostic**|Exibe todos os dados disponíveis para o build. É possível usar este nível de detalhes para ajudar a depurar problemas com scripts de build personalizados e outros problemas de build.|

     Para obter mais informações, consulte [Caixa de diálogo Opções, Projetos e Soluções, Criar e Executar](../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md) e <xref:Microsoft.Build.Framework.LoggerVerbosity>.

    > [!IMPORTANT]
    > É necessário recompilar o projeto para que suas alterações tenham efeito na Janela de **Saída** (todos os projetos) e no arquivo *\<ProjectName>.txt* (apenas projetos C++).

## <a name="use-binary-logs-to-make-it-easier-to-browse-large-log-files"></a>Usar logs binários para facilitar a navegação em arquivos de log grandes

Logs binários são um recurso opcional para projetos do .NET que proporcionam uma experiência de navegação de log mais rica que pode facilitar a localização de informações em logs grandes. Para usar logs binários, instale as [Ferramentas do Sistema para Projetos](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.ProjectSystemTools). Para obter mais informações, consulte [https://msbuildlog.com](https://msbuildlog.com) e [log binário](https://github.com/microsoft/msbuild/blob/master/documentation/wiki/Binary-Log.md)

## <a name="see-also"></a>Veja também

- [Criar e limpar projetos e soluções no Visual Studio](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)
- [Compilação e construção](../ide/compiling-and-building-in-visual-studio.md)
