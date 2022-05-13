This document includes instruction on how to create a new compartment and assign a user to the newly created compartment.

# Creating a compartment

You can create a new compartment or use an existing compartment. You must have permission to create and delete compartments.

1. Open the navigation menu and click **Identity & Security**. Under **Identity**, click **Compartments**. A list of the compartments in your tenancy is displayed.

2. Select the compartment in which you want to create your instance or create a new compartment.

To create a new compartment:

1. Click **Create Compartment** to create the compartment to use for creating an instance.

2. Enter the following:

  * **Name**: Enter a name that is unique across all compartments in your tenancy (maximum 100 characters, including letters, numbers, periods, hyphens, and underscores). For example, enter a name such as OICCompartment.

  * **Description**: Enter a description for this compartment.

  * **Tags**: Enter tags to organize and list resources based on your business needs. See Managing Tags and Tag Namespaces.

3. Click **Create Compartment**.

4. Return to the navigation pane.

# Creating an account

You can follow a tutorial from OCI.

https://docs.oracle.com/en-us/iaas/Content/GSG/Tasks/addingusers.htm

## Create a Compartment and Add a User with Access to It

In this example, create a compartment called "Sandbox" and then create a user with access to only that compartment.

Procedure Overview: To provide access to the Sandbox compartment and all the resources in it, you create a group (SandboxGroup), and then create a policy (SandboxPolicy) to define the access rule.

To enable access for users created in Identity Cloud Service, create a group in IDCS (IDCSSandboxGroup), and map it to the SandboxGroup.

Finally, create an IDCS user and add them to the IDCSSandboxGroup.

### Create a sandbox compartment
1. Open the navigation menu and click Identity & Security. Under Identity, click Compartments.
2. Click Create Compartment.
3. Enter the following:
 * Name: Enter Sandbox.
 * Decription: Enter a description (required), for example: Sandbox compartment for users to try out OCI.
4. Click Create Compartment.

Your compartment is displayed in the list.


### Create an Oracle Cloud Infrastructure group
Next, create the "SandboxGroup" that you will create the policy for.

1. Open the navigation menu and click Identity & Security. Under Identity, click Groups.
2. Click Create Group.
3. In the Create Group dialog:
 * Name: Enter a unique name for your group, for example, SandboxGroup. Note that the name cannot contain spaces.
 * Description: Enter a description (required).
4. Click Create.

### Create a policy
Create the policy to give the SandboxGroup permissions in the Sandbox compartment.

1. Open the navigation menu and click Identity & Security. Under Identity, click Policies.
2. Under List Scope, ensure that you are in your root compartment.
3. Click Create Policy.
4. Enter a unique Name for your policy, for example, SandboxPolicy.

 * Note that the name cannot contain spaces.
 * Enter a Description (required), for example, Grants users full permissions on the Sandbox compartment.
 * Enter the following Statement:

```
Allow group SandboxGroup to manage all-resources in compartment Sandbox
```

This statement grants members of the SandboxGroup group full access to the Sandbox compartment.

5. Click Create.


### Create an Oracle Identity Cloud Service group
Next, create the "IDCS_SandboxGroup" in Oracle Identity Cloud Service.

1. Open the navigation menu and click Identity & Security. Under Identity, click Federation.
2. Click your Oracle Identity Cloud Service federation. For most tenancies, the federation is named OracleIdentityCloudService. The identity provider details page is displayed.
3. Under Resources, click Groups.
4. Click create IDCS Group.
5. In the Create IDCS Group dialog enter the following:
 * Name: Enter a unique name for your group, for example, IDCS_SandboxGroup. Note that the name cannot contain spaces.
 * Description: Enter a description (required).
6. Click Create.

The group is created and it is displayed in the identity provider details page. Next, map the group.


### Map the Oracle Identity Cloud Service Group to the Oracle Cloud Infrastructure group
Next, you need to map the Oracle Identity Cloud Service group to the Oracle Cloud Infrastructure group you created. The mapping gives the members of the IDCS group the permissions you granted to the OCI group.

1. On the identity provider details page, click Group Mapping. The group mappings are displayed.
2. Click Edit Mapping.
3. Click + Add Mapping.
4. From the Identity Provider Group menu list, choose the IDCS_SandboxGroup.
5. From the OCI Group menu list, select the SandboxGroup.
6. Click Submit.


Users that are members of the Oracle Identity Cloud Service groups mapped to the Oracle Cloud Infrastructure groups are now listed in the Console on the Users page. See Managing User Capabilities for Federated Users for more information on assigning these users additional credentials.

### Create a user
1. Open the navigation menu and click Identity & Security. Under Identity, click Federation.
2. Click your Oracle Identity Cloud Service federation. For most tenancies, the federation is named OracleIdentityCloudService. The identity provider details page is displayed.
3. Click Create IDCS User.
4. In the Create IDCS User dialog enter the following:
 * Username: Enter a unique name or email address for the new user. The value will be the user's login to the Console and must be unique across all other users in your tenancy.
 * Email: Enter an email address for this user. The initial sign-in credentials will be sent to this email address.
 * First Name: Enter the user's first name.
 * Last Name: Enter the user's last name.
 * Phone Number: Optionally, enter a phone number.
 * Groups: Select the group you created in the previous step, for example, IDCS_SandboxGroup.
5. Click Create.

The user is created in Oracle Identity Cloud Service. This user can't access their account until they complete the password reset steps.
Click Email Password Instructions to send the password link and instructions to the user.

The password link is good for 24 hours. If the user does not reset their password in time, you can generate a new password link by clicking Reset Password for the user.
When this user signs in they can see the compartments they have access to and they can only view, create, and manage resources in the Sandbox compartment. This user cannot create other users or groups.
