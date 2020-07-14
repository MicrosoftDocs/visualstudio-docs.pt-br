---
title: Shell do Visual Studio (integrado) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, integrated mode features
- Shell [Visual Studio], integrated mode features
ms.assetid: 0b40d495-f17f-4bb9-ace8-b365a7172784
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 907b71d82a3c630bedc48209e735d9cf817432ad
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543150"
---
# <a name="visual-studio-shell-integrated"></a>Shell (integrado) do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Shell integrado do Visual Studio inclui o IDE (ambiente de desenvolvimento integrado), o depurador e a integração de controle do código-fonte. Nenhuma linguagem de programação está incluída. No entanto, o Shell integrado fornece uma estrutura que permite que você adicione linguagens de programação.  
  
 O Shell integrado do Visual Studio é, na verdade, uma combinação do Shell isolado do Visual Studio, além de uma instalação adicional que inclui componentes específicos do Shell integrados.  O aplicativo de shell integrado deve incluir o pacote redistribuível do Shell isolado, bem como o pacote redistribuível do Shell integrado, tanto de [pacotes redistribuíveis do shell do Microsoft Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/).  
  
> [!NOTE]
> Antes de poder acessar os pacotes redistribuíveis do Shell integrado e isolado, você será solicitado a preencher uma breve pesquisa do cliente.  Depois de preencher a pesquisa, você será direcionado para uma página do Visual Studio Connect com links de download de pacote redistribuível.  Você pode encontrar os links de download em visitas posteriores ao site do Visual Studio Connect **, na guia programas &#124; Visual Studio 2015 do Shell integrado e isolado** .  
  
 Se você instalar o aplicativo de shell integrado no mesmo computador que uma versão completa do Visual Studio, os componentes do aplicativo serão integrados diretamente ao Visual Studio.  
  
## <a name="features-in-the-integrated-shell"></a>Recursos no Shell integrado  
  
|Área de recurso|Recurso|  
|-|-|  
|Suporte ao idioma|-Nenhum|  
|IDE|<ul><li>Configurações<br /><br /> <ul><li>Criar configurações</li><li>Importar e exportar configurações</li><li>Redefinir configurações</li></ul></li><li>Integração da **caixa de ferramentas**</li><li>Integração do **lista de tarefas**</li><li>Integração da ajuda</li><li>Caixa de diálogo **Opções**</li><li>Gerenciamento de fontes e cores</li><li>Janela de **saída**</li><li>Janela de **comando**</li><li>Gerenciamento de janelas</li><li>Comandos, menus e associações de teclas</li><li>Tempo de execução de DSL (linguagem específica do domínio)</li></ul>|  
|Sistema de projeto e tipos de projeto|-Soluções e pastas de solução<br />-Gerenciador de configurações de soluções<br />-Gerenciamento de item<br />– Soluções de projeto único e de vários projetos<br />-Designer de Aplicativos (Propriedades de projeto simplificadas)<br />-Adicionar referência Web<br />-Adicionar Referência de Serviço<br />-Projeto único<br />-Tipos de projeto de site<br />-Projetos de aplicativos Web|  
|Build|-Etapas de compilação personalizadas no IDE<br />-Pré-compilação para proteção de propriedade intelectual (IP)<br />-Assinatura de código<br />     MSBuild|  
|Editor|-Ferramentas de navegação de código (localização unificada, definição de origem, herança)<br />-Navegação de código<br />-IntelliSense<br />-SmartTags<br />-Refatoração<br />-Lista de estilos<br />-Filtragem de IntelliSense<br />-   Janela de **definição de código**|  
|Designer|-Windows Presentation Foundation designer<br />-Designer de Formulários do Windows<br />-Web designer e editor de HTML|  
|Dados|-   **Gerenciador de servidores** (simplificado: somente dados). Consulte a observação 1.<br />-   Janela **fontes de dados**<br />-Conjunto completo de controles de dados<br />-Editor de XML<br />-Vinculação de dados à fonte de dados local (. MDF ou. MDB<br />-Vinculação de dados ao objeto<br />-Associação de dados ao serviço Web<br />-Ligação de dados com o servidor de banco local<br />-Ligação de dados com o servidor de banco remoto<br />-Ferramentas DDL para dados remotos<br />-   Extensibilidade de **Gerenciador de servidores** ( [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] exemplos)|  
|Depurador|-Depuração local. Consulte a observação 2.<br />-Depuração gerenciada<br />-Depuração local<br />-Anexar ao processo local<br />-Anexar ao processo remoto<br />-Delegado anônimo<br />-Domínios de aplicativo<br />-Depuração ASPX<br />-Atributos<br />-Interrupção durante Func-eval<br />-Pontos de interrupção<br />-Restrições de ponto de interrupção<br />-Pilha de chamadas<br />-   Janela de **comando**<br />-Depuração entre threads<br />-Dicas de dados<br />-Visualizador de dados<br />-Suporte do depurador para assistentes de depuração gerenciada (MDAs)<br />-Suporte do depurador para encaminhador de tipo<br />-Suporte do DTEEvents para OTB<br />-JMC stepper<br />-Teste de AppID do depurador (DBGCLR)<br />-Perfil do depurador<br />-Ferramentas e opções do depurador<br />-Iterador de depuração<br />-Avaliação de expressão de tempo de design<br />-Avaliador de expressão C#<br />-Desmontagem<br />-Editar e continuar<br />-Janelas do avaliador de expressão (Watch, locais, Autoies)<br />-Auxiliar de exceção<br />-Exceções<br />-Execução<br />- Genéricos<br />-Obtendo fonte correta<br />-HPC/depuração de cluster<br />-Depuração de vários idiomas integrada<br />– Depuração de interoperabilidade<br />-Depuração Just-in-time<br />-Depuração local<br />-Depuração gerenciada<br />-Controle manual (janela Processes)<br />-   Memória<br />-Suporte a minidespejo<br />-Módulos<br />-Depuração de vários processos<br />-Depuração nativa<br />-Novo suporte ao mecanismo de depuração<br />-Depuração de código otimizado<br />-Filtragem de saída do Windows<br />-Processo de hospedagem para depuração gerenciada<br />-Processos<br />-QuickWatch<br />-Registros<br />-Registros na pilha<br />-Depuração remota<br />-Valores de retorno<br />-Depuração de script<br />-Suporte ao serviço de origem<br />-Segurança<br />-Lado a lado<br />-SQL<br />-Servidor de símbolos<br />-Pontos de rastreamento<br />-Thread<br />-Visualizações<br />-Depurador de transformações de linguagem de folha de estilos extensível (XSLT)|  
|Suporte de 64 bits|-depuração de 64 bits para código gerenciado e nativo, todas as linguagens<br />-suporte nativo para x64|  
|Controle do código-fonte (SCC)|-Integração básica de SCC. Consulte a observação 3.<br />-Verificação de ferramentas e opções|  
|Extensibilidade|-Consumir componentes VSPackages e MEF|  
  
## <a name="notes"></a>Observações  
  
#### <a name="1-data-tools"></a>1. ferramentas de dados  
 O Shell integrado inclui ferramentas de desenvolvimento de banco de dados, como o suporte à extensibilidade e o **Gerenciador de soluções**simplificado. No entanto, SQL Server Express, relatórios SQL e Crystal Reports não estão incluídos no Shell integrado.  
  
#### <a name="2-debugging-support"></a>2. suporte à depuração  
 O Shell integrado inclui o mesmo mecanismo de depuração incluído na versão da Comunidade do Visual Studio. O mecanismo de depuração inclui o depurador comum para código gerenciado e também recursos relacionados, como executar, anexar, definir ponto de interrupção, editar e continuar e outros. No entanto, o mecanismo de depuração não dá suporte à depuração de banco de dados SQL Server.  
  
 Embora o suporte para depuração nativa esteja incluído no pacote do depurador básico, você não pode estendê-lo para dar suporte a idiomas adicionais.  
  
#### <a name="3-source-code-control-integration"></a>3. integração de controle do código-fonte  
 O Shell integrado fornece APIs para implementar o SCC (controle de código-fonte) e fornecer os componentes de integração de controle de origem comuns baseados em MSSCCI.  
  
 Embora a integração com SCC não seja um recurso regular da edição pro do Visual Studio, a integração com SCC é fornecida no Shell integrado.  
  
#### <a name="4-build-support"></a>4. suporte à compilação  
 O Shell integrado fornece suporte à compilação. Você pode encontrar informações sobre compilações na [referência do MSBuild](../msbuild/msbuild-reference.md).  
  
## <a name="features-not-included-in-the-integrated-shell"></a>Recursos não incluídos no Shell integrado  
 Veja a seguir uma lista de recursos que não estão incluídos no Shell integrado:  
  
- Designer de Classe  
  
- Proteção PreEmptive – Dotfuscator  
  
- Funcionalidades da linguagem  
  
- VSHost  
  
- Nenhuma linguagem do Visual Studio ou seus modelos de projeto associados ou modelos de item de projeto estão incluídos no Shell integrado. Nenhuma implementação específica de idioma de outros recursos está incluída, por exemplo Visual Basic trechos de código.  
  
## <a name="see-also"></a>Consulte Também  
 [Ampliando a visão geral do Visual Studio](https://msdn.microsoft.com/library/3e9078d7-2763-4cc4-8e20-fac69d747f59)
