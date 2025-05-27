# vscode-setup

1. installing git from https://git-scm.com/
2. checking (vs code needs restart) with:  git --version
3. creating a folder for the project
4. git cloning the contents: git clone <-->
5. Configuring git: git config --global user.name "YourName"
6. Configuring git: git config --global user.email "your.email@example.com"
7. edit the file and test if commit works




# PostgreSQL install
~logined not with root
1. sudo apt update && sudo apt upgrade -y
2. sudo apt install postgresql postgresql-contrib -y
3. checking if install was succesful and running:  sudo systemctl status postgresql
4. Entering Postgresql:  sudo -u postgres psql
5. Create User:   CREATE USER marc WITH PASSWORD 'mypassword';
6. ALTER USER marc WITH SUPERUSER;
7. Creating the Database:
8. ...
9. Exiting Postgres Prompt: \q
