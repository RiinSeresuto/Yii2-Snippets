   Controller:
```php
public function actionCreate() {
	$settings = [];
	
	if ($this->request->isPost) {
		$count = count($this->request->post($setting->tableName()));
		
		for ($i = 0; $i < $count; $i++) {
			$settings[$i] = new Setting();
		} 
		
		if (Setting::loadMultiple($settings, $this->request->post())) {
			foreach ($settings as $setting) {
				$setting->save(false);
			} 
		
			return $this->redirect('index');
		}
	}

$settings[] = new Setting();

return $this->render('create', [
	'settings' => $settings
]);
```

View:
```php
<?php
use yii\helpers\Html;
use yii\widgets\ActiveForm;

$form = ActiveForm::begin();

foreach ($settings as $id => $setting) {
	echo $form->field($setting, "[$id]value")->label($setting->name);
}

echo Html::submitButton('Save'); ActiveForm::end();
```

## Sample

Table with initial count of rows to be added
```php
$model = []
$rows = 6;

if($this->request->isPost){
	for ($i = 0; $i < $rows; $i++) {
		$model[$i] = new Model();
	} 
	
	if (Model::loadMultiple($model, $this->request->post())) {
		foreach ($model as $model) {
			$model->save(false);
		} 
	
		return $this->redirect('index');
	}
}

while (count($model) < $rows) {
	$model[] = new Model();
}
```

Instantiation of model, `$model[] = new Model();` should be after the request checking