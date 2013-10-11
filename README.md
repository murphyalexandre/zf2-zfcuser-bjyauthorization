zf2-zfcuser-bjyauthorization
============================

Zend Framework 2 Skeleton App with ZfcUser and BjyAuthorization.

This repository was made using [this tutorial](http://samminds.com/2013/03/zfcuser-bjyauthorize-and-doctrine-working-together/).

Getting started
===============
First, you need to install the modules using composer. Composer is not in the repository. Install it and run it.

    curl -sS https://getcomposer.org/installer | php
    php composer.phar self-update
    php composer.phar install
    
This should install the Zend Framework, ZfcUser and BjyAuthorize.

Then, the only thing you need to do is setup the database using a local config file in /config/autoload and create the schema.

    return array(
        'doctrine' => array(
            'connection' => array(
                'orm_default' => array(
                    'driverClass' => 'Doctrine\DBAL\Driver\PDOMySql\Driver',
                    'params'      => array(
                        'host'     => 'localhost',
                        'port'     => '3306',
                        'user'     => 'someuser',
                        'password' => 'somepassword',
                        'dbname'   => 'database'
                    )
                )
            )
        )
    );
    
    ./vendor/bin/doctrine-module orm:validate-schema
    ./vendor/bin/doctrine-module orm:schema-tool:create
    
The last step that you need to do is to create the default roles :

    INSERT INTO `role`(`parent_id`, `roleId`) VALUES (NULL, 'guest');
    INSERT INTO `role`(`parent_id`, `roleId`) VALUES (NULL, 'user');
    INSERT INTO `role`(`parent_id`, `roleId`) VALUES (2, 'admin');
