---
title: "Modifier la page de connexion à votre admin Wordpress"
date: "2012-06-25"
categories: 
  - "web"
tags: 
  - "css"
  - "hook"
  - "php"
  - "wordpress"
---

Comment modifier la page de connexion à votre zone d'administration de votre site qui tourne sous Wordpress.

1. Rendez-vous sur le site de [wordpress pour découvrir les fonctions et le CSS à utiliser](http://codex.wordpress.org/Customizing_the_Login_Form "Customizing the Login Form").
2. Créer une feuille de style externe qu'on nommera `login.css` et qui résidera dans le dossier de votre thème, pour ne pas encombrer inutilement `function.php`
3. En vous basant sur le point 1 soyez créatif et remplissez `login.css`. Pour le coup j'ai fait ceci:
    
    \* { -moz-box-sizing:border-box; box-sizing:border-box; }
    html { margin:0; padding:0; }
    body.login { margin:0 auto; padding:0; background:#222 url(images/sogeking.jpg) no-repeat top left scroll; color:#999;  background-size:cover; }
    body.login form { margin:0 auto 5px; width:90%; background-color:rgba(255, 255, 255, .7); color:#222; box-shadow:0 1px 4px rgba(0, 0, 0, 0.3), 0 0 40px rgba(0, 0, 0, 0.1) inset; border:1px solid #f1f1f1; }
    body.login label { color:#222; }
    body.login input\[type=text\],
    body.login input\[type=password\]		{ border:1px solid #aaa; background-color:rgba(255, 255, 255, .5); }
    body.login input\[type=submit\]		{ padding:5px; border-radius:3px; background-color:#222; background-image:-webkit-linear-gradient(#444, #222); background-image:-moz-linear-gradient(#444, #222); background-image:-o-linear-gradient(#444, #222); background-image:linear-gradient(#444, #222); color:#fff; border:none; font-weight:normal; text-shadow:none; }
    body.login input\[type=submit\]:hover { background-image:-webkit-linear-gradient(hsl(0, 80%, 50%), hsl(0, 80%, 30%)); background-image:-moz-linear-gradient(hsl(0, 80%, 50%), hsl(0, 80%, 30%)); background-image:-o-linear-gradient(hsl(0, 80%, 50%), hsl(0, 80%, 30%)); background-image:linear-gradient(hsl(0, 80%, 50%), hsl(0, 80%, 30%)); }
    
    body.login .message,
    body.login #login\_error		{ width:100%; margin:0 auto 10px; padding:8px; border:none; color:#fff; font-size:1.2em; background:rgba(0,0,0,.2); }
    body.login .message a,
    body.login #login\_error a	{ color:#c41d1d; }
    
    body.login #login { padding-top:250px; }
    body.login #login h1,
    body.login #nav, 
    body.login #backtoblog { display:none; }
    
4. Ouvrir le script `function.php`dans votre éditeur favori et ajoutez-y le code suivant:
    
    add\_action('login\_enqueue\_scripts', 'nyamsprod\_login\_style');
    function nyamsprod\_login\_style() {
        echo <link rel="stylesheet" href="', get\_stylesheet\_directory\_uri() ,'/login.css">', PHP\_EOL;
    }
    
5. Souriez ... [votre nouvelle page de connexion est active](http://www.nyamsprod.com/blog/wp-login.php "Ma nouvelle page de connexion") et surtout vous n'avez jamais touché à la page de connexion en tant que telle :)
