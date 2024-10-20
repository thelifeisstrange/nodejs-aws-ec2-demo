# Host a Node.js App on AWS EC2

This guide walks through the steps to host a Node.js application on an AWS EC2 instance using Ubuntu.

## Prerequisites

- AWS account with access to create an EC2 instance.
- Node.js app code pushed to a GitHub repository.

## Setup Instructions

### 1. Create and Connect to an EC2 Instance

- Launch an EC2 instance with Ubuntu.
- Connect to the instance using SSH:

  ```bash
  ssh -i path_to_your_key.pem ubuntu@your_instance_ip
  ```

### 2. Update Packages

Update the package list on the Ubuntu instance:

```bash
sudo apt-get update
```

### 3. Install Node.js

Install Node.js version 20.x:

```bash
curl -sL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
```

### 4. Install Git

Install Git to clone your repository:

```bash
sudo apt-get install git
```

### 5. Clone the GitHub Repository

Push your Node.js app to a GitHub repository, then clone it on the EC2 instance:

```bash
git clone https://github.com/yourusername/your-repo.git
```

Navigate to your project directory:

```bash
cd your-repo
```

### 6. Install Node.js Packages

Install the required packages:

```bash
npm install
```

### 7. Start the Node.js Application

Start the app:

```bash
npm start
```

### 8. Update Security Group Inbound Rules

- Go to the AWS EC2 dashboard.
- Select your instance, then go to **Security** > **Security Groups**.
- Edit the inbound rules to add a custom TCP rule for **port 8000** with **Source: Anywhere** to allow traffic.

### 9. Access Your Application

Visit your app in the browser:

```
http://your_instance_ip:8000
```

### 10. Run the App in the Background with PM2

To keep the Node.js app running in the background:

- Install `pm2` globally:

  ```bash
  sudo npm install pm2 -g
  ```

- Start the app using `pm2`:

  ```bash
  sudo pm2 start index.js
  ```

This will ensure that your app continues running even if you disconnect from the SSH session.

### 11. Verify the App

Check the application by visiting:

```
http://your_instance_ip:8000
```

Now your Node.js app is running on AWS EC2, and `pm2` will keep it active even if the SSH session ends.
