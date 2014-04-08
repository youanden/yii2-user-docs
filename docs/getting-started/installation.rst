Installation
============

This document will guide you through the process of installing Yii2-user using **composer**. Installation is a quick and
easy two-step process. Installation is fully automatic: you don't even need to configure module manually!

.. note::
    Before we start make sure that you have properly configured **db** and **mail** application components.

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

That's all! You have successully finished Yii2-user installation and from now you are ready to use all its functionality.
