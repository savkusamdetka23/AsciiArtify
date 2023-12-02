- [Minimum viable product (MVP) of the deployed application via ArgoCD](#minimum-viable-product-mvp-of-the-deployed-application-via-argocd)
  - [Open installed ArgoCD URL and configure application](#open-installed-argocd-url-and-configure-application)
  - [Demo of the application running with ArgoCD](#demo-of-the-application-running-with-argocd)

#	Minimum viable product (MVP) of the deployed application via ArgoCD
    
## Open installed ArgoCD URL and configure application
After performing steps from POC document, click on the next URL to proceed to ArgoCD https://127.0.0.1:8080

![Alt text](img/image.png)

Use the password from the last executed command from POC document to login as **admin**

![Alt text](img/image-1.png)

On the home page click on **"Create applciation"**

![Alt text](img/image-2.png)

 Provide **AppName**, set the **Project name** as default and enable option for **Namespace auto-creation**

![Alt text](img/image-3.png)

  Scroll a bit down and:
  - set the project **URL from GitHub**: https://github.com/savkusamdetka23/go-demo-app.git
  - choose the path to the **helm** charts in the repo
  - select the **ClusterURL** from the dropdown list
  - set the **Namespace name**
  - click on the button **Create** on the top the page 

![Alt text](img/image-4.png)

When the application is created, you can click on the **synchronization button** on the home page  

![Alt text](img/image-5.png)

![Alt text](img/image-6.png)

![Alt text](img/image-7.png)

  You can click on the application itself to see more details about the application deployment
 
![Alt text](img/image-8.png)

![Alt text](img/image-9.png)

## Demo of the application running with ArgoCD
- Execute next command to forward ports for the application:

      kubectl port-forward -n demo svc/ambassador 8082:80

![Alt text](img/image-10.png)

- Open additional terminal window and download the image you would like to test with the next command to save some image locally (you can choose any other link for the image URL):

      wget -O /workspaces/AsciiArtify/k8s.png https://assets-global.website-files.com/63eab091d2e4cb36843a37be/654a6a7bee26c4d8b272459f_Just-in-time-access-Kubernetes-logo.png

  ![Alt text](img/image-11.png)

- Use the saved image and then pass it as payload to the service:

      curl -F 'image=@k8s.png' localhost:8081/img/

![Alt text](img/image-12.png)