---
ms.openlocfilehash: 766f41b3d838130a5e0b64ba22425496eecb1c71
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584619"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="8b506-101">Dans cet exercice, vous allez créer une inscription de l’application Web Azure AD à l’aide du centre d’administration Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8b506-101">In this exercise, you will create a new Azure AD web application registration using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="8b506-102">Ouvrez un navigateur et accédez au [Centre d’administration Azure Active Directory](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8b506-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="8b506-103">Connectez-vous à l’aide d’un **compte personnel** (compte Microsoft) ou d’un **compte professionnel ou scolaire**.</span><span class="sxs-lookup"><span data-stu-id="8b506-103">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="8b506-104">Sélectionnez **Azure Active Directory** dans le volet de navigation gauche, puis sélectionnez **Inscriptions d’applications** sous **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="8b506-104">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="8b506-105">Une capture d’écran des inscriptions d’applications</span><span class="sxs-lookup"><span data-stu-id="8b506-105">A screenshot of the App registrations</span></span> ](./images/aad-portal-app-registrations.png)

1. <span data-ttu-id="8b506-106">Sélectionnez **Nouvelle inscription**.</span><span class="sxs-lookup"><span data-stu-id="8b506-106">Select **New registration**.</span></span> <span data-ttu-id="8b506-107">Sur la page **Inscrire une application**, définissez les valeurs comme suit.</span><span class="sxs-lookup"><span data-stu-id="8b506-107">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="8b506-108">Définissez le **Nom** sur `Blazor Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="8b506-108">Set **Name** to `Blazor Graph Tutorial`.</span></span>
    - <span data-ttu-id="8b506-109">Définissez les **Types de comptes pris en charge** sur **Comptes dans un annuaire organisationnel et comptes personnels Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="8b506-109">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="8b506-110">Sous **URI de redirection**, définissez la première flèche déroulante sur `Web`, et la valeur sur `https://localhost:5001/authentication/login-callback`.</span><span class="sxs-lookup"><span data-stu-id="8b506-110">Under **Redirect URI**, set the first drop-down to `Web` and set the value to `https://localhost:5001/authentication/login-callback`.</span></span>

    ![Capture d’écran de la page Inscrire une application](./images/aad-register-an-app.png)

1. <span data-ttu-id="8b506-112">Sélectionner **Inscription**.</span><span class="sxs-lookup"><span data-stu-id="8b506-112">Select **Register**.</span></span> <span data-ttu-id="8b506-113">Sur la page du **didacticiel de graphique éblouissant** , copiez la valeur de l' **ID d’application (client)** et enregistrez-la, vous en aurez besoin à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="8b506-113">On the **Blazor Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Une capture d’écran de l’ID d’application de la nouvelle inscription d'application](./images/aad-application-id.png)

1. <span data-ttu-id="8b506-115">Sous **Gérer**, sélectionnez **Authentification**.</span><span class="sxs-lookup"><span data-stu-id="8b506-115">Select **Authentication** under **Manage**.</span></span> <span data-ttu-id="8b506-116">Recherchez la section **Grant implicite** et activez les **jetons d’accès** et les **jetons ID**.</span><span class="sxs-lookup"><span data-stu-id="8b506-116">Locate the **Implicit grant** section and enable **Access tokens** and **ID tokens**.</span></span> <span data-ttu-id="8b506-117">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8b506-117">Select **Save**.</span></span>
