Installation
============

This page describes Yii2-user installation using composer. Installation is a quick and easy two-step process. Before we
start make sure that you have properly configured **db** and **mail** application components.

Downloading Yii2-user using composer
------------------------------------

Add Yii2-user to the require section of your **composer.json** file::

   {
        "require": {
            "dektrium/yii2-user": "*"
        }
   }

And run following command to make **composer** download and install Yii2-user::

    $ php composer.phar update

Updating database schema
------------------------

After you downloaded Yii2-user, the last thing you need to do is update your database schema by applying the migrations::

    $ php yii migrate/up --migrationPath=@vendor/dektrium/yii2-user/migrations

Post-installation
-----------------

.. note::
    You have to configure **mail** application component in order to use all features of Yii2-user.
    
Now you have completed the basic installation of Yii2-user. You can go to the register page and try to sign up.
