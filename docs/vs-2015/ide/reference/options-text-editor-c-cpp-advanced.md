---
title: Opções, Editor de texto, C / C++, Avançado | Microsoft Docs
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
- VS.ToolsOptionsPages.Text_Editor.C\C++.Advanced
- VS.ToolsOptionsPages.Text_Editor.C%2FC%2B%2B.Advanced
- VS.ToolsOptionsPages.Text_Editor.C/C++.Advanced
helpviewer_keywords:
- Text Editor Options dialog box, advanced
ms.assetid: 67c82ae5-fddd-49df-baec-8e7498b156f3
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: aafa46e62af6eadb56d8cf53cb2190bc7403358b
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49285695"
---
# <a name="options-text-editor-cc-advanced"></a>Opções, Editor de Texto, C/C++, Avançado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Ao alterar essas opções, você pode alterar o comportamento relacionado ao IntelliSense e ao banco de dados de navegação quando estiver programando em C ou C++.  
  
 Para acessar essa página, na caixa de diálogo **Opções**, no painel esquerdo, expanda **Editor de Texto**, expanda **C/C++** e escolha **Avançado**.  
  
> [!NOTE]
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="browsingnavigation"></a>Navegação  
 Você nunca deve escolher essas opções, exceto no caso raro em que uma solução é tão grande que a atividade de banco de dados consome uma quantidade inaceitável de recursos do sistema.  
  
 **Desabilitar Banco de Dados**  
 Qualquer uso do banco de dados de navegação de código (SDF), todas as outras opções de Navegação e todos os recursos do IntelliSense exceto por #include Auto Complete são desabilitados.  
  
 **Desabilitar Atualizações de Banco de Dados**  
 O banco de dados será aberto no modo somente leitura e não serão realizadas atualizações conforme os arquivos forem editados. A maioria dos recursos ainda funcionará. No entanto, como são feitas edições, os dados ficarão obsoletos e você obterá resultados incorretos.  
  
 **Desabilitar Auto Atualização de Banco de Dados**  
 O banco de dados de navegação de origem não será atualizado automaticamente quando os arquivos de origem são modificados. No entanto, se você abrir o **Gerenciador de Soluções**, abra o menu de atalho do projeto e escolha **Examinar Novamente a Solução**, todos os arquivos desatualizados serão verificados e o banco de dados será atualizado.  
  
 **Desabilitar Arquivos Implícitos**  
 O banco de dados de navegação de código não coleta dados para arquivos que não estiverem especificados em um projeto. Um projeto contém arquivos de origem e arquivos de cabeçalho que são especificados explicitamente. Os arquivos implícitos são incluídos por arquivos explícitos (por exemplo, afxwin.h, windows.h e atlbase.h). Normalmente, o sistema localiza esses arquivos e também os indexa para vários recursos de navegação (incluindo Navegar Até). Se você escolher essa opção, esses arquivos não serão indexados e alguns recursos não estarão disponíveis para eles. Se você escolher essa opção, "Desabilitar Limpeza Implícita" e "Desabilitar Pastas de Dependências Externas" também são implicitamente escolhidas.  
  
 **Desabilitar Limpeza Implícita**  
 O banco de dados de navegação de código não limpa arquivos implícitos que não são mais referenciados. Essa opção impede que arquivos implícitos sejam removidos do banco de dados quando não são mais usados. Por exemplo, se você adicionar um a diretiva `#include` que referencia mapi.h a um dos seus arquivos de origem, mapi.h será encontrado e indexado. Se você, em seguida, remover o #include e o arquivo não for referenciado em outro lugar, as informações sobre ele eventualmente serão removidas a menos que você escolha essa opção. (Consulte a opção **Verificar Novamente Intervalo da Solução**.) Essa opção é ignorada quando você explicitamente verifica novamente a solução.  
  
 **Desabilitar Pastas de Dependências Externas**  
 A pasta de Dependências Externas para cada projeto não é criada ou atualizada. No **Gerenciador de Soluções**, cada projeto contém uma pasta de Dependências Externas, que contém todos os arquivos implícitos daquele projeto. Se você escolher essa opção, essa pasta não desaparece.  
  
 **Recriar Banco de Dados**  
 Recrie o banco de dados de navegação de código do nada na próxima vez em que a solução for carregada. Se você escolher essa opção, o arquivo de banco de dados SDF será excluído na próxima vez em que você carregar a solução, fazendo assim com que o banco de dados seja recriado e todos os arquivos sejam indexados.  
  
 **Verificar Novamente Intervalo da Solução**  
 Um trabalho de “Verificar Novamente Intervalo da Solução” está agendado para o intervalo que você especificar. Você deve especificar entre 0 e 5000 minutos. O valor padrão é 60 minutos. Enquanto a solução é verificada novamente, os carimbos de data/hora do arquivo são verificados para determinar se o arquivo foi alterado fora do IDE. (As alterações feitas no IDE são rastreadas automaticamente e os arquivos são atualizados.) Os arquivos incluídos implicitamente são verificados para determinar se eles ainda são referenciados.  
  
## <a name="diagnostic-logging"></a>Diagnostic Logging  
 Essas opções são fornecidas no caso de a Microsoft solicitar a coleta de informações avançadas para diagnosticar um problema. As informações de log não são úteis para os usuários e é recomendável deixá-las desabilitadas.  
  
 **Habilitar Registro em Log**  
 Habilita o registro em log do diagnóstico para a janela de saída.  
  
 **Nível de Log**  
 Defina o detalhamento do log, de 0 a 5.  
  
 **Filtro de Log**  
 Filtra os tipos de evento exibidos usando uma bitmask.  
  
 Defina usando uma soma de qualquer uma das seguintes opções:  
  
-   0 – Nenhum  
  
-   1 – Geral  
  
-   2 – Ocioso  
  
-   4 – WorkItem  
  
-   8 – IntelliSense  
  
-   16 – ACPerf  
  
-   32 – ClassView  
  
## <a name="fallback-location"></a>Localização de Fallback  
 A localização de fallback é onde os arquivos de suporte SDF e IntelliSense (por exemplo, iPCH) são colocados quando a localização principal (mesmo diretório que a solução) não é usado. Essa situação pode ocorrer se o usuário não tem as permissões para gravar no diretório da solução ou o diretório da solução está em um dispositivo lento. A localização de fallback padrão é no diretório temporário do usuário.  
  
 **Sempre Utilizar Localização de Fallback**  
 Indica que os arquivos do IntelliSense e banco de dados de navegação de código devem sempre ser armazenados em uma pasta especificada como “Localização de Fallback”, não próximo ao arquivo .sln. O IDE nunca tentará colocar os arquivos SDF ou iPCH próximos ao diretório da solução e sempre tentará usar a localização de fallback.  
  
 **Não Avisar Se Localização De Fallback É Utilizada**  
 Você não será informado ou recebe um prompt se “Localização de Fallback” for usada. Normalmente, o IDE informará se precisar usar a localização de fallback. Esta opção desativa esse aviso.  
  
 **Localização de Fallback**  
 Esse valor é usado como uma localização secundária para armazenar arquivos do IntelliSense ou banco de dados de navegação de código. Por padrão, o diretório temporário é o local de fallback. O IDE criará um subdiretório no caminho especificado (ou no diretório temporário) que inclui o nome da solução junto com um hash do caminho completo para a solução, o que evita problemas com nomes de solução serem idênticos.  
  
## <a name="intellisense"></a>IntelliSense  
 **Informações Rápidas Automático**  
 Habilita as dicas de ferramenta de QuickInfo quando você move o ponteiro sobre o texto.  
  
 **Desabilitar IntelliSense**  
 Desabilita todos os recursos do IntelliSense. O IDE não cria processos VCPkgSrv.exe para atender a solicitações do IntelliSense e nenhum recurso do IntelliSense funcionará (QuickInfo, Lista de Membros, Preenchimento Automático, Ajuda de Parâmetro). A colorização semântica e o realce de referência também são desabilitados. Essa opção não desabilita recursos de navegação que dependem exclusivamente do banco de dados (incluindo a Barra de Navegação, ClassView e janela Propriedade).  
  
 **Desabilitar Auto Atualização**  
 A atualização do IntelliSense será adiada até uma solicitação real para o IntelliSense ser feita. Esse atraso pode resultar em um tempo de execução maior da primeira operação do IntelliSense em um arquivo, mas pode ser útil definir esta opção em computadores muito lentos ou com recursos limitados. Se você escolher essa opção, também escolherá implicitamente as opções “Desabilitar Relatório de Erros” e “Desabilitar Rabiscos”.  
  
 **Desabilitar Relatório de Erros**  
 Desabilita o relatório de erros do IntelliSense através de rabiscos e da janela Lista de Erros. Também desabilita a análise em segundo plano que está associada ao relatório de erros. Se você escolher essa opção, também escolherá implicitamente a opção “Desabilitar Rabiscos”.  
  
 **Desabilitar Rabiscos**  
 Desabilita os rabiscos de erro do IntelliSense. Os “rabiscos” vermelhos não aparecem na janela do editor, mas o erro ainda aparecerá na janela Lista de Erros.  
  
 **Desabilitar Auto Complementação #include**  
 Desabilita o preenchimento automático de instruções `#include`.  
  
 **Usar barra “/” em #include Auto Complete**  
 Dispara o preenchimento automático de instruções `#include` quando "/" é usado. O delimitador padrão é a barra invertida “ \”. O compilador pode aceitar qualquer um, então use esta opção para especificar o que sua base de código usa.  
  
 **Máximo de Unidades de Translação no Cache**  
 O número máximo de unidades de translação será mantido ativo a qualquer momento para solicitações de IntelliSense. Você deve especificar um valor entre 2 e 15. Esse número está diretamente relacionado ao número máximo de processos de VCPkgSrv.exe que serão executados (para uma determinada instância do Visual Studio). O valor padrão é 2, mas se você tiver memória disponível, poderá aumentar esse valor e possivelmente alcançar um desempenho ligeiramente melhor no IntelliSense.  
  
 Para obter mais informações sobre as unidades de translação, consulte [Fases de translação](http://msdn.microsoft.com/library/a7f7a8c9-e8ba-4321-9e50-ebfbbdcce9db).  
  
 **Desabilitar Lista de Membros Agressivos**  
 A lista de membros não aparece enquanto você digita o nome de um tipo ou variável. A lista é exibida somente depois que você digita um dos caracteres de confirmação, conforme definido na opção **Caracteres de Confirmação de Lista de Membros**.  
  
 **Desabilitar Palavras-Chave da Lista de Membros**  
 Palavras-chave da linguagem como `void`, `class` e `switch` não aparecem em sugestões de lista de membros.  
  
 **Desabilitar Snippets de Código da Lista de Membros**  
 Os snippets de código não aparecem em sugestões de lista de membros.  
  
 **Desabilitar Colorização Semântica**  
 Desativa toda a colorização de código, exceto palavras-chave da linguagem, cadeias de caracteres e comentários.  
  
 **Confirmação de Lista de Membro Inteligente**  
 Adiciona uma linha quando você escolhe a tecla Enter no final de uma palavra totalmente digitada.  
  
 **Modo de Filtro da Lista de Membros**  
 Define o tipo de algoritmo de correspondência. **Difuso** localiza as correspondências mais possíveis porque usa um algoritmo semelhante a um verificador ortográfico para localizar correspondências semelhantes, mas não idênticas. **Filtragem inteligente** corresponde subcadeias de caracteres, mesmo que não estejam no início de uma palavra. **Prefixo** corresponde apenas em subcadeias de caracteres idênticas que começam no início da palavra.  
  
 **Caracteres de Confirmação de Lista de Membros**  
 Especifica os caracteres que fazem com que a sugestão Lista de Membros atualmente realçada a ser confirmada. Você pode adicionar ou remover caracteres desta lista.  
  
## <a name="references"></a>Referências  
 **Desabilitar Resolução**  
 Por questões de desempenho, “Localizar Todas as Referências” mostra resultados da pesquisa textual brutos por padrão em vez de usar o IntelliSense para verificar cada candidato. Você pode desmarcar essa caixa de seleção para obter resultados mais precisos em todas as operações de pesquisa. Para filtrar por pesquisa, abra o menu de atalho para a lista de resultados e, em seguida, escolha "Resolver Resultados".  
  
 **Ocultar Não Confirmados**  
 Oculte itens não confirmados nos resultados de “Localizar Todas as Referências”. Se você remover definição da opção "Desabilitar Resolução", poderá usar essa opção para ocultar itens não confirmados nos resultados.  
  
 **Desabilitar Realce de Referência**  
  
## <a name="see-also"></a>Consulte também  
 [Configurando opções do editor específicas a um idioma](../../ide/reference/setting-language-specific-editor-options.md)



