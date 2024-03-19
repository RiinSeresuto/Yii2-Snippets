```php
use kartik\select2\Select2;
```

**Parent Select2**
```php
<?= $form->field($model, 'attribute')->widget(Select2::className(), [
	'data' => $data,
	'options' => [
		'placeholder' => 'Choose chapter ...',
		'id' => 'parentDropdown'
	],
	'pluginOptions' => [
		'allowClear' => true
	],
	'pluginEvents' => [
		'select2:select' => '
			function(){
				var dropdownId = this.value
				dropdownFunction(dropdownParentId)
			}
		'
	]
])->label('Label') ?>
```

**Child Select2**
```php
<?= $form->field($model, 'attribute2')->widget(Select2::className(), [
	'data' => $model->isNewRecord ? [] : $child,
	'options' => [
		'placeholder' => 'Choose Sector ...',
		'id' => 'childDropdown'
	],
	'pluginOptions' => [
		'allowClear' => true
	]
])->label('Sector Outcome') ?>
```

**JavaScript**
```js
function dropdownFunction(dropdownParentId){
	$.ajax({
		url: "/[controller-id]/[action-id]",
		dataType: "json",
		data: {id: dropdownParentId}
		beforeSend: () => {
			$("#childDropdown").html("").select2({
				theme: "krajee-bs3",
				width: "100%",
				placeholder: "Loading..."
			})
		},
		success: (data) => {
			$("#sector-dropdown").html("").select2({
				data: data,
				theme: "krajee-bs3",
				width: "100%",
				placeholder: "-",
				allowClear: true
			})
		}
	})
}
```