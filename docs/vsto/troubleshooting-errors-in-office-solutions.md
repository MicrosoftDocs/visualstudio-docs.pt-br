---
title: Solucionar problemas de erros em soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: bcc5600f38e2d53244d972e4c4c7094182bfa48c
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672945"
---
# <a name="troubleshoot-errors-in-office-solutions"></a>Solucionar problemas de erros em soluções do Office
  Você pode encontrar problemas ao executar as seguintes tarefas durante o desenvolvimento de soluções do Office no Visual Studio:  
  
-   [Criar, atualizar e abrir projetos](#creating)  
  
-   [Usar os designers](#designers)  
  
-   [Escrever código](#code)  
  
-   [Criar projetos](#building)  
  
-   [Depurar projetos](#debugging)  
  
##  <a name="creating"></a> Criar, atualizar e abrir projetos  
 Você pode encontrar os seguintes erros ao criar ou abrir projetos do Office.  
  
### <a name="the-project-cannot-be-created"></a>Não é possível criar o projeto  
 Ocorreu um erro quando você tentou criar ou abrir um projeto do Office, mas o Visual Studio não tem informações suficientes para determinar a causa. Tente fechar seu projeto, sair do Visual Studio e iniciar novamente.  
  
 Se você estiver tentando criar um projeto de nível de documento, é possível que outro documento com o mesmo nome que o documento no novo projeto já está aberto no Excel ou Word. Certifique-se de que todas as outras instâncias do Excel ou Word estão fechadas.  
  
### <a name="control-properties-are-lost-when-you-create-a-new-project-based-on-a-document-from-an-existing-project"></a>Propriedades de controle são perdidas quando você cria um novo projeto com base em um documento de um projeto existente  
 Se você criar um novo projeto do Office com base em um documento de um projeto existente, as propriedades para todos os controles que estão no documento não são copiadas para o novo projeto. As propriedades para todos os controles preexistentes deve ser redefinido manualmente. Como alternativa, você pode preservar as propriedades de controle, criando uma cópia de um projeto existente em vez de criar um novo projeto ou carregar o projeto existente para a nova solução (no designer) e copiando e colando os controles de existente documento para o novo documento.  
  
### <a name="errors-when-you-create-an-excel-workbook-project-based-on-an-existing-workbook"></a>Erros quando você cria um projeto de pasta de trabalho do Excel com base em uma pasta de trabalho existente  
 Se você criar um novo projeto de pasta de trabalho do Excel com base em uma pasta de trabalho existente, é possível encontrar uma combinação dos seguintes erros.  
  
 No Excel: "Aviso de privacidade: este documento contém macros, controles ActiveX, informações de pacote de expansão do XML ou componentes da Web. Eles podem incluir informações pessoais que não podem ser removidas pelo Inspetor de documento."  
  
 No Visual Studio: "Designer não pôde carregar corretamente."  
  
 Esses erros podem ocorrer, que tente criar um projeto com base em uma pasta de trabalho que teve suas informações pessoais removidas usando o Inspetor de documento. Para evitar esse erro, execute as seguintes etapas antes de criar o projeto.  
  
1.  Abra a pasta de trabalho no Excel.  
  
2.  No Excel, abra a Central de confiabilidade.  
  
3.  Sobre o **opções de privacidade** guia claro a **remover informações pessoais das propriedades do arquivo em Salvar** caixa de seleção.  
  
4.  Salve a pasta de trabalho e fechar o Excel.  
  
### <a name="cannot-open-a-project-after-migration"></a>Não é possível abrir um projeto após a migração  
 Depois de um escritório solução for migrada para o Microsoft Office 2010, o projeto não pode ser aberto em um computador de desenvolvimento com apenas o 2007 Microsoft Office system instalado. Você pode ver os erros a seguir.  
  
 "Um ou mais projetos na solução não foram carregados corretamente. Consulte a janela de saída para obter detalhes."  
  
 "Não é possível criar o projeto porque o aplicativo associado a este tipo de projeto não está instalado neste computador. Você deve instalar o aplicativo do Microsoft Office que está associado este tipo de projeto."  
  
 Para resolver esse problema, edite o *. vbproj* ou *csproj* arquivo. Para um projeto do Word, substitua HostPackage = "{763FDC83-64E5-4651-AC9B-28C4FEB985A1}" com HostPackage = "{6CE98B71-D55A-4305-87A8-0D6E368D9600}". Para um projeto do Excel, substitua HostPackage = "{B284B16A-C42C-4438-BDCD-B72F4AC43CFB}" com HostPackage = "{825100CF-0BA7-47EA-A084-DCF3308DAF74}". Para um projeto do Outlook, substitua HostPackage = "{D2B20FF5-A6E5-47E1-90E8-463C6860CB05}" com HostPackage = "{20A848B8-E01F-4801-962E-25DB0FF57389}".  
  
 Como alternativa, certifique-se de que projetos migrados sejam abertos somente em computadores de desenvolvimento com o Microsoft Office 2010 já está instalado.  
  
### <a name="errors-in-upgraded-office-2003-document-level-projects-that-contain-windows-forms-controls"></a>Erros em projetos de nível de documento do Office 2003 atualizados que contêm controles dos Windows Forms  
 Se você atualiza um projeto de nível de documento do Microsoft Office 2003 e o documento contém controles dos Windows Forms, o projeto atualizado pode ter erros de compilação ou tempo de execução. Para evitar esse problema, instale o Visual Studio 2005 Tools para Office Second Edition Runtime no computador de desenvolvimento antes de atualizar o projeto. Esta versão do tempo de execução está disponível como um pacote redistribuível do Microsoft Download Center em [Microsoft Visual Studio 2005 Tools for Office Second Edition Runtime (VSTO 2005 SE) (x86)](http://go.microsoft.com/fwlink/?linkid=49612).  
  
 Depois de concluir a atualização do projeto, você pode desinstalar o Visual Studio 2005 Tools para Office Second Edition Runtime do computador de desenvolvimento, se ele não está sendo usado por outras soluções do Office.  
  
##  <a name="designers"></a> Usar os designers  
 Você pode encontrar os seguintes erros ao trabalhar com o documento, pasta de trabalho ou designer de planilha em projetos de nível de documento.  
  
### <a name="designer-failed-to-load-correctly"></a>Designer não pôde carregar corretamente  
 Visual Studio não é possível abrir o designer nos seguintes casos:  
  
-   Excel ou Word já está aberto e está exibindo uma caixa de diálogo modal. Para abrir o designer, verifique se Excel ou Word tem uma caixa de diálogo Abrir e fechar as caixas de diálogo modal aberta. Se não houver nenhuma caixa de diálogo modal aberta, pode haver alguma outra ação necessária antes de Excel ou Word responde.  
  
-   O projeto está atualmente em depuração. Para abrir o designer, pare ou concluir a depuração.  
  
-   Um Add-in do VSTO do Excel que está instalado no computador de desenvolvimento está exibindo uma caixa de diálogo quando o Excel é iniciado. Para criar um projeto de nível de documento do Excel, primeiro você deve desabilitar o suplemento do VSTO.  
  
### <a name="controls-appear-as-black-rectangles-on-the-document-or-worksheet"></a>Controles são exibidos como retângulos pretos no documento ou planilha  
 Se você agrupar controles em um documento ou planilha, o Visual Studio não reconheça os controles. Controles agrupados não podem ser acessados na **propriedades** janela e eles são exibidos como retângulos pretos no documento ou planilha. Você deve desagrupar os controles para restaurar a funcionalidade.  
  
### <a name="controls-on-a-word-template-are-not-visible-in-visual-studio"></a>Controles em um modelo do Word não são visíveis no Visual Studio  
 Se você abrir um modelo do Word no designer do Visual Studio, os controles no modelo que não estão em conformidade com o texto podem não ser visíveis. Isso ocorre porque o Visual Studio abre modelos do Word na **Normal** modo de exibição. Para exibir os controles, clique o **modo de exibição** , aponte para **modo de exibição do Microsoft Office Word** e, em seguida, clique em **Layout de impressão**.  
  
### <a name="insert-clip-art-command-does-nothing-in-the-visual-studio-designer"></a>Inserir clip art comando não faça nada no designer do Visual Studio  
 Quando o Excel ou Word estiver aberto no designer do Visual Studio, clicando na **Clip-Art** botão a **ilustrações** guia na faixa de opções não abre o **Clip-Art** painel de tarefas. Para adicionar o clip-art, você deve abrir a cópia da pasta de trabalho ou documento que está na pasta do projeto principal (não a cópia que está na *\bin* pasta) fora do Visual Studio, adicionar o clip-art e, em seguida, salve a pasta de trabalho ou o documento.  
  
##  <a name="code"></a> Escrever código  
 Você pode encontrar os seguintes erros ao escrever código em projetos do Office.  
  
### <a name="some-events-of-office-objects-are-not-accessible-when-using-c"></a>Alguns eventos de objetos do Office não são acessíveis ao usar c#  
 Em alguns casos, você poderá ver um erro do compilador semelhante à seguinte quando você tenta acessar um evento específico de uma instância de um tipo de assembly de interoperabilidade primária (PIA) em um projeto do Visual c# do Office.  
  
 "Ambiguidade entre 'Microsoft.Office.Interop.Excel._Application.NewWorkbook' e 'Microsoft.Office.Interop.Excel.AppEvents_Event.NewWorkbook'"  
  
 Esse erro significa que você está tentando acessar um evento que tem o mesmo nome que outra propriedade ou método do objeto. Para acessar o evento, você deve converter o objeto para seus *interface de eventos*.  
  
 Tipos de PIA do Office que têm eventos implementam duas interfaces: uma interface de núcleo com todas as propriedades e métodos e uma interface de eventos que contém os eventos que são expostos pelo objeto. Essas interfaces de evento usam a convenção de nomenclatura *objectname*eventos*n*de evento, como <xref:Microsoft.Office.Interop.Excel.AppEvents_Event> e <xref:Microsoft.Office.Interop.Word.ApplicationEvents2_Event>. Se você não pode acessar um evento que você espera encontrar em um objeto, converta o objeto à sua interface do evento.  
  
 Por exemplo, <xref:Microsoft.Office.Interop.Excel.Application> objetos têm uma <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.NewWorkbook> eventos e um <xref:Microsoft.Office.Interop.Excel._Application.NewWorkbook%2A> propriedade. Para lidar com o <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.NewWorkbook> convertido de evento, o <xref:Microsoft.Office.Interop.Excel.Application> para o <xref:Microsoft.Office.Interop.Excel.AppEvents_Event> interface. O exemplo de código a seguir demonstra como fazer isso em um projeto de nível de documento para Excel.  
  
 [!code-csharp[Trin_VstcoreTroubleshootingExcel#1](../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingExcelCS/ThisWorkbook.cs#1)]  
  
 Para obter mais informações sobre interfaces de evento nos PIAs do Office, consulte [visão geral de classes e interfaces em assemblies de interoperabilidade primários do Office](/previous-versions/office/office-12//ms247299(v=office.12)).  
  
### <a name="cannot-reference-office-pia-classes-in-projects-that-target-the-includenetv40shortsharepointincludesnet-v40-short-mdmd-or-the-includenetv45vstoincludesnet-v45-mdmd"></a>Não é referência de PIA Office classes em projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]  
 Em projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)], código que faz referência a uma classe que é definida em um PIA do Office não será compilado por padrão. Classes de PIAs usam a convenção de nomenclatura *objectname*classe, como <xref:Microsoft.Office.Interop.Word.DocumentClass> e <xref:Microsoft.Office.Interop.Excel.WorkbookClass>. Por exemplo, o código a seguir de um projeto de suplemento do VSTO do Word não será compilado.  
  
```vb  
Dim document As Word.DocumentClass = Globals.ThisAddIn.Application.ActiveDocument  
```  
  
```csharp  
Word.DocumentClass document = (Word.DocumentClass) Globals.ThisAddIn.Application.ActiveDocument;  
```  
  
 Esse código resulta em erros de compilação a seguir:  
  
- Visual Basic: "referência à classe 'DocumentClass' não é permitida quando seu assembly é vinculado usando o modo de não PIA."  
  
- Visual c#: "tipo de interoperabilidade 'Microsoft.Office.Interop.Word.DocumentClass' não pode ser inserido. Use a interface aplicável."  
  
  Para resolver esse erro, modifique o código para fazer referência a interface correspondente em vez disso. Por exemplo, em vez de referência de um <xref:Microsoft.Office.Interop.Word.DocumentClass> de objeto, fazer referência a uma instância da <xref:Microsoft.Office.Interop.Word.Document> interface em vez disso.  
  
```vb  
Dim document As Word.Document = Globals.ThisAddIn.Application.ActiveDocument  
```  
  
```csharp  
Word.Document document = Globals.ThisAddIn.Application.ActiveDocument;  
```  
  
 Projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)], automaticamente inserir todos os tipos de interoperabilidade de PIAs do Office por padrão. Esse erro de compilação ocorre porque o recurso de tipos de interoperabilidade inseridos só funciona com interfaces, classes não. Para obter mais informações sobre interfaces e classes nos PIAs do Office, consulte [visão geral de classes e interfaces em assemblies de interoperabilidade primários do Office](http://go.microsoft.com/fwlink/?LinkId=189592). Para obter mais informações sobre o recurso de tipos de interoperabilidade inseridos em projetos do Office, consulte [Design e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md).  
  
### <a name="references-to-office-classes-are-not-recognized"></a>Referências a classes do Office não são reconhecidas  
 Alguns nomes de classe, por exemplo, aplicativo, estão em vários namespaces, como <xref:Microsoft.Office.Interop.Word> e <xref:System.Windows.Forms>. Por esse motivo, o **importações**/**usando** instrução na parte superior dos modelos de projeto inclui um tipo de taquigrafia qualificando constante, por exemplo:  
  
 [!code-csharp[Trin_VstcoreTroubleshootingWord#2](../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingWordCS/ThisDocument.cs#2)]
 [!code-vb[Trin_VstcoreTroubleshootingWord#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreTroubleshootingWordVB/ThisDocument.vb#2)]  
  
 Esse uso do **importações**/**usando** instrução requer que você diferenciar referências a classes do Office com o qualificador do Word ou Excel, por exemplo:  
  
 [!code-csharp[Trin_VstcoreTroubleshootingWord#3](../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingWordCS/ThisDocument.cs#3)]
 [!code-vb[Trin_VstcoreTroubleshootingWord#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreTroubleshootingWordVB/ThisDocument.vb#3)]  
  
 Se você usar uma declaração não qualificada, por exemplo, você obterá erros:  
  
 [!code-csharp[Trin_VstcoreTroubleshootingWord#4](../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingWordCS/ThisDocument.cs#4)]
 [!code-vb[Trin_VstcoreTroubleshootingWord#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreTroubleshootingWordVB/ThisDocument.vb#4)]  
  
 Mesmo que você importou o namespace do Word ou Excel e ter acesso a todas as classes dentro dele, você deve qualificar totalmente todos os tipos com o Word ou Excel para remover a ambiguidade de namespace.  
  
##  <a name="building"></a> Criar projetos  
 Você pode encontrar os seguintes erros ao compilar projetos do Office.  
  
### <a name="cannot-build-a-document-level-project-that-is-based-on-a-document-with-restricted-permissions"></a>Não é possível compilar um projeto de nível de documento que se baseia em um documento com permissões restritas  
 Visual Studio não pode compilar projetos em nível de documento, se o documento possui permissões restritas. Se seu projeto contém um documento que tem permissões restritas, o projeto não será compilado e você receberá a seguinte mensagem na **Error List** janela.  
  
 "Falha ao adicionar a personalização".  
  
 Se você quiser incluir um documento que tem permissões restritas, use um documento irrestrito enquanto você desenvolve e compila a solução. Em seguida, aplique as permissões restritas ao documento no local de publicação, depois de publicar a solução.  
  
### <a name="compiler-errors-occur-after-a-namedrange-control-is-deleted"></a>Erros de compilador ocorrem depois que um controle NamedRange é excluído  
 Se você excluir um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle de uma planilha que não seja a planilha ativa no designer, o código gerado automaticamente não pode ser removido de seu projeto e podem ocorrer erros de compilador. Para garantir que o código é removido, você sempre deve selecionar a planilha que contém o <xref:Microsoft.Office.Tools.Excel.NamedRange> controle para torná-lo a planilha ativa antes de excluir o controle. Se o código gerado automaticamente não será excluído quando você excluir o controle, você pode fazer com que o designer a fim de excluir o código de ativação a planilha e fazendo uma alteração para que a planilha fica marcada como modificada. Quando você recompilar o projeto, o código é removido.  
  
##  <a name="debugging"></a> Depurar projetos  
 Você pode encontrar os seguintes erros quando você depurar projetos do Office.  
  
### <a name="prompt-to-uninstall-appears-when-you-publish-and-install-a-solution-on-the-development-computer"></a>Prompt para desinstalar aparece quando você publica e instala uma solução no computador de desenvolvimento  
 Quando você depura uma solução do Office, você poderá ver o erro a seguir.  
  
 "A personalização não pode ser instalada porque outra versão instalada no momento e não pode ser atualizada a partir deste local."  
  
 Esse erro indica que anteriormente publicados e instalado a solução do Office no seu computador de desenvolvimento. Para impedir que a mensagem que aparece, desinstale a solução da lista de programas instalados no computador antes de depurar a solução. Como alternativa, você pode criar outra conta de usuário no computador de desenvolvimento para testar a instalação da solução publicada.  
  
### <a name="document-level-projects-created-at-unc-network-locations-do-not-run-from-visual-studio"></a>Projetos de nível de documento criados nos locais de rede UNC não são executados no Visual Studio  
 Se você criar um projeto de nível de documento para Excel ou Word em um local de rede UNC, você deve adicionar o local do documento à lista de locais confiáveis no Excel ou Word. Caso contrário, a personalização não será carregada quando você tentar executar ou depurar o projeto no Visual Studio. Para obter mais informações sobre locais confiáveis, consulte [conceder confiança a documentos](../vsto/granting-trust-to-documents.md).  
  
### <a name="threads-are-not-stopped-correctly-after-debugging"></a>Threads não forem interrompidos corretamente após a depuração  
 Projetos do Office no Visual Studio siga um thread que permite que o depurador fechar o programa corretamente convenção de nomenclatura. Se você criar threads em sua solução, você deve nomear cada thread com o prefixo VSTA_ para garantir que esses threads estão sendo tratados corretamente quando você interrompe a depuração. Por exemplo, você pode definir as `Name` propriedade de um thread que aguarda um evento de rede **VSTA_NetworkListener**.  
  
### <a name="cannot-run-or-debug-any-office-solution-on-the-development-computer"></a>Não é possível executar ou depurar qualquer solução do Office no computador de desenvolvimento  
 Se você não pode executar ou desenvolver um projeto do Office no seu computador de desenvolvimento, você poderá ver a seguinte mensagem de erro.  
  
 "Personalização não pôde ser carregada porque o domínio do aplicativo não pôde ser criado."  
  
 O Visual Studio usa Fusion, o carregador de assembly do .NET Framework, para armazenar em cache os assemblies antes de carregar soluções do Office. Certifique-se de que o Visual Studio pode gravar no cache de fusão e tente novamente. Para obter mais informações, consulte [assemblies de cópia de sombra](/dotnet/framework/app-domains/shadow-copy-assemblies).  
  
### <a name="error-when-stopping-the-debugger-in-a-document-level-project-after-using-edit-and-continue"></a>Erro ao interromper o depurador em um projeto de nível de documento depois de usar Editar e continuar  
 Se você usar **edite** e **continuar** para fazer alterações ao código em um projeto de nível de documento para o Excel ou Word enquanto o projeto estiver no modo de interrupção, você poderá ver uma caixa de diálogo com a seguinte mensagem de erro se você subsequentemente, pare o depurador.  
  
 "Encerrar o processo em seu estado atual pode causar a resultados indesejados, incluindo a perda de dados e instabilidade do sistema".  
  
 Se você clicar **Yes** ou **não** na caixa de diálogo, o Visual Studio encerra o processo de Excel ou Word e interrompe o depurador. Para interromper a depuração do projeto sem exibir essa caixa de diálogo, saia do Excel ou Word diretamente em vez de interromper o depurador do Visual Studio.  
  
## <a name="see-also"></a>Consulte também  
 [Solucionar problemas de soluções do Office](../vsto/troubleshooting-office-solutions.md)   
 [Solucionar problemas de segurança de solução do Office](../vsto/troubleshooting-office-solution-security.md)   
 [Solucionar problemas de implantação de solução do Office](../vsto/troubleshooting-office-solution-deployment.md)  
  
  