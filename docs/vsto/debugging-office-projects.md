---
title: Depurar projetos do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel projects [Office development in Visual Studio], debugging
- Word projects [Office development in Visual Studio], debugging
- Outlook [Office development in Visual Studio], debugging
- debugging [Office development in Visual Studio], Outlook projects
- Office projects [Office development in Visual Studio], debugging
- Outlook [Office development in Visual Studio], projects
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: cc1774e57fafadafc7087bb498e0b77a90e96d85
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669936"
---
# <a name="debug-office-projects"></a>Depurar projetos do Office
  Você pode depurar projetos do Office usando o Microsoft mesmo [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ferramentas que você usa para outros [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projetos. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] recursos do depurador, como a capacidade de inserir pontos de interrupção e exibir as variáveis na **Locals** janela, também estão disponíveis quando você depurar projetos do Office. Para obter mais informações sobre [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] as ferramentas de depuração, consulte [depurar no Visual Studio](/visualstudio/debugger/debugging-in-visual-studio).  
  
> [!TIP]  
>  Para simplificar a depuração, feche todas as instâncias do aplicativo do Office antes de compilar e depurá-lo.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
> [!NOTE]  
>  Interessado em desenvolver soluções que estendem a experiência do Office em toda [várias plataformas](https://dev.office.com/add-in-availability)? Confira a nova [modelo de suplementos do Office](https://dev.office.com/docs/add-ins/overview/office-add-ins). Suplementos do Office têm uma superfície pequena em comparação com soluções e suplementos do VSTO, e você pode criá-los usando quase qualquer tecnologia, como HTML5, JavaScript, CSS3 e XML de programação da web.  
  
## <a name="start-and-stop-the-debugger"></a>Iniciar e parar o depurador  
 Você pode iniciar a depuração de um projeto do Office exatamente como você inicia a depuração de outro [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projetos; por exemplo, você pode pressionar a **F5** chave. Quando você inicia a depuração de um projeto de suplemento do VSTO, um novo processo para o aplicativo do Office de destino é iniciado e o suplemento do VSTO é carregado.  
  
 Quando você inicia a depuração de um projeto de nível de documento, documento ou pasta de trabalho é aberto em um novo processo do Word ou Excel.  
  
 Quando você interrompe o depurador, o depurador encerra o processo de aplicativo abruptamente ou desanexa se você tiver o depurador definido como para desanexar. Todos os outros documentos que são abertos no processo do aplicativo Office encerrado também são fechados sem aviso, e as alterações não salvas serão perdidas. Isso pode incluir todos os documentos ou pastas de trabalho que são abertas enquanto o depurador está em execução.  
  
 Normalmente, é melhor desanexar do processo antes de parar o depurador, para que você pode encerrar o aplicativo do Office da maneira normal. Você também pode desanexar do processo primeiro se desejar trabalhar com uma planilha ou um documento aberto depois de interromper o depurador.  
  
 Se você estiver depurando uma personalização no nível de documento para Word, repetidamente parar o depurador e fazendo com que o Word fechar, de repente, podem levar a modelo Normal se tornar corrompido. Se isso acontecer, você pode excluir o modelo Normal corrompido e ele será recriado automaticamente na próxima vez que você abra o Word. No entanto, todas as macros que foram armazenadas no modelo Normal não são recriadas.  
  
### <a name="debug-office-2013-vsto-add-ins-by-using-either-office-2013-or-office-2016"></a>Depurar o Office 2013 VSTO Add-ins usando o Office 2013 ou Office 2016  
 Se você estiver usando o Visual Studio 2015 e você tem as duas versões do Office instalado lado a lado, o Visual Studio inicia o Office 2016. Se você estiver usando o Visual Studio 2013, Visual Studio inicia o Office 2013.  
  
 Se você quiser depurar o suplemento do VSTO por meio de uma versão diferente do Office (2013 ou 2016), abra o **Designer de projeto**e, na **Debug** guia, escolha o **Iniciar programa externo**botão de opção. Em seguida, navegue até o local do executável do aplicativo de Office apropriado.  
  
## <a name="f10-and-f11-behavior"></a>Comportamento F10 e F11  
 Quando você iniciar a depuração de um projeto do Office **F10** e **F11** não têm o mesmo comportamento que quando você inicia a depuração de outros projetos do Visual Basic ou c#. Em projetos do Visual Basic ou c#, o depurador é interrompido na função principal; em projetos do Office, o Visual Studio não tem controle sobre a função de principal do aplicativo do Office. No entanto, durante a depuração, **F10** e **F11** têm as mesmas funções de projetos do Visual Basic e c#.  
  
## <a name="display-exceptions"></a>Exibir exceções  
 Por causa da maneira que o código gerenciado interage com código não gerenciado, o Visual Studio não exibe erros que são gerados pelos aplicativos do Microsoft Office. Por exemplo, se um suplemento VSTO criado usando ferramentas de desenvolvimento do Office no Visual Studio gera uma exceção, o aplicativo Microsoft Office continua sem exibir um erro. Para ver esses erros, defina o depurador para interromper em exceções do common language runtime. Para obter mais informações, consulte [gerenciar exceções com o depurador](/visualstudio/debugger/managing-exceptions-with-the-debugger).  
  
 Se você definir o depurador para interromper em exceções do common language runtime, todas as exceções agora serão interrompida no depurador, incluindo aqueles que você tratou e algumas exceções de primeira chance do tempo de execução em si, que podem não ser relevante ao seu projeto. Erros referindo-se a msosec não foi encontrada aparecem em cada projeto, mas podem ser ignorados. Essas exceções msosec não afetará sua solução.  
  
 Você também pode usar **tente... Capturar** instruções em torno de seus métodos para capturar exceções.  
  
 Por padrão, o Visual Studio também faz a exibição Just-In-Time erros de depuração para projetos do Office; No entanto, você pode habilitar esse recurso para que você possa ver os erros que são gerados. Para obter mais informações, consulte [depuração no Visual Studio Just-In-Time](/visualstudio/debugger/just-in-time-debugging-in-visual-studio).  
  
## <a name="command-line-arguments"></a>Argumentos de linha de comando  
 Se o **iniciar ação** sobre o **depurar** página de propriedade é definida como **Iniciar projeto**, Visual Studio não usa argumentos de linha de comando ao depurar o projeto, mesmo se você tiver especificados os argumentos de linha de comando como opções de inicialização. Se você quiser usar argumentos de linha de comando ao iniciar a depuração, você deve selecionar um **iniciar ação** diferente de **Iniciar projeto**.  
  
## <a name="source-control"></a>Controle do código-fonte  
 Depurar propriedades não são compartilhadas entre vários usuários sob controle do código-fonte. Projetos Visual Basic e c# armazenam propriedades de depuração em um arquivo específico do usuário (*NomeDoProjeto*. vbproj ou *ProjectName*. csproj), e esse arquivo não está sob controle do código-fonte. Se mais de uma pessoa está depurando, cada pessoa deve inserir manualmente as propriedades de depuração.  
  
## <a name="debug-cached-datasets-in-a-document-level-project"></a>Depurar conjuntos de dados armazenados em cache em um projeto de nível de documento  
 Sempre que você criar um projeto, o conjunto de dados é esvaziado e recriado. Se você quiser depurar um conjunto de dados armazenados em cache, você deve abrir o documento fora do Visual Studio e, em seguida, anexar o depurador.  
  
## <a name="debug-word-document-projects-based-on-the-word-97-2003-document-doc-format"></a>Depurar projetos de documento do Word com base no documento do Word 97-2003 (*. doc) formato  
 Para depurar um projeto de documento do Word com base no documento do Word 97-2003 (*/**. doc) formato, você deve adicionar a pasta do projeto à lista de pastas confiáveis. Para obter mais informações sobre como fazer isso, consulte [conceder confiança a documentos](../vsto/granting-trust-to-documents.md).  
  
## <a name="debug-disabled-add-ins"></a>Suplementos de depuração desabilitada  
 Aplicativos do Microsoft Office podem desabilitar suplementos do VSTO que tenha um comportamento inesperado. Um aplicativo do Microsoft Office desabilita VSTO Add-ins para impedir que o código problemático Carregando toda vez que o aplicativo é iniciado. No entanto, também é fácil causar um comportamento inesperado durante a depuração típico. Para obter informações sobre como habilitar novamente o VSTO Add-ins, consulte [como: habilitar novamente um suplemento VSTO que tenha sido desabilitado](../vsto/how-to-re-enable-a-vsto-add-in-that-has-been-disabled.md).  
  
 Há dois tipos de desabilitar o que os aplicativos do Microsoft Office usam para suplementos do VSTO: difícil desabilitação e desabilitando reversível.  
  
### <a name="hard-disabling"></a>Desabilitando duro  
 Desabilitando duro pode ocorrer quando um suplemento do VSTO faz com que o aplicativo seja encerrado inesperadamente. Também podem ocorrer no computador de desenvolvimento se você parar o depurador enquanto o <xref:Microsoft.Office.Tools.AddIn.Startup> manipulador de eventos no seu suplemento do VSTO está em execução. Quando um suplemento do VSTO é difícil desabilitado, ele aparece na **itens desabilitados** lista no aplicativo.  
  
 Se um aplicativo do Office rígido desabilita um suplemento VSTO criado usando ferramentas de desenvolvimento do Office no Visual Studio, o aplicativo desabilita somente o VSTO Add-in que causou a falha. Outros suplementos do VSTO criados usando ferramentas de desenvolvimento do Office no Visual Studio para o aplicativo Office continuará a ser carregado.  
  
### <a name="soft-disabling"></a>Desabilitando reversível  
 Desabilitando reversível pode ocorrer quando um suplemento do VSTO produz um erro que não faz com que o aplicativo fechar inesperadamente. Por exemplo, um aplicativo flexível pode desativar um suplemento do VSTO se ele lançar uma exceção sem tratamento ao <xref:Microsoft.Office.Tools.AddIn.Startup> manipulador de eventos está em execução. Quando um suplemento do VSTO é desabilitado flexível, ele aparece na **suplementos de aplicativo inativos** lista no aplicativo e o aplicativo altera o valor da **LoadBehavior** entrada do registro para o suplemento do VSTO para indicar que ele é descarregado. Para obter mais informações sobre o **LoadBehavior** entrada de registro, consulte [entradas do registro para suplementos VSTO](../vsto/registry-entries-for-vsto-add-ins.md).  
  
## <a name="troubleshoot-installation-errors-by-using-the-event-viewer"></a>Solucionar problemas de erros de instalação usando o Visualizador de eventos  
 O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] grava mensagens em Visualizador de eventos no Windows para todas as exceções que são geradas quando você instala ou desinstala as soluções do Office. Você pode usar essas mensagens para resolver problemas de implantação e instalação.  
  
## <a name="troubleshoot-startup-errors-by-using-a-log-file-and-error-messages"></a>Solucionar problemas de erros de inicialização usando um mensagens de erro e o arquivo de log  
 O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] pode gravar todos os erros que ocorrem durante a inicialização do log de um arquivo ou exibem cada erro em uma caixa de mensagem. Por padrão, essas opções estão desativadas. Você pode ativar as opções com a criação de variáveis de ambiente.  
  
 Para exibir cada erro em uma caixa de mensagem, crie uma variável de ambiente denominada `VSTO_SUPPRESSDISPLAYALERTS` e defina-o como 0 (zero). Você pode suprimir as mensagens excluindo a variável de ambiente ou defini-lo como 1 (um).  
  
 Para gravar os erros em um arquivo de log, crie uma variável de ambiente denominada `VSTO_LOGALERTS` e defini-lo como 1 (um). O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] cria o arquivo de log na pasta que contém o manifesto de implantação para o suplemento do VSTO, ou na pasta que contém o documento ou pasta de trabalho que está associada com a personalização. Se isso falhar, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] cria o arquivo de log no local *% TEMP %* pasta. Para o nível de aplicativo VSTO Add-ins, o nome padrão é *nome do suplemento*. vsto.log. Para projetos de nível de documento, é o nome do arquivo de log *nome do documento*. *extensão*. log, como ExcelWorkbook1.xlsx.log. Para interromper o log de erros, exclua a variável de ambiente ou defina-o como 0 (zero).  
  
## <a name="see-also"></a>Consulte também  
 [Compilar soluções do Office](../vsto/building-office-solutions.md)   
 [Como: habilitar novamente um suplemento VSTO que tenha sido desabilitado](../vsto/how-to-re-enable-a-vsto-add-in-that-has-been-disabled.md)   
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)  
  
  