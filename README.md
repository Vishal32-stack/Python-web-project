# Python Project Deployment - 5000

## Introduction

This project is a Python web application deployed on an AWS EC2 Linux instance. The app runs on **port 5000** and is kept running in the background using **Gunicorn**, so it stays up even after the terminal session is closed.

**Tech used:** Python 3, pip, venv, Git, Gunicorn, AWS EC2

## Architecture Diagram

```mermaid
flowchart LR
    A[User / Browser] -->|HTTP :5000| B[AWS EC2 Instance]
    B --> C[Gunicorn]
    C --> D[Python App - app.py]
```

> Make sure port **5000** is allowed in the EC2 Security Group (Inbound Rules).

## Input

- Source code cloned from GitHub (`git clone <url>`)
- Python dependencies listed in `requirements.txt`
- Entry point: `app.py`

## Output

The application is accessible in the browser at:

```
http://35.175.194.237:5000/

<img width="2940" height="1912" alt="3036962D-1E97-42CA-BD12-7DDBD1647747" src="https://github.com/user-attachments/assets/74a4a4c1-21f2-446a-8c4a-62f102473374" />


```

## Installation

```bash
# Update packages
sudo yum update

# Install Python 3 and pip
sudo yum install python3 -y
python3 --version
sudo yum install python3-pip -y
pip --version

# Install Git
sudo yum install git -y
git --version

# Clone the project
sudo git clone <url>
cd pythonapp
ls

# Create and activate a virtual environment
sudo python3 -m venv myenv
ls
source myenv/bin/activate

# Install dependencies
sudo pip install -r requirements.txt

# Run the app
sudo python3 app.py
```

Then open `(http://35.175.194.237:5000/)` in your browser.

## Background

Running `python3 app.py` stops when the terminal closes. To keep the app running in the background, use Gunicorn:

```bash
sudo gunicorn --bind 0.0.0.0:5000 app:app --daemon
```

| Part | Meaning |
|------|---------|
| `--bind 0.0.0.0:5000` | Listen on all network interfaces, port 5000 |
| `app:app` | `<filename>:<Flask app object>` (from `app.py`) |
| `--daemon` | Run the process in the background |

To stop it:

```bash
sudo pkill gunicorn
```

## Conclusion

The Python application was successfully deployed on an AWS EC2 instance and is served on port 5000 using Gunicorn, which keeps it running in the background without an open terminal session.

---

**Author:** Vishal ([@Vishal32-stack](https://github.com/Vishal32-stack))
