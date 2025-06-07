

établir coonnexion
```php
$db = new PDO('mysql:host=localhost;dbname=DATABASENAME;charset=utf8mb4', 'USERNAME', 'PASSWORD');
$db->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
//////////////////////////////////// autre version

try{

    $database = "mysql:host=localhost;dbname=website;charset=utf8";
    $username = "sid";
    $password = "1227";
    
    $db = new PDO($database,$username,$password);
}
catch(PDOException $e){
    echo $e->getMessage();
}
?>
```


```php
while ($row = $select->fetch(PDO::FETCH_ASSOC)) { ... }
```

- lorsque le fetch retournera un empty, il retournera false, donc row=false à la fin


```php
$row = $select->fetch(PDO::FETCH_ASSOC);
if ($row) {
    $col = $row['col'];
}
```

- Si on cherche à ``fetch`` un user qui n'existe pas, alors on aura false

```php
$select->execute(array(':id' => $id));
$row = $select->fetch(PDO::FETCH_ASSOC);
```

```php
if ($result !== false) { ... }
```

```php
$insert = $db->prepare(...)
```

```php

//pour user exo
$row = $stmt->fetch(PDO::FETCH_ASSOC);
if ($row) {
    echo "Utilisateur trouvé";
} else {
    echo "Aucun utilisateur trouvé";
}
```


```php
try {
    $stmt = $db->prepare("INSERT INTO users (email) VALUES (:email)");
    $stmt->execute([':email' => $email]);
    echo "Insertion réussie";
} catch (PDOException $e) {
    echo "Erreur SQL : " . $e->getMessage();
}

```