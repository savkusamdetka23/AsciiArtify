	k -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}"|base64 -d;echo

## Open installed ArgoCD URL and configure application
Click to proceed to https://127.0.0.1:8080
![Alt text](image.png)


Use the password from the last executed command to login as **admin**

![Alt text](image-1.png)

On the home page click on **"Create applciation"**

![Alt text](image-2.png)

 Provide **AppName**, set the **Project name** as default and enable option for **Namespace auto-creation**

![Alt text](image-3.png)

  Scroll a bit down and:
  - set the project **URL from GitHub**
  - choose the path to the **helm** charts in the repo
  - select the **ClusterURL** from the dropdown list
  - set the **Namespace name**
  - click on the button **Create** on the top the page 

![Alt text](image-4.png)

When the application is created, you can click on the **synchronization button** on the home page  

![Alt text](image-5.png)

![Alt text](image-6.png)

![Alt text](image-7.png)

  You can click on the application itself to see more details about the application deployment
 
![Alt text](image-8.png)
