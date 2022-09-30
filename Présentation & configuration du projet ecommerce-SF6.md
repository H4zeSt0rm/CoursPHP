# Pour suivre ce tutoriel il faut d'abord suivre [ce tuto]("https://github.com/TheJordanDev/Tutoriels/blob/main/Tuto%20Installer%20Symfony%20sur%20Windows.md").

<details>
    <summary>Liens importants</summary>
    <ul>
        <li><a href="#creation">Création</a></li>
        <li><a href="#mysql">MySQL</a></li>
        <li><a href="#config">Configuration</a></li>
    </ul>
</details>

---

<h1 align="center"><a id="creation">Création</a></h1>

> N'installez pas web-server-bundle, ce dernier est obsolète depuis Symfony 4.4

> Maintenant il faut initialiser un nouveau projet spécial

```shell
symfony new --webapp SP-Ecommerce-SF6
```

> Pour vérifier les dépendances il faut faire:

```shell
symfony check:requirements
```

![](./assets/projet_ecommerce_sf6/step_1.jpg)    

---

<h1 align="center"><a id="mysql">MySQL</a></h1>

> Si vous avez déjà un MySQL Serv d'installé sur votre machine, continuez plus loin

> Pour installer MySQL [suivez ce tuto](https://github.com/H4zeSt0rm/CoursPHP/blob/main/Installer%20MySQL%20sur%20Windows.md)

---

> Pour mettre en place un environnement local il faut maintenant faire une copie du fichier ".env" et l'appeler ".env.local"

> Dans le fichier ".env.local" il faut maintenant faire plusieurs modifications

| Variable     | Valeur                                                                   |
|:------------:|:------------------------------------------------------------------------:|
| APP_ENV      | prod                                                                     |
| DATABASE_URL | mysql://{utilisateur}:{mdp}@127.0.0.1:3306/ecommerce_sf6?serverVersion=8 |
| MAILER_DSN   | smtp://localhost:1025                                                    |

---

<h1 align="center"><a id="config">Configuration</a></h1>

> Première chose à faire après tout ça, activer les extensions PHP, il vous faut **intl** et **pdo**, pour cela rendez vous dans le dossier où vous avez extrait PHP et ouvre le fichier php.ini (affichez les fichiers cachés et les extensions de fichier si vous ne le voyez pas)

![](./assets/projet_ecommerce_sf6/step_2.jpg)



> :warning: **Il y a d'autres valeurs à décommenter**
> 
> - zend_extension=opcache
> 
> - **realpath_cache_size**, il faut aussi modifier la valeur en 5M

> Une fois fais nous pouvons commencer, ouvrez une invite de commande comme expliqué dans le dernier tutoriel et faites les commandes suivantes

```shell
#Cette commande va initialiser la base de donnée
symfony console doctrine:database:create
```

```shell
#Cette commande créé un objet User
symfony console make:user
```

>  Vous allez devoir répondre au questions suivantes en laissant tout vide et faire Enter

> Maintenant nous allons ajouter une info supplémentaire à l'objet User

```shell
symfony console make:entity
```

> Répondez de cette manière au questions suivantes (Si vide faites juste Enter)
> 
> - Users
> 
> - lastname
> 
> - 
> 
> - 100 
> 
> - 
> 
> Quand vous voyez le message *Updated : src/Entity/User.php* faites Enter pour finir la modification

> Nous allons maintenant ajouter un nouvel objet appelé Category

```shell
symfony console make:entity
```

> - Category
> 
> - name
>   
>   - 
>   
>   - 100 
>   
>   - 
> 
> - parent
>   
>   - relation
>   
>   - Category
>   
>   - ManyToOne
>   
>   - 
>   
>   - 
>   
>   - 

> Une fois finis avec l'entité Category faites

```shell
symfony console make:migration
symfony console doctrine:migrations:migrate
```
