---
title: How to create a service principal for Azure AD 
description: Give applications access to Azure Stack resources by creating service principals
services: azure-stack
author: David Woffendin
toc_rootlink: Users
toc_sub1: How To
toc_sub2:
toc_sub3:
toc_sub4:
toc_title: How to create a service principal for Azure AD 
toc_fullpath: Users/How To/azs-how-create-service-principals.md
toc_mdlink: azs-how-create-service-principals.md
---

# How to Give applications access to Azure Stack resources

## Overview

In Azure Stack you are able to give an application access to stack resources by creating a service principal that uses Azure Resource Manager. A service principal lets you delegate specific permissions using **role-based access control**. As a best practice, you should use service principals for your applications. Service principals are preferable to running an app using your own credentials for the following reasons:

* You can assign permissions to the service principal that are different than your own account permissions. Typically, a service principal's permissions are restricted to exactly what the app needs to do.
* You do not have to change the app's credentials if your role or responsibilities change.
* You can use a certificate to automate authentication when running an unattended script.

### Example

You have a configuration management app that needs to inventory Azure resources using Azure Resource Manager. You can create a service principal and assign it to the Reader role. This role gives the app read-only access to Azure resources.

## Getting started

Use the steps in this article as a guide to:

* Create a service principal for your app.
* Register your app and create an authentication key.
* Assign your app to a role.

## Create a service principal for Azure AD

If your Azure Stack uses Azure AD as the identity store, you can create a service principal using the same steps as in Azure, using the Azure portal. Please check that you have the require Azure AD permissions before trying to create a service principle.

### Creating a service principal

To create a service principal for your application:

1. Sign in to your Azure Account through the Public Azure portal.
2. Select **Azure Active Directory** > **App registrations** > **Add**.
    ![Microsoft Azure CSP invitation email](images/azs-portal-new-principle1.png)

3. Provide a name and URL for the application. Select either **Web app / API** or **Native** for the type of application you want to create. After setting the values, select **Create**.

    ![Microsoft Azure CSP invitation email](images/azs-portal-new-principle2.png)

### Get Credentials

When logging in programmatically, use the ID for your application and an authentication key. To get these values:

1. From App registrations in Active Directory, select your application.

2. Copy the Application ID and store it in your application code. The applications in the sample applications use client id when referring to the Application ID.

    ![Microsoft Azure CSP invitation email](images/azs-portal-new-principle3.png)
3. To generate an authentication key, select Keys.

    ![Microsoft Azure CSP invitation email](images/azs-portal-new-principle4.png)
4. Provide a description of the key, and a duration for the key. When done, select Save.

    ![Microsoft Azure CSP invitation email](images/azs-portal-new-principle5.png)
5. After you save the key, the key VALUE is displayed. Write down this value because you can't retrieve the key later. Store the key value where your application can retrieve it.

## Assign the service principal to a role

To access resources in your subscription, you must assign the application to a role. Decide which role represents the right permissions for the application.

 > [!TIP]
 > You can set a role's scope at the level of a subscription, a resource group, or a resource. Permissions are inherited to lower levels of scope. For example, an app with the Reader role for a resource group means that the app can read any of the resources in the resource group.

Use the following steps as a guide for assigning a role to a service principal.

1. In the Azure Stack portal, navigate to the level of scope you want to assign the application to. For example, to assign a role at the subscription scope, select Subscriptions.

2. Select the subscription to assign the application to. In this example, the subscription is highlighted.

    ![Microsoft Azure CSP invitation email](images/azs-portal-new-role1.png)
3. Select **Access Control (IAM)** for the subscription then click **+Add**.

    ![Microsoft Azure CSP invitation email](images/azs-portal-new-role2.png)
4. Select in **Role** the role you wish to assign to the application and then in **Select** search for your application, and select it.

    ![Microsoft Azure CSP invitation email](images/azs-portal-new-role3.png)
5. Select OK to finish assigning the role. You can see your application in the list of users assigned to a role for that scope.

Now that you've created a service principal and assigned a role, your application can access Azure Stack resources.

## Feedback

  If you find an issue with this article, click **Improve this Doc** to suggest a change. If you have an idea for how we could improve any of our services, visit [*UKCloud Ideas*](https://ideas.ukcloud.com). Alternatively, you can contact us at <products@ukcloud.com>.