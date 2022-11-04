

#Git integration with Styra DAS

**Prerequisites:**

- Docker
- [_ **kubectl** _](https://kubernetes.io/docs/tasks/tools/#kubectl) to interact with the Kubernetes cluster
- Istio 1.9.2 or later installed on Kubernetes 1.20 or later/ Install [_ **Istio** _](https://istio.io/latest/docs/setup/getting-started/#download)
- Styra recommends that you use[_ **minikube** _](https://minikube.sigs.k8s.io/docs/start/) version v1.0+ with Kubernetes 1.20

(or)

- Install[_ **K3d Cluster** _](https://k3d.io/v5.3.0/)
- StyraDAS Account. If you don't have a Styra DAS tenant, you can [sign up for a free tenant here](https://www.styra.com/pricing)**(**[**Signup**](https://signup.styra.com/?_ga=2.47247396.283531518.1641954102-757179015.1635396444)**).**

**System creation in DAS:**

- Login to StyraDAS tenent

![](RackMultipart20221104-1-bi4q9t_html_5e687a51b864840c.png)

- Styra DAS account is required
- If you don't have a Styra DAS tenant, you can [sign up for a free tenant here](https://signup.styra.com/?_ga=2.47247396.283531518.1641954102-757179015.1635396444)([Signup](https://signup.styra.com/?_ga=2.47247396.283531518.1641954102-757179015.1635396444))

**Create an Istio System**

To demonstrate the enforcement of ingress and egress policies for a sample application, you can start by creating a new Styra Istio system. Systems are displayed on the left side of the navigation panel.

To add a new Istio system, click the ( ⨁ ) plus icon next to SYSTEMS on the left side of the navigation panel.

![](RackMultipart20221104-1-bi4q9t_html_e915730faca49e55.png)

Create an Istio System in StyraDAS

**Fill in the following fields:**

- System type (required)
- System name (required)
- Description (optional)
- Leave the Read-only switch ON to prevent users from modifying policies.
- Click on Add System Button

**Configure Git Authentication**** [​](https://docs.styra.com/policies/git-management/use-git-storage-workspace#configure-git-authentication):**

The following shows how to configure Git for each Workspace individually.

- Under WORKSPACE, click the workspace name for which you want to save policies in Git.
- Click Settings tab.
- Click Git Repository.

The Styra DAS UI supports the HTTPS and SSH authentication for Git. You can navigate to the Git settings dialog and select the Git authentication mode HTTPS or SSH that will allow you to switch between the two authentication modes. The Git settings may have only one authentication mode selected per workspace level.

HTTPS

- Git username (required): Your Git username.
- Git secret (required): The secret corresponding to your Git username.

Styra recommends to use a GitHub Personal access token. You can generate a token at [github.com/settings/token](https://github.com/settings/tokens) or by clicking through Your-picture and navigate to Settings \>\> Developer Settings \>\> Personal access tokens.

- Git repository (required): A Git HTTPS URL to your Git repository. For example: ![](RackMultipart20221104-1-bi4q9t_html_993f65fe7a2da564.png)
- Git reference: Specify a tag or branch reference (defaults to refs/heads/master—the master branch).
- Git commit SHA: Specify a commit SHA.
- Repository path: (_Optional_) The subdirectory where you want to save the policies.

Click the Save changes button.

- Click on Test connection and we can observe the connected with green tick mark as below

![](RackMultipart20221104-1-bi4q9t_html_5cc68ef4b04d83d4.png)

- We can also notice that the Git repository has been tracked along with the master branch as reference.

![](RackMultipart20221104-1-bi4q9t_html_49d59a1b7deb74b2.png)

**Git as a storage:**

Styra DAS supports using Git as a storage mechanism for policies. Each system can be configured with its own Git repository as storage.

- Make a policy change in the Styra editor.
- Promote the change. Styra pushes this policy to our GitHub repository in a special branch.

![](RackMultipart20221104-1-bi4q9t_html_595bf4a2278e2dd9.png)

After pushing the changes we see the differences in the Github repository as below

![](RackMultipart20221104-1-bi4q9t_html_c8bf187974e9138d.png)

And the rego policy file will be added.

  ![](RackMultipart20221104-1-bi4q9t_html_c41c4b3387fd3c00.png)

**Creation of Stack and adding systems to stack:**

- **Styra DAS account is required**
- **If you don't have a Styra DAS tenant, you can** [**sign up for a free tenant here**](https://signup.styra.com/?_ga=2.47247396.283531518.1641954102-757179015.1635396444)**(**[**Signup**](https://signup.styra.com/?_ga=2.47247396.283531518.1641954102-757179015.1635396444)**)**

**Adding a Stack:**

1. Click the ( ⨁ ) plus icon next to the **STACKS**.
2. In the **Add Stack** , select the **Stack Type** from the drop down list.
3. Enter a **Stack name**..
4. It is optional to type a description in the **Description** field.
5. Click **Add stack**.

![](RackMultipart20221104-1-bi4q9t_html_23b4daf87b78329f.png)

**Add Systems to Stack:**

Your stack identifies the systems through the use of selectors defined by the stack, along with labels defined by individual systems. You must configure the selectors and labels, in order to add systems to your stack.

System label and selector label should match in order to apply stack rules to them.

**Adding selector label:**

1. Open the **Selectors** module.
2. Fill out the include Key and Values fields with a label key-value pair, such as "environment" and "Dev" as shown in the below image..

![](RackMultipart20221104-1-bi4q9t_html_5dc63ece8e79eb91.png)

   3. Click on the **publish** icon in order to activate your changes.

![](RackMultipart20221104-1-bi4q9t_html_89fbf97454fd736b.png)

**Add a label to the system:**

1. Pick a system from the **Systems** section of the navigation panel in which you wanted to apply the stack to.
2. Click on the **Labels** module.
3. Click a ( ⨁ ) plus icon to create a new label.
4. Enter a "Key and Value" pair that matches the selector you defined previously.
5. Click on the publish icon to activate your changes.

![](RackMultipart20221104-1-bi4q9t_html_88fdd5a3053d5d0f.png)

**Verify the connection:**

To verify if the systems are connected to your stack:

1. Return to the stack's Selectors module.
2. Click the Preview button and you can see the corresponding system name and id as shown in the image below.

![](RackMultipart20221104-1-bi4q9t_html_147ae1860b61d538.png)

**Add a Stack Rule:**

1. Click on stack's Mutating or Validating \>\> Rules module.
2. Click Add rule button.
3. Select the rule from the drop down list.
4. Ensure that Monitor is selected for the rule.
5. Click on the preview button and check the output before applying the rule.

**Validate a stack policy:**

You can click Validate while viewing a stack policy to run tests, perform an audit of monitored rules, and replay decisions to see how outcomes across your systems might be affected by your stack's rules.

By validating we can check whether the system is compliant or not as shown in the below images.

  ![](RackMultipart20221104-1-bi4q9t_html_3c79ad16516d50d7.png)

![](RackMultipart20221104-1-bi4q9t_html_d2daf9e1dcf05c53.png)

The Compliance pane only lists violations of the stack's rules and the Decisions pane only displays outcomes that changed because of a stack rule.

![](RackMultipart20221104-1-bi4q9t_html_3b7f444f2f3767b9.png)

After validating you can click the publish icon to apply your changes.

**Git integration configuration (HTTPS) (can happen at the same time as system creation) **

**Prerequisites:**

1. Install styra CLI in your machine. [LINK](https://docs.styra.com/reference/cli/install-use-cli)

For storing github credentials:

curl -H "Content-Type: application/json"  -H 'Authorization: Bearer  token' -X PUT https://TENANT.styra.com/v1/secrets/git/cred -d '{"name": "github id", "secret": "github token" }'

For creating envoy system with git integration configuration

curl -H "Content-Type: application/json"  -H 'Authorization: Bearer token' -X POST  https://TENANT.styra.com/v1/systems -d '{"type": "template.envoy:2.0", "name": "test-system", "source\_control": { "origin": { "url": "{git repo url}", "credentials": "git/cred", "reference": "refs/heads/master" } } }'

     Checking the git integration connection for system created through API.

![](RackMultipart20221104-1-bi4q9t_html_ba5826a7d7334d4b.png)

**Creating a System in Styra DAS using API**

Prerequisite:

- Styra DAS account is required
- If you don't have a Styra DAS tenant, you can [sign up for a free tenant here](https://signup.styra.com/?_ga=2.47247396.283531518.1641954102-757179015.1635396444)([Signup](https://signup.styra.com/?_ga=2.47247396.283531518.1641954102-757179015.1635396444))
- You must have an API token that has the WorkspaceAdministrator role to work with API

**Create a API Token using GUI:**

- Go to  WorkSpace —-- Settings —- API Tokens and click on  Add  API Token as shown below.

                  ![](RackMultipart20221104-1-bi4q9t_html_9d68f32d5ab00af9.png)

- Add the required fields and click on Add API token and save the API Token

               ![](RackMultipart20221104-1-bi4q9t_html_ec73ae9750e42101.png)

**Create a Envoy System:**

To Create an Envoy system using API run the below command .(Linux terminal,Git bash)

Documentation [Link](https://docs.styra.com/api#tag/systems/operation/CreateSystem) : [https://docs.styra.com/api#tag/systems/operation/CreateSystem](https://docs.styra.com/api#tag/systems/operation/CreateSystem)

| curl -H "Content-Type: application/json"  -H 'Authorization: Bearer \<API\_TOKEN\>' -X POST  https://\<TENANT\>.styra.com/v1/systems -d '{"type": "template.envoy:2.0", "name": "Envoy"}' |
| --- |

- In the place of API\_TOKEN & TENANT  we have to pass the API Token  and Tenant Id of your Styra Das Account.

- To create a System Using API
  - System type (required)
  - System name (required)

We can see the system Created in the UI as shown below..         ![](RackMultipart20221104-1-bi4q9t_html_bc5199b248fe6127.png)





                                       **Git Integration**

**Git integration configuration for systems (can happen at the same time as system creation)**

Prerequisites:

-  Styra DAS account is requiredIf you don't have a Styra DAS tenant, you can    [sign up for a free tenant here](https://signup.styra.com/?_ga=2.47247396.283531518.1641954102-757179015.1635396444)([Signup](https://signup.styra.com/?_ga=2.47247396.283531518.1641954102-757179015.1635396444))
- You must have an API token that has the WorkspaceAdministrator role to work with API
- GITHUB account.

**Git Configuration:**

- Styra DAS supports either HTTPS or SSH authentication for Git.

**configure SSH Git authentication**

- To configure Git Authentication using API
  - SSH key(Required):  SSH Key is a alternate way of identify the users that does not

                                                               Require username and password everytime.

- SSH Key Passphrase(optional): Passphrase is used to protect the SSH Key  from

                                                         being used by someone.

- Git repository(Required):  A Git SSH URL  to your Git repository.
- Git reference: Specify a tag or branch reference (defaults to refs/heads/master—the master branch).
- Git commit SHA: Specify a commit SHA.
- Repository path: (_Optional_) The subdirectory where you want to save the policies.

**Generate SSH Key**

-  To Generate SSH key run the following command in the git bash  with your (git hub) email address in the place of Email.

                         ssh-keygen -t rsa - **b** 4096 -C "Email"

![](RackMultipart20221104-1-bi4q9t_html_3bf23ddab7a712a3.png)

- Click enter
- Enter passphrase or leave it blank and click enter
- SSH key is created in the .ssh  folder

           ![](RackMultipart20221104-1-bi4q9t_html_956a93d58625bb52.png)

- Copy the **id\_rsa.pub** key and add it to your Github account.
-  To add the key to github  go to **settings —SSH and GPG keys** and click on the **new ssh key** and paste the public  key and save it.
- Once you have attained your private SSH key( **id\_rsa** ), you must convert it to the following sample format.
- This format requires you to pass the full key in a single line while making sure to include \n pre-pending and appending the key.  use the helper bash script to format your private key.

| #!/bin/bash
 # Requires AWk and SED to be installed.
 export SSH\_FILE\_PATH="$HOME/.ssh/id\_rsa" #replace this with path to your private SSH key

 line\_count=`wc -l ${SSH_FILE_PATH} | awk '{print $1}'`
 last\_new\_line=`expr $line_count - 1`

 cat $SSH\_FILE\_PATH | sed '1s/$/\\n/' | sed ""$last\_new\_line"s/$/\\\n/" | tr -d '\n' |
| --- |

- Run the bash script(command: bash filename.sh) and Save the private key
- Once you have your private SSH key created on your repository, you will need to create the two secret objects required for configuring SSH authentication: **passphrase** and **SSH private Key**.

**Create a secret passphrase id:**

- To Create a secret Passphrase   run the below command.
- Note: If you don't create a passphrase  with SSH key generation leave the secret as    empty and run the following command.

| curl -H "Content-Type: application/json"  -H 'Authorization: Bearer API\_TOKEN' -X **PUT**   https://TENANT.styra.com/v1/secrets/git/ssh/passphrase -d '{
     "description": "passphrase for git ssh key",
     "name": "ssh-passphrase",
     "secret": "passphrase\_key"
 }' |
| --- |

**Create a secret SSH private key:**

- To Create a secret SSH Private Key  run the below command.
- In **Secre** t paste the **private key** which is generated from the helper bash script.

| curl -H "Content-Type: application/json"  -H 'Authorization: Bearer API\_TOKEN' -X **PUT**   https://TENANT.styra.com/v1/secrets/git/ssh/key -d '{
     "description": "git ssh key",
     "name": "ssh\_key",
     "secret":"Enter the private SSH key"
 }' |
| --- |

**Git integration configuration (SSH) can happen at the same time as system creation.**

- To Create a system with git integration(SSH)  run the below command.

| curl -H "Content-Type: application/json"  -H 'Authorization: Bearer API\_TOKEN' -X POST  https://TENANT.styra.com/v1/systems -d '{
     "name": "Envoy",
     "description": "Envoy system",
     "type": "template.envoy:2.0",
     "read\_only": false,
     "source\_control": {
         "origin": {
             "credentials": "",
             "reference": "refs/heads/main",
             "ssh\_credentials": {
                 "passphrase": "git/ssh/passphrase",
                 "private\_key": "git/ssh/key"
             },
             "url": "git@github.com:venu67776/envoy.git"
         }
     }
 }'


 |
| --- |

- The envoy system created with ssh Git integration as shown below.

    ![](RackMultipart20221104-1-bi4q9t_html_cdbd363a1054ba0b.png)

![](RackMultipart20221104-1-bi4q9t_html_589571409fcec635.png)

(After clicking the Test-connection button in DAS- The above error came)

Note:Error Resolved (Make sure copy the Entire key from -----BEGIN OPENSSH PRIVATE KEY----- to -----END OPENSSH PRIVATE KEY----- which was generated by **bash script** ) to resolve the above error.

**Configure HTTPS  Git authentication**

- To configure Git Authentication using HTTPS
  - Git username (required): Your Git username
  - Git secret (required): The secret corresponding to your Git username.
  - Git repository(Required):  A Git SSH URL  to your Git repository.
  - Git reference: Specify a tag or branch reference (defaults to refs/heads/main—the main branch).
  - Git commit SHA: Specify a commit SHA.
  - Repository path: (_Optional_) The subdirectory where you want to save the policies.
- Note: **Git secret** : Styra recommends to use a GitHub Personal access token. You can generate a token at [github.com/settings/token](https://github.com/settings/tokens) or by clicking through **Your-picture and navigate to Settings \>\> Developer Settings \>\> Personal access tokens**.
- Once you have your Git username and  token , you will need to create the  secret object required for configuring HTTPS authentication.

**Create a secret for https credentials**

- Setup a secret that allows Styra to read and write to your Git repository.
- To create a Secret run the following command

| curl -H "Content-Type: application/json"  -H 'Authorization: Bearer API\_TOKEN' -X **PUT**   https://TENANT.styra.com/v1/secrets/git/httpscred -d '{
     "name": "git-user-name",
     "secret": "token value"
 }' |
| --- |

Here

-       **git/httpscred**   is the id of the secret.
-       **name** is the Git user id
-       **secret** is a password or token for that user

**Git integration configuration (HTTPS) can happen at the same time as system creation.**

- To Create a system with git integration(HTTPS)  run the below command.

| curl -H "Content-Type: application/json"  -H 'Authorization: Bearer API\_TOKEN' -X POST  https://TENANT.styra.com/v1/systems -d '{
     "name": "Envoy-https",
     "description": "envoy-test",
     "type": "template.envoy:2.0",
     "read\_only": false,
     "source\_control": {
         "origin": {
             "url": "https://github.com/venu67776/envoy.git",
             "credentials": "git/httpscred",
             "reference": "refs/heads/main"
         }
     }
 }' |
| --- |

The envoy system created with https Git integration as shown below.

![](RackMultipart20221104-1-bi4q9t_html_7d6f2d23a65186ff.png)

**Standard Okta setup to Styra DAS**

Prerequisites:

- Okta account you can create a new okta free trial account by following link [OKTA](https://www.okta.com/free-trial/)

Login to Okta admin and navigate to **Applications**

  ![](RackMultipart20221104-1-bi4q9t_html_cf4d6a86272e8646.png)

Click on **Create App integration**

Then provide the required details to configure okta.

**Okta Configurations:**

- **Sign-in method:**  **OpenID Connect**
- **Application type: Web Application**

Choose the options as mentioned below given the reference image for it **.**

![](RackMultipart20221104-1-bi4q9t_html_c97ea5be12e98727.png)

Click on Next.

Enter the following details in the settings.

- **Application name:** Styra (or anything you prefer).
- **Application logo:** Upload one.
- **Login redirect URIs:** https://\<das-id\>.styra.com/v1/oauth2/callback.
- **Logout redirect URIs:** None.
- **Assignments:** Choose any one as per your preference.

Click on Save

# **SSO Using Google for StyraDAS**

How to configure Google and then configure [Styra DAS](https://success-l1-dev.styra.com/)

Prerequisites:

1. GCP Account [Signin](https://accounts.google.com/ServiceLogin/signinchooser?continue=https%3A%2F%2Fcloud.google.com%2F_d%2Freturn%3Fcontinue%3Dhttps%253A%252F%252Fcloud.google.com%252Flanding%252Ffree-trial%253Futm_source%253Dgoogle%2526utm_medium%253Dcpc%2526utm_campaign%253Djapac-IN-all-en-dr-bkws-all-all-trial-e-dr-1009882%2526utm_content%253Dtext-ad-none-none-DEV_c-CRE_498697929826-ADGP_Hybrid%252520%25257C%252520BKWS%252520-%252520EXA%252520%25257C%252520Txt%252520~%252520GCP%252520~%252520General_cloud%252520computing%252520-%252520cloud-KWID_43700024740317766-aud-1596662389094%25253Akwd-353549070178%2526userloc_9300156-network_g%2526utm_term%253DKW_gcp%252520console%2526ds_rl%253D1264446%2526gclid%253DEAIaIQobChMI2JXfr7bc-QIVfYJLBR0cMAikEAAYASAAEgK1EvD_BwE%2526gclsrc%253Daw.ds&flowName=GlifWebSignIn&flowEntry=ServiceLogin)
2. Styra DAS(If you don't have a Styra DAS tenant, you can [sign up for a free tenant here](https://signup.styra.com/?_ga=2.47247396.283531518.1641954102-757179015.1635396444)([Signup](https://signup.styra.com/?_ga=2.47247396.283531518.1641954102-757179015.1635396444))

**Google OpenID Connect Configuration**

NOTE: To prepare Google OpenID Connect for signing on to \<das-id\>.styra.com

**Steps:**

1. Sign in to the Google Developers Console at https://console.developers.google.com/start
2. Select an **existing project** or click Create **New Project** to create a new one

  ![](RackMultipart20221104-1-bi4q9t_html_25a2c5c93638a4da.png)

1. From the left-hand navigation panel, click Credentials.

![](RackMultipart20221104-1-bi4q9t_html_99146a57f4e98c2f.png)

4.Click **Create Credentials** button to open the menu, and then click **OAuth client ID**.

![](RackMultipart20221104-1-bi4q9t_html_ef1e356e1edb17bc.png)

Note: To create an **OAuth client ID** you must first configure your **consent screen**

![](RackMultipart20221104-1-bi4q9t_html_45313fef2d5b1c69.png)

What is the OAuth [consent screen](https://developers.google.com/workspace/guides/configure-oauth-consent)?

When you use OAuth 2.0 for authorization, your app requests authorizations for one or more scopes of access from a Google Account. Google displays a consent screen to the user including a summary of your project and its policies and the requested scopes of access.

- Fill the Mandatory(\*) fields and click on Save & Continue

![](RackMultipart20221104-1-bi4q9t_html_132b1ca2309701ef.png) ![](RackMultipart20221104-1-bi4q9t_html_6d4908280264298d.png)

5. For Application type, select **Web application**.

![](RackMultipart20221104-1-bi4q9t_html_4ea7082f1e6be590.png)

6. Enter the form with the following details and click Create.

- **Name** : Styra (or anything you prefer).
- **Authorized redirect URIs:** https://\<das-id\>.styra.com/v1/oauth2/callback

![](RackMultipart20221104-1-bi4q9t_html_d4811b6eb116295e.png) ![](RackMultipart20221104-1-bi4q9t_html_3e8c415e0e713055.png)

7. The OAuth client created window will pop up with two pieces of data, Your **Client ID** and **Your Client Secret**. You must record this information in order to configure Styra in the next section.

![](RackMultipart20221104-1-bi4q9t_html_f49eee18c10ed75b.png)

At this point, Google is configured and you must configure \<das-id\>.styra.com

**Styra Configuration** [**​**](https://docs.styra.com/administration/sso-authentication/oidc/google#styra-configuration)

1. Sign in to \<das-id\>.styra.com with your username and password.

![](RackMultipart20221104-1-bi4q9t_html_7d0838e842a14e4b.png)

2. Go to your **Workspace, click Access Control \>\> Single Sign-On Providers** and then click **OpenID Connect \>\> + Add OpenID Connect Provider**.

![](RackMultipart20221104-1-bi4q9t_html_cfe869da914bd66d.png)

3. Enter the form with the following details:

![](RackMultipart20221104-1-bi4q9t_html_d3ff6922d8bc8b6f.png)

- **Provider name** : Google (or anything you prefer).
- **I**** ssuer URL**: https://accounts.google.com.
- **Client ID** : Copy the Client ID value recorded in Step 6 of the previous section.
- **Client Secret:** Copy the Client Secret value recorded in Step 6 of the previous section.
- **Allowed Domains** : Type the allowed authentication domain(s) of your users. For example, retail.acme.com(zelarsoft.com).
  - If the identity provider supports multiple domains, only users with these domains are allowed to access the service.
- **Invited users only** :
  - **If enabled** , the authenticated user must have a pre-existing account in the service.
  - **If disabled** , a new user account will be created just-in-time for any authenticated user, as long as the user's domain matches one of the allowed domains (and the identity provider has assigned this user to the Styra application).
- **Enabled:** set it to TRUE.

![](RackMultipart20221104-1-bi4q9t_html_7d0838e842a14e4b.png)

1. If you selected just-in-time provisioning for the users, you can now **logout** from \<das-id\>.styra.com and **sign-in again** using Google.
2. Google is now displayed on \<das-id\>.styra.com login screen above the username and password. (As shown in the screenshot above)

**Errors & Troubleshooting:**

**Error: 1**

Only the allowed domain(zelarsoft.com) users can login using SSO with Google into StyraDAS.

 Note: If other Domain(\*\*\*\*.com) users try to login using SSO with google they get below authorization error.

![](RackMultipart20221104-1-bi4q9t_html_be41a8683132879b.png) ![](RackMultipart20221104-1-bi4q9t_html_fd6b3e63fa4c3536.png)

**Error: 2**

 If we **Enable** Invited users only in OpenID Connect Provider, Only those who are invited can login using SSO with google.

If we **Disable** , when user tries to login using SSO with google the below Error will display.

![](RackMultipart20221104-1-bi4q9t_html_3625331de0565ba1.png) ![](RackMultipart20221104-1-bi4q9t_html_c5eb263f43be0273.png)

**Error:3**   If **Client Id** and **client secret** are incorrect the below Error will get.

![](RackMultipart20221104-1-bi4q9t_html_b1334af492c4f2d5.png) ![](RackMultipart20221104-1-bi4q9t_html_93bdc3a0f9c0f77.png)

**SSO using OKTA with SAML**

Prerequisite:

- Styra DAS account is required
- If you don't have a Styra DAS tenant, you can [sign up for a free tenant here](https://signup.styra.com/?_ga=2.47247396.283531518.1641954102-757179015.1635396444)([Signup](https://signup.styra.com/?_ga=2.47247396.283531518.1641954102-757179015.1635396444))
- OKTA account([signup](https://login.okta.com/signin/register/?SAMLRequest=fc%2B7CsJAEAXQXvAflu1NNJUMeZBGELTx1a%2FrYILJTtyZGD%2FfSBRiYzlw77lMnD3rSj3Qc0ku0YtgrhU6S5fSXRN9PKxmS52l00nMpq6iBvJWCrfDe4ss6vStRe9aDzmGIZfo1jsgwyWDMzUyiIV9vt1AH4XGk5ClSvewUgMNa%2BYW%2FVj5jxhm9NLP67QQaSAMu64L6CYmsFSHlnzT4ZlLwTgcL6Sf8%2FeX9AU%3D))
- To login into your OKTA account it is mandatory to download **OKTA verify app** in your Android/IOS.

**Configure Okta SSO SAML**

1. [Login](https://login.okta.com/signin/?SAMLRequest=fc%2B7CsJAEAXQXvAflu1NNJUMeZBGELTx1a%2FrYILJTtyZGD%2FfSBRiYzlw77lMnD3rSj3Qc0ku0YtgrhU6S5fSXRN9PKxmS52l00nMpq6iBvJWCrfDe4ss6vStRe9aDzmGIZfo1jsgwyWDMzUyiIV9vt1AH4XGk5ClSvewUgMNa%2BYW%2FVj5jxhm9NLP67QQaSAMu64L6CYmsFSHlnzT4ZlLwTgcL6Sf8%2FeX9AU%3D) to Okta

1. On the **administrator dashboard** , click **Add Applications** and select **Create New App Integration.**

![](RackMultipart20221104-1-bi4q9t_html_cf4d6a86272e8646.png)

1. Enter the following details in the form and then click Create.
  - Sign in method: Select SAML 2.0.

![](RackMultipart20221104-1-bi4q9t_html_54c7770b8cf391e4.png)

1. Enter the following details in the General Settings form and click **Next**.
  - App name: **Styra (or anything you prefer).**

![](RackMultipart20221104-1-bi4q9t_html_570441c3fc6d6327.png)

1. Enter the following details in the SAML Settings located in the **General Settings** form and then click **Next**.

![](RackMultipart20221104-1-bi4q9t_html_294062ddc0cb9832.png)

- **Single sign on URL:** For example, in https://styra-das-id.styra.com/v1/saml/ssosaml/callback replace styra-das-id.styra.com with your tenant name and ssosaml with the provider name.

- This provider name will be used when you configure the settings on styra-das-id.styra.com.

- Use this for Recipient URL and Destination URL: Make sure to check this box.
- **Audience URI (SP Entity ID)**: For example, in https://styra-das-id.styra.com/v1/saml/ **ssosaml** /metadata replace styra-das-id.styra.com with your **tenant name and ssosaml** with the provider name.

- This provider name will be used when you configure the settings on styra-das-id.styra.com.

- Name ID Format: **EmailAddress**.

![](RackMultipart20221104-1-bi4q9t_html_b7fb7ed42d0a75e4.png)

1. Select an appropriate option on the **Help Okta Support** understand how you configured this application form and click **Finish**.

1. The next form shows the settings you have created.
  - On the **General tab,** confirm the **SAML settings and configure** any additional specific settings if needed.

![](RackMultipart20221104-1-bi4q9t_html_55eca28f78522542.png)

1. Select the **Sign On tab** and click on the **View Setup Instructions button**.
  - From the **Optional section at the bottom** , record the **IDP metadata** from **the Provide the following IDP metadata to your SP provider field**. This value will be used when you configure the settings on styra-das-id.styra.com.

![](RackMultipart20221104-1-bi4q9t_html_d454fd04d72b3d95.png)

1. Now, select the **Assignments tab** to identify the users entitled to access styra-das-id.styra.com.
  - Click **Assign** , select **Assign to People**.

![](RackMultipart20221104-1-bi4q9t_html_c7639fa3fdfb1032.png)

- Click **Assign** and Save to go back to the selected people.
- When all the users are assigned, click **Done**.

![](RackMultipart20221104-1-bi4q9t_html_a41785f898175dc5.png)

**Styra Configuration** [**​**](https://docs.styra.com/administration/sso-authentication/saml/okta#styra-configuration)

After you configure Okta, you must configure styra-das-id.styra.com.

1. Login to styra-das-id.styra.com with your **username and password**.

![](RackMultipart20221104-1-bi4q9t_html_89c96acb800d2036.png)

1. Go to your Workspace, click A **ccess Control \>\> Single Sign-On Providers and then click SAML \>\> + Add SAML Provider.**

![](RackMultipart20221104-1-bi4q9t_html_5e9ebb7e8bf6b043.png)

1. Enter the following details in the form.
  - **Provider name:** Enter the name for your identity provider setting.
  - **Private key:** Use  command to generate a private key and the associated certificate. Enter the private key.

| openssl req -x509 -newkey rsa:2048 -keyout private.key -out certificate.cert -days 3650 -nodes -subj "/CN=styra-das-id.styra.com" |
| --- |

Note: Type the above command in your terminal, it will generate private.key and certificate.cert files.

![](RackMultipart20221104-1-bi4q9t_html_72b532ecc10798ab.png)

- **Private key certificate:** Enter the above generated certificate.

- **Identity provider metadata** : Enter the IDP metadata.

![](RackMultipart20221104-1-bi4q9t_html_d454fd04d72b3d95.png)

- **Email attribute** : Leave it empty as the SAML response from Okta does have the email address in the Subject tag.
- **Allowed Domains:** Type the allowed authentication domain(s) of your users. For example, (zelarsoft.com). If the identity provider supports multiple domains, only users with these domains are allowed to access the service.

![](RackMultipart20221104-1-bi4q9t_html_d85d3d63b7398815.png)

- Allow identity provider to initiate sign in:

  - **If enabled,** identity provider can initiate the single sign on.
  - **If disabled** , identity provider can't initiate the single sign on.
- Invited users only:
  - **If enabled,** the authenticated user must have a pre-existing account in the service.
  - **If disabled,** a new user account will be created just-in-time for any authenticated user, as long as the user's domain matches one of the allowed domains (and the identity provider has assigned the new user to the Styra application).
- **Enabled:** Set it to TRUE.

![](RackMultipart20221104-1-bi4q9t_html_d0d715569011c957.png)

1. If you have selected just-in-time provisioning for the users, then you can now logout from styra-das-id.styra.com and sign-in again through SAML. SAML is now displayed on the styra-das-id.styra.com login screen above the username and password.

![](RackMultipart20221104-1-bi4q9t_html_b42702563be2e5b8.png)

**ERRORS:**

![](RackMultipart20221104-1-bi4q9t_html_c97c6b1491f07359.png)

If the person is not added into OKTA account he cannot login to Styra DAS using SSO with SAML. The above error will be displayed if the person try to access DAS.

**Troubleshooting:**

![](RackMultipart20221104-1-bi4q9t_html_c8bc84af21908cb2.png) ![](RackMultipart20221104-1-bi4q9t_html_15722944840041bf.png)

The above screenshot shows how to add people into OKTA account to use DAS.

**ADD Users in DAS by using API with workspace admin and viewer access.**

To **add users** first we need to **invite them** using the below command:

| curl -H "Content-Type: application/json" -H 'Authorization: Bearer \<API\_Token\>' -X POST [https://success-l1-dev.styra.com/v1/invitations](https://success-l1-dev.styra.com/v1/invitations) -d '{ "roles": ["admin"], "user\_id": "User\_Emailid" }' |
| --- |

Note: User will get Email from Support team to active your account

To **Create/Update** a user :

| curl -H "Content-Type: application/json"  -H 'Authorization: Bearer \<API\_Token\>' -X PUT https://success-l1-dev.styra.com/v1/users/\<User\_Emailid\> -d '{"enabled":true, "roles": ["admin"] }' |
| --- |

To see the **List of users** :

| curl -H "Content-Type: application/json"  -H 'Authorization: Bearer \<API\_Token\>' -X GET https://success-l1-dev.styra.com/v1/users |
| --- |

To **Delete** the user:

| curl -H "Content-Type: application/json"  -H 'Authorization: Bearer \<API\_Token\>' -X DELETE https://success-l1-dev.styra.com/v1/users/\<User\_EmailId\> |
| --- |

**Error:** If we create a user without inviting the user into the DAS tenant we get below authorization error.

![](RackMultipart20221104-1-bi4q9t_html_41fbce93e4297bd5.png)

**Authzv2** - ticket-#1999

- **For SaaS tenants:** Contact Styra's customer success representative to enable [feature flags](https://docs.styra.com/administration/user-management/user-authentication).
- For adding new dev team members as users with appropriate  system roles and permissions need to follow this [Doc.](https://docs.styra.com/administration/role-based-access-control/authorization)
- **Note** : we need Access control tab and permissions tab in the das tenant. We should have  AuthV2 enabled for our [tenant](https://success-l1-dev.styra.com/) to add users with system roles and permissions.
