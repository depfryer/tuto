alors tu connais
* private  (seul la classe ou elle est initié y a acces)
* public (tout le monde y as acces)
* protected (la classe et c'est fille y on acces)
ensuite dans mon code il ya style 
```php
/**
     * Roman constructor.
     * @param $nom
     * @param $nbPage
     */
```
il s'agit de commentaire et permet de créé un doc, ou bien de savoir ce que fait la fonction
```php
<?php

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
pour créé un roman il faut que tu fasse
$monPremierRoman = new Roman('Ton Titres',52)

cela pour effet d'avoir un objet avec plusieurs proprieté 
et si par exemple tu as oublié le nom de ton roman
pour le retrouver tu fais
$monPremierRoman->getNom()

il s'agit d'un getter car il te donne une propriété 
et tu obtient donc 
Ton Titres
et la malheurs tu realise que t'as fait une faute 
tu peux faire
$monPremierRoman = new Roman('Ton Titre',52)
mais bon ce n'est pas super du coup tu decide d'utiliser la fonction SetNom
ce qui donne 
$monPremierRoman->setNom('Ton titre') //il n'y a plus la faute

et maintenant si tu reutilise get 
tu obtiens quoi ?
l'avantage de faire ca c'est tout simplement la possibilité de faire plein de roman different
avec un nom et un nombre de page different
$tonSecondRoman = new Roman('hey',28)

Si tu veux obtenir le nombre de page de ton 2nd livre tu fais comment ??
et changer le nombres de page ? attention au piege
 

 

 

 

 

 

 

 

 

ensuite tu decide de faire une BD mais par contre tu decide de rajouter le dessinateur donc tu fais 
```php
<?php
class BD {

    private $nom;
    private $nbPage;
    private $dessinateur/**
 * BD constructor.
 * @param $nom
 * @param $nbPage
 * @param $dessinateur
 */public function __construct($nom, $nbPage, $dessinateur)
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
 

 
 

 

 

 

 
  


 
 


 

 

 

 


si tu as trouvé que c'etait quasiment le même code bien joué
et pour le moment ca va mais si tu veux crée une class BD,puis pourquoi pas un livre pour enfant ect
ca commence a faire beaucoup de fois le même code

et imagine t'as créé toute tes classe et tu realise que tu veux rajouter l'auteur 
l'horreur 
un telle code ne sera jamais maintenable
et c'est la qu'a l'on va decouvrir le principe de 'mere fille'
donc comme dans la vie 
la fille recupere les genes de la mere (donc des propriete et des fonctions)
ce qui permet un truc magnifique
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
quoi mais ya pas de difference est bah pour le moment c'est juste Roman renommer Livre
mais c'est a partir de ce moment que la magie opere
```php
class Roman extends Livre{

}
```
et la Genial tu peut faire
 ```php
new Roman('sss',42)
```
et Ca marche
donc on fait de même avec BD
```php
class BD extends Livre{

}
```
mais la on a a un leger probleme
en effet BD avait dessinateur en plus
et bien rien de plus simple il suffit de faire
```pHP
class BD extends Livre {
    private $dessinateur;

    public function __construct($nom, $nbPage, $dessinateur)
    {
        parent::__construct($nom, $nbPage);
        $this->dessinateur = $dessinateur;
    }
    ```
et la on a rajouté la possibilité de rajouté un dessinateur
la methode
 parent::__construct($nom, $nbPage);
et un moyen afin de reutiliser le code de la mêre (dans notre cas livre)
par contre si tu souhaite rajouté un parametre au livre il faudra aussi pensé a le rajouté ici (sinon il va pas aimer
dans ce cas une solution est (je l'ai recuperer du jS) de non plus faire passé des variables
mais un tableau
style
```php 
{'nom':'Ton Titre','nbPage':22, ......}

ce qui donnera pour livre 
```php
public function __construct($tableau)
    {
        $this->nom = $tableau['nom'];
        $this->nbPage = $tableau['nbPage'];
    }
//j'ai juste mis le constructeur

//pour la BD

 public function __construct($tableau)
    {
        parent::__construct($tableau);
        this->dessinateur = $tableau['dessinateur'];
    }
```
mais la je te donne un bon coup d'avance
et comme ca si jamais tu veux rajouté une propriété a livre tu peux


Maintenant fais moi juste la structure donc les variables et le construteur (si besoin est) afin de pouvoir faire
* un Roman (nom ,auteurs , date)
* une BD(auteurs , date, nom, dessinateur, ecrivain)
* un Manga( date,nom ,auteurs , dessinateur,sens de lecture,ecrivain)
* un CD (nom ,auteurs , date de sortie , nombre de piste)
c'est tout pour le moments
