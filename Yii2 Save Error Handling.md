
```php
if($model->save()){
	//some codes
} else {
	$errors = $model->errors;

	foreach($errors as $attribute => $error){
		echo "Attribute: $attribute has error: " . implode(', ', $error) . "<br />";
	}
}
```