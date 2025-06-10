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
7. Creating the Database:
8. ...
9. Exiting Postgres Prompt: \q



# Python Flask install
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
18. Exit Venv: deactivate
19. Setting up Ngix:
20. Installing Ngix: sudo apt install nginx -y
21. Editing the Congfig: sudo nano /etc/nginx/sites-available/flask_app
22.   Pasting Config:
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
