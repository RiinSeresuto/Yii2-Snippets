```php
<?= GridView::widget([
	'dataProvider' => $privateDataProvider,
	//'filterModel' => $searchModel,
	'tableOptions' => ['class' => 'row-border'],
	'columns' => [
		['class' => 'yii\grid\SerialColumn'],
		//'id',
		[
			'label' => 'Indicator',
			'footer' => '<strong>Indicator</footer>',
			'value' => function ($model) {
					return $model->lpdpIndicatorShoppingListDetails->indicator;
				}
		],
		[
			'class' => 'yii\grid\ActionColumn',
			'template' => '<div>{view} {update} {delete}</div>',
			'buttons' => [
				'view' => function ($url, $model) use ($term) {
						$url = Url::to(['view', 'id' => $model->id, 'term' => $term]);
						return Html::a('<i class="bx bx-show"></i>', $url, [
							'title' => Yii::t('yii', 'View'),
						]);
					},
				'update' => function ($url, $model) use ($term) {
						$url = Url::to(['update', 'id' => $model->id, 'term' => $term]);
						return Html::a('<i class="bx bx-edit-alt"></i>', $url, [
							'title' => Yii::t('yii', 'Update'),
						]);
					},
				'delete' => function ($url, $model) use ($term) {
						return Html::a('<i class="bx bx-trash"></i>', [
							'delete',
							'id' => $model->id, 'term' => $term
						], [
							'title' => Yii::t('yii', 'Delete'),
							'data' => [
								'confirm' => Yii::t('yii', 'Are you sure you want to delete this item?'),
								'method' => 'post',
							],
						]);
					},
			],
		],
	],
	'summary' => false,
	'showFooter' => true
]); ?>
```
"This gridview configures the table class itself for design using Bootstrap. Additionally, it customizes the template of the action columns for design purposes. The table footer is displayed, while the summary, (e.g. 10 of 100) is hidden, as it is configured by the datatable."

## Configuration for action column template
```php
[
	'class' => 'yii\grid\ActionColumn',
	'template' => '<div>{view} {update} {delete}</div>',
	'buttons' => [
		'view' => function ($url, $model) use ($term) {
			$url = Url::to(['view', 'id' => $model->id, 'term' => $term]);
			return Html::a('View', $url, [ 'title' => Yii::t('yii', 'View'), ]);
		},
		'update' => function ($url, $model) use ($term) {
			$url = Url::to(['update', 'id' => $model->id, 'term' => $term]);
			return Html::a('Update', $url, [ 'title' => Yii::t('yii', 'Update'), ]);
		},
		'delete' => function ($url, $model) use ($term) {
			return Html::a('Delete', [ 'delete', 'id' => $model->id, 'term' => $term ],
			[
				'title' => Yii::t('yii', 'Delete'),
				'data' => [
					'confirm' => Yii::t('yii', 'Delete item?'),
					'method' => 'post',
				],
			]);
		},
	],
]
```

