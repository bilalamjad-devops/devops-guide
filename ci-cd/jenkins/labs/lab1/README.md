## What this does?
This repo along with https://github.com/bilalamjad-devops/kubernetesmanifest creates a Jenkins pipeline with GitOps to deploy code into a Kubernetes cluster. CI part is done via Jenkins and CD part via ArgoCD (GitOps).


- Kubernetes (Minikube)
- Jenkins
- ArgoCD


### Kubernetes (Minikube):

You can use any Kubernetes or use any cloud service provider. I am using Minikube.


### Jenkins:

Jenkins is used for CI. We work on 3 things; Plugins, Credentials and Job. 



**Plugins**

We are installing the following plugins.

- Docker plugin  
- Docker Pipeline
- GitHub Integration Plugin
- Parameterized trigger Plugin

<img width="1600" height="900" alt="cloudwithRaj - 3" src="https://github.com/user-attachments/assets/8fddf0fb-c4dd-485d-9df2-3005c081481c" />

<img width="1600" height="900" alt="cloudwithRaj - 4" src="https://github.com/user-attachments/assets/9c719ac1-e2d0-4f39-a0ad-195194a69271" />


**Credentials**

<img width="1600" height="900" alt="cloudwithRaj - 5 credentials " src="https://github.com/user-attachments/assets/b079f0dd-194a-4dd1-9986-6947218a13a4" />

<img width="1600" height="900" alt="cloudwithRaj - 6" src="https://github.com/user-attachments/assets/fb0a4ff5-9aba-457e-b86c-9b1bb175268f" />



We are storing the following credentials.

- DockerHub
- GitHub

DockerHub:

We are storing DockerHub credentials in Jenkins so Jenkins can push docker image to our DockerHub account.

<img width="1600" height="900" alt="cloudwithRaj - 7" src="https://github.com/user-attachments/assets/9874457e-9a48-4f15-ba24-aa1cf13f51ed" />

<img width="1600" height="900" alt="cloudwithRaj - 9" src="https://github.com/user-attachments/assets/c95887fb-3480-4ceb-9b93-d972efb19f7e" />

<img width="1600" height="900" alt="cloudwithRaj - 10" src="https://github.com/user-attachments/assets/cacb7046-d4a4-42d8-9cc5-8e1b28f500bf" />

<img width="1600" height="900" alt="cloudwithRaj - 11" src="https://github.com/user-attachments/assets/8745e7d0-cf8a-4ea6-ac78-957bf7dc22ca" />


<img width="1600" height="900" alt="cloudwithRaj - 12" src="https://github.com/user-attachments/assets/c1c2bbd0-66b5-4762-9b6f-38969fd04524" />

<img width="1600" height="900" alt="cloudwithRaj - 13" src="https://github.com/user-attachments/assets/077127fd-0ad3-4c69-b45b-456d4200f0bb" />

<img width="1600" height="900" alt="cloudwithRaj - 14" src="https://github.com/user-attachments/assets/d9837db6-934a-44cf-a264-73e6ed3d29bc" />




GitHub:



We are storing GitHub credentials in Jenkins so Jenkins can change tag of our docker image to our DockerHub account.


<img width="1600" height="900" alt="cloudwithRaj - 7" src="https://github.com/user-attachments/assets/8ff93d16-1cab-4e1a-b060-a9086e4b5af5" />


<img width="1600" height="900" alt="cloudwithRaj - 15" src="https://github.com/user-attachments/assets/37f68e44-8b07-41f0-910a-44ed10c459d0" />

<img width="1600" height="900" alt="cloudwithRaj - 16" src="https://github.com/user-attachments/assets/84b54090-bac3-460b-b5a6-25eceadbdc95" />


<img width="1600" height="900" alt="cloudwithRaj - 17" src="https://github.com/user-attachments/assets/bcebecd9-94d7-4cbd-8400-d78fdec14294" />


<img width="1600" height="900" alt="cloudwithRaj - 18" src="https://github.com/user-attachments/assets/57feb552-02bd-4808-8fd4-391d975bf862" />



<img width="1600" height="900" alt="cloudwithRaj - 19" src="https://github.com/user-attachments/assets/b3aa6e0b-19a9-412d-b5a1-73697a5f2e46" />


<img width="1600" height="900" alt="cloudwithRaj - 20" src="https://github.com/user-attachments/assets/df04f040-32f5-4ffc-a9f2-0f61c78a26a9" />


<img width="1600" height="900" alt="cloudwithRaj - 21" src="https://github.com/user-attachments/assets/0d04e14a-7d41-456f-b09b-d6c08d5df186" />


<img width="1600" height="900" alt="cloudwithRaj - 22" src="https://github.com/user-attachments/assets/7a314ccd-274a-4c30-8b2d-ea1c328e7770" />



<img width="1600" height="900" alt="cloudwithRaj - 23" src="https://github.com/user-attachments/assets/f01be06c-c22a-4139-b4a6-07ce0e671431" />


**Job**

We make 2 jobs<img width="1600" height="900" alt="cloudwithRaj - 32" src="https://github.com/user-attachments/assets/354e6649-d679-43ea-8d81-ddb73d997fa4" />


buildimage:

<img width="1600" height="900" alt="cloudwithRaj - 24" src="https://github.com/user-attachments/assets/28186ca9-ad43-4975-800f-3d13c0ed9907" />

<img width="1600" height="900" alt="cloudwithRaj - 25" src="https://github.com/user-attachments/assets/12bebade-bf70-49b2-9270-a85093588036" />

<img width="1600" height="900" alt="cloudwithRaj - 26" src="https://github.com/user-attachments/assets/61ff1258-06c4-4fbf-af7e-839f16addd2e" />


updatemanifest:

<img width="1600" height="900" alt="cloudwithRaj - 27" src="https://github.com/user-attachments/assets/b8b7b51c-98af-45c3-aa65-a6499bc0ff6b" />


<img width="1600" height="900" alt="cloudwithRaj - 28" src="https://github.com/user-attachments/assets/b97a78e3-644c-4d5f-b0e6-4176d9db066f" />


<img width="1600" height="900" alt="cloudwithRaj - 29" src="https://github.com/user-attachments/assets/089054c1-0cc9-4a86-bf31-b1fb5ddf7726" />


<img width="1600" height="900" alt="cloudwithRaj - 30" src="https://github.com/user-attachments/assets/be6bf4f0-1ec4-49b8-a9bd-9ca0550754b0" />


<img width="1600" height="900" alt="cloudwithRaj - 31" src="https://github.com/user-attachments/assets/335bf908-380e-4eb0-bdf5-848e01cf80c3" />



<img width="1600" height="900" alt="cloudwithRaj - 32" src="https://github.com/user-attachments/assets/f3287716-e341-43f1-89e7-843ab6dd0dd4" />



<img width="1600" height="900" alt="cloudwithRaj - 33" src="https://github.com/user-attachments/assets/e19b59f0-1dfc-4c7c-acac-42e1c6e0e5be" />












### ArgoCD:


