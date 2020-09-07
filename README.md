# Bitfumes
<b>Description: </b>Bitfumes is a real time single page forum app. It uses Laravel in backend and Vue js in frontend . so powerful .<br>
It's implemented from [**Real Time Single Page Forum App with Pusher Laravel & vuejs**](https://www.udemy.com/course/real-time-single-page-forum-app-with-pusher-laravel-vuejs/)

## Dependencies
1- Laravel framework <br>
2- Vuejs <br>
3- Axios<br>
4- Vuetify<br>
5- Pusher <br>


## Installation

Clone this repository

```bash
git clone git@github.com:bitfumes/real-time-single-page-forum-app.git
```

Go inside the directory

```bash
cd real-time-single-page-forum-app
```

Now install composer

```bash
composer install
```

Generate key on .env file

```bash
cp .env.example .env
php artisan key:generate
```

## Setting for Pusher

Go to .env file and change Broadcast drive to pusher

```
BROADCAST_DRIVER=pusher
```

and also give credentials of your pusher on .env file

```
PUSHER_APP_ID=xxxxxx
PUSHER_APP_KEY=xxxxxxxxxxxxxxxxxxxx
PUSHER_APP_SECRET=xxxxxxxxxxxxxxxxxxxxxx
PUSHER_APP_CLUSTER=xxx
```

open bootstrap.js file and provide pusher key there also.

```javascript
window.Echo = new Echo({
    broadcaster: 'pusher',
    key: "xxxxxxxxxxxxxxxxxxxxx",
    cluster: "xxx",
    encrypted: true,
    ...
```

## Screenshots
![](https://github.com/mostafamt/real-time-single-page-forum-app/blob/master/resources/assets/img/screenshots/Screenshot1.png)
![](https://github.com/mostafamt/real-time-single-page-forum-app/blob/master/resources/assets/img/screenshots/Screenshot2.png)
![](https://github.com/mostafamt/real-time-single-page-forum-app/blob/master/resources/assets/img/screenshots/Screenshot3.png)
![](https://github.com/mostafamt/real-time-single-page-forum-app/blob/master/resources/assets/img/screenshots/Screenshot4.png)
![](https://github.com/mostafamt/real-time-single-page-forum-app/blob/master/resources/assets/img/screenshots/Screenshot5.png)
