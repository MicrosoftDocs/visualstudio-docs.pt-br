---
title: Página de publicação, Designer de projeto (desenvolvimento do Office no Visual Studio)
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VST.ProjectProperties.Publish.2007System
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- deploying applications [Office development in Visual Studio]
- publishing, Office solutions
- Property Pages dialog box, Publish [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: e4d315a00f527953500b47095ee4080b4eafd4cc
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672711"
---
# <a name="publish-page-project-designer-office-development-in-visual-studio"></a>Página de publicação, Designer de projeto (desenvolvimento do Office no Visual Studio)
  O **Publish** página do **Designer de projeto** é usado para configurar as propriedades de implantação.  
  
 Para acessar essa página, selecione o projeto no **Gerenciador de soluções**e, em seguida, na **Project** menu, escolha *Projectname* **propriedades** . Se o **Publish** página não for exibida, escolha o **publicar** guia.  
  
> [!NOTE]  
>  Você também pode definir o local de publicação **Assistente de publicação**. Para obter mais informações, consulte [como: publicar uma solução do Office usando o ClickOnce](https://msdn.microsoft.com/2b6c247e-bc04-4ce4-bb64-c4e79bb3d5b8).  
  
## <a name="uielement-list"></a>Lista UIElement  
 **Local da pasta de publicação (site da web, servidor ftp ou caminho do arquivo)**  
 Necessário.  
  
 O local da pasta de publicação é o diretório ao qual o Visual Studio copia os arquivos de solução, como os manifestos, assemblies e outros arquivos do build. Você deve ter acesso de gravação a esse diretório.  
  
 As opções incluem o computador local, um compartilhamento de arquivo UNC ou um site HTTP/HTTPS. O caminho pode ser local (*c:\foldername\publishfolder*), relativo (*publicar\\*), ou em um local totalmente qualificado (*\\\servername\foldername* ou http://<em>servername/foldername</em>).  
  
 Por padrão, é o local de publicação *http://localhost/projectname/* se você tiver o IIS instalado, ou o *publicar\\*  directory se você não tiver o IIS instalado.  
  
 **URL da Pasta de Instalação**  
 Opcional.  
  
 A URL da pasta de instalação é o diretório do qual o usuário final instalará a personalização. Também é o caminho que a solução usará para verificar se há atualizações. O caminho pode ser o mesmo que o local da pasta de publicação, mas isso não é um requisito.  
  
 As opções incluem o computador local, um compartilhamento de arquivo UNC ou um site HTTP/HTTPS. O caminho pode ser local (*c:\foldername\publishfolder*), relativo (*publicar\\*), ou em um local totalmente qualificado (*\\\servername\foldername* ou http://<em>servername/foldername</em>). Todos os locais HTTP/HTTPS devem ser criados com caracteres US-ASCII. Não há suporte para caracteres Unicode.  
  
 Se o caminho de instalação for definido, os arquivos de personalização devem ser nesse local para os usuários instalarem a personalização. O local deve ser definido somente se você souber o local de implantação final.  
  
 Se os arquivos de instalação estão em um local relativo do documento ou o programa de instalação, como com a opção de CD, deixe essa caixa em branco.  
  
 Esse valor pode ser atribuído por um administrador mais tarde. Para obter mais informações, consulte [como: alterar o caminho de instalação de uma solução do Office](https://msdn.microsoft.com/d0eaa07b-2d72-4902-899f-2f9fb165b8fd).  
  
 **Pré-requisitos**  
 Os pré-requisitos podem ser incluídos com o programa de instalação ou baixados por demanda durante a instalação.  
  
- **Baixar pré-requisitos do site do fornecedor do componente**: Use esta opção para baixar esses pré-requisitos da Microsoft.  
  
- **Baixar os pré-requisitos no mesmo local que meu aplicativo**: Use esta opção para os pré-requisitos no seu instalador do pacote. Incluir os arquivos de pré-requisito com o programa de instalação aumenta o tamanho da solução.  
  
- **Baixar os pré-requisitos no seguinte local**: Use esta opção para disponibilizar os pré-requisitos para os usuários finais separadamente como outro programa de instalação em uma página da web ou compartilhamento de rede.  
  
  **Atualizações**  
  O intervalo de atualização determina a frequência com que a solução verifica se há atualizações. O padrão é verificar a cada sete dias.  
  
  Verificar se há atualizações sempre que uma personalização no nível de documento ou um suplemento do VSTO é carregada seria mantê-lo atualizado, mas isso afetaria o desempenho de inicialização.  
  
  Se você estiver implantando por meio de um CD ou unidade removível, defina isso como **nunca verificar se há atualizações**.  
  
  **Opções (Descrição)**  
  As opções de publicação para as propriedades a seguir podem ser definidas:  
  
- Idioma de publicação: a localidade da solução do Office.  
  
- Nome do publicador: o nome da empresa ou o desenvolvedor como ele aparece na **adicionar ou remover programas** ou **programas e recursos**.  
  
- Nome do produto: o nome da solução do Office, como ele aparece na **adicionar ou remover programas** ou **programas e recursos**.  
  
- URL de suporte: o local para os usuários finais contatar o suporte técnico para a solução do Office.  
  
  **Opções (configurações do Office)**  
  As opções de publicação para as propriedades a seguir podem ser definidas:  
  
- Nome da solução: o nome da solução do Office como ela aparece no aplicativo do Office.  
  
- Descrição: a descrição da solução do Office como ela aparece no aplicativo do Office.  
  
- Comportamento de carregamento de suplementos do VSTO.  
  
  -   Carregar na inicialização: Especifica que o suplemento do VSTO carrega quando o aplicativo do Office é iniciado.  
  
  -   Carregar sob demanda: Especifica que o suplemento do VSTO carrega quando o aplicativo requer, como quando um usuário clica em um elemento de interface do usuário que usa a funcionalidade no suplemento do VSTO.  
  
  **Idioma de publicação** essa opção define o idioma dos termos de licença do Software Microsoft e inclui os pacotes de idiomas na lista de pré-requisitos. Ele não afeta o idioma da personalização. O idioma no programa de instalação é determinado pelos idiomas instalados do Visual Studio.  
  
  Para obter mais informações sobre como alterar o **idioma de publicação**, consulte [como: alterar o idioma de publicação para um aplicativo ClickOnce](/visualstudio/deployment/how-to-change-the-publish-language-for-a-clickonce-application).  
  
  **Versão da publicação**  
  Define o número de versão para a personalização. Quando o número de versão é alterado, o aplicativo é publicado como uma atualização. Uma nova pasta é criada para cada versão durante o processo de compilação para evitar a substituição da versão anteriormente publicada. Cada parte da versão de publicação (**principais**, **secundárias**, **Build**, **revisão**) pode conter até cinco dígitos.  
  
  **Incrementar automaticamente a revisão com cada versão**  
  Opcional. Quando selecionada (padrão), o **revisão** parte do número de versão é incrementado em um cada vez que a personalização é publicada. Isso faz com que a personalização a ser publicado como uma atualização.  
  
  **Publicar Agora**  
  Publica o aplicativo usando as configurações atuais. Equivalente à **terminar** botão na **Assistente de publicação**.  
  
## <a name="see-also"></a>Consulte também  
 [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)   
 [Implantar uma solução do Office usando o ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md)   
 [Pré-requisitos de solução do Office para implantação](https://msdn.microsoft.com/9f672809-43a3-40a1-9057-397ce3b5126e)  
  
  