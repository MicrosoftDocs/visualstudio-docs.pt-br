---
title: Atribuir GUIDs específicos a assinantes do Visual Studio | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.date: 02/18/2021
ms.topic: conceptual
description: Saiba como os administradores podem especificar GUID de assinatura para assinantes
ms.openlocfilehash: 3c92a3e6cc35230f6bcf10320e92a50dc5ffb85b
ms.sourcegitcommit: 79a6be815244f1cfc7b4123afff29983fce0555c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249679"
---
# <a name="assign-specific-subscriptions-in-the-visual-studio-subscriptions-administration-portal"></a>Atribuir assinaturas específicas no portal de administração de assinaturas do Visual Studio

Agora, os administradores podem usar o portal de administração de assinaturas do Visual Studio para atribuir assinaturas específicas a assinantes individuais.  Isso pode ser útil em situações em que a organização tem equipes temporárias ou fornecedores que precisam de acesso a uma assinatura por um curto período.  Os administradores podem atribuir uma assinatura que já foi parcialmente usada, deixando suas novas assinaturas para uso de termo mais longo.  

Assista ao vídeo ou Continue lendo para saber como atribuir GUIDs de assinaturas específicas a usuários. 

<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4t4cl]


## <a name="assign-specific-subscription-guids-to-users"></a>Atribuir GUIDs de assinatura específicos para os usuários

O processo de atribuição de assinaturas específicas a indivíduos envolve o aproveitamento de dois processos de administração existentes para atribuir identificadores globais exclusivos (GUIDs) de assinatura específica a usuários individuais.  O processo de três etapas inclui a exportação de uma lista de suas assinaturas e atribuições atuais, usando essa lista para identificar os GUIDs específicos que você deseja atribuir e, em seguida, usar o processo de adição em massa para carregar as novas atribuições.

### <a name="export-your-subscriptions-information"></a>Exportar suas informações de assinaturas

Para executar a exportação:
1. Entre no [portal de administração](https://manage.visualstudio.com).
2. Selecione a guia **Exportar** e o arquivo será baixado no computador local. O arquivo inclui o nome da conta do contrato que contém suas assinaturas do usuário e também a data da exportação.
> [!div class="mx-imgBorder"]
> ![Exportar assinantes](_img/exporting-subscriptions/exporting-subscriptions.png "Clique em exportar para salvar a lista de suas assinaturas atribuídas com as informações do Assinante.")

### <a name="identify-the-guids-you-want-to-assign"></a>Identificar os GUIDs que você deseja atribuir

Se você já usou a ferramenta de exportação anteriormente, observará que novos campos foram adicionados à planilha produzida.  Isso ajudará a determinar o status de cada assinatura e quais você deseja atribuir aos usuários.  

- **Status da assinatura**: esse campo indicará "atribuído" ou "não atribuído".  Se uma assinatura tiver um status "atribuído", ela também terá informações de usuário associadas a ele, como nome, email, etc. 
- **Status de uso**: o status de uso indicará "novo", o que significa que ele nunca foi atribuído a um usuário ou "usado", o que indica que ele foi atribuído a um usuário em algum momento.  

Você pode usar os valores nesses campos junto com outras informações na planilha para determinar quais assinaturas você deseja atribuir a usuários individuais. Você pode aplicar um filtro no Excel para ajudar a restringir a lista por status, nível de assinatura, data de validade, etc. 

### <a name="upload-your-new-assignments"></a>Carregar suas novas atribuições

A etapa final é baixar o modelo de **adição em massa** , preencher as informações necessárias para as assinaturas que você deseja atribuir e carregar o modelo.  Para obter uma descrição completa desse processo, consulte o artigo [adicionar vários usuários](assign-license-bulk.md) .  

> [!IMPORTANT]
> Para garantir um upload bem-sucedido, verifique se:
> - Você está usando o modelo vinculado na caixa de diálogo quando você seleciona **Adicionar em massa**.  Não use uma cópia armazenada localmente do modelo, pois ela pode não conter todos os campos obrigatórios.  Usar um modelo antigo fará com que o carregamento falhe. 
> - Todos os campos mostrados conforme **necessário** no modelo são concluídos.
> - Não há erros listados na coluna **mensagem de erro** .
> - Cada GUID é usado apenas uma vez no modelo. 
> - O nível de assinatura no modelo corresponde à assinatura do GUID na lista exportada. 
> - O GUID ainda não foi atribuído a outro usuário na lista exportada. 

## <a name="frequently-asked-questions"></a>Perguntas frequentes
### <a name="q-how-do-i-change-which-subscription-is-currently-assigned-to-an-individual-user"></a>P: Como fazer alterar qual assinatura está atribuída atualmente a um usuário individual?
R: se você quiser alterar qual GUID é atribuído a um usuário, primeiro você deve excluir a assinatura para esse usuário.  Para obter mais informações, consulte nosso artigo [excluir assinaturas](delete-license.md) para obter mais informações.  Depois de excluir a assinatura para esse usuário, use o processo descrito acima para exportar a lista e carregar as novas informações de assinatura.  

## <a name="resources"></a>Recursos
- [Suporte a assinaturas](https://visualstudio.microsoft.com/subscriptions/support/)

## <a name="see-also"></a>Confira também
- [Documentação do Visual Studio](/visualstudio/)
- [Documentação do Azure DevOps](/azure/devops/)
- [Documentação do Azure](/azure/)
- [Documentação do Microsoft 365](/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
Agora que você atribuiu assinaturas aos usuários, descubra como executar outras tarefas de administração.
- [Atribuir assinaturas individuais](assign-license.md)
- [Atribuir várias assinaturas](assign-license-bulk.md)
- [Editar assinaturas](edit-license.md)
- [Excluir assinaturas](delete-license.md)
- [Determinar o uso máximo](maximum-usage.md)


