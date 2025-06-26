# vscode-setup

1. installing git from https://git-scm.com/
2. checking (vs code needs restart) with:  `git --version`
4. creating a folder for the project
5. git cloning the contents: git clone <-->
6. Configuring git: git config --global user.name "YourName"
7. Configuring git: git config --global user.email "your.email@example.com"
8. edit the file and test if commit works




# PostgreSQL install
~logined not with root
1. sudo apt update && sudo apt upgrade -y
2. sudo apt install postgresql postgresql-contrib -y
3. checking if install was succesful and running:  sudo systemctl status postgresql
4. Entering Postgresql:  sudo -u postgres psql
5. Create User:   CREATE USER marc WITH PASSWORD 'mypassword';
6. ALTER USER marc WITH SUPERUSER;
7. Creating the Database:  CREATE DATABASE main_db;
8. Adding permissions for DB:  GRANT ALL PRIVILEGES ON DATABASE main_db TO marc;
9. Change to the Database to use commands: \c main_db;
10. Checking whats in a Database: SELECT * FROM db_name;
11. ...
12. Exiting Postgres Prompt: \q



# Python Flask install
1. Installing Required Packages: sudo apt install -y python3 python3-pip python3-venv git
2. sudo apt install python3.12-venv
3. Changing to opt: cd /opt
4. Creating the WebApp folder: sudo mkdir flask_app
5. Setting up Premissions: sudo chown -R marc:marc /opt/flask_app
6. Moce to /opt/flask_app folder.
7. Moving the Flask app files in this directory so the app.py is there.
8. Starting the Virtual Enviroment: sudo python3 -m venv venv
9. Starting the Virtual Enviroment: source venv/bin/activate
10. to be sure do sudo apt update
11. If requirements.txt is avaliable: pip install -r requirements.txt
12. If not already installed for PostgreSQL do: sudo apt install build-essential python3-dev libpq-dev -y
13. if it was not in requirements.txt: pip install flask        and      pip install psycopg2       (also for PostgreSQL)
14. Checking which packeges are installed: pip list
15. Testing if the Webserver starts: python app.py
16. Stay in the (venv)
17. Installing gunicorn for WSGI HTTP server: pip install gunicorn
18. Starting the Server:  gunicorn -w 5 -b 0.0.0.0:5000 app:app
19. Website should now be reachable
20. Exit Venv: deactivate
21. Setting up Ngix:
22. Installing Ngix: sudo apt install nginx -y
23. Editing the Congfig: sudo nano /etc/nginx/sites-available/flask_app
24.   Pasting Config:
```
server {
    listen 80;
    server_name your-domain.com;  # Replace with your actual domain or server IP

    location / {
        proxy_pass http://127.0.0.1:5000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    error_log /var/log/nginx/flask_app_error.log;
    access_log /var/log/nginx/flask_app_access.log;
}
```
22. sudo ln -s /etc/nginx/sites-available/flask_app /etc/nginx/sites-enabled/
23. Testing Config: sudo nginx -t
24. sudo systemctl restart nginx
25. Use Systemd to Run Gunicorn
26. Opeing another Config: sudo nano /etc/systemd/system/flask_app.service
27. Pasting This:
```
[Unit]
Description=Gunicorn instance to serve Flask application
After=network.target

[Service]
User=marc
Group=www-data
WorkingDirectory=/opt/flask_app
Environment="PATH=/opt/flask_app/venv/bin"
ExecStart=/opt/flask_app/venv/bin/gunicorn --workers 4 --bind 127.0.0.1:5000 app:app

[Install]
WantedBy=multi-user.target
```
28. sudo systemctl start flask_app
29. sudo systemctl enable flask_app
30. Check Status: sudo systemctl status flask_app
31. Acces Website with IP or Domain to test.
32. Finally using Certbot for https







# backend js
1. cd /opt
2. mkdir backend_task
3. cd backend_task
4. Move js File in this directory   potenially use sudo nano /opt/backend_task/backend.js
5. sudo apt update
6. sudo apt install -y nodejs npm
7. check if succesfull with node -v  and  npm -v
8. make excecutable with  sudo chmod +x /opt/backend_task/backend.js
9. Create a systemd service fiel with: sudo nano /etc/systemd/system/backend.service
10. Paste the following:
```
[Unit]
Description=Node.js Background Task
After=network.target

[Service]
ExecStart=/usr/bin/node /opt/backend_task/backend.js
Restart=always
User=marc
Group=www-data
Environment=NODE_ENV=production
WorkingDirectory=/opt/backend_task

[Install]
WantedBy=multi-user.target
```
10. for dependencies:  sudo npm init -y
11. installing some dependencies: sudo npm install dotenv pg
12. checking if installed:  ls node_modules
13. sudo systemctl daemon-reload
14. sudo systemctl start backend.service
15. checking the status:  sudo systemctl status backend.service
16. see the logs with: sudo journalctl -u backend.service -f
17. 
