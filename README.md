# Mileage Calculator in Symfony

This code writen in OOP style for calculation mileage in symfony4 project and use PHP7.2 and DQL for rewrite data in database.

# What doing..

### This code getting all data task what need for calculation and rewrite...
```php
//Example
    $allCars = $one->getCars(); 
    $periodical = $one->getIsPeriodical(); 
    $mileage = $one->getMileage(); 
    $carId = $allCars->getId(); 
    $interval = $mileage->getRepeatInterval(); 
    $remindAt = $mileage->getReminderMileage(); 
    $mileageAtCreated = $mileage->getMileageAtCreate(); 
    $itemArray->car = $carId; 
    $itemArray->period = $periodical; 
    $itemArray->interval = $interval; 
    $itemArray->remindAt = $remindAt; 
    $itemArray->mileageAtCreated = $mileageAtCreated;
```
### And with help linear function forecast mileage...
```php
//Example 
// Calculation of the current mileage according to the linear function graph. 
    $difference = ($lastMileage - $firstMileage) / ($lastDate - $firstDate);
    $mileageAtTime = $firstMileage - $difference * $firstDate; $currentDate = $this->currentDate(); 
    $currentMileage = $difference * ($currentDate) + $mileageAtTime;
```
### Check task on periodical or no and rewrite results in database...
```php
//Exaple
    public function periodical($itemArray) { 
        $itemArray = json_decode($itemArray); 
        foreach ($itemArray as $value) { 
            $currentMileage = $value->currentMileage; 
            $mileageAtCreated = $value->mileageAtCreated; 
            $interval = $value->interval; 
            $resultInterval = ($currentMileage - ($mileageAtCreated)); 
            if ($resultInterval >= $interval) { 
                $qb = new QueryBuilder($this->entityManager); 
                $qb->update(Task::class, 't') ->set('t.mileageAtCreated', ':tas')
                                              ->andWhere('t.id =:val') 
                                              ->setParameter('val', $taskId) 
                                              ->setParameter('tas', $currentMileage)
                                              ->getQuery() 
                                              ->execute(); 
            } 
        } 
        return 'REWRITE';
    }
```
