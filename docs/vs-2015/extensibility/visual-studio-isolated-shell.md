---
title: Shell isolado do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Shell [Visual Studio], shell-based applications%2C isolated mode
- Visual Studio shell, isolated mode
- isolated shell-based applications [Visual Studio]
- Visual Studio shell, shell-based applications%2C isolated mode
- Shell [Visual Studio], isolated mode
ms.assetid: d2620e71-be9e-44c9-b5b7-03a4c8d9cf0b
caps.latest.revision: 36
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: d7fcb0a838f2849ab74d202785709164ec5af6d7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51740662"
---
# <a name="visual-studio-isolated-shell"></a>Shell isolado do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O shell isolado do Visual Studio permite que você crie aplicativos autônomos que podem ser executados lado a lado com outras versões do Visual Studio. Ele é usado principalmente para hospedar ferramentas especializadas que podem usar os serviços do Visual Studio, mas também ter uma aparência personalizada e identidade visual. Recursos do Visual Studio e grupos de comando de menu podem ser facilmente ativados e desativada. Aplicativo títulos, ícones de aplicativo e telas de abertura são totalmente personalizáveis. Para obter uma lista de recursos personalizáveis, consulte [personalizar o Shell isolado](../extensibility/customizing-the-isolated-shell.md).  
  
 Para trabalhar com um projeto do shell isolado, você deve instalar o SDK do Visual Studio. A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
 Para criar um aplicativo de shell isolado, comece com um projeto do Visual Studio Shell isolado. Este projeto contém tudo o que você precisa para desenvolver e testar seu próprio aplicativo de shell isolado. Quando você estiver pronto para escrever o programa de instalação que implanta seu aplicativo, você deve obter o pacote redistribuível do shell isolado do [pacote redistribuível do Microsoft Visual Studio Shell (isolado)](http://go.microsoft.com/fwlink/?LinkId=616022).  
  
> [!NOTE]
>  Antes de poder acessar o pacote redistribuível do shell isolado, você será solicitado a preencher uma breve pesquisa do cliente.  Depois de preencher a pesquisa, você será direcionado para uma página do Visual Studio Connect com links de download do pacote redistribuível.  Você pode encontrar os links de download em visitas subsequentes ao site do Visual Studio conectar-se na **programas &#124; VISUAL STUDIO 2015 integrado e ISOLADO SHELL** guia.  
  
> [!NOTE]
>  Para obter mais informações sobre como implantar um aplicativo de baseados em shell isolado, consulte [instruções passo a passo: Criando um aplicativo básico de Shell isolado](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md).  
  
## <a name="working-with-the-isolated-shell"></a>Trabalhando com o shell isolado  
 Um aplicativo de shell isolado do Visual Studio tem acesso completo aos serviços do Visual Studio e oferece suporte à personalização especial e identidade visual. Há várias maneiras que você pode personalizar um aplicativo de shell isolado:  
  
- Você pode usar os VSPackages e Managed Extensibility Framework (MEF) partes de componentes para estender um aplicativo de shell isolado, assim como você usaria em qualquer outra extensão do Visual Studio. Para obter mais informações, consulte [estender o Shell isolado](../extensibility/extending-the-isolated-shell.md).  
  
- Para tornar os recursos do Visual Studio e grupos de comando de menu disponíveis ou não disponíveis, atualize o arquivo. VSCT no projeto de (UI) de interface do usuário do aplicativo.  
  
- Para remover **opções** páginas ou outros componentes do shell do Visual Studio do aplicativo, atualize o arquivo. pkgundef do aplicativo.  
  
- Para modificar o comportamento do shell ou outros aspectos da aparência, atualize o arquivo. pkgdef do aplicativo.  
  
- Alguns aspectos do shell também podem ser especificados quando o aplicativo é iniciado. Para fazer isso, atualize os parâmetros na chamada para o ponto de entrada do início do appenvstub.dll.  
  
  Para obter mais informações sobre os diferentes elementos que você pode personalizar, veja [elementos do Shell isolado](../extensibility/elements-of-the-isolated-shell.md).  
  
## <a name="standard-features-of-the-isolated-shell"></a>Recursos padrão do Shell isolado  
 Os seguintes recursos são padrão para todas as edições do Visual Studio.  
  
|Categoria de Recurso|Recurso|  
|----------------------|-------------|  
|Recursos do IDE|Configurações de importação/exportação<br /><br /> Instalador de controle de caixa de ferramentas<br /><br /> Lista de tarefas & lista de erros<br /><br /> Janela Saída<br /><br /> Start Page<br /><br /> Janela Propriedades<br /><br /> Caixa de Ferramentas<br /><br /> Gerenciador de Soluções<br /><br /> Janela de Indicadores<br /><br /> Exibição de Classe<br /><br /> Pesquisador de Objetos<br /><br /> Janela Comando<br /><br /> Estrutura de Tópicos do Documento<br /><br /> Exibição de recurso<br /><br /> Ferramenta externa<br /><br /> Windows Communication Foundation (WCF) adicionar referência de serviço<br /><br /> Suporte a LINQ (consulta) integrada de linguagem|  
|Designer/Editor|Ferramentas (localização unificada, definição de fonte, herança) de navegação de código<br /><br /> IntelliSense<br /><br /> Marcas inteligentes<br /><br /> Gerenciador de Snippets de Código<br /><br /> Snippets de código<br /><br /> Refatoração<br /><br /> Listagem bonita<br /><br /> Filtragem IntelliSense<br /><br /> Janela de definição de código<br /><br /> Designer de aplicativos<br /><br /> Designer de Formulários do Windows<br /><br /> Designer do Windows Presentation Foundation (WPF)|  
|Depuração|Avaliador de expressão c#<br /><br /> Depuração local<br /><br /> Depuração gerenciada<br /><br /> Editar e continuar<br /><br /> Depuração de thread cruzado<br /><br /> Visualizações<br /><br /> DataTips<br /><br /> Depuração nativa<br /><br /> Depuração de script<br /><br /> Depuração Interop<br /><br /> Depuração Just-in-time (JIT)<br /><br /> Depuração de vários processos<br /><br /> Depuração de XSLT<br /><br /> Anexar ao processo local<br /><br /> Pontos de rastreamento<br /><br /> Restrições de ponto de interrupção|  
|Dados|Gerenciador de servidores (simplificado – apenas os dados)<br /><br /> Associar dados a dados local (. Arquivos MDF ou. MDB)<br /><br /> Associação de dados ao objeto<br /><br /> Associação de dados ao serviço Web<br /><br /> Conjunto completo de controles de dados<br /><br /> Editor de XML<br /><br /> Associação de dados ao servidor de banco de dados local<br /><br /> janela Fontes de Dados|  
|Web|Editor de HTML<br /><br /> Navegador da Web<br /><br /> O Web Forms designer<br /><br /> Projeto de Site<br /><br /> Projeto de aplicativo Web|  
|Extensibilidade|Consome componentes VSPackages e MEF|  
  
## <a name="see-also"></a>Consulte também  
 [Shell (isolado ou integrado)](../extensibility/shell-isolated-or-integrated.md)

