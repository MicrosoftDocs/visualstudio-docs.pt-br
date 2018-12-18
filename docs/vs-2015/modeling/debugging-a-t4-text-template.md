---
title: Depurando um modelo de texto T4 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- text templates, troubleshooting
- text templates, debugging
ms.assetid: 0877fdf2-20bf-42da-b3cc-4c5856b80821
caps.latest.revision: 30
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: f299b89f7f59cbfc043bb77e6e56c3e5fac22d16
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49298903"
---
# <a name="debugging-a-t4-text-template"></a>Depurando um modelo de texto T4
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode definir pontos de interrupção em modelos de texto. Para depurar um modelo de texto de tempo de design, salve o arquivo de modelo de texto e, em seguida, escolha **depurar modelo T4** no menu de atalho do arquivo no Gerenciador de soluções. Para depurar um modelo de texto de tempo de execução, simplesmente depure o aplicativo ao qual ele pertence.  
  
 Para depurar um modelo de texto, você deve compreender as etapas do processo de transformação de modelo. Diferentes tipos de erro podem ocorrer dentro de cada etapa. As etapas são da seguinte maneira.  
  
|Etapa|Modelo de tempo de design: quando isso acontecer|Modelo de tempo de execução: quando isso acontecer|  
|----------|--------------------------------------------|-----------------------------------------|  
|Código é gerado a partir do modelo de texto.<br /><br /> Erros nas diretivas, ou incompatíveis ou fora de ordem `<#…#>` marcas.|Quando você salva o modelo ou invocar a transformação de texto.|Quando você salva o modelo ou invocar a transformação de texto.|  
|Código gerado é compilado.<br /><br /> Erros de compilação em seu código de modelo.|Imediatamente após a etapa anterior.|Juntamente com o código do aplicativo.|  
|Código é executado.<br /><br /> Erros de tempo de execução em seu código de modelo.|Imediatamente após a etapa anterior.|Quando seu aplicativo for executado e invoca o código de modelo.|  
  
 Na maioria dos casos, os números de linha no código do modelo são fornecidos no relatório de erros. Quando o relatório de erros se refere a um nome de arquivo temporário, a causa comum é um colchete incompatível no código do modelo de texto.  
  
 Você pode definir pontos de interrupção em modelos de texto e de depuração como de costume.  
  
## <a name="common-errors-and-fixes"></a>Erros comuns e correções  
 A tabela a seguir lista os erros mais comuns e suas correções.  
  
|Mensagem de erro|Descrição|Solução|  
|-------------------|-----------------|--------------|  
|Falha ao carregar a classe base{0}' da qual transformação classe herdada.|Ocorre se você não encontrar a classe base especificada no `inherits` parâmetro em uma diretiva de modelo. A mensagem fornece o número de linha de diretiva do modelo.|Certifique-se de que a classe especificada existe e se o assembly que ele exista na está especificado em uma diretiva de assembly.|  
|Falha ao resolver a incluir o texto do arquivo:{0}|Ocorre quando você não conseguir encontrar um modelo incluído. A mensagem fornece o nome do arquivo de inclusão solicitada.|Certifique-se de que o caminho do arquivo é relativo ao caminho do modelo original, ou que o arquivo está em um local que está registrado com o host ou que há um caminho completo para o arquivo.|  
|Erros foram gerados ao inicializar o objeto de transformação. A transformação não será executada.|Ocorre quando o 'Initialize ()' da classe de transformação falhou ou retornou false.|O código na função Initialize () é proveniente da classe de transformação de base especificada na \<#@template#> diretiva e de processadores de diretriz. O erro que causou initialize falha provavelmente está na lista de erros. Investigue o motivo da falha. Você pode examinar o código gerado real para Initialize (), seguindo os procedimentos para depurar um modelo.|  
|O assembly '{0}'para o processador de diretriz'{1}' não foi concedido o conjunto de permissões FullTrust. Somente os assemblies confiáveis podem fornecer processadores de diretriz. Esse processador de diretriz não será carregado.|Ocorre quando o sistema não concede permissões FullTrust a um assembly que contém um processador de diretriz. A mensagem fornece o nome do assembly e o nome do processador de diretriz.|Certifique-se de que você só usar assemblies confiáveis no computador local.|  
|O caminho '{0}' deve ser local neste computador ou parte de uma zona confiável.|Ocorre quando uma diretiva ou diretiva de assembly faz referência a um arquivo que é não em seu computador local ou na região de sua rede confiável.|Certifique-se de que o diretório onde estão localizadas a diretiva ou diretivas de assembly está em sua zona confiável. Você pode adicionar um diretório de rede para sua zona confiável por meio do Internet Explorer.|  
|Vários erros de sintaxe como "Inválido token ' catch'" ou "um namespace não pode conter diretamente membros"|Há muitas chaves de fechamento em seu código de modelo. O compilador confundi-lo com o código de geração de padrão.|Verifique o número de fechamento de chaves e colchetes dentro de delimitadores de código.|  
|Loops ou condicionais não compilado ou executado corretamente. Por exemplo: `<#if (i>10)#> Number is: <#= i #>`.<br /><br /> Esse código sempre gera o valor de i. Somente "número é:" é condicional.|No c#, sempre use chaves para cercar blocos de texto que são inseridos em instruções de controle.|Adicionar chaves: `<#if (i>10) { #>    Number is: <#= i #><# } #>`.|  
|"Expressão muito complexa" ao processar um modelo de tempo de design ou compilar um modelo de tempo de execução (pré-processado).<br /><br /> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para de funcionar durante a tentativa de inspecionar o código gerado por um modelo de tempo de execução.|Bloco de texto é muito longo. T4 converte os blocos de texto em uma expressão de concatenação de cadeia de caracteres, com uma cadeia de caracteres literal para cada linha do modelo. Blocos de texto muito longas podem ultrapasse os limites de tamanho do compilador.|Divida o bloco de texto longo com um bloco de expressão, como:<br /><br /> `<#= "" #>`|  
  
## <a name="warning-descriptions-and-fixes"></a>Correções e descrições de aviso  
 A tabela a seguir lista os avisos mais comuns, juntamente com correções, se disponível.  
  
|Mensagem de aviso|Descrição|Solução|  
|---------------------|-----------------|--------------|  
|Carregando o arquivo de inclusão '{0}' retornou uma cadeia de caracteres nula ou vazia.|Ocorre se um arquivo de modelo de texto incluído está em branco. A mensagem fornece o nome do arquivo do arquivo incluído.|Remova a diretiva include ou certifique-se de que o arquivo tem algum conteúdo.|  
|Compilando transformação:|Precede a essa cadeia de caracteres para todos os erros ou avisos quando ele compila a transformação de origem do compilador. Essa cadeia de caracteres significa que o compilador gerou um erro ou aviso.|Se você tiver um problema ao tentar localizar a DLL, você precisa fornecer o caminho completo ou um nome forte totalmente qualificado, se a DLL está no GAC.|  
|O parâmetro '{0}' já existe na diretiva. O parâmetro duplicado será ignorado.|Ocorre quando um parâmetro é especificado mais de uma vez em uma diretiva. A mensagem fornece o nome do parâmetro e o número da linha da diretiva.|Remova a especificação de parâmetro duplicado.|  
|Ocorreu um erro ao carregar o arquivo de inclusão '{0}'. A diretiva de inclusão será ignorada.|Ocorre quando você não consegue localizar um arquivo especificado em um `include` diretiva. A mensagem fornece o nome do arquivo e o número da linha da diretiva.|Certifique-se de que o arquivo de inclusão existe no mesmo diretório do arquivo de modelo de texto original ou em um dos diretórios de inclusão que são registrados com o host.|  
|Uma classe base inválida foi especificada para a classe de transformação. A classe base deve derivar de TextTransformation.|Ocorre quando o `inherits` parâmetro em uma diretiva de modelo especifica uma classe que não herda de `TextTransformation`. A mensagem fornece o número de linha de diretiva do modelo.|Especifique uma classe que deriva de `TextTransformation`.|  
|Uma cultura inválida foi especificada na diretiva 'template'. A cultura deve estar no formato "xx-XX". A cultura invariável será usada.|Ocorre quando o parâmetro de cultura em uma diretiva de modelo for especificado incorretamente. A mensagem fornece o número de linha de diretiva do modelo.|Altere o parâmetro de cultura para uma cultura válida no formato "xx-XX".|  
|Um valor de depuração inválido '{0}' foi especificado na diretiva do modelo. O valor de depuração deve ser "true" ou "false". O padrão de "false" será usado.|Ocorre quando o `debug` parâmetro em uma diretiva de modelo for especificado incorretamente. A mensagem fornece o número de linha de diretiva do modelo.|Defina o parâmetro de depuração como "true" ou "false".|  
|Um valor de HostSpecific inválido '{0}' foi especificado na diretiva do modelo. O valor de HostSpecific deve ser "true" ou "false". O padrão de "false" será usado.|Ocorre quando o parâmetro de host específico em um `template` diretiva for especificada incorretamente. A mensagem fornece o número de linha de diretiva do modelo.|Defina o parâmetro de específicos do host como "true" ou "false".|  
|Um idioma inválido '{0}' foi especificado na diretiva 'template'. O idioma deve ser "C#" ou "VB". O valor padrão de "C#" será usado.|Ocorre quando um idioma sem suporte é especificado no `template` diretiva. Somente "C#" ou "VB" são permitidos (diferencia maiusculas de minúsculas). A mensagem fornece o número de linha de diretiva do modelo.|Defina o `language` parâmetro na diretiva do modelo para "C#" ou "VB".|  
|Várias diretivas de saída foram encontradas no modelo. Todos, exceto o primeiro deles serão ignorados.|Ocorre quando várias `output` diretivas são especificadas em um arquivo de modelo. A mensagem fornece o número de linha de diretiva de saída duplicado.|Remover duplicata `output` diretivas.|  
|Várias diretivas de modelo foram encontradas no modelo. Todos, exceto o primeiro deles serão ignorados. Vários parâmetros para a diretiva de modelo devem ser especificados dentro de uma diretiva de modelo.|Ocorre se você especificar vários `template` diretivas dentro de um arquivo de modelo de texto (incluindo arquivos incluídos). A mensagem fornece o número de linha de diretiva do modelo duplicado.|Agregar os diferentes `template` diretivas em um `template` diretiva.|  
|Nenhum processador foi especificado para uma diretiva chamada '{0}'. A diretiva será ignorada.|Ocorre se você especificar uma `custom` diretiva, mas não fornecem um `processor` atributo. A mensagem fornece o nome da diretiva e o número de linha.|Fornecer um `processor` atributo com o nome da `directive` processador para a diretiva.|  
|Um processador chamado '{0}'não pôde ser encontrado na diretiva chamada'{1}'. A diretiva será ignorada.|Ocorre quando o sistema não é possível localizar o `directive` processador especificado dentro de um `custom` diretiva. A mensagem fornece o nome da diretiva, nome do processador e o número da linha da diretiva.|Defina o `processor` atributo na diretiva para o nome do processador de diretriz.|  
|Um parâmetro obrigatório '{0}'para a diretiva'{1}' não foi encontrado. A diretiva será ignorada.|Ocorre quando o sistema não fornece um parâmetro obrigatório de diretiva. A mensagem fornece o nome do parâmetro ausente, o nome da diretiva e o número de linha.|Forneça o parâmetro ausente.|  
|O processador chamado '{0}'não oferece suporte a diretiva chamada'{1}'. A diretiva será ignorada.|Ocorre quando um processador de diretriz não dá suporte a uma diretiva. A mensagem fornece o nome e número de linha da diretiva transgressor junto com o nome do processador de diretriz.|Corrija o nome da diretiva.|  
|A diretiva inclusa do arquivo '{0}' faz com que um loop infinito.|Exibida se as diretivas de inclusão circular forem especificados (por exemplo, um arquivo de inclui o arquivo B, que inclui um arquivo).|Não especifique circular diretivas de inclusão.|  
|Executando transformação:|Precede a essa cadeia de caracteres para todos os erros ou avisos que são gerados durante a execução de transformação.|Não aplicável.|  
|Uma marca de início ou término inesperada foi encontrada dentro de um bloco. Certifique-se de que você não digitou incorretamente uma marca de início ou término, e que você não tem todos os blocos aninhados no modelo.|Exibido quando você tem um inesperado \<# ou #>. Ou seja, se você tiver um \<# após outra marca aberta que não foram fechada, ou você tem um #> quando não há nenhuma marca aberta não fechada antes dele. A mensagem fornece o número da linha da marca incompatível.|Remova a marca de início ou término incompatível, ou use um caractere de escape.|  
|Uma diretiva foi especificada em um formato incorreto. A diretiva será ignorada. Especifique a diretiva no formato `<#@ name [parametername="parametervalue"]*  #>`|Exibida pelo analisador se uma diretiva não for especificada no formato correto. A mensagem fornece o número da linha da diretiva incorreto.|Certifique-se de que todas as diretivas estão no formato `<#@ name [parametername="parametervalue"]*  #>`. Para obter mais informações, consulte [diretivas de modelo de texto T4](../modeling/t4-text-template-directives.md).|  
|Falha ao carregar Assembly '{0}'para o processador de diretiva registrado'{1}'<br /><br /> {2}|Ocorre quando um processador de diretriz não pôde ser carregado pelo host. A mensagem identifica o assembly fornecido para o processador de diretriz e o nome do processador de diretriz.|Certifique-se de que o processador de diretriz está registrado corretamente e se o assembly existe.|  
|Falha ao localizar o tipo '{0}'no Assembly'{1}'para o processador de diretiva registrado'{2}'<br /><br /> {3}|Ocorre quando um tipo de processador de diretriz não foi possível carregar seu assembly. A mensagem fornece o nome do tipo, assembly e processador de diretriz.|O vshost encontra informações de processador de diretriz (nome de assembly e tipo) no registro. Certifique-se de que o processador de diretriz está registrado corretamente, e se o tipo existe no assembly.|  
|Houve um problema ao carregar o assembly '{0}'|Ocorre quando há um problema ao carregar um assembly. A mensagem fornece o nome do assembly.|Você pode especificar os assemblies a serem carregados no \<@# assembly #> diretivas e por processadores de diretriz. A mensagem de erro que segue essa cadeia de caracteres deve fornecer mais dados sobre por que o carregamento do assembly falhou.|  
|Houve um problema ao criar e inicializar o processador de uma diretiva chamada '{1}'. O tipo do processador é {0}. A diretiva será ignorada.|Ocorre quando o sistema não foi possível criar ou inicializar um processador de diretriz. A mensagem fornece o nome e número de linha da diretiva e o tipo do processador.|Certifique-se de que você usar o processador de diretriz correto e se o processador de diretriz tem um construtor padrão público. Caso contrário, use as opções de depuração para descobrir por que o método Initialize () do processador de diretriz está falhando. Para obter mais informações, consulte [modelos de solução de problemas de texto](../modeling/debugging-a-t4-text-template.md).|  
|Ocorreu uma exceção durante o processamento de uma diretiva chamada '{0}'.|Ocorre quando um processador de diretriz lança uma exceção quando o processamento de uma diretiva.|Certifique-se de que os parâmetros para o processador de diretriz estão corretos.|  
|O host lançou uma exceção ao tentar resolver a referência de assembly '{0}'.|Ocorre quando o host gera uma exceção ao tentar resolver uma referência de assembly. A mensagem fornece o assembly de referência de cadeia de caracteres.|Assembly referências provenientes \<@# assembly #> diretivas e de processadores de diretriz. Certifique-se de que o parâmetro 'name' fornecido no parâmetro assembly está correto.|  
|Tente especificar sem suporte {1} valor '{0}' para a diretiva {2}|Ocorre pelo RequiresProvidesDirectiveProcessor (todos os nossos processadores de diretriz gerados derivam dele), quando você fornece não suportado requer ou fornece um argumento.|Certifique-se de que os nomes em name = 'value' pares fornecidos na requer e fornece parâmetros estão corretos.|



