---
title: Solucionar erros em soluções do Office
ms.date: 02/02/2017
ms.topic: troubleshooting
f1_keywords:
- VST.Project.DesignerDisabled
- VST.Designer.CannotActivate
- VST.Project.ExcelBusy
- VST.SelectDocWizard.AlreadyCustomized
- VST.SelectDocWizard.DocPath
- VST.Project.CannotOpen
- VST.Designer.ErrorsOccurred
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- troubleshooting [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8d73dadd10342d3616291fb93efbb447bd7ecaee
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537313"
---
# <a name="troubleshoot-errors-in-office-solutions"></a>Solucionar erros em soluções do Office
  Você pode encontrar problemas ao executar as seguintes tarefas ao desenvolver soluções do Office no Visual Studio:

- [Criar, atualizar e abrir projetos](#creating)

- [Usar os designers](#designers)

- [Escrever código](#code)

- [Criar projetos](#building)

- [Depurar projetos](#debugging)

## <a name="create-upgrade-and-open-projects"></a><a name="creating"></a>Criar, atualizar e abrir projetos
 Você pode encontrar os erros a seguir ao criar ou abrir projetos do Office.

### <a name="the-project-cannot-be-created"></a>O projeto não pode ser criado
 Ocorreu um erro quando você tentou criar ou abrir um projeto do Office, mas o Visual Studio não tinha informações suficientes para determinar a causa. Tente fechar o projeto, sair do Visual Studio e iniciar novamente.

 Se você estiver tentando criar um projeto de nível de documento, é possível que outro documento com o mesmo nome que o documento no novo projeto já esteja aberto no Excel ou no Word. Verifique se todas as outras instâncias do Excel ou do Word estão fechadas.

### <a name="control-properties-are-lost-when-you-create-a-new-project-based-on-a-document-from-an-existing-project"></a>As propriedades de controle são perdidas quando você cria um novo projeto com base em um documento de um projeto existente
 Se você criar um novo projeto do Office com base em um documento de um projeto existente, as propriedades de todos os controles que estão no documento não serão copiadas no novo projeto. Você deve redefinir as propriedades para todos os controles preexistentes manualmente. Como alternativa, você pode preservar as propriedades de controle criando uma cópia do projeto existente em vez de criar um novo projeto ou carregando o projeto existente na nova solução (no designer) e copiando e colando os controles do documento existente para o novo documento.

### <a name="errors-when-you-create-an-excel-workbook-project-based-on-an-existing-workbook"></a>Erros ao criar um projeto de pasta de trabalho do Excel com base em uma pasta de trabalho existente
 Se você criar um novo projeto de pasta de trabalho do Excel com base em uma pasta de trabalho existente, poderá ver uma combinação dos erros a seguir.

 Do Excel: "aviso de privacidade: Este documento contém macros, controles ActiveX, informações do pacote de expansão XML ou componentes da Web. Elas podem incluir informações pessoais que não podem ser removidas pelo inspetor de documento. "

 No Visual Studio: "o designer não pôde ser carregado corretamente."

 Esses erros podem ocorrer quando você tenta criar um projeto baseado em uma pasta de trabalho que tenha suas informações pessoais removidas usando o Inspetor de documento. Para evitar esse erro, execute as etapas a seguir antes de criar o projeto.

1. Abra a pasta de trabalho no Excel.

2. No Excel, abra a central de confiabilidade.

3. Na guia **Opções de privacidade** , desmarque a caixa de seleção **remover informações pessoais de propriedades do arquivo ao salvar** .

4. Salve a pasta de trabalho e feche o Excel.

### <a name="cannot-open-a-project-after-migration"></a>Não é possível abrir um projeto após a migração
 Depois que uma solução do Office é migrada para Microsoft Office 2010, o projeto não pode ser aberto em um computador de desenvolvimento com apenas o sistema de Microsoft Office 2007 instalado. Você pode ver os erros a seguir.

 "Um ou mais projetos na solução não foram carregados corretamente. Consulte a Janela de Saída para obter detalhes. "

 "Não é possível criar o projeto porque o aplicativo associado a este tipo de projeto não está instalado neste computador. Você deve instalar o aplicativo Microsoft Office que está associado a este tipo de projeto. "

 Para resolver esse problema, edite o arquivo *. vbproj* ou *. csproj* . Para um projeto do Word, substitua HostPackage = "{763FDC83-64E5-4651-AC9B-28C4FEB985A1}" por HostPackage = "{6CE98B71-D55A-4305-87A8-0D6E368D9600}". Para um projeto do Excel, substitua HostPackage = "{B284B16A-C42C-4438-BDCD-B72F4AC43CFB}" por HostPackage = "{825100CF-0BA7-47EA-A084-DCF3308DAF74}". Para um projeto do Outlook, substitua HostPackage = "{D2B20FF5-A6E5-47E1-90E8-463C6860CB05}" por HostPackage = "{20A848B8-E01F-4801-962E-25DB0FF57389}".

 Como alternativa, verifique se os projetos migrados são abertos apenas em computadores de desenvolvimento com o Microsoft Office 2010 já instalado.

### <a name="errors-in-upgraded-office-2003-document-level-projects-that-contain-windows-forms-controls"></a>Erros em projetos de nível de documento do Office 2003 atualizados que contêm controles de Windows Forms
 Se você atualizar um projeto de nível de documento Microsoft Office 2003 e o documento contiver Windows Forms controles, o projeto atualizado poderá ter erros de compilação ou tempo de execução. Para evitar esse problema, instale o tempo de execução do Visual Studio 2005 Tools para Office Second Edition no computador de desenvolvimento antes de atualizar o projeto. Esta versão do tempo de execução está disponível como um pacote redistribuível do centro de download da Microsoft em [Microsoft Visual Studio 2005 Tools for Office Second Edition Runtime (VSTO 2005 se) (x86)](https://www.microsoft.com/download/details.aspx?id=2392).

 Depois de concluir a atualização do projeto, você poderá desinstalar o tempo de execução das ferramentas do Visual Studio 2005 para Office Second Edition do computador de desenvolvimento se ele não estiver sendo usado por outras soluções do Office.

## <a name="use-the-designers"></a><a name="designers"></a>Usar os designers
 Você pode encontrar os erros a seguir ao trabalhar com o documento, a pasta de trabalho ou o designer de planilha em projetos de nível de documento.

### <a name="designer-failed-to-load-correctly"></a>Falha ao carregar o designer corretamente
 O Visual Studio não pode abrir o designer nos seguintes casos:

- O Excel ou o Word já está aberto e está exibindo uma caixa de diálogo modal. Para abrir o designer, verifique se o Excel ou o Word tem uma caixa de diálogo modal aberta e feche todas as caixas de diálogo modais abertas. Se não houver nenhuma caixa de diálogo modal aberta, pode haver alguma outra ação necessária antes que o Excel ou o Word responda.

- O projeto está sendo depurado no momento. Para abrir o designer, pare ou conclua a depuração.

- Um suplemento do VSTO do Excel que está instalado no computador de desenvolvimento está exibindo uma caixa de diálogo quando o Excel é iniciado. Para criar um projeto de nível de documento do Excel, primeiro você deve desabilitar o suplemento do VSTO.

### <a name="controls-appear-as-black-rectangles-on-the-document-or-worksheet"></a>Os controles aparecem como retângulos pretos no documento ou na planilha
 Se você agrupar controles em um documento ou planilha, o Visual Studio não reconhecerá mais os controles. Os controles agrupados não podem ser acessados na janela **Propriedades** e aparecem como retângulos pretos no documento ou na planilha. Você deve desagrupar os controles para restaurar sua funcionalidade.

### <a name="controls-on-a-word-template-are-not-visible-in-visual-studio"></a>Controles em um modelo do Word não são visíveis no Visual Studio
 Se você abrir um modelo do Word no designer do Visual Studio, os controles no modelo que não estão alinhados com o texto podem não estar visíveis. Isso ocorre porque o Visual Studio abre modelos do Word no modo de exibição **normal** . Para exibir os controles, clique no menu **Exibir** , aponte para **Microsoft Office modo de exibição de palavra** e clique em layout de **impressão**.

### <a name="insert-clip-art-command-does-nothing-in-the-visual-studio-designer"></a>O comando Inserir Clip-Art não faz nada no designer do Visual Studio
 Quando o Excel ou o Word estiver aberto no designer do Visual Studio, clicar no botão **Clip-Art** na guia **ilustrações** da faixa de palavras não abre o painel de tarefas **Clip-Art** . Para adicionar clip-art, você deve abrir a cópia da pasta de trabalho ou do documento que está na pasta principal do projeto (não a cópia que está no diretório *\Bin* ) fora do Visual Studio, adicionar o clip-art e, em seguida, salvar a pasta de trabalho ou o documento.

## <a name="write-code"></a><a name="code"></a>Escrever código
 Você pode encontrar os erros a seguir ao escrever código em projetos do Office.

### <a name="some-events-of-office-objects-are-not-accessible-when-using-c"></a>Alguns eventos de objetos do Office não estão acessíveis ao usar o C\#
 Em alguns casos, você pode ver um erro do compilador como o seguinte quando tenta acessar um evento específico de uma instância de um tipo de módulo de interoperabilidade primária do Office (PIA) em um projeto do Visual C#.

 "Ambiguidade entre ' Microsoft. Office. Interop. Excel. _Application. NewWorkbook ' e ' Microsoft. Office. Interop. Excel. AppEvents_Event. NewWorkbook '"

 Esse erro significa que você está tentando acessar um evento que tem o mesmo nome de outra propriedade ou método do objeto. Para acessar o evento, você deve converter o objeto em sua *interface de evento*.

 Os tipos de PIA do Office que têm eventos implementam duas interfaces: uma interface principal com todas as propriedades e métodos e uma interface de evento que contém os eventos expostos pelo objeto. Essas interfaces de evento usam a Convenção de nomenclatura *objectname*eventos*n*_Event, como <xref:Microsoft.Office.Interop.Excel.AppEvents_Event> e <xref:Microsoft.Office.Interop.Word.ApplicationEvents2_Event> . Se você não puder acessar um evento que você espera encontrar em um objeto, converta o objeto em sua interface de evento.

 Por exemplo, os <xref:Microsoft.Office.Interop.Excel.Application> objetos têm um <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.NewWorkbook> evento e uma <xref:Microsoft.Office.Interop.Excel._Application.NewWorkbook%2A> propriedade. Para manipular o <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.NewWorkbook> evento, converta o <xref:Microsoft.Office.Interop.Excel.Application> para a <xref:Microsoft.Office.Interop.Excel.AppEvents_Event> interface. O exemplo de código a seguir demonstra como fazer isso em um projeto de nível de documento para o Excel.

 [!code-csharp[Trin_VstcoreTroubleshootingExcel#1](../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingExcelCS/ThisWorkbook.cs#1)]

 Para obter mais informações sobre interfaces de evento nos PIAs do Office, consulte [visão geral de classes e interfaces nos assemblies de interoperabilidade primária do Office](/previous-versions/office/office-12//ms247299(v=office.12)).

### <a name="cannot-reference-office-pia-classes-in-projects-that-target-the-net_v40_short-or-the-net_v45"></a>Não é possível fazer referência a classes do PIA do Office em projetos direcionados ao [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou ao[!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]
 Em projetos que se destinam ao [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou ao [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] , o código que faz referência a uma classe que é definida em um pia do Office não será compilado por padrão. As classes nos PIAs usam a classe *objectname*da Convenção de nomenclatura, como <xref:Microsoft.Office.Interop.Word.DocumentClass> e <xref:Microsoft.Office.Interop.Excel.WorkbookClass> . Por exemplo, o código a seguir de um projeto de suplemento do VSTO do Word não será compilado.

```vb
Dim document As Word.DocumentClass = Globals.ThisAddIn.Application.ActiveDocument
```

```csharp
Word.DocumentClass document = (Word.DocumentClass) Globals.ThisAddIn.Application.ActiveDocument;
```

 Esse código resulta nos seguintes erros de compilação:

- Visual Basic: "a referência à classe ' DocumentClass ' não é permitida quando seu assembly está vinculado usando o modo no-PIA."

- Visual C#: "tipo de interoperabilidade" Microsoft.Office.Interop.Word.DocumentClass "não pode ser inserido. Em vez disso, use a interface aplicável. "

  Para resolver esse erro, modifique o código para fazer referência à interface correspondente em vez disso. Por exemplo, em vez de fazer referência a um <xref:Microsoft.Office.Interop.Word.DocumentClass> objeto, faça referência a uma instância da <xref:Microsoft.Office.Interop.Word.Document> interface.

```vb
Dim document As Word.Document = Globals.ThisAddIn.Application.ActiveDocument
```

```csharp
Word.Document document = Globals.ThisAddIn.Application.ActiveDocument;
```

 Projetos que se destinam ao [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou ao [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] , inserem automaticamente todos os tipos de interoperabilidade dos pias do Office por padrão. Esse erro de compilação ocorre porque o recurso tipos de interoperabilidade inserido só funciona com interfaces, não com classes. Para obter mais informações sobre interfaces e classes nos PIAs do Office, consulte [visão geral de classes e interfaces nos assemblies de interoperabilidade primária do Office](/previous-versions/office/office-12/ms247299(v=office.12)). Para obter mais informações sobre o recurso tipos de interoperabilidade inseridos em projetos do Office, consulte [projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md).

### <a name="references-to-office-classes-are-not-recognized"></a>Referências a classes do Office não são reconhecidas
 Alguns nomes de classe, por exemplo, aplicativo, estão em vários namespaces, como <xref:Microsoft.Office.Interop.Word> e <xref:System.Windows.Forms> . Por esse motivo, a instrução **Imports** / **usando** na parte superior dos modelos de projeto inclui uma constante de qualificação abreviada, por exemplo:

 [!code-csharp[Trin_VstcoreTroubleshootingWord#2](../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingWordCS/ThisDocument.cs#2)]
 [!code-vb[Trin_VstcoreTroubleshootingWord#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreTroubleshootingWordVB/ThisDocument.vb#2)]

 Esse uso da instrução **Imports** / **using** exige que você diferencie as referências às classes do Office com o qualificador do Word ou Excel, por exemplo:

 [!code-csharp[Trin_VstcoreTroubleshootingWord#3](../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingWordCS/ThisDocument.cs#3)]
 [!code-vb[Trin_VstcoreTroubleshootingWord#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreTroubleshootingWordVB/ThisDocument.vb#3)]

 Você receberá erros se usar uma declaração não qualificada, por exemplo:

 [!code-csharp[Trin_VstcoreTroubleshootingWord#4](../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingWordCS/ThisDocument.cs#4)]
 [!code-vb[Trin_VstcoreTroubleshootingWord#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreTroubleshootingWordVB/ThisDocument.vb#4)]

 Embora você tenha importado o namespace do Word ou do Excel e tenha acesso a todas as classes dentro dele, você deve qualificar totalmente todos os tipos com o Word ou o Excel para remover a ambiguidade do namespace.

## <a name="build-projects"></a><a name="building"></a>Compilar projetos
 Você pode encontrar os erros a seguir ao criar projetos do Office.

### <a name="cannot-build-a-document-level-project-that-is-based-on-a-document-with-restricted-permissions"></a>Não é possível criar um projeto de nível de documento baseado em um documento com permissões restritas
 O Visual Studio não poderá criar projetos de nível de documento se o documento tiver permissões restritas. Se o seu projeto contiver um documento que tenha permissões restritas, o projeto não será compilado e você receberá a seguinte mensagem na janela de **lista de erros** .

 "Falha ao adicionar a personalização."

 Se você quiser incluir um documento que tenha permissões restritas, use um documento irrestrito enquanto desenvolve e cria a solução. Em seguida, aplique as permissões restritas ao documento no local de publicação, depois de publicar a solução.

### <a name="compiler-errors-occur-after-a-namedrange-control-is-deleted"></a>Erros do compilador ocorrem depois que um controle NamedRange é excluído
 Se você excluir um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle de uma planilha que não seja a planilha ativa no designer, o código gerado automaticamente não poderá ser removido do seu projeto e poderão ocorrer erros de compilador. Para verificar se o código foi removido, você deve sempre selecionar a planilha que contém o <xref:Microsoft.Office.Tools.Excel.NamedRange> controle para torná-la a planilha ativa antes de excluir o controle. Se o código gerado automaticamente não for excluído quando você excluir o controle, você poderá fazer com que o designer exclua o código ativando a planilha e fazendo uma alteração para que a planilha fique marcada como modificada. Quando você recria o projeto, o código é removido.

## <a name="debug-projects"></a><a name="debugging"></a>Depurar projetos
 Você pode encontrar os erros a seguir ao depurar projetos do Office.

### <a name="prompt-to-uninstall-appears-when-you-publish-and-install-a-solution-on-the-development-computer"></a>A solicitação de desinstalação aparece quando você publica e instala uma solução no computador de desenvolvimento
 Ao depurar uma solução do Office, você poderá ver o erro a seguir.

 "A personalização não pode ser instalada porque outra versão está atualmente instalada e não pode ser atualizada a partir desse local."

 Esse erro indica que você já publicou e instalou a solução do Office em seu computador de desenvolvimento. Para impedir que a mensagem apareça, desinstale a solução na lista de programas instalados no computador antes de depurar a solução. Como alternativa, você pode criar outra conta de usuário em seu computador de desenvolvimento para testar a instalação da solução publicada.

### <a name="document-level-projects-created-at-unc-network-locations-do-not-run-from-visual-studio"></a>Projetos de nível de documento criados em locais de rede UNC não são executados no Visual Studio
 Se você criar um projeto de nível de documento para Excel ou Word em um local de rede UNC, deverá adicionar o local do documento à lista de locais confiáveis no Excel ou no Word. Caso contrário, a personalização não será carregada quando você tentar executar ou depurar o projeto no Visual Studio. Para obter mais informações sobre locais confiáveis, consulte [conceder confiança a documentos](../vsto/granting-trust-to-documents.md).

### <a name="threads-are-not-stopped-correctly-after-debugging"></a>Os threads não são interrompidos corretamente após a depuração
 Os projetos do Office no Visual Studio seguem uma Convenção de nomenclatura de thread que permite que o depurador feche o programa corretamente. Se você criar threads em sua solução, deverá nomear cada thread com o prefixo VSTA_ para garantir que esses threads sejam tratados corretamente quando você parar a depuração. Por exemplo, você pode definir a `Name` propriedade de um thread que aguarda um evento de rede para **VSTA_NetworkListener**.

### <a name="cannot-run-or-debug-any-office-solution-on-the-development-computer"></a>Não é possível executar ou depurar nenhuma solução do Office no computador de desenvolvimento
 Se não for possível executar ou desenvolver um projeto do Office em seu computador de desenvolvimento, você poderá ver a seguinte mensagem de erro.

 "Não foi possível carregar a personalização porque o domínio do aplicativo não pôde ser criado."

 O Visual Studio usa Fusion, o carregador de assembly .NET Framework, para armazenar em cache os assemblies antes de carregar soluções do Office. Verifique se o Visual Studio pode gravar no cache de fusão e tente novamente. Para obter mais informações, consulte [assemblies de cópia de sombra](/dotnet/framework/app-domains/shadow-copy-assemblies).

### <a name="error-when-stopping-the-debugger-in-a-document-level-project-after-using-edit-and-continue"></a>Erro ao parar o depurador em um projeto de nível de documento depois de usar editar e continuar
 Se você usar **Editar** e **continuar** para fazer alterações no código em um projeto de nível de documento do Excel ou do Word enquanto o projeto estiver no modo de interrupção, você poderá ver uma caixa de diálogo com a seguinte mensagem de erro se parar o depurador posteriormente.

 "Encerrar o processo em seu estado atual pode causar resultados indesejados, incluindo a perda de dados e a instabilidade do sistema".

 Se você clicar em **Sim** ou **não** na caixa de diálogo, o Visual Studio encerrará o processo do Excel ou do Word e interromperá o depurador. Para interromper a depuração do projeto sem exibir essa caixa de diálogo, saia do Excel ou do Word diretamente em vez de parar o depurador no Visual Studio.

## <a name="see-also"></a>Confira também
- [Solucionar problemas de soluções do Office](../vsto/troubleshooting-office-solutions.md)
- [Solucionar problemas de segurança da solução do Office](../vsto/troubleshooting-office-solution-security.md)
- [Solucionar problemas de implantação de solução do Office](../vsto/troubleshooting-office-solution-deployment.md)
