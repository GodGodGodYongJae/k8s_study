# 🔖 기초 컴포넌트

```java
// Some code
@Override
  public Stream<CarDiaryExcelDto> searchCarDiaryForExcel(DateSearch search) {
    return jpaQueryFactory
        .select(
            Projections.constructor(
                CarDiaryExcelDto.class,
                carDiary.id,
                carDiary.diaryDate,
                car.carNo,
                car.id,
                carDiary.driveDistance,
                carDiary.loadAmount,
                carDiary.deliveryAmount,
                carDiary.oilPrice,
                carDiary.oilStation,
                carDiary.ureaPrice,
                carDiary.inspection,
                carDiary.maintenance,
                carDiary.maintenancePrice,
                carDiary.etcMemo
            )
        )
        .from(carDiary)
        .join(carDiary.car, car)
        .where(
            searchDate(search.getStartDate(), search.getEndDate()), searchCondition(search)
            ,carDiary.deleted.isFalse()
        )
        .orderBy(carDiary.diaryDate.desc())
        .createQuery()
        .getResultStream();
  }
```
