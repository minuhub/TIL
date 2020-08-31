# 2-3 어드바이스 동작시점
- before : 비즈니스 메소드 동작 전
- after : 비즈니스 메소드 동작 후 무조건
- after-returning : 비즈니스 메소드 동작 후 성공적이면
- after-throwing : 비즈니스 메소드 동작 후 에러나면
- around : 비즈니스 메소드 동작 전,후

# 2-4 JointPoint와 바인드변수
어드바이스의 메소드를 의미있게 구현하려면, 어드바이스의 동작 시점에 따라 필요한 정보를 매개변수로 받아야 한다.  
이때, 정보는 비즈니스 메소드의 시그니처(리턴타입,이름,매개변수) 또는returnObj, exceptObj 등이다.  
(예를들어 after-throwing 에서 예외발생시, 예외발생한 비즈니스 메소드 이름, 클래스,패키지 등을 알아야 예외처리 가능.)  

### JointPoint란?
JointPoint인터페이스는 클라이언트가 호출한 비즈니스 메소드에 관한 여러가지 정보를 가지고 있다. 
어드바이스 메소드의 매개변수로 JointPoint 객체를 넘겨준다.  

JointPoint 인터페이스의 메소드들  
- Signature getSignature() : 클라이언트가 호출한 메소드의 시그니처(리턴타입,이름,매개변수) 정보가 저장된 Signature객체 리턴
- Object getTarget() : 클라이언트가 호출한 비즈니스 메소드를 포함하는 비즈니스 객체 리턴
- Object[] getArgs() : 클라이언트가 메소드를 호출할 때 넘겨준 인자 목록을 Object배열로 리턴

### 바인드 변수
비즈니스 메소드 실행 후 동작하는 advice의 경우, 비즈니스 메소드의 JointPoint와 별개로 비즈니스 메소드의 실행 결과값도 필요 할 수 있다.  
비즈니스 메소드가 리턴한 결괏값을 바인드 변수에 바인드 하여 매개변수로 advice로 넘겨준다.  
어떤 값인지 모르기 때문에 Object타입으로 선언(예외처리를 할때는 Exception으로 선언)  

### 어드바이스별로 넘겨줘야할 매개변수들
Before 어드바이스 : JointPoint객체  
After Returning 어드바이스 : JointPoint객체, returnObj(비즈니스 메소드가 어떤 값을 리턴했는지에 대한 정보)  
After Throwing 어드바이스 : JointPoint, exceptObj(바인드 변수, 비즈니스 메소드에서 발생한 예외객체)  
Around 어드바이스 : proceedingJointPoint객체  
