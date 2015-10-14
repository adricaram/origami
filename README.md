
#Origami ORM V 0.0.10 / Documentation


Origami ORM was build for CodeIgniter3 application, it's a programming technique for converting data between 
incompatible type systems in object-oriented programming languages.

#####**WHY USE ORIGAMI ORM ?**

  * **Security** : 
      Origami can encoding file in base64 and encrypting adress (certified eTrust).
  
  * **Lighter than others** :
      Origami only use essential package.

  * **Friendly use** :
      Easy and better understand.
      

  * **Model Generator** :
      Model Generator is a controller who create automatically your entity, you don't need to create them manually
                                  
----------

| Documentation|
|-------------| ----------- |
| Schema |
| CRUD |
| RelationShip |
| Query Builder |
| Transactions |
| Security |
----------
# Schema
###- **Validation**


```php
class Validation
{
    const OPTION_TYPE_EMAIL = 'email';
    const OPTION_TYPE_URL = 'url';
    const OPTION_TYPE_IP = 'ip';
    const OPTION_TYPE_INT = 'int';
    const OPTION_TYPE_FLOAT = 'float';
    const OPTION_TYPE_EXCLUSION = 'exclusion';
    const OPTION_TYPE_INCLUSION = 'inclusion';
    const OPTION_TYPE_FORMAT = 'format';
    const OPTION_TYPE_LENGTH = 'length';
    const OPTION_TYPE_PRESENCE = 'presence';
    const OPTION_TYPE_CALLBACK = 'callback';
    const OPTION_MIN = 'min';
    const OPTION_MAX = 'max';
    const OPTION_LIST = 'list';
    const OPTION_MATCHER = 'matcher';
    const OPTION_CALLBACK = 'callback';
    const OPTION_MESSAGE = 'message';
}
```

###- **Association**

```php
class Association
{
    const TYPE_HAS_ONE = 'has_one';
    const TYPE_HAS_MANY = 'has_many';
    const TYPE_BELONGS_TO = 'belongs_to';
}
```

###- **Field**

```php
class Field
{
    const TYPE_INTEGER = 'int';
    const TYPE_INT = self::TYPE_INTEGER;
    const TYPE_FLOAT = 'float';
    const TYPE_DOUBLE = self::TYPE_FLOAT;
    const TYPE_STRING = 'string';
    const TYPE_DATE = 'date';
    const DATEFORMAT = 'Y-m-d H:i:s';
    const ALLOWNULL = 'allow_null';
    const ENCRYPT = 'encrypt';
    const BINARY = 'binary';
    const DEFAULTVALUE_NOW = 'now';
}
```

###- *Table*
```php
class Table
{

    private $name; //table name
    
    public function __construct(\Origami\Entity\Manager\Config &$config)
    {
        $this->setName($config);
    }
```
**Return the table name :**
```php
   public function getName()
    {
        return $this->name;
    }
```
**Edit the table name :**
```php
   public function setName(\Origami\Entity\Manager\Config &$config)
    {
        $this->name = $config->getTable();
    }

}
```
###- *Primary key*
```php
class PrimaryKey
{
	private $name;  //Primary key name.

    public function __construct(\Origami\Entity\Manager\Config &$config)
    {
        $this->setName($config);
    }
```
**Like the table class you can return the name of your primary key with**`getName` **and 
edit her with** `setName`

# CRUD

###- *Add*
**first, create new entity :**
```php
$user = new \Entity\test\user();
```
**And add value :**
```php
$user->firstname = 'John';
$user->lastname = 'Do';
```
**Then save it !**
```php
$user->save();
```
###- *Get*
**The** `get()` **function allow you to get a request in the database, 
with Origami you have to use** `find_one()` **:**
```php
    public function get()
    {
        $user = \Entity\test\user::find_one();
        $user = new \Entity\test\user($user->id);
    }
```
###- *Edit*
**The** `set()` **function using** `find_one()` **to find the value and return the new value save :**
```php
    public function set()
    {
        $user = \Entity\test\user::find_one();
        $user->firstname = 'John';

        return $user->save();
    }
```

###- *Delete*
**You can delete a value with** `find_one()` **to get your value and return** `remove()` **to delete it :**
```php
    public function del()
    {
        $user = \Entity\test\user::find_one();

        return $user->remove();
    }
```

# RelationShip

# Query Builder
**Origame use Active Record Class of code igniter 3 :**

| Query Builder Code Igniter 3 | Query Builder Origami     | 
|---------------------------------- | ----------------------|
| `$this->db->get()`                | `$this->db->group_start()`    |
| `$this->db->get_compiled_select()`| `$this->db->or_group_start()`    |
|`$this->db->get_where()`           | `$this->db->not_group_start()`    |
| `$this->db->select()`             | `$this->db->or_not_group_start()`    |
| `$this->db->select_max()`         | `$this->db->group_end()`    |
| `$this->db->select_min()`         | `$this->db->offset()`    |
| `$this->db->select_avg()`         | `$this->db->result()`    |
| `$this->db->select_sum()`         | `$this->db->find()`    |
| `$this->db->from()`               | `$this->db->find_one()`    |
| `$this->db->join()`               | `$this->db->count()`    |
| `$this->db->or_where()`|
| `$this->db->where_in()`|
| `$this->db->or_where_in()`|
| `$this->db->where_not_in()`|
| `$this->db->or_where_not_in()`|
| `$this->db->like()`|
| `$this->db->or_like()`|
| `$this->db->not_like()`|
| `$this->db->or_not_like()`|
| `$this->db->group_by()`|
| `$this->db->distinct()`|
| `$this->db->having()`|
| `$this->db->or_having()`|
| `$this->db->order_by()`|
| `$this->db->limit()`|
| `$this->db->count_all_results()`|
| `$this->db->count_all()`|
| `$this->db->group_start()`|
| `$this->db->or_group_start()`|
| `$this->db->not_group_start()`|
| `$this->db->or_not_group_start()`|
| `$this->db->group_end()`|
| `$this->db->insert()`|
| `$this->db->get_compiled_insert()`|
| `$this->db->insert_batch()`|
| `$this->db->replace()`|
| `$this->db->set()`|
| `$this->db->update()`|
| `$this->db->update_batch()`|
| `$this->db->delete()`|
| `$this->db->empty_table()`|
| `$this->db->truncate()`|
| `$this->db->get_compiled_delete()`|
| `$this->db->start_cache()`|
| `$this->db->stop_cache()`|
| `$this->db->flush_cache()`|
| `$this->db->reset_query()`|


**Create an offset in sql :**
```php
    public function offset($offset)
    {
       \Origami\DB::get($this->config->getDataBase())->offset($offset);

        return $this;
    }
```
**Request a result :**
```php
 private function result()
    {
        // Request
        $results = $this->select()->from($this->config->getTable())->get()->result_array();
        
        // If request fail (no result)
        if (empty($results)) {
            return array();

            // If request success
        } else {
            $objects = array();

            foreach ($results as $result) {
                // Nom de la classe
                $class = $this->config->getClass();

                // Creer le tableau de résultat
                $objects[] = new $class($result, array(
                    'new' => TRUE,
                    'silence' => FALSE
                ));
            }

            return $objects;
        }
    }
```
**Find one model :**
```php
   public function find_one()
    {
		// Limite la requête a un objet
        \Origami\DB::get($this->config->getDataBase())->limit(1);

        // Exécute la requête
        $objects = $this->find();

        // Retoune le premier résultat
        return (isset($objects[0])) ? $objects[0] : NULL;
    }
```
**Find some models**
```php
    public function find()
    {
		$objects = $this->result();
		
		// Si aucun résultat trouvé
        if (empty($objects)) {
            return array();
        }

        // Retoune les objets
        return $objects;
    }
```
**Count the result found :**
```php
    public function count()
    {
		 return (int) \Origami\DB::get($this->config->getDataBase())->count_all_results($this->config->getTable());
    }

```
**Request error handler :**
```php
       private function setConfig(\Origami\Entity\Manager\Config &$config)
    {
       $this->config = &$config;
    }
```


# Transaction

**can be used when you want to make sure all the statements you specify are executed.
If at least one statement fails, all the changes will be rolled back and 
database will be in its initial state.**

```php
  \Origami\DB::get('test')->trans_start();
  \Origami\DB::get('test')->trans_complete();
  return \Origami\DB::get('test')->trans_status();
```

# Secuity
- Encryption
- Encoding

| Var | Name |
| ------------- | ----------- |
| OPTION_TYPE_EMAIL      | email |
| OPTION_TYPE_URL     | url     |
| OPTION_TYPE_IP     | ip     |
| OPTION_TYPE_INT     | int     |
| OPTION_TYPE_FLOAT     | float     |
| OPTION_TYPE_EXCLUSION     | exclusion     |
| OPTION_TYPE_INCLUSION     | inclusion     |
| OPTION_TYPE_FORMAT     | format     |
| OPTION_TYPE_LENGHT     | lenght     |
| OPTION_TYPE_PRESENCE     | presence     |
| OPTION_TYPE_CALLBACK     | callback     |
| OPTION_MIN     | min     |
| OPTION_MAX     | max     |
| OPTION_LIST     | list     |
| OPTION_MATCHER     | matcher     |
| OPTION_CALLBACK     | callback     |
| OPTION_MESSAGE     | message     |


----------
	

 
