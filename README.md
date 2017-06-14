Alors tu connais
* private (seul la classe ou elle est initiée y a accès)
* public (tout le monde y a accès)
* proteste (la classe et c'est fille y ont accès)
Ensuite dans mon code il Ya style 
```php
/**
     * Roman constructor.
     * @param $nom
     * @param $nbPage
     */
```
Il s'agit de commentaire et permet de créer un doc, ou bien de savoir ce que fait la fonction
```php
<? php

class Roman {

    private $nom;
    private $nbPage;

    /**
     * Roman constructor.
     * @param $nom
     * @param $nbPage
     */
    public function __construct($nom, $nbPage)
    {
        $this->nom = $nom;
        $this->nbPage = $nbPage;
    }

    /**
     * @return mixed
     */
    public function getNom()
    {
        return $this->nom;
    }

    /**
     * @param mixed $nom
     */
    public function setNom($nom)
    {
        $this->nom = $nom;
    }

    /**
     * @return mixed
     */
    public function getNbPage()
    {
        return $this->nbPage;
    }

    /**
     * @param mixed $nbPage
     */
    private function setNbPage($nbPage)
    {
        $this->nbPage = $nbPage;
    }
}
```
je t'ai fait une classe
Pour créer un roman il faut que tu fasses
```php
    $monPremierRoman = new Roman('Ton Titres',52)
```
Cela pour effet d'avoir un objet avec plusieurs propriétés 
Et si par exemple tu as oublié le nom de ton roman
Pour le retrouver tu fais
```php
    $monPremierRoman->getNom()
```
Il s'agit d'un getter car il te donne une propriété 
Et tu obtiens donc 
Ton Titres
Et le malheur tu réalises que t'as fait une faute 
Tu peux faire
```php
    $monPremierRoman = new Roman('Ton Titre',52)
```
Mais bon ce n'est pas super du coup tu décides d'utiliser la fonction SetNom
Ce qui donne 
```php
    $monPremierRoman->setNom('Ton titre') //il n'y a plus la faute
```
Et maintenant si tu réutilise guet 
Tu obtiens quoi ?
L’avantage de faire ça c'est tout simplement la possibilité de faire plein de roman diffèrent
Avec un nom et un nombre de page diffèrent
```php
    $tonSecondRoman = new Roman('hey',28)
```
Si tu veux obtenir le nombre de page de ton 2nd livre tu fais comment ??
Et changer le nombre de page ? attention au piège
 

 

 

 

 

 

 

 

 

Ensuite tu décides de faire une BD mais par contre tu décides de rajouter le dessinateur donc tu fais 
```php
<?php
class BD {

    private $nom;
    private $nbPage;
    private $dessinateur
    /**
     * BD constructor.
     * @param $nom
     * @param $nbPage
     * @param $dessinateur
     */
    public function __construct($nom, $nbPage, $dessinateur)
    {
        $this->nom = $nom;
        $this->nbPage = $nbPage;
        $this->dessinateur = $dessinateur;
    }
    /**
     * BD constructor.
     * @param $nom
     * @param $nbPage
     */
    
    
    /**
     * @return mixed
     */
    public function getNom()
    {
        return $this->nom;
    }
    
    /**
     * @param mixed $nom
     */
    public function setNom($nom)
    {
        $this->nom = $nom;
    }
    
    /**
     * @return mixed
     */
    public function getNbPage()
    {
        return $this->nbPage;
    }
    
    /**
     * @param mixed $nbPage
     */
    public function setNbPage($nbPage)
    {
        $this->nbPage = $nbPage;
    }
}
```
Que realise tu ? 
 

 
 

 

 

 

 
  


 
 


 

 

 

 


Si tu as trouvé que c'était quasiment le même code bien joué
Et pour le moment ça va mais si tu veux créer une class BD, puis pourquoi pas un livre pour enfant et
Ça commence à faire beaucoup de fois le même code

Et imagine t'as créé toute tes classes et tu réalises que tu veux rajouter l'auteur 
L’horreur 
Un telle code ne sera jamais maintenable
Et c'est là qu'a l'on va découvrir le principe de 'mère fille'
Donc comme dans la vie 
La fille récupère les gènes de la mère (donc des propriétés et des fonctions)
Ce qui permet un truc magnifique
```php
<?php
    
class Livre {
    
     protected $nom;
     protected $nbPage;
    
    /**
     * Roman constructor.
     * @param $nom
     * @param $nbPage
     */
    public function __construct($nom, $nbPage)
    {
        $this->nom = $nom;
        $this->nbPage = $nbPage;
    }
    
    /**
     * @return mixed
     */
    public function getNom()
    {
        return $this->nom;
    }
    
    /**
     * @param mixed $nom
     */
    public function setNom($nom)
    {
        $this->nom = $nom;
    }
    
    /**
     * @return mixed
     */
    public function getNbPage()
    {
        return $this->nbPage;
    }
    
    /**
     * @param mixed $nbPage
     */
    public function setNbPage($nbPage)
    {
        $this->nbPage = $nbPage;
    }
}
```
Quoi mais il n’y a pas de différence est bah pour le moment c'est juste Roman renommer Livre
Mais c'est à partir de ce moment que la magie opère
```php
class Roman extends Livre{

}
```
Et la Génial tu peux faire
```php
    New Roman('sss',42)
```
Et Ça marche
Donc on fait de même avec BD
```php
class BD extends Livre {

}
```
Mais là on a un léger problème
En effet BD avait dessinateur en plus
Et bien rien de plus simple il suffit de faire
```php
class BD extends Livre {
    Private $dessinateur ;

    Public fonction __construit($nom, $nb Page, $dessinateur)
    {
        parent::__construct($nom, $nbPage);
        $this->dessinateur = $dessinateur;
    }
....
}

```

Et là on a rajouté la possibilité de rajouté un dessinateur
La méthode

```php
    parent::__construct($nom, $nbPage);
```
Et un moyen afin de réutiliser le code de la mère (dans notre cas livre)
Par contre si tu souhaites rajouter un paramètre au livre il faudra aussi penser a le rajouté ici (sinon il ne va pas aimer
Dans ce cas une solution est (je l'ai récupéré du JS) de non plus faire passer des variables
Mais un tableau
Style
```php 
    {'nom' : 'Ton Titre','nbPage' :22, ...}
```

Ce qui donnera pour livre 
```php
    public function __construct($tableau)
        {
            $this->nom = $tableau['nom'] ;
            $this->nbPage = $tableau['nbPage'] ;
        }
//j'ai juste mis le constructeur

//pour la BD

 public function __construct($tableau)
    {
        parent::__construct($tableau);
        this->dessinateur = $tableau['dessinateur'];
    }
```
Mais là je te donne un bon coup d'avance
Et comme ça si jamais ne tu veux rajouter une propriété a livré tu peux


Maintenant fais-moi juste la structure donc les variables et le constructeur (si besoin est) afin de pouvoir faire
* un Roman (nom, auteurs, date)
* une BD (auteurs, date, nom, dessinateur, écrivain)
* un Manga (date, nom, auteurs, dessinateur, sens de lecture, écrivain)
* un CD (nom, auteurs, date de sortie, nombre de piste)
C’est tout pour le moment
