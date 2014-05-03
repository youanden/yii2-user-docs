Overriding models
=================

When you are creating application with Yii2-user you can find that you need to override models or forms.
Yii2-user is very extensible and allows you to override any model. Yii2-user does not create models using
"new" statement, instead it uses component named "ModelManager" which creates requested models. Here is
default model manager configuration:

.. code-block:: php

    <?php
    return [
        ...
        'modules' => [
            ...
            'user' => [
                'class' => 'dektrium\user\Module',
                'components' => [
                    'manager' => [
                        // Active record classes
                        'userClass'    => 'dektrium\user\models\User',
                        'profileClass' => 'dektrium\user\models\Profile',
                        'accountClass' => 'dektrium\user\models\Account',
                        // Model that is used on resending confirmation messages
                        'resendFormClass' => 'dektrium\user\models\ResendForm',
                        // Model that is used on logging in
                        'loginFormClass' => 'dektrium\user\models\LoginForm',
                        // Model that is used on password recovery
                        'passwordRecoveryFormClass' => 'dektrium\user\models\RecoveryForm',
                        // Model that is used on requesting password recovery
                        'passwordRecoveryRequestFormClass' => 'dektrium\user\models\RecoveryRequestForm',
                    ],
                ],
            ],
            ...
        ],
        ...
    ];


Example
-------

Assume you decided to override user class and change registration process. Let's create new user class under `@app/models`.

.. code-block:: php

    <?php
    namespace app/models;

    use dektrium\user\models\User as BaseUser;

    class User extends BaseUser
    {
        public function register()
        {
            // do your magic
        }
    }

In order to make Yii2-user use your class you need to configure manager component as follows:

.. code-block:: php

    <?php
    return [
        ...
        'modules' => [
            ...
            'user' => [
                'class' => 'dektrium\user\Module',
                'components' => [
                    'manager' => [
                        'userClass' => 'app\models\User',
                    ],
                ],
            ],
        ],
    ];

Well done! Yii2-user now uses your User model.
