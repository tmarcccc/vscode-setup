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



#Python Flask install
1. Installing Required Packages: sudo apt install -y python3 python3-pip python3-venv git
2. sudo apt install python3.12-venv
3. Changing to opt: cd /opt
4. Creating the WebApp folder: sudo mkdir flask_app
5. Setting up Premissions: sudo chown -R marc:marc /opt/flask_app
6. Moving the Flask app files in this directory so the app.py is there.
7. Starting the Virtual Enviroment: sudo python3 -m venv venv
8. Starting the Virtual Enviroment: source venv/bin/activate
9. If requirements.txt is avaliable: pip install -r requirements.txt
10. if it was not in requirements.txt: pip install flask
11. Checking which packeges are installed: pip list
12. Testing if the Webserver starts: python app.py
13. Stay in the (venv)
14. Installing gunicorn for WSGI HTTP server: pip install gunicorn
15. Starting the Server:  gunicorn -w 5 -b 0.0.0.0:5000 app:app
16. Website should now be reachable
17. Setting up Ngix: 
