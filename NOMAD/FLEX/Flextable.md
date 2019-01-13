
```
flexbox를 다루려면 주축과 교차축이라는 두 개의 축에 대한 정의를 알아야 합니다. 
주축은 flex-direction 속성을 사용하여 지정하며 교차축은 이에 수직인 축으로 결정됩니다. 
flexbox의 동작은 결국 이 두 개의 축에 대한 문제로 환원되기 때문에 이들이 어떻게 동작하는지 처음부터 이해하는 것이 중요합니다.
```

**주축은 flex-direction에 의해 정의되며 4개의 값을 가질수 있습니다.**

- column
- column-reverse
- row
- row-rwverse

**flex-wrap Flex 컨테이너 역활 공간분할은 해당 행에서만 이루어지고 다른행에 영향을 미치지 않습니다.**

- nowrap
- wrap

**justify-content 속성은 주축을 따라 flex 항목 행을 정렬하는 방식을 지정합니다.**

- stretch
- flex-start
- flex-end
- center
- space-around
- space-between
- space-evenly
