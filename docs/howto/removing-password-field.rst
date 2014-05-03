Removing password field from registration form
==============================================

In some projects you may need to remove password field from registration form and generate password
automatically and send it to the user by email. In this howto I would like to show you how you can implement
this in three steps:

1. Removing password field from safe attributes
2. Generating and sending password
3. Updating registration form

Before we start
---------------

First of all you need to override User model and view files as described in special guides.

Step 1: Removing password field from safe attributes
----------------------------------------------------

Open **app\\models\\User** class and add following method in order to override **register** scenario:

.. code-block:: php

    <?php
    namespace app\models;

    class User
    {
        /**
         * @inheritdoc
         */
        public function scenarios()
        {
            $scenarios = parent::scenarios();
            $scenarios['register'] = ['username', 'email'];
            return $scenarios;
        }
    }


Step 2: Generating and sending password
---------------------------------------

As we removed password field we need to generate it. Best place for generating password is **beforeValidate**
method. But how will we generate password? Yii2-user has special **Password** helper that contains
**generatePassword** method. It generates user-friendly random password containing at least one lowercase
letter, one uppercase letter and one digit.

To deliver generated password to user we have to send user a welcome message which will include generated
password. Yii2-user includes helpful **Mailer** class that have **sendWelcomeMessage** method that can be used
to send password to user.

.. code-block:: php

    <?php
    namespace app\models;

    class User
    {
        /**
         * @inheritdoc
         */
        public function beforeValidate()
        {
            if (parent::beforeValidate()) {
                // we only need to generate password if scenario is "register"
                if ($this->scenario == 'register') {
                    // generate password with length 6
                    $this->password = Password::generate(6);
                    // send password to user
                    $this->module->mailer->sendWelcomeMessage($this);
                }
                return true;
            }
            return false;
        }
    }


Step 3: Updating registration form
----------------------------------

Last step includes removing password field from registration form. It is pretty easy: create and open 
**@app/views/user/registration/register.php** and paste there following code:

.. code-block:: php

    <?php

    use yii\helpers\Html;
    use yii\widgets\ActiveForm;
    use yii\captcha\Captcha;

    /**
     * @var yii\web\View $this
     * @var yii\widgets\ActiveForm $form
     * @var dektrium\user\models\User $user
     */
    $this->title = Yii::t('user', 'Sign up');
    $this->params['breadcrumbs'][] = $this->title;
    ?>
    <div class="row">
        <div class="col-md-4 col-md-offset-4">
            <div class="panel panel-default">
                <div class="panel-heading">
                    <h3 class="panel-title"><?= Html::encode($this->title) ?></h3>
                </div>
                <div class="panel-body">
                    <div class="alert alert-info">
                        <p>Password will be generated automatically and delivered you by email</p>
                    </div>
                    <?php $form = ActiveForm::begin([
                        'id' => 'registration-form',
                    ]); ?>

                    <?= $form->field($model, 'username') ?>

                    <?= $form->field($model, 'email') ?>

                    <?= Html::submitButton(Yii::t('user', 'Sign up'), ['class' => 'btn btn-success btn-block']) ?>

                    <?php ActiveForm::end(); ?>
                </div>
            </div>
            <p class="text-center">
                <?= Html::a(Yii::t('user', 'Already registered? Sign in!'), ['/user/security/login']) ?>
            </p>
        </div>
    </div>

