---
title: Visual Studio Shell (integrado) | Microsoft Docs
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
- Visual Studio shell, integrated mode features
- Shell [Visual Studio], integrated mode features
ms.assetid: 0b40d495-f17f-4bb9-ace8-b365a7172784
caps.latest.revision: 26
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 3eb0c8dd0588e1af9b3aad500c8bc9f899b44513
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51765275"
---
# <a name="visual-studio-shell-integrated"></a>Visual Studio Shell (integrado)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O shell integrado do Visual Studio inclui o ambiente de desenvolvimento integrado (IDE), o depurador e a integração de controle do código-fonte. Nenhuma linguagem de programação é incluída. No entanto, o shell integrado fornecem uma estrutura que permite que você adicione linguagens de programação.  
  
 O shell integrado do Visual Studio é, na verdade, uma combinação do shell isolado do Visual Studio com uma instalação adicional que incluem componentes específicos do shell integrado.  Seu aplicativo de shell integrado deve incluir os dois o shell isolado pacote redistribuível do [pacote redistribuível do Microsoft Visual Studio Shell (isolado)](http://go.microsoft.com/fwlink/?LinkId=616022) , bem como o pacote redistribuível do shell integrado partir [Microsoft Visual Studio (integrado) pacote redistribuível do Shell](http://go.microsoft.com/fwlink/?LinkId=616021).  
  
> [!NOTE]
>  Antes de poder acessar os pacotes redistribuíveis do shell isolado e integrado, será solicitado que você preencha uma breve pesquisa do cliente.  Depois de preencher a pesquisa, você será direcionado para uma página do Visual Studio Connect com links de download do pacote redistribuível.  Você pode encontrar os links de download em visitas subsequentes ao site do Visual Studio conectar-se na **programas &#124; VISUAL STUDIO 2015 integrado e ISOLADO SHELL** guia.  
  
 Se você instalar o aplicativo de shell integrado no mesmo computador como uma versão completa do Visual Studio, componentes do seu aplicativo serão integrados diretamente no Visual Studio.  
  
## <a name="features-in-the-integrated-shell"></a>Recursos do Shell integrado  
  
|||  
|-|-|  
|Área de recursos|Recurso|  
|Suporte ao idioma|– None|  
|IDE|<ul><li>Configurações<br /><br /> <ul><li>Criar configurações</li><li>Importar e exportar configurações</li><li>Redefinir configurações</li></ul></li><li>**Caixa de ferramentas** integração</li><li>**Lista de tarefas** integração</li><li>Integração da Ajuda</li><li>**Opções de** caixa de diálogo</li><li>Gerenciamento de fontes e cores</li><li>**Saída** janela</li><li>**Comando** janela</li><li>Gerenciamento de janelas</li><li>Associações de teclas, menus e comandos</li><li>Tempo de execução de linguagem específica do domínio (DSL)</li></ul>|  
|Sistema de projeto e tipos de projeto|-Soluções e pastas de solução<br />-Gerenciador de configuração<br />-Gerenciamento item<br />-Projeto único e vários projetos de soluções<br />-Application Designer (Propriedades do projeto simplificado)<br />-Adicionar referência Web<br />-Adicionar referência de serviço<br />Projeto único<br />-Tipos de projeto de site da Web<br />-Projetos de aplicativos web|  
|Build|-Etapas de build personalizado no IDE<br />-Pré-compilação para a proteção de propriedade intelectual (IP)<br />-Assinatura de código<br />     MSBuild|  
|Editor|-Ferramentas (localização unificada, definição de fonte, herança) de navegação de código<br />-Navegação de código<br />-IntelliSense<br />-SmartTags<br />-Refactoring<br />-Listagem bonita<br />-Filtragem IntelliSense<br />-   **Definição de código** janela|  
|Designer|-Windows Presentation Foundation Designer<br />-Windows Forms Designer<br />-Web Designer e Editor de HTML|  
|Dados|-   **Gerenciador de servidores** (simplificado: somente os dados). Consulte a Observação 1.<br />-   **Fontes de dados** janela<br />-Todo o conjunto de controles de dados<br />-Editor de XML<br />-Dados associar a fonte de dados local (. Arquivos MDF ou. MDB)<br />-Associar dados objeto<br />-Data associar ao serviço Web<br />-Data ligar ao servidor de banco de dados local<br />-Data ligar ao servidor de banco de dados remoto<br />-Ferramentas DDL para dados remotos<br />-   **Gerenciador de servidores** extensibilidade ([!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] exemplos)|  
|Depurador|-Depuração local. Consulte a Observação 2.<br />-Depuração gerenciada<br />-Depuração local<br />-Anexar ao processo local<br />-Anexar ao processo remoto<br />-Delegado anônimo<br />-Domínios de aplicativo<br />-Depuração ASPX<br />-Atributos<br />-Break durante Func eval<br />-Os pontos de interrupção<br />-Restrições de ponto de interrupção<br />-A pilha de chamadas<br />-   **Comando** janela<br />-Depuração thread cruzado<br />-Dicas de dados<br />-Visualizador de dados<br />-Suporte a depurador assistentes de depuração gerenciados (MDAs)<br />-Suporte do encaminhador de tipo depurador<br />-Suporte a DTEEvents OTB<br />-JMC escalonador<br />-Teste de AppID debugger (DBGCLR)<br />-Perfil depurador<br />-Ferramentas e opções de depurador<br />-Depuração de iterador<br />-Avaliação da expressão tempo de design<br />-C# o avaliador de expressão<br />-Desmontagem<br />-Editar e continuar<br />-Windows do avaliador de expressão (inspeção, locais, Autos)<br />-Auxiliar de exceção<br />-Exceções<br />-Execução<br />- Genéricos<br />-Introdução a fonte correta<br />-Depuração/Cluster HPC<br />-Multi-language depuração integrada<br />-Depuração interOp<br />-Depuração just-in-time<br />-Depuração local<br />-Depuração gerenciada<br />-Controle manual (janela de processos)<br />-Memória<br />-Suporte minidespejo<br />-Módulos<br />-Depuração de vários processos<br />-Depuração nativa<br />-Suporte ao mecanismo de depuração novo<br />-Depuração de código otimizado<br />-Para filtros do windows output<br />-Processo de hospedagem para depuração gerenciada<br />-Processos<br />-Quickwatch<br />-Registra<br />-Registros na pilha<br />-Depuração remota<br />-Valores de retorno<br />-Depuração de script<br />-Suporte do serviço origem<br />-Segurança<br />Side-by-side<br />-SQL<br />-Servidor de símbolos<br />-Pontos de rastreamento<br />-Thread<br />-Visualizações<br />-Depurador extensível de folha de estilos XSLT (linguagem)|  
|Suporte de 64 bits|-depuração de 64 bits para código gerenciado e nativo, todos os idiomas<br />-suporte a x64 nativo|  
|Controle do código fonte (SCC)|-Integração do SCC básica. Consulte a Observação 3.<br />-Ferramentas e opções de verificação|  
|Extensibilidade|-Consumir componentes VSPackages e MEF|  
  
## <a name="notes"></a>Observações  
  
#### <a name="1-data-tools"></a>1. Ferramentas de Dados  
 O shell integrado inclui ferramentas de desenvolvimento de banco de dados, como suporte à extensibilidade de dados e a simplificada **Gerenciador de soluções**. No entanto, Crystal Reports, relatórios SQL e SQL Server Express não estão incluído no shell integrado.  
  
#### <a name="2-debugging-support"></a>2. Depuração de suporte  
 O shell integrado inclui o mesmo mecanismo de depuração que está incluído na versão de comunidade do Visual Studio. O mecanismo de depuração inclui o depurador comuns para código gerenciado e também recursos relacionados, como a execução, anexação, definir ponto de interrupção, editar e continuar e outras pessoas. No entanto, o mecanismo de depuração não oferece suporte depuração de banco de dados do SQL Server.  
  
 Embora o suporte para depuração nativa está incluído no pacote do depurador básico, você não pode estendê-lo para dar suporte a idiomas adicionais.  
  
#### <a name="3-source-code-control-integration"></a>3. Integração de controle do código-fonte  
 O shell integrado fornece APIs para implementar o controle do código-fonte (SCC) e para fornecer o controle de origem com base em MSSCCI comum componentes de integração.  
  
 Embora a integração do SCC não é um recurso regular da edição Pro do Visual Studio, a integração do SCC é fornecida no shell integrado.  
  
#### <a name="4-build-support"></a>4. Suporte ao build  
 O shell integrado fornece suporte de compilação. Você pode encontrar informações sobre compilações na [referência do MSBuild](../msbuild/msbuild-reference.md).  
  
## <a name="features-not-included-in-the-integrated-shell"></a>Recursos não incluídos no Shell integrado  
 A seguir está uma lista dos recursos que não estão incluídos no shell integrado:  
  
-   Designer de Classe  
  
-   DotFuscator preemptivo  
  
-   Funcionalidades da linguagem  
  
-   VSHost  
  
-   Nenhum linguagens do Visual Studio ou em seus modelos de projeto associado ou modelos de item de projeto, são incluídos no shell integrado. Nenhum implementações específicas de idioma de outros recursos estão incluídas, para trechos de código do Visual Basic de exemplo.  
  
## <a name="see-also"></a>Consulte também  
 [Estendendo a visão geral do Visual Studio](http://msdn.microsoft.com/library/3e9078d7-2763-4cc4-8e20-fac69d747f59)