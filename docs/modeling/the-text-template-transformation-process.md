---
title: O processo de transformação de modelo de texto
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, transformation process
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 1ace7528eb1685765fe5c7ff11ce9b3c3234a941
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49919150"
---
# <a name="the-text-template-transformation-process"></a>O processo de transformação de modelo de texto
O processo de transformação do modelo de texto utiliza um arquivo de modelo de texto como entrada e gera um novo arquivo de texto como saída. Por exemplo, você pode usar modelos de texto para gerar o código Visual Basic ou c#, ou você pode gerar um relatório HTML.

 Três componentes fazem parte desse processo: o mecanismo, o host e os processadores de diretriz. O mecanismo controla o processo. ele interage com o host e o processador de diretriz para produzir o arquivo de saída. O host fornece qualquer interação com o ambiente, como localizar arquivos e assemblies. O processador de diretriz adiciona funcionalidade, como ler dados de um arquivo XML ou um banco de dados.

 O processo de transformação do modelo de texto é executado em duas etapas. Primeiro, o mecanismo cria uma classe temporária, que é conhecida como a classe de transformação gerada. Essa classe contém o código que é gerado pelas diretivas e os blocos de controle. Depois disso, o mecanismo compila e executa a classe de transformação gerada para produzir o arquivo de saída.

## <a name="components"></a>Componentes

|Componente|Descrição|Personalizável (Sim/não)|
|-|-|-|
|mecanismo|O componente de mecanismo controla o processo de transformação do modelo de texto|Nº|
|Host|O host é a interface entre o mecanismo e o ambiente do usuário. O Visual Studio é um host do processo de transformação de texto.|Sim. Você pode escrever um host personalizado.|
|Processadores de diretriz|Processadores de diretiva são classes que lidam com diretivas em modelos de texto. Você pode usar diretivas para fornecer dados a um modelo de texto de uma fonte de entrada.|Sim. Você pode escrever os processadores de diretriz personalizados|

## <a name="the-engine"></a>O mecanismo
 O mecanismo recebe o modelo como uma cadeia de caracteres do host, que lida com todos os arquivos que são usados no processo de transformação. O mecanismo de, em seguida, solicita que o host para localizar quaisquer processadores de diretriz personalizados e outros aspectos do ambiente. O mecanismo, em seguida, compila e executa a classe de transformação gerada. O mecanismo retorna o texto gerado para o host, que normalmente salva o texto em um arquivo.

## <a name="the-host"></a>O Host
 O host é responsável por qualquer coisa que se relaciona com o ambiente de fora do processo de transformação, incluindo o seguinte:

-   Localizando arquivos de texto e binários solicitados pelo mecanismo de ou em um processador de diretriz. O host pode pesquisar diretórios e cache de assembly global para localizar assemblies. O host pode localizar o código de processador de diretriz personalizado para o mecanismo. O host também pode localizar e ler arquivos de texto e retornar seus conteúdos como cadeias de caracteres.

-   Fornecendo listas de assemblies padrão e namespaces que são usados pelo mecanismo para criar a classe de transformação gerada.

-   Desde que o domínio de aplicativo que é usado quando o mecanismo compila e executa a classe de transformação gerada. Um domínio de aplicativo separado é usado para proteger o aplicativo host de erros no código do modelo.

-   Gravar o arquivo de saída gerada.

-   Definindo a extensão padrão para o arquivo de saída gerada.

-   Tratamento de erros de transformação do modelo de texto. Por exemplo, o host pode exibir os erros na interface do usuário ou gravá-las em um arquivo. (No Visual Studio, os erros são exibidos na janela de mensagem de erro.)

-   Se um usuário chamou uma diretiva sem fornecer um valor, fornecendo um valor de parâmetro necessário. O processador de diretriz pode especificar o nome da diretiva e o parâmetro e solicitar que o host para fornecer um valor padrão se ele tiver um.

## <a name="directives-and-directive-processors"></a>Diretivas e processadores de diretriz
 Uma diretiva é um comando em seu modelo de texto. Ele fornece parâmetros para o processo de geração. Normalmente, as diretivas definem a origem e o tipo de modelo ou outra entrada e a extensão de nome de arquivo do arquivo de saída.

 Um processador de diretriz pode processar um ou mais diretivas. Quando você transformar um modelo, você deve ter instalado um processador de diretriz que pode lidar com as diretivas em seu modelo.

 As diretivas funcionam adicionando código na classe de transformação gerada. Você pode chamar as diretivas de um modelo de texto e os processos do mecanismo todas as chamadas de diretiva quando ele cria a classe de transformação gerada. Depois de chamar com êxito uma diretiva, o restante do código que você escreve em seu modelo de texto pode contar com a funcionalidade que a diretiva fornece. Por exemplo, você pode fazer a seguinte chamada para o `import` diretiva em seu modelo:

 `<#@ import namespace="System.Text" #>`

 O processador de diretriz padrão converte isso para um `using` instrução na classe de transformação gerada. Você pode usar o `StringBuilder` classe no restante do seu código de modelo sem qualificá-lo como `System.Text.StringBuilder`.