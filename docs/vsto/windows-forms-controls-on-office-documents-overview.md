---
title: Controles de formulários do Windows na visão geral de documentos do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- old data showing in error [Office development in Visual Studio]
- Windows Forms controls [Office development in Visual Studio], Word
- Windows Forms controls [Office development in Visual Studio], adding
- Windows Forms controls [Office development in Visual Studio], arranging
- data [Office development in Visual Studio], old data showing in error
- user controls [Office development in Visual Studio], Windows Forms
- Windows Forms controls [Office development in Visual Studio]
- Windows Forms controls [Office development in Visual Studio], removing
- application development [Office development in Visual Studio], Windows Forms controls
- controls [Office development in Visual Studio], Windows Forms controls
- Office [Office development in Visual Studio], Windows Forms controls
- Office documents [Office development in Visual Studio, controls
- documents [Office development in Visual Studio], Windows Forms controls
- document-level customizations [Office development in Visual Studio], Windows Forms controls
- Windows Forms controls [Office development in Visual Studio], about Windows Forms controls
- Office applications [Office development in Visual Studio], Windows Forms
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 51c671a583e4e96b51ae6627de1fce738696fe22
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49892773"
---
# <a name="windows-forms-controls-on-office-documents-overview"></a>Controles de formulários do Windows na visão geral de documentos do Office
  Controles dos Windows Forms são objetos que os usuários podem interagir com a inserção ou manipular dados. Nos projetos em nível de documento do Microsoft Office Excel e Microsoft Office Word, você pode adicionar controles de formulários do Windows para o documento ou pasta de trabalho em seu projeto em tempo de design, ou você pode adicionar programaticamente esses controles em tempo de execução. Você pode adicionar esses controles programaticamente para qualquer documento aberto ou a planilha em tempo de execução em um suplemento do VSTO para Excel ou Word.  
  
 Para obter mais informações, consulte [como: adicionar formulários do Windows controla a documentos do Office](../vsto/how-to-add-windows-forms-controls-to-office-documents.md).  
  
 [!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]  
  
## <a name="use-windows-forms-controls"></a>Use os controles dos Windows Forms  
 Você pode adicionar controles dos Windows Forms a documentos e elementos de (UI) de interface de usuário personalizável, incluindo o Windows Forms, painéis de tarefas personalizados e painéis de ações. Controles de formulários do Windows geralmente têm o mesmo comportamento em documentos, como nesses outros elementos de interface do usuário, mas existem algumas diferenças. Para obter informações, consulte [limitações dos Windows Forms a controles em documentos do Office](../vsto/limitations-of-windows-forms-controls-on-office-documents.md).  
  
 A decisão se deseja adicionar controles dos Windows Forms a um documento ou outro elemento da interface do usuário depende de vários fatores. Ao projetar a interface do usuário da sua solução, considere os usos dos controles de formulários do Windows conforme descrito na tabela a seguir.  
  
 Em um documento.  
 -   Quando você deseja exibir os controles de 100% do tempo.  
  
- Quando você deseja que os usuários insiram dados diretamente no documento, por exemplo, em documentos com base em formulários em que a superfície de edição está bloqueado.  
  
- Quando você deseja que os controles para exibir em linha com os dados no documento. Por exemplo, se você estiver adicionando botões para cada linha de um objeto de lista, você deseja que eles alinhada com cada item de lista.  
  
  No painel de ações ou um painel de tarefas personalizado.  
  -   Quando você deseja fornecer informações contextuais para o usuário.  
  
- Quando você quiser apenas os resultados sejam exibidos no documento e não a controles de consulta e dados.  
  
- Quando você deseja garantir que os controles não são impressas no documento.  
  
- Quando você deseja garantir que os controles não interfiram ao modo de exibição do documento.  
  
  Em um formulário do Windows.  
  -   Quando você deseja controlar o tamanho da interface do usuário.  
  
- Quando você quiser impedir que os usuários ocultem ou excluindo os controles.  
  
- Quando você deseja obter entradas do usuário e impedir que o usuário fazer qualquer coisa no documento até que a entrada é recebida.  
  
## <a name="add-windows-forms-controls-programmatically"></a>Adicionar controles dos Windows Forms de forma programática  
 Você pode adicionar controles dos Windows Forms a documentos do Word e planilhas do Excel em tempo de execução. O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] fornece métodos auxiliares para adicionar os controles Windows Forms mais comuns. Esses métodos auxiliares permitem que você adicionar controles ao seu documento do Office e o acesso a funcionalidade de controle Windows Forms combinada e funcionalidade desses controles relacionados ao Office rapidamente.  
  
 Para obter mais informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
## <a name="use-windows-forms-controls-in-document-level-projects"></a>Usar controles dos Windows Forms em projetos de nível de documento  
 Alguns aspectos do uso de controles Windows Forms em documentos são exclusivos para projetos de nível de documento, que permitem projetar a interface do usuário do seu documento usando o designer do Visual Studio.  
  
### <a name="create-custom-user-controls"></a>Criar controles de usuário personalizada  
 Você pode adicionar um controle de usuário ao seu projeto e, em seguida, adicioná-lo para o **caixa de ferramentas**. Em seguida, você pode arrastar o controle de usuário diretamente para o documento da mesma maneira que adicionaria um controle dos Windows Forms ao documento. Há algumas coisas para ter em mente ao criar controles de usuário:  
  
-   Não crie uma **lacrado** controle de usuário. Quando você arrasta o controle ao documento, o Visual Studio gera uma classe wrapper derivada de controle do usuário para estendê-lo e dar suporte a seu uso no documento. Se o controle de usuário estiver **lacrado**, Visual Studio não é possível gerar a classe de wrapper.  
  
-   Controles de usuário devem ter o <xref:System.Runtime.InteropServices.ComVisibleAttribute> atributo definido como **verdadeiro**. Controles de usuário criados dentro de um projeto do Office têm esse atributo definido como **verdadeira** por padrão, mas o usuário controles que fazem parte dos projetos externos podem não ter esse atributo definido como **verdadeiro**.  
  
-   Depois de adicionar um controle de usuário para o documento, não renomeie ou exclua o <xref:System.Windows.Forms.UserControl> classe do projeto. Se você precisar alterar o nome de um controle de usuário, você deve primeiro excluí-la do documento e, em seguida, adicioná-lo novamente depois que o nome foi alterado.  
  
### <a name="arrange-controls-at-design-time"></a>Organizar controles em tempo de design  
 Se você adicionar vários controles a documentos do Word e Excel no tempo de design, você pode configurar rapidamente o alinhamento de todos os controles selecionados usando o **Microsoft Office Word** e **Microsoft Office Excel**barras de ferramentas do Visual Studio. Essas barras de ferramentas estão disponíveis somente quando um documento ou planilha é aberta no designer.  
  
 Quando você seleciona vários controles no designer, você pode usar os botões a seguir nessas barras de ferramentas para organizar os controles:  
  
-   **Alinhar à esquerda**  
  
-   **Alinhar centros**  
  
-   **Alinhar os direitos**  
  
-   **Alinhar partes superiores**  
  
-   **Alinhar meios**  
  
-   **Alinhar partes inferiores**  
  
-   **Igualar espaçamento Horizontal**  
  
-   **Igualar espaçamento Vertical**  
  
> [!NOTE]  
>  Em projetos do Word, esses botões são habilitados somente se os controles selecionados não estiverem alinhado com o texto. Por padrão, os controles que você adiciona ao documento em tempo de design estão de acordo com o texto.  
  
### <a name="prevent-old-data-from-appearing-in-excel-workbooks-during-loading"></a>Impedir que os dados antigos que aparecem em pastas de trabalho do Excel durante o carregamento  
 Quando você adiciona controles dos Windows Forms a documentos ou planilhas em tempo de design, os controles permanecem no documento quando o usuário fecha o documento. Também são chamados de controles adicionados em tempo de design *controles estáticos*.  
  
 Quando uma pasta de trabalho do Excel que contém controles estáticos é aberta, a pasta de trabalho exibe um bitmap do controle em um controle ActiveX, até que o código de personalização é executado e carrega o controle real. O Excel cria esse bitmap e armazena-o na pasta de trabalho sempre que a pasta de trabalho é salvo. O bitmap mostra o controle como ele apareceu a última vez em que a pasta de trabalho foi salvo, incluindo quaisquer dados que o controle estava exibindo. Para obter mais informações sobre o controle ActiveX que contém controles dos Windows Forms e bitmaps, consulte [limitações dos Windows Forms a controles em documentos do Office](../vsto/limitations-of-windows-forms-controls-on-office-documents.md).  
  
 Em determinadas condições, o código não é carregado e apenas o bitmap é exibido, como quando o usuário abre a pasta de trabalho no modo de design. Além disso, se o usuário abre a pasta de trabalho em um computador que não tenha o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] instalado, a personalização não pode executar para carregar os controles e, portanto, somente o bitmap do controle está visível. Você deve sempre remover informações pessoais dos controles em pastas de trabalho antes de salvar a pasta de trabalho e enviá-la para outro usuário para garantir que suas informações pessoais não são divulgadas acidentalmente.  
  
### <a name="match-control-size-to-cell-size-on-an-excel-worksheet"></a>Tamanho do controle de correspondência para o tamanho da célula em uma planilha do Excel  
 Você pode definir o controle a ser redimensionado automaticamente quando o tamanho da célula pai é alterado. Para obter mais informações, consulte [como: redimensionar controles dentro de células da planilha](../vsto/how-to-resize-controls-within-worksheet-cells.md).  
  
### <a name="add-components-that-are-shared-by-all-worksheets"></a>Adicionar componentes que são compartilhados por todas as planilhas  
 Você pode adicionar componentes que você deseja compartilhar entre todas as planilhas, como um <xref:System.Data.DataSet>, para o Designer de pasta de trabalho, em vez de para planilhas. O componente será exibido na bandeja de componentes.  
  
### <a name="formula-for-embedding-controls-on-an-excel-worksheet"></a>Fórmula para a inserção de controles em uma planilha do Excel  
 Quando você seleciona um controle no Excel, você verá **=EMBED("WinForms.Control.Host","")** na **barra de fórmulas**. Esse texto é necessário e não deve ser excluído.  
  
### <a name="layout-style-of-controls-on-a-word-document"></a>Estilo de layout de controles em um documento do Word  
 Quando você adiciona um controle para o documento do Word em um projeto de nível de documento usando o designer do Visual Studio, o controle é adicionado em linha com texto. Para alterar o estilo de layout do controle, clique com botão direito do controle e, em seguida, clique em **Formatar controle**. Selecione um estilo de quebra na **Layout** página do **Formatar objeto** caixa de diálogo.  
  
 Quando você adiciona um controle a um documento do Word em tempo de execução, você pode especificar o estilo de layout do novo controle usando diferentes `Add` \< *classe de controle*> sobrecargas do método da <xref:Microsoft.Office.Tools.Word.ControlCollection> classe:  
  
- Para adicionar o controle de acordo com o texto, use uma sobrecarga que aceita um <xref:Microsoft.Office.Interop.Word.Range> que especifica o local do controle.  
  
- Para adicionar o controle como uma forma flutuante, use uma sobrecarga que aceita as coordenadas esquerdas e superior do controle.  
  
  Para obter mais informações, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).  
  
  Se você abrir um modelo do Word no designer do Visual Studio, os controles não embutido no modelo podem não estar visíveis porque o Visual Studio abre o modelo no **Normal** modo de exibição. Para exibir os controles, altere a exibição para **Layout de impressão**.  
  
### <a name="controls-outside-the-main-document-body"></a>Controles fora do corpo do documento principal  
 Não há suporte para controles dos Windows Forms ou dentro de um subdocumento dentro de um cabeçalho ou rodapé.  
  
### <a name="add-components-at-design-time"></a>Adicionar componentes em tempo de design  
 Determinados controles ou componentes não são visíveis no documento e em vez disso, são exibidos em uma bandeja de componentes. Visual Studio fornece uma bandeja de componentes para cada janela de documento. Bandeja de componentes é exibida na tela somente se existirem de componentes no documento.  
  
## <a name="see-also"></a>Consulte também  
 [Controles em documentos do Office](../vsto/controls-on-office-documents.md)   
 [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Visão geral do painel de ações](../vsto/actions-pane-overview.md)   
 [Controles dos Windows Forms](/dotnet/framework/winforms/controls/index)   
 [Limitações de controles de Windows Forms em documentos do Office](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)   
 [Como: adicionar controles dos Windows Forms a documentos do Office](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)   
 [Como: redimensionar controles dentro de células da planilha](../vsto/how-to-resize-controls-within-worksheet-cells.md)   
 [Como: ocultar controles em planilhas durante a impressão](../vsto/how-to-hide-controls-on-worksheets-when-printing.md)   
 [Passo a passo: Alterar a formatação da planilha usando controles CheckBox](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)   
 [Passo a passo: Alterar a formatação do documento usando controles CheckBox](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)   
 [Passo a passo: Exibir texto em uma caixa de texto em uma planilha usando um botão](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)   
 [Passo a passo: Exibir texto em uma caixa de texto em um documento usando um botão](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md)   
 [Limitações de controles de Windows Forms em documentos do Office](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)   
 [Explicação passo a passo: Um gráfico em um documento usando botões de opção de atualização](../vsto/walkthrough-updating-a-chart-in-a-document-using-radio-buttons.md)   
 [Explicação passo a passo: Um gráfico em uma planilha usando botões de opção de atualização](../vsto/walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons.md)  
  
  