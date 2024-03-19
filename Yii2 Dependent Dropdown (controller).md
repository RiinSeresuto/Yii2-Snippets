```php
use yii\helpers\Json;
```

```php
public function actionGetSomething($id)
{
	$data[] = ['id' => '', 'text' => ''];
	$models = Molde::find()->where(['chapters_id' => $chapter_id])->all();

	foreach ($models as $model) {
		$data[] = [
			'id' => $model->id,
			'text' => $model->name,
		];
	}
	
	return Json::encode($data);
}
```