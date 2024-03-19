```js
$.ajax({
	url: "/[controller-id]/[action-id]",
	dataType: "json", // to be recieved data
	data: {actionControllerParameter: data}, // data to be sent
	beforeSend: () => {
		//before send code
	},
	success: (data) => {
		//loop to all data
		$.each(data, function(key, value){
			//some codes
		})
	}
})
```


Sample:
```js
$("#submit-add-term").on('click', (e) => {
    var form = $('#add-term')
    var formData = form.serialize()

    $.ajax({
        url: form.attr("action") + "/create-term",
        type: form.attr("method"),
        dataType: 'json',
        data: formData,
        beforeSend: () => {
            $("#submit-add-term").prop('disabled', true)
            $("#submit-add-term").text("Saving...")
        },
        success: data => {
            if(data.success == true){
                $("#lpdpterms-start").val('')
                $("#lpdpterms-end").val('')
                $("#submit-add-term").prop('disabled', false)
                $("#submit-add-term").text("Add New Term")
            }
        }
    })

    return false
})
```

The code above shows the form submission that used AJAX instead of regular form submission

controller:
```php
use yii\helpers\Json;
```

```php
public function actionCreateTerm()
{
	$model = new LpdpTerms();

	if (Yii::$app->request->isAjax) {
		if ($model->load(Yii::$app->request->post()) && $model->save()) {
			return Json::encode(['success' => true]);
		}
	} else {
		return Json::encode(['success' => false]);
	}
}
```