## Introduction
- Deploy different policies for each OU individually. Windows manages such policies through **Group Policy Objects (GPO)**.
- GPOs can contain policies aimed at either users or computers, allowing you to set a baseline on specific machines and identities.

### To configure GPOs, you can use the **Group Policy Management** tool, available from the start menu:
![[AD_basics15.png]]
- The first thing you will see when opening it is your complete OU hierarchy, as defined before.
- To configure Group Policies, you first create a GPO under **Group Policy Objects** and then link it to the GPO where you want the policies to apply.

**Example** - you can see there are some already existing GPOs in your machine:
![[AD_basics16.png]]
- We can see in the image above that 3 GPOs have been created.
- From those, the `Default Domain Policy` and `RDP Policy` are linked to the `thm.local` domain as a whole, and the `Default Domain Controllers Policy` is linked to the `Domain Controllers` OU only.
- Something important to have in mind is that any GPO will apply to the linked OU and any sub-OUs under it. For example, the `Sales` OU will still be affected by the `Default Domain Policy`.

#### Let's examine the `Default Domain Policy`
**Scope** - 
- The first tab you'll see when selecting a GPO shows its **scope**, which is where the GPO is linked in the AD.
- For the current policy, we can see that it has only been linked to the `thm.local` domain:
![[AD_basics17.png]]
- As you can see, you can also apply **Security Filtering** to GPOs so that they are only applied to specific users/computers under an OU. By default, they will apply to the **Authenticated Users** group, which includes all users/PCs.

**Settings** - 
- The **Settings** tab includes the actual contents of the GPO and lets us know what specific configurations it applies.
- As stated before, each GPO has configurations that apply to computers only and configurations that apply to users only.
- In this case, the `Default Domain Policy` only contains Computer Configurations:
![[AD_basics18.png]]

## GPO editing
- Since this GPO applies to the whole domain, any change to it would affect all computers.
- Let's change the minimum password length policy to require users to have at least 10 characters in their passwords.
- To do this, right-click the GPO and select **Edit**:
![[AD_basics19.png]]
**This will open a new window where we can navigate and edit all the available configurations. To change the minimum password length, go to**
```python
Computer Configurations -> Policies -> Windows Setting -> Security Settings -> Account Policies -> Password Policy
```
![[AD_basics20.png]]

#### you can double-click the policy and read the **Explain** tab on each of them:
![[AD_basics21.png]]

## GPO distribution
- GPOs are distributed to the network via a network share called `SYSVOL`, which is stored in the DC.
- All users in a domain should typically have access to this share over the network to sync their GPOs periodically.
- The SYSVOL share points by default to the `C:\Windows\SYSVOL\sysvol\` directory on each of the DCs in our network.
- Once a change has been made to any GPOs, it might take up to 2 hours for computers to catch up

**If you want to force any particular computer to sync its GPOs immediately, you can always run the following command on the desired computer:**
```powershell
PS C:\> gpupdate /force
```

### Creating some GPOs for THM Inc.
**As part of our new job, we have been tasked with implementing some GPOs to allow us to:**
1. Block non-IT users from accessing the Control Panel.
2. Make workstations and servers lock their screen automatically after 5 minutes of user inactivity to avoid people leaving their sessions exposed.

##### Restrict Access to Control Panel
- Let's create a new GPO called `Restrict Control Panel Access` and open it for editing.
**Since we want this GPO to apply to specific users, we will look under `User Configuration` for the following policy:**
![[AD_basics22.png]]
Notice we have enabled the **Prohibit Access to Control Panel and PC settings** policy.
- Once the GPO is configured, we will need to link it to all of the OUs corresponding to users who shouldn't have access to the Control Panel of their PCs.

**In this case, we will link the `Marketing`, `Management` and `Sales` OUs by dragging the GPO to each of them:**
![[AD_basics23.png]]

##### Auto Lock Screen GPO
- Regarding screen locking for workstations and servers, we could directly apply it over the `Workstations`, `Servers` and `Domain Controllers` OUs we created previously.
- While this solution should work, an alternative consists of simply applying the GPO to the root domain, as we want the GPO to affect all of our computers. Since the `Workstations`, `Servers` and `Domain Controllers` OUs are all child OUs of the root domain, they will inherit its policies.
**Note:** You might notice that if our GPO is applied to the root domain, it will also be inherited by other OUs like `Sales` or `Marketing`. Since these OUs contain users only, any Computer Configuration in our GPO will be ignored by them.

**Let's create a new GPO, call it `Auto Lock Screen`, and edit it. The policy to achieve what we want is located in the following route:**
![[AD_basics24.png]]
- We will set the inactivity limit to 5 minutes so that computers get locked automatically if any user leaves their session open.

- After closing the GPO editor, we will link the GPO to the root domain by dragging the GPO to it:
![[AD_basics25.png]]
Once the GPOs have been applied to the correct OUs, we can log in as any users in either Marketing, Sales or Management for verification.

**Note:** If you created and linked the GPOs, but for some reason, they still don't work, remember you can run `gpupdate /force` to force GPOs to be updated.