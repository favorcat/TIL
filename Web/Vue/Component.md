# App.vue에서 Component 참조 방법

프로젝트를 만들다 보면 코드가 길어져 여러 컴포넌트로 나눈 후 App.vue에서 참조를 한다.    
이 경우 참조 방법은 다음과 같다.    
```
<template>
    <A/>
</template>

<script>
import A from '경로';

export default {
    components: {
        A,
    }
}
</script>