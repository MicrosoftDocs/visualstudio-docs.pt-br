---
title: Globalização e localização de soluções do Excel
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- globalization [Office development in Visual Studio], configuring
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ade59e757778ac7858732f5bf9880b9f88eacd69
ms.sourcegitcommit: ef828606e9758c7a42a2f0f777c57b2d39041ac3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39567449"
---
# <a name="globalization-and-localization-of-excel-solutions"></a>Globalização e localização de soluções do Excel
  Esta seção contém informações sobre considerações especiais para soluções do Microsoft Office Excel que serão executadas em computadores que têm configurações diferentes do inglês para Windows. A maioria dos aspectos da globalização e localização de soluções do Microsoft Office são os mesmos encontrados ao criar outros tipos de soluções usando o Visual Studio. Para obter informações gerais, consulte [Globalize e Localizando aplicativos](/visualstudio/ide/globalizing-and-localizing-applications).  
  
 Por padrão, os controles de host no trabalho do Microsoft Office Excel corretamente em qualquer configuração regional do Windows, desde que todos os dados que são passados ou manipulados usando o código gerenciado é formatado usando formatação de texto para inglês (Estados Unidos). Em projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)], esse comportamento é controlado pelo common language runtime (CLR).  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="format-data-in-excel-with-various-regional-settings"></a>Formatar dados no Excel com várias configurações regionais  
 Você deve formatar todos os dados que tem a formatação sensíveis à localidade, como datas e moeda, usando o formato de dados de inglês (Estados Unidos) (localidade 1033 ID) antes de passá-lo para o Microsoft Office Excel ou ler os dados do código em seu projeto do Office.  
  
 Por padrão, quando você desenvolve uma solução do Office no Visual Studio, o modelo de objeto do Excel espera a formatação de dados de localidade 1033 ID (Isso também é chamado bloqueio de modelo de objeto para a localidade 1033 ID). Esse comportamento corresponde a maneira que funciona de Visual Basic for Applications. No entanto, você pode modificar esse comportamento em suas soluções do Office.  
  
### <a name="understand-how-the-excel-object-model-always-expects-locale-id-1033"></a>Entender como o modelo de objeto do Excel sempre espera localidade 1033 ID  
 Por padrão, as soluções do Office que você cria usando o Visual Studio não são afetadas pelas configurações de localidade do usuário final e sempre se comportam como se a localidade é inglês (Estados Unidos). Por exemplo, se você obter ou definir o <xref:Microsoft.Office.Interop.Excel.Range.Value2%2A> propriedade no Excel, os dados deve ser formatada da maneira que espera a identificação de localidade 1033. Se você usar um formato de dados diferentes, você poderá obter resultados inesperados.  
  
 Mesmo que você use o formato inglês (Estados Unidos) de dados que são passados ou manipulados pelo código gerenciado, o Excel interpreta e exibe os dados corretamente de acordo com a configuração de localidade do usuário final. Excel pode formatar os dados corretamente porque o código gerenciado passa o formato da localidade 1033 ID juntamente com os dados, que indica que os dados estejam em inglês (Estados Unidos) e, portanto, deve ser reformatado para corresponder à configuração de localidade do usuário.  
  
 Por exemplo, se os usuários finais têm suas opções regionais definidas para a localidade alemão (Alemanha), eles esperam a data de 29 de junho de 2005, a ser formatada assim: 29.06.2005. No entanto, se sua solução passa a data para o Excel como uma cadeia de caracteres, você deve formatar a data de acordo com o formato inglês (Estados Unidos): 6/29/2005. Se a célula é formatada como uma célula data, o Excel exibirá a data no formato de alemão (Alemanha).  
  
### <a name="pass-other-locale-ids-to-the-excel-object-model"></a>Passar outras IDs de localidade para o modelo de objeto do Excel  
 O common language runtime (CLR) automaticamente passa 1033 de ID de localidade para todos os métodos e propriedades no modelo de objeto do Excel que aceitam dados sensíveis à localidade. Não é possível alterar esse comportamento automaticamente para todas as chamadas para o modelo de objeto. No entanto, você pode passar uma ID de localidade diferentes para um método específico usando <xref:System.Type.InvokeMember%2A> para chamar o método e passando a ID de localidade para o *cultura* parâmetro do método.  
  
## <a name="localize-document-text"></a>Localizar texto do documento  
 O documento, modelo ou pasta de trabalho em seu projeto provavelmente inclui texto estático, que deve ser localizados separadamente do assembly e outros recursos gerenciados. Uma maneira simples de fazer isso é fazer uma cópia do documento e traduzir o texto usando o Microsoft Office Word ou Microsoft Office Excel. Esse processo funciona mesmo se você não fizer alterações no código, porque qualquer número de documentos pode ser vinculado ao mesmo assembly.  
  
 Ainda Certifique-se de que qualquer parte do seu código que interage com o texto do documento continua corresponder ao idioma do texto e que indicadores, intervalos nomeados, e outros campos de exibição acomodar qualquer reformatação do documento do Office que era necessário ajuste de comprimento diferente de gramática e texto. Modelos de documentos que contêm relativamente pequeno texto, você talvez queira considerar armazenar o texto em arquivos de recurso e, em seguida, carregando o texto em tempo de execução.  
  
### <a name="text-direction"></a>Direção do texto  
 No Excel, você pode definir uma propriedade da planilha para renderizar o texto à direita para esquerda. Hospedar controles ou qualquer controle que tem um `RightToLeft` corresponder a propriedade, que é imposta pelo designer de automaticamente estas configurações em tempo de execução. O Word não tem uma configuração de documento para o texto bidirecional (você apenas alterar o alinhamento do texto), para que os controles não podem ser mapeados para essa configuração. Em vez disso, você deve definir o alinhamento do texto para cada controle. É possível escrever código para percorrer todos os controles e forçá-los para renderizar o texto da direita para esquerda.  
  
### <a name="change-culture"></a>Alterar a cultura  
 O código de personalização de nível de documento geralmente compartilha o thread de interface do usuário principal do Excel, para que as alterações feitas para a cultura do thread afeta todo o resto que está em execução no thread em questão; a alteração não está restrita a sua personalização.  
  
 Controles dos Windows Forms são inicializados antes que o nível de aplicativo VSTO Add-ins são iniciados pelo aplicativo host. Nessas situações, a cultura deve ser alterada antes de configurar os controles de interface do usuário.  
  
## <a name="install-the-language-packs"></a>Instalar os pacotes de idiomas  
 Se você tiver configurações de inglês para Windows, você pode instalar o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] pacotes de idiomas para ver [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] mensagens no mesmo idioma do Windows. Se qualquer usuário final execute suas soluções com configurações diferentes do inglês para Windows, eles devem ter o pacote de idioma correto para ver mensagens de tempo de execução no mesmo idioma, como Windows. O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] pacotes de idiomas estão disponíveis as [Centro de download da Microsoft](http://www.microsoft.com/downloads).  
  
 Além disso, os pacotes de idiomas redistribuível do .NET Framework são necessários para as mensagens do ClickOnce. Os pacotes de idiomas do .NET Framework estão disponíveis a partir de [Centro de download da Microsoft](http://www.microsoft.com/downloads).  
  
## <a name="regional-settings-and-excel-com-calls"></a>Configurações regionais e chamadas de COM do Excel  
 Sempre que um cliente gerenciado chama um método em um objeto COM e ele precisa transmitir informações específicas da cultura, ele faz isso usando o <xref:System.Globalization.CultureInfo.CurrentCulture%2A> (localidade) que corresponde da localidade do thread atual. A localidade do thread atual é herdada de configurações regionais do usuário por padrão. No entanto, quando você faz uma chamada para o modelo de objeto do Excel de uma solução do Excel criada usando as ferramentas de desenvolvimento do Office no Visual Studio, o formato de dados de inglês (Estados Unidos) (localidade 1033 ID) é passado para o modelo de objeto do Excel automaticamente. Você deve formatar todos os dados que tem a formatação sensíveis à localidade, como datas e moeda, usando o formato de dados de inglês (Estados Unidos) antes de passá-lo para o Microsoft Office Excel ou ler os dados do código do seu projeto.  
  
## <a name="considerations-for-storing-data"></a>Considerações para o armazenamento de dados  
 Para garantir que seus dados serão corretamente interpretados e exibidos, você também deve considerar que podem ocorrer problemas quando um aplicativo está armazenando dados, como as fórmulas de planilha do Excel, em literais de cadeia de caracteres (embutido em código) em vez de em objetos fortemente tipados. Você deve usar os dados formatados supondo que um estilo de cultura invariável ou em inglês (Estados Unidos) (valor LCID 1033).  
  
### <a name="applications-that-use-string-literals"></a>Aplicativos que usam literais de cadeia de caracteres  
 Os valores possíveis que podem ser embutidos incluem literais de data que são escritos no formato inglês (Estados Unidos) e as fórmulas de planilha do Excel que contêm nomes de função localizadas. Outra possibilidade pode ser uma cadeia de caracteres embutido em código que contém um número, como "1.000"; em algumas culturas, isso é interpretado como mil, mas em outras culturas, ele representa um ponto zero. Cálculos e comparações executadas em um formato incorreto podem resultar em dados incorretos.  
  
 O Excel interpreta qualquer cadeias de caracteres de acordo com o LCID que é passado com a cadeia de caracteres. Isso pode ser um problema se o formato da cadeia de caracteres não corresponde ao LCID que é passado. Soluções do Excel criadas usando as ferramentas de desenvolvimento do Office no Visual Studio usam o LCID 1033 (en-US) ao passar todos os dados. O Excel exibe os dados de acordo com as configurações regionais e idioma da interface do usuário do Excel. Visual Basic for Applications (VBA) também funciona dessa maneira. cadeias de caracteres são formatadas como en-US e VBA quase sempre passa 0 (neutro de idioma) como o LCID. Por exemplo, o código VBA a seguir exibe um valor formatado corretamente de 12 de maio de 2004, de acordo com a configuração de localidade do usuário atual:  
  
```vb
'VBA  
Application.ActiveCell.Value2 = "05/12/04"  
```  
  
 O mesmo código, quando usado em uma solução criada usando as ferramentas de desenvolvimento do Office no Visual Studio e passado para o Excel por meio da interoperabilidade COM, produz os mesmos resultados quando a data é formatada no estilo de en-US.  
  
 Por exemplo:  
  
 [!code-vb[Trin_VstcoreCreatingExcel#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/Sheet1.vb#6)]
 [!code-csharp[Trin_VstcoreCreatingExcel#6](../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/Sheet1.cs#6)]  
  
 Você deve trabalhar com dados fortemente tipados em vez de literais de cadeia de caracteres sempre que possível. Por exemplo, em vez de armazenar uma data em uma cadeia de caracteres literal, armazená-lo como um <xref:System.Double>, em seguida, convertê-lo para um <xref:System.DateTime> objeto para manipulação.  
  
 O exemplo de código a seguir usa uma data que um usuário insere em célula A5, armazena-o como uma <xref:System.Double>, em seguida, convertê-lo para um <xref:System.DateTime> objeto para exibição na célula A7. A7 da célula deve ser formatada para exibir uma data.  
  
 [!code-vb[Trin_VstcoreCreatingExcel#7](../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/Sheet1.vb#7)]
 [!code-csharp[Trin_VstcoreCreatingExcel#7](../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/Sheet1.cs#7)]  
  
### <a name="excel-worksheet-functions"></a>Funções de planilha do Excel  
 Nomes de função de planilha são convertidos internamente para a maioria das versões de idioma do Excel. No entanto, devido à linguagem potencial e problemas de interoperabilidade COM é recomendável que você use nomes de função apenas em inglês no seu código.  
  
### <a name="applications-that-use-external-data"></a>Aplicativos que usam dados externos  
 Qualquer código que é aberta ou caso contrário, usa dados externos, como arquivos que incluem valores separados por vírgulas (arquivos CSV) exportados de um sistema herdado, também pode ser afetado se esses arquivos são exportados usando qualquer formato, além de en-US. Acesso de banco de dados não pode ser afetado porque todos os valores devem ser em formato binário, a menos que o banco de dados armazena datas como cadeias de caracteres ou executa operações que não usam o formato binário. Além disso, se você construir consultas SQL usando os dados do Excel, você precisa garantir que eles estejam no formato de en-US, dependendo da função que você usar.  
  
## <a name="see-also"></a>Consulte também  
 [Como: destinar a interface de usuário multilíngue do Office](../vsto/how-to-target-the-office-multilingual-user-interface.md)   
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  