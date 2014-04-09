Configuration
=============

This guide covers the basic configuration settings for the Yii2-user.

Available configuration options
-------------------------------

- **confirmable** Whether users have to confirm their accounts by clicking confirmation link sent them by email.
  In order to enable this option you have to configure **mail** application component. Defaults to **True**,

- **confirmWithin** The time in seconds before a confirmation token becomes invalid. After expiring this time user
  have to request new confirmation token on special page. Defaults to **86400** (24 hours).

- **allowUnconfirmedLogin** Whether users are allowed to sign in without activating their accounts. Default to **False**.

- **rememberFor** The time in seconds you want the user will be remembered without asking for credentials. Defaults
  to **1209600** (2 weeks).

- **recoverWithin** The time in seconds before a recovery token becomes invalid. After expiring this time user
  have to request new recovery message. Defaults to **21600** (6 hours).

- **admins** An array of user's usernames who can manage users from admin panel. Defaults to empty array.

- **cost** Cost parameter used by the Blowfish hash algorithm. Defaults to **10**.

Configuration example
---------------------

The configuration is done in the application's ``config/web.php`` file.

.. code-block:: php

    <?php return [
        ...
        'modules' => [
            ...
            'user' => [
                'class' => 'dektrium\user\Module',
                'allowUnconfirmedLogin' => true
                'confirmWithin' => 21600,
                'cost' => 12,
                'admins' => ['admin']
            ],
            ...
        ],
        ...
    ];


