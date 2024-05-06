# Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes
## Architect Diagram

## Implementation
### Setup environment to develop code on Cloud Shell
- Create new project on GCP platform with name `cricket-score-app-on-gke` and remember to enable billing account for this project
- Go to cloud shell on GCP console
- Do some command on cloud shell

```
# Set project ID
gcloud config set project cricket-score-app-on-gke

# Clone source code
git clone https://github.com/vishal-bulbule/real-time-crick-score-app.git

```
- Next , open editor on Cloud shell and open this foler `real-time-crick-score-app` include the source code

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/9d505bb5-090a-4c6f-9a1e-ca9823c87f70)

- Verify the source directory

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/6c7fe9e1-bcc3-4e61-b7aa-988e7fd36d89)


### Run test some file 

- Open this file `test.py` and replace `X-RapidAPI-Key`. 

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/f4c88381-1484-40cc-8cec-479f62bfb0f0)

- Go to this [link](https://rapidapi.com/cricketapilive/api/cricbuzz-cricket) to get the new key

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/9272264e-7dc1-46ca-b580-7196adf0ad89)

- On terminal run this command `python ./test.py` you will see the result like this

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/f259bb1d-4991-48bd-8cfd-0deb947c9738)

- So you will see the result in JSON format, go to `test2.py` to transform this JSON result into table format
- Before run this command `python ./test2.py`, you can install this module `pip3 install tabulate`. Remeber to change the `RapidAPI key` in this `test2.py` file

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/479035bb-19ef-4ab6-acb7-3a282e1fb972)

### Run application
- Go to this file `app.py` and change `RapidAPI key`
- Run this command `python ./app.py`

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/5b0d9af3-1ab5-47cf-bf77-abc05f7838b4)

- Use it to see the application on port 8080

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/1c0e8e0e-7437-4f25-a06d-f154344926ce)

- You will see the application

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/16ca8f84-bc5c-4d80-9e1f-ea604560c1d9)

### Setup kubernetes cluster
- Make sure to enable Kubernetes Engine API

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/43f2b682-c85f-46e3-9a17-7d10b14bd258)

- Go to [Kubernetes Engine](https://console.cloud.google.com/kubernetes/list/overview?hl=vi&project=cricket-score-app-on-gke) on GCP console
- Click on `Create` cluster on Auto pilot mode

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/d5ee720e-c5fa-4615-85fd-eb13a2dfca51)

- Make everything by default and click on `Submit`

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/94f6c111-844c-4d46-9a13-0a5de5aa6ef4)

- Waiting for miniutes to spin up the new cluster

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/6bcbbc8b-1304-4c0d-bf2a-546fc4e8b3d0)

### Convert application to container
- Let's create [Artifact repository](https://console.cloud.google.com/artifacts?referrer=search&hl=vi&project=cricket-score-app-on-gke) on GCP to store docker contianer image

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/1c16fbc9-e6c6-458b-a9fa-e826be4ad2de)

- Give a name `my-repo` and set region `us-central1` and click on `Create`

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/4b3dc58f-3b0f-45da-a129-944a72baf8b4)

- Go to the cloud shell, verify the `Dockerfile` (Docker has been installed on cloud shell by default)

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/a5e98cbb-0d19-46ea-8938-608a7ca873e5)

- Run this command to build the image `docker build -t crick-app .`
- Check the image `docker images`

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/a59bc081-2c73-4abe-9e09-2d8b79c67574)

- Run container on port 8080 `docker run -p 8080:8080 crick-app` and press `Ctrl + C` to kill process

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/248b0082-f1f2-40fc-89a9-fa72b9f7f08e)

### Upload container to repository
- Add tag for container image

  ```
  docker tag crick-app us-central1-docker.pkg.dev/cricket-score-app-on-gke/my-repo/crick-app
  ```
- Push this container image

  ```
  docker push us-central1-docker.pkg.dev/cricket-score-app-on-gke/my-repo/crick-app
  ```

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/5a48189e-1c27-4fce-924a-265ed5f66d83)

- Go back to Artifact Repository to verify the new image

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/c512733d-ffef-4633-9cb2-ea2dd2f793fe)

### Deplot workload on autopilot cluster
- Click on `autopilot-cluster-1` cluster and click `Deploy`

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/8cf62b1f-e23c-4767-8d62-64cc23ae6021)

- Choose existing container image and click on select

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/e913d098-245a-4771-bdc9-cacc8cd4b6a6)

- Choose this container image and click `Done` and `Continue`

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/b63e4c89-e00f-48b0-b104-2bfc7ce939ef)

- Next, change the name `crick-app` and click `Continue`

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/b2183136-aa71-4825-9b68-ab5538a3a8e9)

- Check on `Expose deployment as a new service` and chage port `8080` like this and click `Deploy`

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/58ebd7b5-6350-4696-9241-a4bc579ecec5)

- Waiting for minutes to complete

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/71a38106-f529-44c3-b7aa-79c9ef571205)

- Find this URL end-point

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/74e861ea-bf47-493e-9250-3b2d23853245)

- Verify the application running on autopilot cluster on GKE

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/ebc011f9-3a43-4a91-b8d9-5763c45e1b54)

### Build CI/CD pipepline to build conatainer and runnning on GKE autopilot
- Create new private repository with name `real-time-crick-score-app`
- Go to `Settings` -> `Developer Settings` -> Generate new token (Classic) with name `crick-app-demo` and save this token

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/b911ec93-8298-4a8d-8a50-35594c785806)

- Go back to cloud shell create new folder and move to this foler and do this command. Replace with username github repo and this token that just save in previous step

  ```
  git clone https://<your_username>:<your_personal_access_token>@github.com/hieunguyen0202/real-time-crick-score-app.git

  ```
- After that move everything related to source code application into this folder

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/aa8b0314-43d0-4334-ab7d-e1f166f927ce)

- Do some command to push this source code to github

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/820cf438-5b95-45c2-97c5-7417d0631072)

- Verify this source code
  
  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/7e42d2d7-9552-42ec-87a0-1d39c006d239)

