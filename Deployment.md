# Ezgate Deployment
This file serves as a comprehensive guide for deploying the application. It outlines the necessary steps, including adding remotes, creating branches, merging branches, setting up GitHub Actions for deployment, and pushing code changes. Additionally, it provides instructions for connecting to the EC2 instance via SSH and emphasizes the importance of following the deployment sequence. Finally, it concludes with guidance on monitoring the deployment process through GitHub Actions and verifying the successful deployment by accessing the application. Overall, this file acts as a reference for deploying the application efficiently and effectively. 

> [!NOTE]
> I have not used ChatGPT to write description.



![Ezgate Logo](https://ezgate.s3.amazonaws.com/ezgate-logo.png)
## Add Remote
Add remote in both frontend and backend folders

To add the link of the repository as a remote, use the following command:

```bash
git remote add deploy https://github.com/AdilMir1433/ezgate.git
```


> [!NOTE]
> I have used **deploy** as remote name

## Create Branches

Create branches in both frontend and backend.

For frontend, branch name should be ***ezgate-frontend*** and for backend it should be ***deploy-to-ec2***. You can create branch and make it your current working directory as follows

### Frontend

```bash
git checkout -b ezgate-frontend
```

### Backend

```bash
git checkout -b deploy-to-ec2
```

> [!IMPORTANT]
> Make sure you are in the branch that you just created.

## Merge Branches
It's important to have the lastest code in the deploymet branch so make sure you merge the branch with it's parent branch.

For frontend, the parent branch is ***master***. For backend, parent branch is ***ezgate-backend-modified***

### Frontend
```bash
git merge master
```

### Backend
```bash
git merge ezgate-backend-modified
```

> [!TIP]
> Pull latest code from repos in the parent branches before merging.

## GitHub Actions

To deploy the application, we utilize AWS, Docker, and GitHub Actions. The deployment process involves running the application on an EC2 instance. We automate this process using GitHub Actions.

Follow the following steps to connect the EC2 terminal with your local terminal.

- Download the [pem](https://drive.google.com/file/d/1dSw7Guyd79QZCoxqMEC0oK6xXA0n_ehO/view?usp=drive_link) file
    
- Open **terminal** and cd into the directory where you downloaded the file

- In terminal, run the following commands **one by one**

    ```bash
    chmod 400 "ez-gate3.pem"
    ```

    ```
    ssh -i "ez-gate3.pem" ubuntu@ec2-44-211-167-40.compute-1.amazonaws.com
    ```

    [!NOTE] if it says something related to fingerprint, just types `yes`

## Push And Deploy
Now navigate back to your code where you merged your branches.

Now add the files to your git, add a commit message and push your code. 

### Frontend

```bash
git add .

git commit -m "<Your Message without the angle brackets>"

git push deploy ezgate-frontend
```

### Backend

```bash
git add .

git commit -m "<Your Message without the angle brackets>"

git push deploy deploy-to-ec2
```
> [!CAUTION]
> Push code to a branch first then go to github actions page and wait for it's deployment then deploy the other part.

After you have pushed your code, go the [GitHub Actions Page](https://github.com/AdilMir1433/ezgate/actions) 

from there, you’ll see Many workflows there. Click on the top one. When you open it, there will be 2 Jobs available, **build** and **deploy**. First the build will run and once it it completed successfully, Navigate to the deploy job. If there are no errors in the **CI/CD Pipeline** file, deployment would be success. Wait for few seconds and then open [ezgate.ai](https://ezgate.ai) in new tab of your browser and voila! application is deployed successfully 


## Authors

- [Haleema Shahid](https://github.com/Haleema-Shahid)
- [Ismaeel Mughal](https://github.com/IsmaeelMughal)
- [Adil Mir](https://github.com/AdilMir1433)

