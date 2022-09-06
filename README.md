Ip Behaviors
==============
Ip Behaviors

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist budipratama/yii2-ipbehaviors "@dev"
```

or add

```
"budipratama/yii2-ipbehaviors": "@dev"
```

to the require section of your `composer.json` file.


Usage
-----
IpBehaviors automatically fills the specified attributes with the current ip user login.
To use IpBehaviors, insert the following code your ActiveRecord class:
 ```php
 use budipratama\behaviors\IpBehaviors;
 
  public function behaviors()
  {
      return [
            [
                'class' => IpBehaviors::class
            ],
      ];
  }
  ```   
By default, IpBehaviors will fill the first_ip and last_ip attributes with the current username when created row the associated AR object is being inserted. it will fill the last_ip attribute with the username when the AR object is being updated. The user value is obtained by username.
Because attribute values will be set automatically by this behavior, they are usually not user input and should therefore not be validated, i.e. first_ip and last_ip should not appear in the rules() method of the model.
For the above implementation to work with MySQL database, please declare the columns(first_ip, last_ip) as varchar(15).
If your attribute names are different, you may configure the $createdAtAttribute, $updatedAtAttribute and $value properties like the following:
 ```php 
  public function behaviors()
  {
      return [
            [
                'class' => IpBehaviors::class,
                'createdAtAttribute' => 'first_ip',
                'updatedAtAttribute' => 'last_ip',
                'value' => function(){
                    return \Yii::$app->request->userIp;
                }
            ],
      ];
  } 
  ```