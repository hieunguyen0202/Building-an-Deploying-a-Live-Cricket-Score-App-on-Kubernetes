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

- Open this file `test.py` and replace `X-RapidAPI-Key`. 

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/f4c88381-1484-40cc-8cec-479f62bfb0f0)

- Go to this [link](https://rapidapi.com/cricketapilive/api/cricbuzz-cricket) to get the new key

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/9272264e-7dc1-46ca-b580-7196adf0ad89)

- On terminal run this command `python ./test.py` you will see the result like this

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/f259bb1d-4991-48bd-8cfd-0deb947c9738)

- So you will see the result in JSON format, go to `test2.py` to transform this JSON result into table format
- Before run this command `python ./test2.py`, you can install this module `pip3 install tabulate`. Remeber to change the `RapidAPI key` in this `test2.py` file

  ![image](https://github.com/hieunguyen0202/Building-an-Deploying-a-Live-Cricket-Score-App-on-Kubernetes/assets/98166568/479035bb-19ef-4ab6-acb7-3a282e1fb972)

  
