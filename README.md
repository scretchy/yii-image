Introduction of YiiImage
========================

Object-Event-Oriented Yii extension for Image manipulation 

Installation and Configuring 
============================

  1. Extract those files to folder "extention/yii-image"
  2. You can set configuration in main config.

``` php

<?php
// protected/configs/main.php

return array(

    'import' => array(
        /**
        
        ...
        
        */
        'ext.yii-image.*',
    ),

    'components' => array(
        /**
        
        ...
        
        */
        'image' => array(
            'class' => 'YiiImage',
            'activeDriverName' => 'gd', // avaliable: gd, imagick, gimagick
        ),
    ),
);

```

Using
=====

``` php

<?php

$img = Yii::app()->image->create(new YiiImageBox(800, 600));

$drawer = $img->draw();
$drawer->onBeforeDrawPolygon = function (YiiImageDrawerEventOnDrawPolygon $event)
{
    var_dump($event->color);
};
$drawer->line(new YiiImagePoint(3, 3), new YiiImagePoint(50, 50), new YiiImageColor('#00FF00'))
       ->ellipse(new YiiImagePoint(300, 300), new YiiImageBox(200, 400), new YiiImageColor('#FF0000'))
       ->polygon(array(
            new YiiImagePoint(200, 400),
            new YiiImagePoint(300, 400),
            new YiiImagePoint(300, 410),
            new YiiImagePoint(200, 430),
            new YiiImagePoint(210, 330),
        ), new YiiImageColor('#0000FF'));

$img->save($path, array('format' => 'png'));

```