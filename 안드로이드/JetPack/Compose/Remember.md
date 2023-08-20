* remember vs rememberSaveable

remember 함수는 Composition 내에서 컴포저블 객체들이 유지될때만 올바르게 동작한다. 화면이 회전 되었을 때는 Activity가 재시작되기 때문에 모든 상태를 다 잃게 된다. 화면 회전 뿐만 아니라 어떠한 환경구성이 변경되던 또는 프로세스가 죽더라도 이러한 일은 발생하기 마련이다.

remember를 사용하는 대신에 rememberSaveable을 사용해보자. **이 함수는 화면회전과 같은 환경구성 변경 및 프로세스의 종료에서도 상태를 보존시킨다.**