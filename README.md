editorjs - module for Yii 2
===========================

Use the [https://editorjs.io/](https://editorjs.io/) in forms from Yii2.

Install
-------

Install via Composer:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ bash
composer require quanzo/yii2-editorjs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

or add

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ bash
"quanzo/yii2-editorjs" : "*"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

to the `require` section of your `composer.json` file.

Config
------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ php
$config = [
...
    'modules' => [
...
        'editorjs' => [
            'class' => 'x51\yii2\modules\editorjs\Module',
            /*'uploadDir' => 'upload', // the name of the directory in the root of the site to save information                
            'useDateDir' => true; // Pictures will be uploaded to folders with the current date
            'useUserIdDir' => true; // pictures will be arranged in folders with user id
            'maxImageWidth' => 1000; // image size limit
            'uploadImageFromUrl' => true; // permission to download images by url (see download controller)
            'classRender' => '\\x51\\yii2\\modules\\editorjs\\classes\\Render'; // class for converting json (editorjs) to html
            'useCDN' => false; // use javascript download via cdn.jsdelivr.net 
            // static page crete from editorjs
            'staticPageDir' => '@app/pages/'; // path to the folder with static editorjs pages
            'extWithDot' => '.json';
            'shortcode' => ''; // name of the shortcode processing module (if processing is needed)
            // if need use access filter
            'as access' => [
                'class' => '\yii\filters\AccessControl',
                'rules' => [
                    [
                        'controllers' => ['editorjs/static', 'editorjs/upload'],
                        'roles' => ['admin'],
                        'allow' => true
                    ],
                    [
                        'roles' => ['?'],
                        'allow' => true
                    ]
                ]
            ]*/
        ],
...
    ],
...
];
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Using
-----

### Show static page

Use `\x51\yii2\modules\editorjs\actions\StaticPageAction` in Controller for show
static page.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ php
    public function actions()
    {
        return [            
            'spage' => [
                'class' => '\x51\yii2\modules\editorjs\actions\StaticPageAction',
                'editorjsModuleName' => 'editorjs',
                'on '.\x51\yii2\modules\editorjs\actions\StaticPageAction::EVENT_BEFORE_RUN => function ($event) {
                    Yii::$app->view->registerAssetBundle('\x51\yii2\modules\editorjs\assets\RenderAssets');
                }

            ],
        ];
    }
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Editor.js in form
-----------------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$form = ActiveForm::begin();
echo $form->field($model, 'post_type')->textInput(['maxlength' => true]);
.....
Yii::$app->getModule('editorjs')->editorjs('editorjs-container', $model->formName(), 'textNameFieldInModel', $model->textNameFieldInModel);
.....
ActiveForm::end();
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Can be used for any form. The result is in a hidden field. Field name
`formName[textNameFieldInModel]`. If you do not specify a form name, then the
result in field `textNameFieldInModel`.
