Update the Wagen India on ubuntu server

connect to remote server
`ssh aman@65.108.77.67`
Pass: `Analytics@Hetzner4WB`


Update the Remote Server
`sudo apt update`
`sudo apt upgrade`


1. Check the running screen 
screen doc: https://linuxize.com/post/how-to-use-linux-screen/ 
`screen -r`

2. close the current runnign django_server and celery_worker screen
To attach a screen : 
`screen -r 392898.django_server`
`screen -r 393313.celery_worker`
Then control+ C =

Detach a screen
`screen -d 404581.celery_worker`

To delete a screen 
`screen -S 356415.celery_worker -X quit`

Start a new screen
`screen -S django_server`
`screen -S celery_worker`

Edit the setting.py file
`nano settings.py`


3. Remove the existing webapp folder inside
aman@hetzner4wb:~/wagen_india/webapp/wagen
`rm -r webapp`

4. Copy the updated "webapp" code from local terminal to server using 
`scp -r /Users/amanchaudhary/Desktop/webapp aman@65.108.77.67:/home/aman/wagen_india/webapp/wagen`
`scp -r /Users/amanchaudhary/Desktop/views.py aman@65.108.77.67:/home/aman/wagen_india/webapp/wagen/webapp`
`scp -r /Users/amanchaudhary/Desktop/report_custom_pdf.html aman@65.108.77.67:/home/aman/wagen_india/webapp/wagen/webapp/templates`
`sudo mv /home/aman/report_custom_pdf.html /home/aman/wagen_india/webapp/wagen/webapp/templates`


Activate the venv inside "aman@hetzner4wb:~/wagen_india/webapp$"
`virtualenv -p /usr/bin/python3 venv`
`source venv/bin/activate`
`pip install -r requirements.txt`
`cd wagen`

5. Run the django_server and celery_worker screen

`screen -r 392898.django_server`
`python manage.py runserver 0.0.0.0:8000`
You can access the dashboard at `http://65.108.77.67:8000/`


`screen -r 393313.celery_worker`
`celery -A wagen worker -l INFO`

To go out of the screen, use `ctrl-a-d`.

Activate vent
Run Django server
