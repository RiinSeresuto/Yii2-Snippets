transaction is a sequence of one or more SQL statements that are executed as a single unit of work

```php
$transaction = Yii::$app->db->beginTransaction();

try{
	//some codes
	$transaction->commit()
} catch (\Exception $e) {
	$transaction->rollBack();
	throw $e;
} catch (\Throwable $e) {
	$transaction->rollBack();
	throw $e;
}
```
