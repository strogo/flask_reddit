flask\_reddit
=============

**flask_reddit** is an extendable + minimalist [Reddit](http://reddit.com) clone.

This was built so beginners who want a standard CRUD + reddit-like application
can quickly get to work.

We utilize: 
- `flask` as the web framework.
- `nginx` as the HTTP server  
- `gunicon` as the wsgi server.
- `MySQL` for our database 
- `flask-sqlalchemy` as our ORM.
- `bootstrap-journal` theme makes us beautiful.
- `virtualenv` emcompasses everything. 
- `supervisord` makes sure our service never crashes.

And thats pretty much it!

All of the configutations are in this repository. Deployment instructions 
will be out soon.

Features
--------
- threaded comments
- up voting
- subreddits
- user karma
- search
- rate limiting
- ajax form posting
- user profiles

Build Instructions
------------------

- First, create a virtualenv on your server and clone this repository:

```bash
virtualenv reddit-env
cd reddit-env 
source bin/activate
git clone https://github.com/codelucas/flask_reddit.git
```

- Set up an instance of MySQL on your server. Note your username and password.

`sudo aptitude install mysql-server libmysqlclient-dev`

- Set up an instance of nginx on your server. (Don't worry more detailed instructions to come)

`sudo aptitude install nginx`

- Configure your nginx settings located in `flask\_reddit/server/nginx.conf`.

- Add your settings into your global conf file located in `/etc/nginx/nginx.conf`

- Restart nginx to recognize your settings `sudo service nginx restart`

- Due to sensitive configuration information, I have hidden my personal
`config.py` file in the gitignore. But, I have provided a clean and easy
to use config template in this repo named `app_config.py`. 

- **Fill out the `app_config.py` file with your own information and then rename it to
`config.py` so flask recognizes it by using `mv app_config.py config.py`.**
Please be sure to fill out the mysql db settings similarly to how you set it up!, 
username, pass, etc

- Install all of the required python modules which this server uses.

`pip install -r requirements.txt`

- Run the kickstarter script to build the first user and subreddits.

`python2.7 kickstart.py`

- Run the gunicorn server.

`sudo sh run_gunicorn.sh`

**Note that we have now deployed two servers: `nginx` and `gunicorn`. `nginx` is our
*internet facing* HTTP server on port 80 while `gunicorn` is our *wsgi server* which 
is serving up our flask python application locally. `nginx` reads client
requests and *decides* which requests to foreward to our `gunicorn` server. For example,
`nginx` serves static content like images very well but it forwards url routes 
to the homepage to gunicorn.**

For a full list of details, view our configs at `server/nginx.conf` and 
`server/gunicorn_config.py`.

*Note, for this build to work there are paths that you must change in the `wsgi.py` file, 
the server configs located in `server` directory and the `run_gunicorn.sh` file.*

*Refer to the flask project configuration options to understand what to put in your own
config.py file.*

Do not hesiate to <a href="http://codelucas.com">contact</a> me <Lucas Ou-Yang> for help or concerns.

