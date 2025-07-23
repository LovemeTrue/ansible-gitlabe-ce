## Ansible project for automatic creation of projects in GitLab CE and pushing code to a repository with a local VM.

### Project structure:
```
├── group_vars # Переменные
│   └── all
│       ├── main.yml
│       └── projects-config.yml # Конфиг проектов
├── inventory
│   └── hosts.ini # Хосты для ansible
├── projects # Dockerfile и исходный код проектов
│   ├── flask-app
│   │   ├── app.py
│   │   ├── Dockerfile
│   │   ├── README.md
│   │   └── requirements.txt
│   └── java-app
│       ├── Dockerfile
│       ├── HelloWorldServer.java
│       ├── README.md
│       └── requierments.txt
├── README.md
├── roles
│   └── gitlab-management # Роль для управления GitLab
│       ├── tasks
│       │   ├── generate-ssh-key.yml
│       │   ├── loop-over-projects.yml
│       │   ├── main.yml
│       │   ├── register-ssh-key.yml
│       │   └── single-project-create-push.yml
│       ├── templates
│       │   └── project_config.json.j2
│       └── vars
│           └── main.yml
├── secrets.yml
└── site.yml

```

### Nessesary steps before running ansible playbook:
### 1. After deploy of Gitlab CE, necessary to go to UI and create token in: Settings -> Access Tokens.
### 2. Create file `secrets.yml` in root directory with command: 
```
ansible-vault create secrets.yml
```
### And add to it: `gitlab_token: <TOKEN>`

### 3. To add password for user ansible in file `secrets.yml`:
```
ansible-vault edit secrets.yml -> 'gitlab_password: <PASSWORD>'
```
### 4. To run playbook:
```
ansible-playbook -i localhost, -c local site.yml --ask-vault-pass 
```
