
ImageBehaviorNeo
 Add some functions to origin ImageBehavior SkieDr made.
   1. can set any upload directory and file path you want.
   2. add Validation rules
 
 
 Origin of this behavior is written by By Skiedr.
    @author Yevgeny Tomenko aka SkieDr
    http://bakery.cakephp.org/articles/skiedr/2007/08/28/actas-image-column-behavior
 
 
 


  ----------How to use--------------------
   if you use the following model and  save the record(id:20, bar_id:3),
    file path is "webroot/upload/foodir/3/20.jpg".
 
  <?php 
  class FooImage extends AppModel {
 
   public $actsAs = array(
      'Image'=>array(
        'baseDir' => 'upload/',  <- webroot/upload/
        'modelName' => 'foodir',  <- webroot/upload/foodir/
        'separatedir' => 'bar_id',  <- set column name of DB
        'filenameKey' => 'id',  <- set column name of DB
 
         'fields'=>array(
          'image'=>array(
            'thumbnail'=>array('create'=>true),
            'resize'=>array(
              'width'=>'200','height'=>'200',
              'aspect'=>true,'allow_enlarge'=>true,
              ),
            'versions'=>array(
              array(
               'prefix'=>'small','width'=>'70','height'=>'70',
                'aspect'=>true,'allow_enlarge'=>true,
              ),
              )))));
 
 
   public $validate = array(
      'image' => array(
       array(
          'rule' => array('validationFileSize', 3000000), //3M
          'message' => 'File size is over',
          ),
        array(
          'rule' => array('validationFileFormat'),
          'message' => 'You can upload only image files',
          ),
        ),
      );
  ?> 
 
 
