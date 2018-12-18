---
title: 'Como: gerenciar arquivos de dados locais em seu projeto | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.data.LocalConnectionConverter
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- mdf files
- local data
- .mdb files
- .mdf files
- data [Visual Studio], local
- mdb files
ms.assetid: 3ffa1aa9-17e4-422c-a02f-09224828cdfc
caps.latest.revision: 29
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 16e2d38dda97bd8a7f130254b2f23be9f17e0ac4
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49271369"
---
# <a name="how-to-manage-local-data-files-in-your-project"></a>Como gerenciar arquivos de dados locais no projeto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um arquivo de banco de dados local pode ser incluído como um arquivo em um projeto. Na primeira vez que você se conectar a um arquivo de banco de dados local, você pode escolher criar uma cópia em seu projeto ou conecte-se ao arquivo existente em seu local atual. Se você se conectar ao arquivo existente, ele será deixado no local original. Se você optar por copiar o arquivo no seu projeto, o Visual Studio cria uma cópia dele, adiciona-o ao seu projeto e modifica a conexão para apontar para a cópia. Outras conexões, como aqueles no Gerenciador de servidores também são modificados.  
  
 A configuração padrão da propriedade depende do tipo de arquivo de banco de dados que você está usando. O comportamento do **Copy to Output Directory** propriedade não se aplica a Web ou projetos C++.  
  
 Durante o desenvolvimento, você talvez queira exibir os efeitos do seu código no banco de dados sem fazer essas alterações permanentes. Você pode fazer isso pela configuração do **Copy to Output Directory** propriedade do arquivo como true. Cada vez que as compilações do projeto ou você pressionar F5, o arquivo é copiado para a pasta bin e as alterações são feitas nesse arquivo, não para o arquivo na pasta raiz do seu projeto. O arquivo de banco de dados na pasta raiz do projeto é alterado ao editar o esquema de banco de dados ou dados usando **Gerenciador de servidores**, **Database Explorer** ou em outra janela de ferramenta.  
  
 A tabela a seguir descreve as configurações do **Copy to Output Directory** propriedade.  
  
|Configuração|Comportamento|  
|-------------|--------------|  
|**Copiar se mais recente** (padrão para arquivos. sdf)|O arquivo de banco de dados é copiado do diretório do projeto para o **bin** diretório na primeira hora que o projeto é compilado. Cada vez subsequente que você compila o projeto, o **data de modificação** propriedade dos arquivos é comparada. Se o arquivo na pasta do projeto for mais recente, ele é copiado para o **bin** pasta, substituindo o arquivo que está atualmente lá. Se o arquivo na **bin** pasta for mais recente, nenhum arquivo será copiado. Essa configuração mantém todas as alterações feitas aos dados durante o tempo de execução, o que significa que sempre que você executa o aplicativo e salva as alterações dos dados, essas alterações são visíveis na próxima vez que você executar o aplicativo. **Cuidado:** não recomendamos essa opção para arquivos. mdb ou. mdf. O arquivo de banco de dados pode mudar mesmo quando nenhuma alteração é feita aos dados. Simplesmente abrindo uma conexão em um arquivo de dados (por exemplo, expandindo a **tabelas** nó no **Gerenciador de servidores**) pode marcá-lo como mais recente.|  
|**Copiar sempre** (padrão para arquivos. mdf e. mdb)|O arquivo de banco de dados é copiado do diretório do projeto no diretório /bin sempre que você criar seu aplicativo. Portanto, se você cria seu aplicativo e salve as alterações no arquivo no diretório /bin, essas alterações serão sobrescritas na próxima vez que o arquivo original é copiado para o diretório /bin.|  
|**Não copiar**|O arquivo nunca é copiado ou substituído pelo sistema do projeto. Você deve copiar manualmente o arquivo do diretório do projeto para o diretório de saída se você usar essa configuração.|  
  
## <a name="procedure"></a>Procedimento  
  
#### <a name="to-respond-to-the-local-database-file-dialog-box"></a>Para responder a caixa de diálogo de arquivo de banco de dados Local  
  
-   Clique em **Sim** se você quiser que o Visual Studio para copiar o arquivo de banco de dados no seu projeto e modificar a conexão para apontar para a cópia em seu projeto. Para obter mais informações sobre como trabalhar com arquivos de banco de dados em seu projeto, consulte [visão geral de dados locais](../data-tools/local-data-overview.md).  
  
-   Clique em **não** se você não quiser que o Visual Studio para copiar o arquivo de banco de dados no seu projeto. Em vez disso, os pontos de conexão para o arquivo no local original e o arquivo de banco de dados não é adicionado como um arquivo ao projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Conectando a dados em um arquivo de banco de dados Local (Windows Forms)](../data-tools/walkthrough-connecting-to-data-in-a-local-database-file-windows-forms.md)   
 [Conectar-se a dados em um banco de dados do Access (Windows Forms)](../data-tools/connect-to-data-in-an-access-database-windows-forms.md)