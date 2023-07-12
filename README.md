# sio-control
un controle en bts sio sur lol en php fallait mettre les joueur sur une page qui etait dans la base de donner du prof


<?php

include "debut_pages_affichable.php";

$CO = new PDO("mysql:dbname=lol;host=192.168.0.20", "sio", "sio");

$query_champions= $CO->query("SELECT * FROM champions ORDER BY Nom");
$result = "";
while($champions = $query_champions->fetch(PDO::FETCH_ASSOC)) {
  $id = $champions["id"];
  $nom = $champions["Nom"];
  $nickname = $champions["Surnom"];
  $image = $champions["apparence"];
  $dess = $champions["Description"];
  $role = $champions["Role"];

  $query_role = $CO->query("SELECT nom FROM role WHERE id = $role");
  while($roles = $query_role->fetch(PDO::FETCH_ASSOC)) {
    $role = $roles["nom"];
  }

  $query_skins = $CO->query("SELECT * FROM skin WHERE id_champ = $id");
  $skins = "";
  while($skin = $query_skins->fetch(PDO::FETCH_ASSOC)) {
    $skins .= $skin["nom"] . ", ";
  }

  $result .= "  
  
    <div class=champ>
  
      <img src=$image alt=$nom>
      <div class=contente>
        <div class=nom>$nom - '$nickname'</div>
        <div class=role>$role</div>
        <div class=dess>$dess</div>
        <div class=skin1><b>Skin : </b>$skins</div>
      </div>
    </div>";
}
echo $result
?>

<style>


 .champ {
    
        display: flex;
        background-color: black;
        margin: 15px;
        width: 85%;
        height: 26%;
        color: white;
        text-shadow: 1px 1px red ;
    }


    .champ img {
        width: 50%;

    }

    

.champ:hover img {
  transform: scale(1.1);
}
 


    .nom {
        font-weight: bold;
        color:orange;
    font-size:30px;
    text-shadow: 1px 1px red ;
    }



    .contente {
        display: flex;
        margin: 15px;
        align-content: space-between;
        flex-direction: column;
        justify-content: space-between;
    }

</style>
