---
title: Globalização e localização de soluções do Excel
description: Saiba mais sobre considerações especiais para Microsoft Office soluções do Excel que serão executadas em computadores com configurações diferentes do inglês para o Windows.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- globalization [Office development in Visual Studio], configuring
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f3d77085808fb54cd0a0517cc6d039e2345a1872
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827975"
---
# <a name="globalization-and-localization-of-excel-solutions"></a>Globalização e localização de soluções do Excel
  Esta seção contém informações sobre considerações especiais para Microsoft Office soluções do Excel que serão executadas em computadores com configurações diferentes do inglês para o Windows. A maioria dos aspectos de globalizar e localizar soluções de Microsoft Office são as mesmas que você encontra ao criar outros tipos de soluções usando o Visual Studio. Para obter informações gerais, consulte [globalizar e localizar aplicativos](../ide/globalizing-and-localizing-applications.md).

 Por padrão, os controles de host no Microsoft Office Excel funcionam corretamente em qualquer configuração regional do Windows, desde que todos os dados passados ou manipulados usando código gerenciado sejam formatados usando a formatação em inglês (Estados Unidos). Em projetos direcionados [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] para o ou o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] , esse comportamento é controlado pelo Common Language Runtime (CLR).

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="format-data-in-excel-with-various-regional-settings"></a>Formatar dados no Excel com várias configurações regionais
 Você deve Formatar todos os dados que têm formatação sensível à localidade, como datas e moeda, usando o formato de dados em inglês (Estados Unidos) (ID de localidade 1033) antes de passá-lo para Microsoft Office Excel ou ler os dados do código em seu projeto do Office.

 Por padrão, quando você desenvolve uma solução do Office no Visual Studio, o modelo de objeto do Excel espera a formatação de dados da ID de localidade 1033 (isso também é chamado de bloquear o modelo de objeto para a ID de localidade 1033). Esse comportamento corresponde à maneira como o Visual Basic for Applications funciona. No entanto, você pode modificar esse comportamento em suas soluções do Office.

### <a name="understand-how-the-excel-object-model-always-expects-locale-id-1033"></a>Entenda como o modelo de objeto do Excel sempre espera a ID de localidade 1033
 Por padrão, as soluções do Office que você cria usando o Visual Studio não são afetadas pelas configurações de localidade do usuário final e sempre se comportam como se a localidade fosse Inglês (Estados Unidos). Por exemplo, se você obtiver ou definir a <xref:Microsoft.Office.Interop.Excel.Range.Value2%2A> propriedade no Excel, os dados deverão ser formatados da maneira esperada pela ID de localidade 1033. Se você usar um formato de dados diferente, poderá obter resultados inesperados.

 Embora você use o formato Inglês (Estados Unidos) para dados que são passados ou manipulados pelo código gerenciado, o Excel interpreta e exibe os dados corretamente de acordo com a configuração de localidade do usuário final. O Excel pode formatar os dados corretamente porque o código gerenciado passa a ID de localidade 1033 junto com os dados, o que indica que os dados estão no formato Inglês (Estados Unidos) e, portanto, devem ser reformatados para corresponder à configuração de localidade do usuário.

 Por exemplo, se os usuários finais tiverem suas opções regionais definidas para a localidade alemão (Alemanha), eles esperam que a data 29 de junho de 2005 seja formatada desta forma: 29.06.2005. No entanto, se sua solução passar a data para o Excel como uma cadeia de caracteres, você deverá Formatar a data de acordo com o formato Inglês (Estados Unidos): 6/29/2005. Se a célula for formatada como uma célula de data, o Excel exibirá a data no formato alemão (Alemanha).

### <a name="pass-other-locale-ids-to-the-excel-object-model"></a>Passe outras IDs de localidade para o modelo de objeto do Excel
 O Common Language Runtime (CLR) passa automaticamente a ID de localidade 1033 para todos os métodos e propriedades no modelo de objeto do Excel que aceitam dados sensíveis à localidade. Não é possível alterar esse comportamento automaticamente para todas as chamadas para o modelo de objeto. No entanto, você pode passar uma ID de localidade diferente para um método específico usando <xref:System.Type.InvokeMember%2A> para chamar o método e passando a ID de localidade para o parâmetro *Culture* do método.

## <a name="localize-document-text"></a>Localizar texto do documento
 O documento, modelo ou pasta de trabalho em seu projeto provavelmente inclui texto estático, que deve ser localizado separadamente do assembly e de outros recursos gerenciados. Uma maneira simples de fazer isso é fazer uma cópia do documento e traduzir o texto usando Microsoft Office Word ou Microsoft Office Excel. Esse processo funciona mesmo que você não faça nenhuma alteração no código, pois qualquer número de documentos pode ser vinculado ao mesmo assembly.

 Você ainda deve certificar-se de que qualquer parte do seu código que interaja com o texto do documento continue a corresponder ao idioma do texto e que os indicadores, os intervalos nomeados e outros campos de exibição acomodam qualquer reformatação do documento do Office que fosse necessário para se ajustar para gramática e comprimento de texto diferentes. Para modelos de documento que contêm relativamente pouco texto, convém considerar armazenar o texto em arquivos de recursos e, em seguida, carregar o texto em tempo de execução.

### <a name="text-direction"></a>Direção do texto
 No Excel, você pode definir uma propriedade da planilha para renderizar o texto da direita para a esquerda. Os controles de host ou qualquer controle que tenha uma `RightToLeft` propriedade, que é colocado no designer, correspondem automaticamente a essas configurações em tempo de execução. O Word não tem uma configuração de documento para texto bidirecional (basta alterar seu alinhamento de texto), para que os controles não possam ser mapeados para essa configuração. Em vez disso, você deve definir o alinhamento de texto para cada controle. É possível escrever código para percorrer todos os controles e forçá-los a renderizar texto da direita para a esquerda.

### <a name="change-culture"></a>Alterar cultura
 O código de personalização no nível do documento normalmente compartilha o thread da interface do usuário principal do Excel, portanto, quaisquer alterações feitas na cultura do thread afetarão tudo o que estiver em execução nesse thread; a alteração não é restrita à sua personalização.

 Windows Forms controles são inicializados antes que os suplementos do VSTO no nível do aplicativo sejam iniciados pelo aplicativo host. Nessas situações, a cultura deve ser alterada antes de definir os controles da interface do usuário.

## <a name="install-the-language-packs"></a>Instalar os pacotes de idiomas
 Se você tiver configurações diferentes do inglês para o Windows, poderá instalar os [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] pacotes de idiomas para ver [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] as mensagens no mesmo idioma que o Windows. Se qualquer usuário final executar suas soluções com configurações diferentes do inglês para o Windows, eles deverão ter o pacote de idiomas correto para ver as mensagens de tempo de execução no mesmo idioma que o Windows. Os [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] pacotes de idiomas estão disponíveis no [centro de download da Microsoft](https://www.microsoft.com/download).

 Além disso, os pacotes de idiomas .NET Framework redistribuíveis são necessários para mensagens do ClickOnce. Os pacotes de idiomas .NET Framework estão disponíveis no [centro de download da Microsoft](https://www.microsoft.com/download).

## <a name="regional-settings-and-excel-com-calls"></a>Configurações regionais e chamadas COM do Excel
 Sempre que um cliente gerenciado chama um método em um objeto COM e precisa passar informações específicas de cultura, ele faz isso usando o <xref:System.Globalization.CultureInfo.CurrentCulture%2A> (localidade) que corresponde à localidade do thread atual. A localidade do thread atual é herdada das configurações regionais do usuário por padrão. No entanto, quando você faz uma chamada para o modelo de objeto do Excel de uma solução do Excel criada usando as ferramentas de desenvolvimento do Office no Visual Studio, o formato de dados em inglês (Estados Unidos) (ID de localidade 1033) é passado para o modelo de objeto do Excel automaticamente. Você deve Formatar todos os dados que têm formatação sensível à localidade, como datas e moeda, usando o formato de dados em inglês (Estados Unidos) antes de passá-lo para Microsoft Office Excel ou ler os dados do código do projeto.

## <a name="considerations-for-storing-data"></a>Considerações sobre o armazenamento de dados
 Para garantir que os dados sejam interpretados e exibidos corretamente, você também deve considerar que os problemas podem ocorrer quando um aplicativo estiver armazenando dados, como fórmulas de planilha do Excel, em literais de cadeia de caracteres (embutidos em código) em vez de em objetos fortemente tipados. Você deve usar dados formatados supondo um estilo Culture-invariável ou inglês (Estados Unidos) (o valor LCID 1033).

### <a name="applications-that-use-string-literals"></a>Aplicativos que usam literais de cadeia de caracteres
 Os valores possíveis que podem ser embutidos em código incluem literais de data que são gravados no formato Inglês (Estados Unidos) e fórmulas de planilha do Excel que contêm nomes de funções localizadas. Outra possibilidade pode ser uma cadeia de caracteres embutida em código que contenha um número como "1.000"; em algumas culturas, isso é interpretado como 1000, mas em outras culturas, ele representa um ponto zero. Os cálculos e as comparações executadas no formato incorreto podem resultar em dados incorretos.

 O Excel interpreta todas as cadeias de caracteres de acordo com o LCID que é passado com a cadeia de caracteres. Isso pode ser um problema se o formato da cadeia de caracteres não corresponder ao LCID que é passado. As soluções do Excel criadas usando as ferramentas de desenvolvimento do Office no Visual Studio usam o LCID 1033 (en-US) ao passar todos os dados. O Excel exibe os dados de acordo com as configurações regionais e o idioma da interface do usuário do Excel. Visual Basic for Applications (VBA) também funciona dessa forma; as cadeias de caracteres são formatadas como en-US e o VBA quase sempre passa 0 (neutro à linguagem) como o LCID. Por exemplo, o código VBA a seguir exibe um valor formatado corretamente para 12 de maio de 2004, de acordo com a configuração de localidade do usuário atual:

```vb
'VBA
Application.ActiveCell.Value2 = "05/12/04"
```

 O mesmo código, quando usado em uma solução criada usando as ferramentas de desenvolvimento do Office no Visual Studio e passado para o Excel por meio da interoperabilidade COM, produz os mesmos resultados quando a data é formatada no estilo en-US.

 Por exemplo:

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/Sheet1.vb" id="Snippet6":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/Sheet1.cs" id="Snippet6":::

 Você deve trabalhar com dados fortemente tipados em vez de literais de cadeia de caracteres sempre que possível. Por exemplo, em vez de armazenar uma data em um literal de cadeia de caracteres, armazená-la como um <xref:System.Double> e, em seguida, convertê-la em um <xref:System.DateTime> objeto para manipulação.

 O exemplo de código a seguir leva uma data que um usuário insere na célula A5, armazena-a como um <xref:System.Double> , em seguida, converte-a em um <xref:System.DateTime> objeto para exibição na célula A7. A célula A7 deve ser formatada para exibir uma data.

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/Sheet1.vb" id="Snippet7":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/Sheet1.cs" id="Snippet7":::

### <a name="excel-worksheet-functions"></a>Funções de planilha do Excel
 Os nomes das funções de planilha são traduzidos internamente para a maioria das versões de idioma do Excel. No entanto, devido a problemas de interoperabilidade COM e de linguagem potencial, é recomendável que você use apenas nomes de funções em inglês em seu código.

### <a name="applications-that-use-external-data"></a>Aplicativos que usam dados externos
 Qualquer código que abre ou, de outra forma, usa dados externos, como arquivos que incluem valores separados por vírgulas (arquivos CSV) exportados de um sistema herdado, também poderá ser afetado se esses arquivos forem exportados usando qualquer formato além de en-US. O acesso ao banco de dados pode não ser afetado porque todos os valores devem estar no formato binário, a menos que o banco de dados armazene datas como cadeias de caracteres ou execute operações que não usem o formato binário. Além disso, se você construir consultas SQL usando dados do Excel, talvez seja necessário garantir que elas estejam no formato en-US, dependendo da função usada.

## <a name="see-also"></a>Consulte também

- [Como: direcionar a interface do usuário multilíngüe do Office](../vsto/how-to-target-the-office-multilingual-user-interface.md)
- [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)